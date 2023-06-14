## Linux ALL


```
$ sudo apt-get install gcc-arm-linux-gnueabihf qemu
$ mkdir qemu-arm && cd qemu-arm
$ wget https://mirrors.edge.kernel.org/pub/linux/kernel/v5.x/linux-5.15.6.tar.gz && tar xvf linux-5.15.6.tar.gz
$ wget https://busybox.net/downloads/busybox-1.36.0.tar.bz2 && tar xvf busybox-1.36.0.tar.bz2
$ cd linux-5.15.6
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- defconfig
# add all 9p virtio related configs
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig

```
