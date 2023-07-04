#### Git


```bash
# Установка
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install git

# Проверка, что установлен
$ git --version

$ git config --global user.name "Jon"                 # данная команда позволяет настраивать Git
$ git config --global user.email "jon@gmail.com"      # данная команда позволяет настраивать Git

$ git init                  # создаёт в директории пустой Git-репозиторий

$ git add .                 # добавляет все непроиндексированные файлы в индекс
$ git add filename          # добавляет файл в индекс
$ git add dirname           # добавляет каталог в индекс

$ git commit -m "Comment"   # записывает изменения в локальный репозиторий
$ git status                # сведения о текущем состоянии репозитория

$ git push                  # отправить локальные коммиты в удалённый репозиторий
$ git pull                  # загрузка свежих данных из удалённого репозитория

$ git clone                 # создание локальной копии удалённого репозитория
$ git merge                 # объединить ветки репозитория

$ git checkout <branch_name>      # переключение между ветками репозитория
$ git checkout -b <new_branch>    # создать новую ветку и переключиться на неё
```
