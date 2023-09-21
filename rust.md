#### Rust

```
# Установка компилятора Rust
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh

# При ошибке
# curl: (23) Failure writing output to destination
$ sudo snap remove curl
$ sudo apt-get install curl

# Проверка установки
$ rustc --version

# Обновление компилятора Rust
$ rustup update

# Удаление компилятора Rust
$ rustup self uninstall
```
