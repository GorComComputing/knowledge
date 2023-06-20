## Linux i386 GRUB


```
# Установка компилятора и библиотек для i386
$ sudo apt install gcc-multilib g++-multilib
# Компиляция с параметром -static
$ gcc -m32 -ggdb3 -O0 -pedantic-errors -std=c89   -Wall -Wextra -pedantic -static  -o init_i386 init.c

# Собираем ядро Linux
$ cd linux/
$ make ARCH=i386 i386_defconfig
$ make ARCH=i386 -j2

# Запускаем ядро Linux и корневую файловую систему в Qemu
$ qemu-system-i386 -kernel linux/arch/x86/boot/bzImage -initrd busybox/~/initramfs.cpio.gz --append "root=/dev/ram init=/init_i386"

# 1. Создаём виртуальный диск размером 64Мб (если надо больше, делаем больше):
$ dd if=/dev/zero of=out.img seek=64MB count=1K bs=1

# 2. Размечаем под ext2 партицию:
$ sudo parted out.img
(parted) mklabel msdos
(parted) mkpart primary ext2 32k 100%
(parted) toggle 1 boot
(parted) quit
# Партиция имеет сдвиг в 32К от начала диска. Это, видимо, для размещения MBR + Stage 1.5 для груба.

# 3. Монтируем диск и его партицию на два отдельных девайса:
$ sudo losetup /dev/loop0 out.img
$ sudo kpartx -v -a /dev/loop0
$ sudo losetup /dev/loop1 /dev/mapper/loop0p1

# 4. Форматируем партицию под ext2:
$ sudo mke2fs /dev/loop1

# 5. Монтируем партицию как диск:
$ sudo mount -t ext2 /dev/loop1 /mnt

# 6. Устанавливаем груб на свежесозданный диск. Обратите внимание, что последним параметром он принимает физический диск:
$ sudo mkdir -p /mnt/boot/grub
$ sudo grub-install --boot-directory=/mnt/boot/ --modules="ext2 part_msdos" /dev/loop0

# 7. Добавляем grub.cfg и другие файлы по вкусу
$ find -print0 | cpio -0oH newc | gzip -9 > ../initramfs.cpio.gz
$ sudo cp busybox/~/initramfs.cpio.gz /mnt/boot/
$ sudo cp linux/arch/x86/boot/bzImage /mnt/boot/

# 8. Подметаем за собой:
$ sudo umount /mnt
$ sudo kpartx -d /dev/loop1
$ sudo kpartx -d /dev/loop0

# 9. Стартуем в Qemu:
$ sudo qemu-system-x86_64 -hda /home/andrew/dev/boot/out.img -m 1024

# Запись файла образа на флешку
$ sudo dd if=out.img of=/dev/sdb bs=1024 conv=notrunc        

# Загрузка Qemu с флешки  (Ctrl+Alt+G пустить захват мыши)
$ sudo qemu-system-i386 -hda /dev/sdb -boot c -usb

# Параметры ядра Linux в GRUB
grub> ls                    # показать список разделов диска
grub> ls (hd0,msdos1)/      # показать содержимое раздела
grub> set root=(hd0,msdos1) # выбор загрузочного раздела
grub> linux /boot/bzImage root=/dev/hda   # указать, где лежит ядро и передать параметры
grub> initrd /boot/initramfs.cpio.gz      # указать, где лежит корневая файловая система
grub> boot                                # запуск ядра Linux

grub> reboot                              # перезагрузка
```
