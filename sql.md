#### SQL


```SQL
-- Комментарий
-- DDL: CREATE, ALTER, DROP
-- DML: SELECT, INSERT, UPDATE, DELETE

-- Выбрать данные
SELECT columns
  FROM tables
  [JOIN joins]
  [WHERE search_condition]
  [GROUP BY grouping_columns]
  [HAVING search_condition]
  [ORDER BY sort_columns]

SELECT au_fname, au_lname FROM authors;
SELECT au_fname, au_lname FROM authors WHERE state = 'NY' ORDER BY au_lname;
SELECT * FROM authors;

-- Создание псевдонимов столбцов (AS)
SELECT au_fname AS "First name",
       au_lname AS "Last name",
       city AS "City",
       state,
       zip AS "Postal code"
  FROM authors;

-- Удаление повторяющихся строк (DISTINCT)
SELECT DISTINCT state
  FROM authors;

-- Сортировка по одному столбцу
SELECT columns
  FROM table
  ORDER BY sort_column [ASC | DESC];

-- Сортировка по нескольким столбцам
SELECT columns
  FROM table
  ORDER BY sort_column1 [ASC | DESC],
           sort_column2 [ASC | DESC],
           sort_column3 [ASC | DESC],
           sort_columnN [ASC | DESC];

-- Сортировка по нескольким столбцам по номеру столбца
SELECT au_fname, au_lname, city, state
  FROM authors
  ORDER BY 4 ASC,
           2 DESC;

-- Результат выражения в столбце price * sales AS "Revenue"
SELECT title_id, price, sales, price * sales AS "Revenue"
  FROM titles
  ORDER BY "Revenue" DESC;

-- Условие (WHERE)
SELECT columns
  FROM table
  WHERE test_column op value;

SELECT au_id, au_fname, au_lname
  FROM authors
  WHERE au_lname <> 'Hull';

SELECT title_name, price * sales AS 'Revenue'
  FROM titles
  WHERE price * sales > 1000000;

-- Комбинирование условий с помощью AND, OR, NOT
SELECT title_name, type, price
  FROM titles
  WHERE type = 'biography' AND price < 20;

SELECT title_id, type, price
  FROM titles
  WHERE NOT type = 'biography' AND NOT price < 20;

-- Скобки изменяют приоритет
SELECT title_name, sales, price
  FROM titles
  WHERE NOT (price < 20) AND (sales > 15000);

-- Сравнение по шаблону (LIKE)
SELECT columns
  FROM table
  WHERE test_column [NOT] LIKE 'pattern';

-- Сравнение по шаблону (BETWEEN)
SELECT columns
  FROM table
  WHERE test_column [NOT] BETWEEN low_value AND high_value;

SELECT title_id, price
  FROM titles
  WHERE price BETWEEN 10 AND 19.95;

-- Фильтрация (с помощью IN)
SELECT columns
  FROM table
  WHERE test_column [NOT] IN (value1, value2,…);

SELECT au_fname, au_lname, state
  FROM authors
  WHERE state NOT IN ('NY', 'NJ', 'CA');

-- Проверка на null
SELECT columns
  FROM table
  WHERE test_column IS [NOT] NULL;

-- Создание произвольного столбца равного 5
SELECT 2 + 3;

SELECT au_id, 2 + 3
  FROM authors;

-- Объединение строк ( с помощью ||)
SELECT au_fname || ' ' || au_lname AS "Author name"
  FROM authors
  ORDER BY au_lname ASC, au_fname ASC;

-- Объединение строк в условии ( с помощью ||)
SELECT au_id, au_fname, au_lname
  FROM authors
  WHERE au_fname || ' ' || au_lname = 'Klee Hull';

-- Преобразование типа к символьному CAST(sales AS CHAR(7))
SELECT CAST(sales AS CHAR(7)) || ' copies sold of title ' || title_id AS "Biography sales"
  FROM titles
  WHERE type = 'biography' AND sales IS NOT NULL
  ORDER BY sales DESC;

-- Переключение регистра символов (LOWER, UPPER)
SELECT LOWER(au_fname) AS "Lower", UPPER(au_lname) AS "Upper"
  FROM authors;

-- Удаление пробелов (в начале, в конце, оба)
SELECT '<' || ' AAA ' || '>' AS "Untrimmed",
       '<' || TRIM(LEADING FROM ' AAA ') || '>' AS "Leading",
       '<' || TRIM(TRAILING FROM ' AAA ') || '>' AS "Trailing",
       '<' || TRIM(' AAA ') || '>' AS "Both";

-- Удаляет первый символ H
SELECT au_lname, TRIM(LEADING 'H' FROM au_lname) AS "Trimmed name"
  FROM authors;

-- Определение длины строки с помощью CHARACTER_LENGTH(au_fname) 
SELECT au_fname, CHARACTER_LENGTH(au_fname) AS "Len"
  FROM authors;

-- Поиск в строке и вывод номера позиции в строке
SELECT au_fname, POSITION('e' IN au_fname) AS "Pos e", au_lname, POSITION('ma' IN au_lname) AS "Pos ma"
  FROM authors;

-- Вставка строк
INSERT INTO table
  VALUES(value1, value2, …, valueN);

INSERT INTO authors
  VALUES('A08', 'Michael', 'Polk', '512-953-1231', '4028 Guadalupe St', 'Austin', 'TX', '78701');

-- Вставка строк с помощью названий столбцов
INSERT INTO table
  (column1, column2, …, columnN)
  VALUES(value1, value2, …, valueN);

INSERT INTO authors
  (au_id, au_fname, au_lname, phone, address, city, state, zip)
  VALUES('A09', 'Irene', 'Bell', '415-225-4689', '810 Throckmorton Ave', 'Mill Valley', 'CA', '94941');

-- Вставка строк из другой таблицы
INSERT INTO publishers
  SELECT pub_id, pub_name, city, state, country
    FROM new_publishers
    WHERE city = 'Los Angeles';

INSERT INTO publishers
  (pub_id, pub_name, city, state, country)
  SELECT pub_id, pub_name, city, state, country
    FROM new_publishers
    WHERE country <> 'USA';

INSERT INTO publishers
  (pub_id, pub_name, city, state, country)
  SELECT *
    FROM new_publishers
    WHERE pub_name = 'XXX';

-- Изменение строк
UPDATE table
  SET column = expr
  [WHERE search_condition];

UPDATE titles
  SET contract = 0;

UPDATE titles
  SET price = price * 2.0
  WHERE type = 'history';

UPDATE titles
  SET sales = sales * 0.5
  WHERE sales >
    (SELECT AVG(sales)
      FROM titles);

-- Удаление строк
DELETE FROM table
  [WHERE search_condition];

-- Удаление всех строк
DELETE FROM royalties;

DELETE FROM authors
  WHERE au_lname = 'Hull';

-- Создание таблицы
CREATE TABLE titles
  (
  title_id CHAR(3),
  title_name VARCHAR(40),
  type VARCHAR(10),
  pub_id CHAR(3),
  pages INTEGER,
  price DECIMAL(5,2)
  sales INTEGER,
  pubdate DATE,
  contract SMALLINT
  );

-- Создание таблицы и запрет нулевого значения (NOT NULL)
CREATE TABLE authors
  (
  au_id CHAR(3) NOT NULL,
  au_fname VARCHAR(15) NOT NULL,
  au_lname VARCHAR(15) NOT NULL,
  phone VARCHAR(12) NULL,
  address VARCHAR(20) NULL,
  city VARCHAR(15) NULL,
  state CHAR(2) NULL,
  zip CHAR(5) NULL
  );

-- Присвоение значения по умолчанию (DEFAULT)
CREATE TABLE titles
  (
  title_id CHAR(3) NOT NULL,
  title_name VARCHAR(40) NOT NULL DEFAULT '',
  type VARCHAR(10) NULL DEFAULT 'undefined',
  pub_id CHAR(3) NOT NULL,
  pages INTEGER DEFAULT NULL,
  price DECIMAL(5,2) NOT NULL DEFAULT 0.00,
  sales INTEGER NULL,
  pubdate DATE NULL DEFAULT CURRENT_DATE,
  contract SMALLINT NOT NULL DEFAULT (3 * 7) - 21
  );

-- Задание первичного ключа (PRIMARY KEY)
CREATE TABLE publishers
  (
  pub_id CHAR(3) PRIMARY KEY,
  pub_name VARCHAR(20) NOT NULL,
  city VARCHAR(15) NOT NULL,
  state CHAR(2) NULL,
  country VARCHAR(15) NOT NULL
  );
















```
