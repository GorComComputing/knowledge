#### Linux iMX6ULL-NANO-2E (Buildroot)


```bash
# Установка Buildroot
$ git clone git://git.buildroot.net/buildroot
$ cd buildroot
$ git checkout 2019.11.1

# Очистка
$ make clean

# перенести файл с конфигурацией устройства в каталог buildroot/configs
$ sudo cp imx6ullsk_nano_2eth_defconfig.txt /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/configs/imx6ullsk_nano_2eth_defconfig

# Выбор типовой конфигурации для iMX6ULL-NANO-2E
$ make imx6ullsk_nano_2eth_defconfig

# перенести файл с конфигурацией устройства в каталог buildroot/
$ sudo cp .config /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/.config
 
# Меню конфигурации Buildroot
$ make menuconfig

# перенести файл с ядром Linux в каталог buildroot/dl/linux/
$ sudo cp linux_imx_4.9.x_1.0.0_ga-sk.tar.bz2 /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/dl/linux/
# перенести файл с U-Boot в каталог buildroot/dl/u-boot/
$ sudo cp uboot_imx_4.9.x_1.0.0_ga-sk.tar.bz2 /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/dl/u-boot/
 
# Запуск сборки
$ make -j4	    # количество ядер в процессоре для ускорения сборки

# После сборки бинарные файлы лежат здесь
$ ls output/images

# Запуск Linux после сборки в QEMU
$ cd output/images
$ sudo ./start-qemu.sh

# Меню конфигурайии Linux kernel
$ sudo make linux-menuconfig

# Меню конфигурайии BusyBox
$ sudo make busybox-menuconfig

# Сборка BusyBox
$ sudo make busybox

# Показать список целей
$ sudo make show-targets

# Показать список возможных конфигураций
$ sudo make list-defconfigs
```

Установить приглашение ввода [user@hostname]:currentpath$:  
в файле /etc/profile 
```
PS1='\u@\h:\w$'
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

Основные команды:
```
$ make 				# сборка системы
$ make menuconfig 		# запуск меню настроек и состава требуемых пакетов
$ clean 			# очистка системы, ВНИМАНИЕ!!! Полностью удаляется содержимое папки output, что удалит все изменения в исходных кодах и настройки, перед чисткой нужно позаботится об этом.
$ make linux-menuconfig 	# запуск конфигуратора ядра Linux
$ make linux-rebuild 		# принудительная сборка ядра Linux
$ make busybox-menuconfig 	# запуск конфигуратора Busybox
$ make busybox-rebuild 		# принудительная сборка Busybox
$ make uboot-rebuild 		# принудительная сборка загрузчика U-boot
```

