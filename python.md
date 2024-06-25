Установка python:
```
$ sudo apt-get install python3
# Проверка установки python
$ python3 --version

# Установка пакетного менеджера
$ sudo apt install python3-pip

$ sudo pip3 install ipython
# Проверка установки ipython
$ python3 -m pip show ipython
$ ipython --version
```
Python
```
$ python3
>>> exit()
```
Выполнение сценария Python:
```
$ touch hello.py
$ vi hello.py
$ python3 hello.py
```
IPython
```
$ ipython
In [1]: exit()
```
Jupiter Notebook
```
$ sudo pip3 install jupyter
$ jupyter notebook
$ jupyter notebook password

# Сервер запустится по адресу
# https://localhost:8888/tree
```
requirements.txt
```
# Создание файла с зависимостями проекта requirements.txt
$ pip freeze > requirements.txt

# Установка модулей из файла requirements.txt
$ pip install -r requirements.txt

# Обновить компоненты вместо их повторной установки
$ pip install -U -r requirements.txt

# Выводит список устаревших пакетов
$ pip list --outdated

# Обновивить пакет по его имени (PackageName)
$ pip install -U PackageName
```
