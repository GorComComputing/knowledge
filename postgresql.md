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
\conninfo
# Выход
\q

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
CREATE TABLE имя_таблицы (имя_колонки1 тип_колонки (длина) ограничения, имя_колонки2 тип_колонки (длина), имя_колонки3 тип_колонки (длина));

CREATE TABLE playground (equip_id serial PRIMARY KEY, type varchar (50) NOT NULL, color varchar (25) NOT NULL, location varchar(25) check (location in ('north', 'south', 'west', 'east', 'northeast', 'southeast', 'southwest', 'northwest')), install_date date );

# Отобразить таблицы
\dt


```
