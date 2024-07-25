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
$ cargo --version

# Обновление компилятора Rust
$ rustup update

# Удаление компилятора Rust
$ rustup self uninstall

# Компиляция
$ rustc main.rs
$ ./main

# Создание проекта с Cargo
$ cargo new hello_cargo

# Сборка проекта с Cargo
$ cargo build
$ ./target/debug/hello_cargo

# Сборка и запуск одной командой
$ cargo run

# Проверяет код на ошибки без компиляции
$ cargo check

# Сборка релиза (с оптимизацией)
$ cargo build --release
```

```
# Для сборки ядра ОС
$ cargo build -Zbuild-std=core,compiler_builtins --target x86_64-os.json

```
