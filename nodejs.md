#### Node.js

```
# Установка nodejs и npm
$ sudo apt update
$ sudo apt install nodejs npm

# Проверка работоспособности
$ node -v
$ npm -v
```


```bash

# Установка
$ sudo rm -rf /usr/local/bin/npm /usr/local/share/man/man1/node* ~/.npm sudo rm -rf /usr/local/lib/node* sudo rm -rf /usr/local/bin/node* sudo rm -rf /usr/local/include/node*
$ sudo apt-get purge nodejs npm
$ sudo apt autoremove

# Скачать последний tar.xz NodeJS файл с https://nodejs.org/en/download/
$ cd ~/Загрузки

# Где #.#.# это номер скачанной версии
$ tar -xf node-v#.#.#-linux-x64.tar.xz
$ sudo mv node-v#.#.#-linux-x64/bin/* /usr/local/bin/
$ sudo mv node-v#.#.#-linux-x64/lib/node_modules/ /usr/local/lib/

# Закрыть терминал и открыть новый
# Проверка работоспособности
$ node -v
$ npm -v

# создать проект Create React
$ npm install -g create-react-app

# Создать новый проект в выбранном каталоге
$ create-react-app helloworld
$ cd helloworld

# установить React Router
$ npm i react-router-dom --save

# Запуск web-сервера и проверка приложения
$ npm start        

# Сборка проекта
$ npm run build

```         
