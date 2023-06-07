#### Buildroot


```bash
# Установка Buildroot
$ git clone git://git.buildroot.net/buildroot
$ cd buildroot
$ git checkout 2023.02.1

# Очистка
$ sudo make clean

# Выбор типовой конфигурации ARM для QEMU
$ sudo make qemu_arm_versatile_defconfig
 
# Меню конфигурайии Buildroot
$ sudo make menuconfig
 
# Запуск сборки
$ sudo make 
$ sudo make -j4	    # количество ядер в процессоре для ускорения сборки

# После сборки бинарные файлы лежат здесь
$ ls output/images

# Меню конфигурайии Linux kernel
$ sudo make linux-menuconfig

# Меню конфигурайии BusyBox
$ sudo make busybox-menuconfig

# Сборка BusyBox
$ sudo make busybox

# Показать список целей
$ sudo make show-targets
```

Установить приглашение ввода [user@hostname]:currentpath$:  
в файле /etc/profile 
```
PS1='[\u@\h]:\w$:'
export PS1

# if [ "$PS1" ]; then
# 	if [ "`id -u`" -eq 0 ]; then
# 		export PS1='# '
# 	else
# 		export PS1='$ '
# 	fi
# fi
```

Для передачи файлов в QEMU:
```
# Параметры конфигурации Buildroot
Target packages -> Filesystem and flash utilities -> sshfs (FUSE)

# Параметры конфигурации Linux kernel
# enable it to be built as an inbuilt module (* instead of M in menuconfig)
File systems -> FUSE (Filesystem in Userspace) support 

# Монтирование файловой системы хоста в QEMU (вводится в QEMU)
$ sshfs -o allow_other,default_permissions <username>@10.0.2.2:<host path> /mnt
```
Параметры процессора:
```
Target options
	-> Target Architecture 			= ARM (little endian)
	-> Target Binary Format 		= ELF
	-> Target Architecture Variant 		= cortex-A7
	-> Target ABI 				= EABIhf
	-> Floating point strategy 		= NEON/VFPv4
	-> ARM instruction set 			= Thumb2
```

