#### Linux iMX6ULL-NANO-2E (Buildroot)


```bash
# Установка Buildroot
$ git clone git://git.buildroot.net/buildroot
$ cd buildroot
$ git checkout 2019.11.1

# Очистка
$ make clean

# Перенести файл с конфигурацией устройства в каталог buildroot/configs
$ sudo cp imx6ullsk_nano_2eth_defconfig.txt /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/configs/imx6ullsk_nano_2eth_defconfig

# Выбор типовой конфигурации для iMX6ULL-NANO-2E
$ make imx6ullsk_nano_2eth_defconfig

# Перенести файл с конфигурацией в каталог buildroot/
$ sudo cp .config /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/.config
 
# Меню конфигурации Buildroot
$ make menuconfig

# Перенести файл с ядром Linux в каталог buildroot/dl/linux/
$ sudo cp linux_imx_4.9.x_1.0.0_ga-sk.tar.bz2 /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/dl/linux/
# Перенести файл с U-Boot в каталог buildroot/dl/u-boot/
$ sudo cp uboot_imx_4.9.x_1.0.0_ga-sk.tar.bz2 /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/dl/uboot/
# Перенести каталог starterkit в каталог buildroot/board/
$ sudo cp -r starterkit /var/lib/lxc/work/rootfs/home/gor/imx6ull-nano-2e/buildroot/board/
$ sudo chown gor board/starterkit
$ mkdir output/images/src
# Перенести файл genimage.cfg.template_imx6 в каталог buildroot/board/freescale/common/imx/
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
```bash
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
```bash
$ make 				# сборка системы
$ make menuconfig 		# запуск меню настроек и состава требуемых пакетов
$ clean 			# очистка системы, ВНИМАНИЕ!!! Полностью удаляется содержимое папки output, что удалит все изменения в исходных кодах и настройки, перед чисткой нужно позаботится об этом.
# Чтобы удалить все продукты сборки (включая каталоги сборки, хост, промежуточные и целевые деревья, образы и цепочку инструментов)
$ make clean			# пересобирает Toolchain

$ make linux-menuconfig 	# запуск конфигуратора ядра Linux
$ make linux-rebuild 		# принудительная сборка ядра Linux
$ make busybox-menuconfig 	# запуск конфигуратора Busybox
$ make busybox-rebuild 		# принудительная сборка Busybox
$ make uboot-menuconfig		# запуск конфигуратора U-boot
$ make uboot-rebuild 		# принудительная сборка загрузчика U-boot
$ make uclibc-menuconfig	# запуск конфигуратора uClibc

$ make busybox			# Сборка BusyBox
$ make show-targets		# Показать список целей
$ make list-defconfigs		# Показать список возможных конфигураций
$ make sdk			# генерирует Toolchain

$ make distclean		# Сброс Buildroot для новой цели. Чтобы удалить все продукты сборки, а также конфигурацию
```
Настройки сети (в файле /etc/network/interfaces закомментировать eth1):
```bash
#auto eth1
#iface eth1 inet static
#	address 192.168.63.136
#	netmask 255.255.255.0
#	gateway 192.168.63.1
```
Добавление своего пакета в Buildroot:
```bash
# В каталоге buildroot/package/ создать каталог нового пакета
$ cd package/
$ mkdir helloARM
$ cd helloARM/

# Создать файл Config.in
$ touch Config.in
$ vi Config.in
# Добавляем в файл:
# Строка bool, help строчка и другая информация метаданных о параметре конфигурации должны быть с отступом в одну табуляцию. Сам текст справки должен иметь отступ в одну табуляцию и два пробела, строки должны быть перенесены так, чтобы вместить 72 столбца, где табуляция соответствует 8, поэтому в самом тексте 62 символа. В тексте справки после пустой строки должен быть указан восходящий URL-адрес проекта.

config BR2_PACKAGE_HELLOARM
        bool "helloARM"
	default y
        help
          This is a comment that explains what helloARM is.

          https://helloARM


# Создать файл helloARM.mk
$ touch helloARM.mk
$ vi helloARM.mk
# Добавляем в файл:

################################################################################
#
# helloARM
#
################################################################################

HELLOARM_VERSION = 0.01
# HELLOARM_SOURCE = helloARM-$(HELLOARM_VERSION).tar.gz
HELLOARM_SITE = package/helloARM/src
HELLOARM_SITE_METHOD = local# Other methods like git,wget,scp,file etc. are also available.
# HELLOARM_INSTALL_STAGING = YES
# HELLOARM_INSTALL_TARGET = YES
# HELLOARM_DEPENDENCIES = host-pkgconf

define HELLOARM_BUILD_CMDS
    $(MAKE) CC="$(TARGET_CC)" LD="$(TARGET_LD)" -C $(@D)
endef

define HELLOARM_INSTALL_TARGET_CMDS
    $(INSTALL) -D -m 0755 $(@D)/helloARM  $(TARGET_DIR)/usr/bin
    $(INSTALL) -D -m 0755 $(@D)/helloGO  $(TARGET_DIR)/usr/bin
endef

$(eval $(generic-package))



# В файл package/Config.in добавить пункт меню в раздел Target packages (после busybox):

menu "Target packages"

        source "package/helloARM/Config.in"


# В каталоге buildroot/package/helloARM/ создать каталог для исходных кодов
$ mkdir package/helloARM/src
$ cd package/helloARM/src/

# В каталоге buildroot/package/helloARM/src/ можно создавать файлы с исходными кодами
# ... например, на C
$ touch helloARM.c
$ vi helloARM.c

#include <stdio.h>
int main(void) {
	printf("Hello C ARM\n");
}

# ... или, например, на Go
$ touch helloGO.go
$ vi helloGO.go

package main
import "fmt"
func main() {
    fmt.Println("Hello Go ARM")
}


# Установка компилятора Go
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install golang git
$ go env -w GO111MODULE=off
# Проверка работы Go (по умолчанию Go находится в каталоге /bin/)
$ go version


# В этом же каталоге buildroot/package/helloARM/src/ добавить Makefile
$ touch Makefile
$ vi Makefile


#CC=/home/gor/imx6ull-nano-2e/buildroot/output/host/usr/bin/arm-buildroot-linux-uclibcgnueabihf-gcc
#GO=/bin/go

.PHONY: clean
.PHONY: all

all: helloARM helloGO

helloARM: helloARM.c
        $(CC) -o $@ $<

helloGO: *.go deps
        GOOS=linux GOARCH=arm go build -o $@ $<

clean:
        rm -f helloARM
        rm -f helloGO

.PHONY:deps
deps:
	#go get github.com/gorilla/sessions




# Можно пробовать запускать сборку Buildroot
$ make menuconfig
$ make -j4

# После сборки скомпилированные бинарные файлы новго пакета будут лежать в корневой файловой системе Linux в каталоге /usr/bin/
```

Управление GPIO
```bash
# Формула определение номера пина GPIO в Linux
# linux gpio number = (gpio_bank – 1) * 32 + gpio_bit

# Включить 1 на пине 51
$ echo 51 > /sys/class/gpio/export
$ echo out > /sys/class/gpio/gpio51/direction 	# задает направление in\out 
$ echo 1 > /sys/class/gpio/gpio51/value

# Прочитать pin 51
$ cd /sys/class/gpio/
$ echo 51 > export
$ cat /sys/class/gpio/gpio51/value
```
Добавить скрипт в автозагрузку Linux
```bash
# Создать фал скрипта в директории /etc/init.d/ (touch)
# Задать скрипту права на выполнение (chmod +x)
# Добавить ссылку на скрипт в директорию /etc/rc.d (ln -s)
```
