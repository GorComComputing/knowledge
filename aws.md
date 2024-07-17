#### AWS S3
```
# Установка AWS CLI
$ sudo apt update
$ sudo apt install unzip

# Скачайте последний пакет AWS CLI
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$ unzip awscliv2.zip
$ sudo ./aws/install

# Проверьте установку
$ aws --version
```
```
# Настройка AWS CLI
$ aws configure

Вам будут заданы следующие вопросы:

    AWS Access Key ID [None]: Введите ваш Access Key ID.
    AWS Secret Access Key [None]: Введите ваш Secret Access Key.
    Default region name [None]: Введите ваш регион (например, us-east-1).
    Default output format [None]: Введите формат вывода (например, json).
```
```
# Создание нового бакета
$ aws s3 mb s3://my-new-bucket

# Загрузка файла в бакет
$ aws s3 cp myfile.txt s3://my-new-bucket/

# Скачивание файла из бакета
$ aws s3 cp s3://my-new-bucket/myfile.txt ./myfile.txt

# Список всех бакетов
$ aws s3 ls

# Список файлов в бакете
$ aws s3 ls s3://my-new-bucket

# Удаление файла из S3
$ aws s3 rm s3://my-new-bucket/myfile.txt
```
