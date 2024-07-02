#### SCSS

```
# Сначала установите Node.js и npm (если еще не установлены)
$ sudo apt update
$ sudo apt install nodejs npm
# Проверка установки
$ node -v
$ npm -v

# Установка SASS
$ sudo npm install -g sass

# Компиляция SCSS в CSS
$ sass styles.scss styles.css

# Автоматическая компиляция при изменениях
$ sass --watch styles.scss:styles.css
```
Пример файла styles.scss
```
$primary-color: #333;

body {
  font-family: Arial, sans-serif;
  color: $primary-color;
}

.container {
  width: 80%;
  margin: 0 auto;
}
```
