#### Библиотеки C++

CivetWeb - для создания web-сервера
```
# Установка
$ git clone https://github.com/civetweb/civetweb.git
$ cd civetweb
$ mkdir build1
$ cd build1
$ cmake ..
$ make
$ sudo make install

# Пример компиляции с использованием библиотеки CivetWeb
$ g++ -std=c++11 -o myserver main.cpp -lcivetweb
```
