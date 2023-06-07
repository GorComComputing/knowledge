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

# Монтирование файловой систему хоста в QEMU (вводится в QEMU)
$ sshfs -o allow_other,default_permissions <username>@10.0.2.2:<host path> /mnt
 
```

