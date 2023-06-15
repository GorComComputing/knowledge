## Linux ALL


```
# Устанавливаем компилятор и скачиваем исходники ядра Linux и BusyBox
$ sudo apt-get install gcc-arm-linux-gnueabihf qemu
$ mkdir qemu-arm && cd qemu-arm
$ wget https://mirrors.edge.kernel.org/pub/linux/kernel/v5.x/linux-5.15.6.tar.gz && tar xvf linux-5.15.6.tar.gz
$ wget https://busybox.net/downloads/busybox-1.36.0.tar.bz2 && tar xvf busybox-1.36.0.tar.bz2

# Собираем ядро Linux
$ cd linux-5.15.6
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- defconfig

# add all 9p virtio related configs:
#    CONFIG_NET_9P=y
#    CONFIG_NET_9P_VIRTIO=y
#    CONFIG_NET_9P_DEBUG=y (Optional)
#    CONFIG_9P_FS=y
#    CONFIG_9P_FS_POSIX_ACL=y
#    CONFIG_PCI=y
#    CONFIG_VIRTIO_PCI=y
# and these PCI and virtio options:
#    CONFIG_PCI=y
#    CONFIG_VIRTIO_PCI=y
#    CONFIG_PCI_HOST_GENERIC=y (only needed for the QEMU Arm 'virt' board)
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig

$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j4

# Собираем BusyBox
$ cd busybox-1.36.0
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- defconfig

# Busybox Settings ==> Build Options SELECT Build BusyBox as a static binary(no shared libs)
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- install

# Готовим корневую файловую систему
$ cd _install
$ mkdir proc sys dev etc etc/init.d

# Создаем файл etc/init.d/rcS со следующим содержимым:

  #!/bin/sh
  mount -t proc none /proc
  mount -t sysfs none /sys
  /sbin/mdev -s

$ chmod +x etc/init.d/rcS 
$ find . | cpio -o --format=newc > ../rootfs.img

# Запускаем полученную систему в QEMU
$ qemu-system-arm -m 256 -M virt -kernel <linux_dir>/arch/arm/boot/zImage -initrd <busybox_dir>/rootfs.img -nographic -append "console=ttyAMA0 root=/dev/ram rdinit=/sbin/init" -virtfs local,path=<host_path_to_share>,security_model=passthrough,mount_tag=host_share

# В гостевой системе подключаем каталог из хост-системы
$ mkdir -p /mnt/host_share && mount -t 9p -o trans=virtio host_share /mnt/host_share -oversion=9p2000.L
```

<!-- https://habr.com/ru/companies/ruvds/articles/524532/ -->
<!-- https://habr.com/ru/articles/149598/ -->
<!-- https://habr.com/ru/articles/146877/ -->
