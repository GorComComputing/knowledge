#### BusyBox


```bash
# Каталог технической подготовки
$ mkdir ~/rootfs
$ cd ~/rootfs
$ mkdir bin dev etc home lib proc sbin sys tmp usr var
$ mkdir usr/bin usr/lib usr/sbin
$ mkdir var/log


# Клонирование с репозитория
$ git clone git://busybox.net/busybox.git
$ cd busybox
$ git checkout 1_35_0

# Сборка BusyBox
$ PATH=~/x-tools/armv7-rpi2-linux-gnueabihf/bin:$PATH
$ make distclean
$ make defconfig
$ make menuconfig ARCH=arm CROSS_COMPILE=armv7-rpi2-linux-gnueabihf-
$ make -j 2 ARCH=arm CROSS_COMPILE=armv7-rpi2-linux-gnueabihf-
$ make install

# Создание архива
$ cd ~/rootfs
$ sudo chown -R root:root *
$ find . | cpio -H newc -ov --owner root:root > ../initramfs.cpio
$ cd ..
$ gzip initramfs.cpio
$ mkimage -A arm -O linux -T ramdisk -d initramfs.cpio.gz uRamdisk
# При ошибке: Команда «mkimage» не найдена
$ sudo apt install u-boot-tools

# Запуск Linux kernel с BusyBox в QEMU
$ QEMU_AUDIO_DRV=none qemu-system-arm  -m 256M -nographic -M vexpress-a9 -kernel zImage -dtb vexpress-v2p-ca9.dtb -append "console=ttyAMA0 rdinit=/bin/sh" -initrd initramfs.cpio.gz
```
```
# Параметры конфигурации BusyBox
Settings -> Build static binary (no shared libs) [Y]
```
