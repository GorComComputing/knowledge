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
$ make distclean
$ make defconfig
$ make menuconfig
$ make -j 2 ARCH=arm CROSS_COMPILE=armv7-rpi2-linux-gnueabihf-
$ make install
```
