#### Node.js



```bash
# Установка
$ sudo apt update
$ sudo apt install nodejs
$ sudo apt install npm

# Проверка работоспособности
$ nodejs -v
$ npm -v

# создать проект Create React
$ npm install -g create-react-app

# Фикс ошибки с версией
$ npm cache clean -f 
$ sudo npm install -g n
$ sudo n latest

# Создать новый проект в выбранном каталоге
$ create-react-app helloworld
$ cd helloworld
$ npm start        # проверка приложения

# Eще фикс ошибки (Cannot find module 'semver')
$ sudo apt-get remove nodejs
$ sudo apt-get remove npm
$ sudo rm -rf ~/.npm
$ sudo rm -rf /usr/local/lib/node_modules
$ curl -0 -L https://npmjs.org/install.sh | sudo sh
```         
