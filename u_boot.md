#### U-Boot


```bash
# Установка
$ git clone git://git.denx.de/u-boot.git
$ cd u-boot
$ git checkout v2015.07

# Компиляция U-Boot
$ make CROSS_COMPILE=arm-cortex_a8-linux-gnueabihf- am335x_boneblack_vboot_defconfig      # Для QEMU: qemu_arm_defconfig
$ make -j 4 CROSS_COMPILE=arm-cortex_a8-linux-gnueabihf-
$ sudo apt-get install --reinstall libssl-dev     # при ошибке: fatal error: openssl/evp.h: No such file or directory

# Запуск U-Boot в QEMU
$ qemu-system-arm  -machine virt -nographic -bios u-boot.bin
```
