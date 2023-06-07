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

Для передачи файлов в QEMU:
```
# Параметры конфигурации Buildroot
Target packages -> Filesystem and flash utilities -> sshfs (FUSE)

# Параметры конфигурации Linux kernel
# enable it to be built as an inbuilt module (* instead of M in menuconfig)
File systems -> FUSE (Filesystem in Userspace) support 

# Монтирование файловой систему хоста в QEMU (вводится в QEMU)
$ sshfs -o allow_other,default_permissions <username>@10.0.2.2:<host path> /mnt
```

