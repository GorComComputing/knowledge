#### Crosstool-NG


```bash
# Установка
$ sudo apt-get install automake bison chrpath flex g++ git gperf gawk libexpat1-dev libncurses5-dev libsdl1.2-dev libtool python2.7-dev texinfo
$ tar xf crosstool-ng-1.20.0.tar.bz2
$ cd crosstool-ng-1.20.0
$ ./configure --enable-local
$ make
$ make install

# Показать список всех компиляторов
$ ./ct-ng list-samples

# Показать информацию о компиляторе
$ ./ct-ng show-arm-cortex_a8-linux-gnueabi

# Выбрать компилятор
$ ./ct-ng arm-cortex_a8-linux-gnueabi

# Редактировать конфигурацию
$ ./ct-ng menuconfig

#Собрать компилятор
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
