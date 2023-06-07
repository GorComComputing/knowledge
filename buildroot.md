#### Buildroot


```bash
# Очистка
$ sudo make clean

# Выбор типовой конфигурации ARM для QEMU
$ sudo make qemu_arm_versatile_defconfig
 
# Меню конфигурайии Buildroot
$ sudo make menuconfig
 
# Меню конфигурайии Linux kernel
$ sudo make linux-menuconfig

# Запуск сборки
$ sudo make 
 
```

