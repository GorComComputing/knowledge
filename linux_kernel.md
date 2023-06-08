#### Linux kernel


```bash
# Клонирование с репозитория
$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git linux
$ cd linux
$ git checkout v5.19.0

# Выбор типовой конфигурации
$ make ARCH=arm multi_v7_defconfig

# Запуск меню конфигуратора
$ make ARCH=arm menuconfig 

# Компиляция ядра Linux
$ make -j 4 ARCH=arm CROSS_COMPILE=arm-cortex_a8-linux-gnueabihf- zImage

# Компиляция деревьев устройств
$ make ARCH=arm dtbs

# Компиляция модулей (разбросаны по всему дереву исходного кода)
$ make -j 4 ARCH=arm CROSS_COMPILE=arm-cortex_a8-linux-gnueabihf- modules
# Компилирует модули в каталог /lib/modules/[версия ядра]
$ make -j 4 ARCH=arm CROSS_COMPILE=arm-cortex_a8-linux-gnueabihf- INSTALL_MOD_PATH=$HOME/rootfs modules_install

# Узнать версию собранного ядра
$ make kernelversion 
$ make kernelrelease

# Удаление промежуточных файлов сборки
$ make clean
# Полная очистка
$ make distclean

# Запуск Linux kernel в QEMU
$ QEMU_AUDIO_DRV=none qemu-system-arm  -m 256M -nographic -M vexpress-a9 -kernel zImage -dtb vexpress-v2p-ca9.dtb -append "console=ttyAMA0"
```
