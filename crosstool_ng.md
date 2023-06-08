#### Crosstool-NG


```bash
# Установка
$ sudo apt-get install automake bison chrpath flex g++ git gperf gawk libexpat1-dev libncurses5-dev libsdl1.2-dev libtool python2.7-dev texinfo
# Скачать текущую версию с сайта http://crosstool-ng.org/download/crosstool-ng
$ tar xf crosstool-ng-1.20.0.tar.bz2
$ cd crosstool-ng-1.20.0
$ ./configure --enable-local
$ sudo apt install libtool-bin libtool-doc      # при ошибке: configure: error: Required tool not found: libtool
$ sudo apt install help2man                     # при ошибке
$ make
$ sudo make install

# Показать список всех компиляторов
$ ./ct-ng list-samples

# Показать информацию о компиляторе
$ ./ct-ng show-arm-cortex_a8-linux-gnueabi

# Выбрать компилятор
$ ./ct-ng arm-cortex_a8-linux-gnueabi

# Редактировать конфигурацию
$ ./ct-ng menuconfig

# Собрать компилятор
$ ./ct-ng build
$ PATH=~/x-tools/arm-cortex_a8-linux-gnueabihf/bin:$PATH

# Компиляция программ
$ arm-cortex_a8-linux-gnueabihf-gcc hello.c -o hello

# Узнать тип файла
$ file hello


# Узнать платформу компилятора
$ gcc -dumpmachine 

$ arm-cortex_a8-linux-gnueabihf-gcc --version

$ arm-cortex_a8-linux-gnueabihf-gcc -v
```
Параметры в $ ./ct-ng menuconfig
```
Paths and misc options --->
      [ ] Render the toolchain read-only
Target options --->
      Floating point (hardware(FPU))
C-library --->
      extra config (--enable-obsolete-rpc)
```
В файле ./config заменить текущую версию 'zlib-1.2.12' на 'zlib-1.2.13'
```
$ vi ./config
```

