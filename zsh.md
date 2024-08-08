#### Zsh
```
# Установка
$ sudo apt update
$ sudo apt install zsh

# Проверка установки
$ zsh --version

# Установите Oh My Zsh
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Сделайте Zsh оболочкой по умолчанию
$ chsh -s $(which zsh)

# Установите Powerlevel10k
$ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
# Установить шрифты Nerd Fonts
$ sudo apt install fonts-powerline

# Откройте файл ~/.zshrc и замените строку с темой на
# ZSH_THEME="powerlevel10k/powerlevel10k"
$ nano ~/.zshrc
```
Перенос путей PATH из Bash
```
# Перенос путей - скопировать подобные строки 
$ nano ~/.bashrc

export PATH=$PATH:/usr/local/go/bin
export PATH=$PATH:$HOME/.local/bin:$HOME/bin

$ nano ~/.zshrc

# Чтобы изменения вступили в силу
$ source ~/.zshrc

# Если нужен еще раз конфигуратор
$ p10k configure
```
Разделение истории для каждой вкладки
```
# Отключить мгновенную запись истории команд
$ unsetopt share_history

# Сохранение истории при выходе из оболочки
$ setopt append_history

# Чтение истории при запуске
$ setopt inc_append_history

```
