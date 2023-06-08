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

# Узнать версию собранного ядра
$ make kernelversion 
$ make kernelrelease
```
