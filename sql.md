#### SQL


```SQL
--Комментарий
# DDL: CREATE, ALTER, DROP
# DML: SELECT, INSERT, UPDATE, DELETE
SELECT au_fname, au_lname FROM authors;
SELECT au_fname, au_lname FROM authors WHERE state = 'NY' ORDER BY au_lname;

--Выбрать данные
SELECT columns
  FROM tables
  [JOIN joins]
  [WHERE search_condition]
  [GROUP BY grouping_columns]
  [HAVING search_condition]
  [ORDER BY sort_columns]
```
