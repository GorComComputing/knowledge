## Linux i386 GRUB


```
# Загрузка Qemu с флешки  (Ctrl+Alt+G пустить захват мыши)
$ sudo qemu-system-i386 -hda /dev/sdb -boot c -usb

# Параметры ядра Linux в GRUB
grub> ls                    # показать список разделов диска
grub> ls (hd0,msdos1)/      # показать содержимое раздела
grub> set root=(hd0,msdos1) # выбор загрузочного раздела
grub> linux /boot/bzImage root=/dev/hda   # указать, где лежит ядро и передать параметры
grub> initrd /boot/initramfs.cpio.gz      # указать, где лежит корневая файловая система
grub> boot                                # запуск ядра Linux
```
