#### PostgreSQL


```bash
# Установка
$ sudo apt update
$ sudo apt -y install postgresql

# Переключение на пользователя postgres
$ sudo -i -u postgres

# Запуск PostgreSQL
$ psql
# Посмотреть информацию о саединении
postgres=# \conninfo
# Выход
postgres=# \q

# Создание пользователя
$ createuser --interactive

# Создание базы данных
$ createdb alex

# Для подключения к базе нужно зайти в пользователя
$ sudo su - alex

# Запуск PostgreSQL
$ psql
# Можно выбрать другую базу при запуске
$ psql -d postgres

# Создание таблицы
postgres=# CREATE TABLE имя_таблицы (имя_колонки1 тип_колонки (длина) ограничения, имя_колонки2 тип_колонки (длина), имя_колонки3 тип_колонки (длина));

postgres=# CREATE TABLE playground (equip_id serial PRIMARY KEY, type varchar (50) NOT NULL, color varchar (25) NOT NULL, location varchar(25) check (location in ('north', 'south', 'west', 'east', 'northeast', 'southeast', 'southwest', 'northwest')), install_date date );

postgres=# create table users (Id serial primary key, Name character varying(30), Age integer);

# Отобразить таблицы
postgres=# \dt

# Подключение к базе 
postgres=# \c test2
# Создание базы
postgres=# create database test2;

# Запросы
postgres=# insert into users (Name, Age) values ('Tom', 33);
postgres=# select * from users;
postgres=# DELETE FROM objects WHERE id = 4;

# Выгрузка базы в файл
$ pg_dump -U username -f backup.dump database_name -Fc
# Восстановленеи базы из файла
$ pg_restore -U username -d dbname -1 filename.dump

# Изменение пароля пользователя
postgres=# ALTER ROLE postgres WITH PASSWORD 'postgres';
```
Установка PostgreSQL на OpenWrt
```bash
# Установка
$ opkg update
$ opkg install pgsql-server pgsql-cli
$ uci set postgresql.config.PGDATA=/overlay/Embd_linux/data/pgsql/data
$ uci set postgresql.config.PGLOG=/overlay/Embd_linux/data/pgsql/data/pgsql.log
$ uci commit postgresql

# Инициализация базы
$ mkdir -p /overlay/Embd_linux/data/pgsql/data
$ chown postgres  /overlay/Embd_linux/data/pgsql/data
$ sed -i "s|/var/run/postgres:/bin/false|/var/run/postgres:/bin/sh|" /etc/passwd
$ mkdir -p /var/run/postgres
$ ./busybox su - postgres
$ LC_COLLATE="C" initdb --pwprompt -D /overlay/Embd_linux/data/pgsql/data/
$ exit

# Запуск Postgres
$ /etc/init.d/postgresql start

# Создание базы данных
$ createdb db_name
$ psql -d template1 -U postgres
template1=# \q
```
