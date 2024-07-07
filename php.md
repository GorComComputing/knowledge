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
Composer
```
# Установка
$ php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
# Проверка хэша установочного файла
# Замените 'expected-hash-value' на актуальное значение
$ php -r "if (hash_file('sha384', 'composer-setup.php') === 'expected-hash-value') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

# Запуск установки
$ sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer

# Удаление установочного файла
$ php -r "unlink('composer-setup.php');"

# Проверка установки Composer
$ composer --version

# Создание проекта
# Создать файл composer.json, затем выполнить команду
$ composer install
```
composer.json
```
{
    "require": {
        "monolog/monolog": "^2.3"
    }
}
```
