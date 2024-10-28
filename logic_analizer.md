#### Logic Analizer

```
# Установка Logic Analizer
# Скачать с сайта 
$ chmod +x Logic-<версия>.AppImage

# Если не установлена библиотека libfuse2, установить
$ sudo apt update
$ sudo apt install libfuse2

# Запуск
$ ./Logic-2.4.14-linux-x64.AppImage --no-sandbox
```
Файл запуска Logic Analizer
```
#!/bin/bash
./Logic-2.4.14-linux-x64.AppImage --no-sandbox
```
