#### MySQL


```bash
# Установка
$ sudo apt-get update
$ sudo apt-get install mysql-server

# Задать пароль для root (mysql888)
$ sudo mysqladmin password -u root -p

# Конфигурирование (на вопрос о смене пароля - No, остальные - Yes)
$ sudo mysql_secure_installation

# Запуск консольного клиента (-p с паролем)
$ mysql -u root -p
$ mysql -u root -h 192.168.63.60 -p

# Выход
mysql> exit;

# Показать существующие базы
mysql> show databases;

# Создать базу
mysql> CREATE DATABASE my_tst;

# Создание пользователя
mysql> CREATE USER 'user'@'%' IDENTIFIED BY 'password';
# Выдать пользователю полные права на базу 
mysql> GRANT ALL PRIVILEGES ON my_tst.* TO 'user'@'%' WITH GRANT OPTION;

# Выбрать базу 
mysql> use my_tst;

# Удалить базу
mysql> drop database my_tst;

# Удалить mysql
$ sudo apt remove mysql-server mysql-client
# Удалить полностью mysql
$ sudo apt purge mysql-server mysql-client




```
