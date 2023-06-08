#### U-Boot


```bash
# Установка
$ git clone git://git.denx.de/u-boot.git
$ cd u-boot
$ git checkout v2015.07

# Компиляция U-Boot
$ make CROSS_COMPILE=arm-cortex_a8-linux-gnueabihf-am335x_boneblack_defconfig
$ make CROSS_COMPILE=arm-cortex_a8-linux-gnueabihf-
```
