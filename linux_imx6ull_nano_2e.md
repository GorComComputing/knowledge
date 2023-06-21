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
$ sudo cp uboot_imx_4.9.x_1.0.0_ga-sk.tar.bz2 /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/dl/uboot/
# перенести каталог starterkit в каталог buildroot/board/
$ sudo cp -r starterkit /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/board/
$ sudo chown gor board/starterkit
$ mkdir output/images/src
# перенести файл genimage.cfg.template_imx6 в каталог buildroot/board/freescale/common/imx/
$ sudo cp -r freescale/common/imx/genimage.cfg.template_imx6 /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/board/freescale/common/imx/

# Запуск сборки
$ make -j4	    # количество ядер в процессоре для ускорения сборки

# После сборки бинарные файлы лежат здесь
$ ls output/images/

# Для обновления корневой файловой системы или ядра Linux на модуле SK-iMX6ULL-NANO-2E, необходимо скопировать файлы output/images/rootfs.tar и output/images/u-boot.imx в mfgtools\Profiles\Linux\OS Firmware\files\ 
# Замкните между собой контакты посадочного места J1 на самом модуле (это необходимо только на этапе сброса или включения питания), подключите USB кабель к разъему X7.
# Windows должна обнаружить новое HID устройство (установка дополнительных драйверов не требуется).
# Запустите MfgTool2.exe
# Нажмите кнопку «Start», в консоли будет отображаться рабочий процесс, после завершения отключите-включите питание или нажмите кнопку “RESET” (J1 должен быть разомкнут).
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
Параметры процессора для SK-iMX6ULL-NANO-2E:
```
Target options
	-> Target Architecture 			= ARM (little endian)
	-> Target Binary Format 		= ELF
	-> Target Architecture Variant 		= cortex-A7
	-> Target ABI 				= EABIhf
	-> Floating point strategy 		= NEON/VFPv4
	-> ARM instruction set 			= Thumb2
```
Основные команды Buildroot:
```
$ make 				# сборка системы
$ make menuconfig 		# запуск меню настроек и состава требуемых пакетов
$ clean 			# очистка системы, ВНИМАНИЕ!!! Полностью удаляется содержимое папки output, что удалит все изменения в исходных кодах и настройки, перед чисткой нужно позаботится об этом.
$ make linux-menuconfig 	# запуск конфигуратора ядра Linux
$ make linux-rebuild 		# принудительная сборка ядра Linux
$ make busybox-menuconfig 	# запуск конфигуратора Busybox
$ make busybox-rebuild 		# принудительная сборка Busybox
$ make uboot-rebuild 		# принудительная сборка загрузчика U-boot

$ make busybox			# Сборка BusyBox
$ sudo make show-targets	# Показать список целей
$ sudo make list-defconfigs	# Показать список возможных конфигураций
```
Настройки сети:
```
В файле /etc/network/interfaces закомметировать eth1:

#auto eth1
#iface eth1 inet static
#	address 192.168.63.136
#	netmask 255.255.255.0
#	gateway 192.168.63.1
```

