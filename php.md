#### PHP
```
# Установка
$ sudo apt update
$ sudo apt install php php-pgsql

# Проверка установки
$ php -v

# Запуск веб-сервера
$ php -S localhost:8000

# Запуск в терминале
$ php script.php John 25
```
index.php
```
<?php
echo "Hello, World!";
echo "<br>";
echo "Current date and time: " . date('Y-m-d H:i:s');
?>
```
script.php
```
<?php
if ($argc != 3) {
    echo "Usage: php script.php <name> <age>\n";
    exit(1);
}

$name = $argv[1];
$age = $argv[2];

echo "Hello, my name is $name and I am $age years old.\n";
?>
```
