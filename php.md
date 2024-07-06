#### PHP
```
# Установка
$ sudo apt update
$ sudo apt install php

# Проверка установки
$ php -v

# Запуск веб-сервера
$ php -S localhost:8000

# Запуск в терминале
$ php index.php
```
index.php
```
<?php
echo "Hello, World!";
echo "<br>";
echo "Current date and time: " . date('Y-m-d H:i:s');
?>
```
