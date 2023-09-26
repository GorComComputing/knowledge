#### Tcl

```bash
# Узнать, где лежит программа tclsh
$ which tclsh

$ chmod +x hello.tcl

```
Пример скрипта на Tcl:
```tcl
#!/usr/bin/tclsh
# hello.tcl
puts "Hello, world"
```
Команды Tcl:
```tcl
# Печатает строку
% puts "Hello, world"

# Вычисляет выражение
% expr 3+2

# Выполняет команду bash
% exec ls

# Перейти в каталог
% cd ..

# [] передать в качестве параметра
% puts [exec ls]
```
