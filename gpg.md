#### GPG - утилита шифрования файлов

```
# Зашифровать файл с паролем
$ gpg -c file

# Расшифровать файл с паролем
$ gpg file.gpg

# Сгенерировать публичный и приватный ключи
$ gpg --gen-key

# Список доступных ключей
$ gpg --list-keys

# Установить уровень доверия ключа
$ gpg --edit-key "Eugeny Goryachev"
gpg> trust
5

# Зашифровать файл с ключом
gpg -e -r "Eugeny Goryachev" file

# Расшифровать файл с ключом
$ gpg -d file.gpg
```
