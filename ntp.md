#### NTP


```bash
$ timedatectl status                         # информация о системном времени
$ timedatectl timesync-status                # информация о NTP 
$ timedatectl list-timezones | column        # список всех часовых поясов из каталога /usr/share/zoneinfo/
$ timedatectl set-timezone Europe/Samara     # установить часовой пояс
$ date                                       # выводит текущую дату и время
```

[Список NTP-серверов:](https://support.ntp.org/Servers/StratumTwoTimeServers)
```
pool.ntp.org
time.apple.com
```

chrony:
- chronyd - демон
- chronyc - инструмент командной строки
В файле /etc/chrony/chrony.conf список NTP-серверов. В конце файла добавить строку и перезапустить сервер времени:
```
$ sudo nano /etc/chrony/chrony.conf

server pool.ntp.org
allow 192.168/16
```
```
# Установка
$ sudo apt install chrony

# на Linux из Buildroot
$ chronyd                       # запуск демона
$ /etc/init.d/chrony start      # запустить chrony
$ /etc/init.d/chrony stop       # остановить chrony
$ /etc/init.d/chrony restart    # перезапустить chrony 

$ chronyc activity          # Статус активности и количество подключенных серверов и пиров
$ chronyc tracking          # показать какой сервер отслеживает chrony
#     Reference ID — идентификатор и имя сервера, с которым компьютер в настоящее время синхронизирован;
#     Stratum — количество переходов к серверу с установленными эталонными часами;
#     Ref time — время по Гринвичу, в которое было выполнено последнее измерение из эталонного источника;
#     System time — задержка системных часов от синхронизированного сервера;
#     Last offset — расчетное смещение последнего обновления часов;
#     RMS offset — долгосрочное среднее арифметическое значения смещения;
#     Frequency — частота, на которой часы системы будут работать неправильно, если хронограф не проведет коррекцию. Она выражена в ppm — ч/м (частей на миллион);
#     Residual freq — остаточная частота указывает на разницу между измерениями от опорного источника и используемой в настоящее время частотой;
#     Skew — расчетная погрешность, связанная с погрешностью частоты;
#     Root delay — суммарная задержка сетевого пути к опорному серверу, с которым синхронизируется компьютер;
#     Leap status — статус скачка (изменения) времени, который может иметь одно из следующих значений:
#         «Normal» – означает нормальную корректировку времени;
#         «Insert second» – означает, что произведена корректировка времени добавлением дополнительной секунды в последнюю минуту текущего месяца;
#         «Delete second» – означает, что произведена корректировка времени удалением дополнительной секунды из последней минуты текущего месяца;
#         «Not synchronised» – означает, что компьютер в данный момент времени не синхронизирован.
$ chronyc sources -v        # список серверов доступных системе
$ chronyc sourcestats -v    # дополнительная статистика каждого сервера
$ sudo chronyc ntpdata 91.189.94.4    # сведения о сервере
$ chronyc offline           # сообщить Chrony, что вы больше не подключены к Интернет
$ chronyc online            # сообщить Chrony, что вы снова подключены к Интернет

$ sudo systemctl status chronyd       # узнать статус демона chronyd
$ service chrony status
$ etc/init.d/chronyd status

$ sudo systemctl restart chronyd      # перезапуск демона chronyd
$ /etc/init.d/chrony restart          # перезапуск сервера времени

$ sudo timedatectl set-ntp true       # синхронизировать сервер


$ sudo chronyc clients                # показать список добавленных клиентов

$ chronyc makestep                    # ручное обновление времени

# Добавить службу в автозапуск
$ systemctl enable chrony             # [On SystemD]
$ chkconfig --add chronyd             # [On Init]

# Остановить chrony
$ systemctl stop chrony               # [On SystemD]
$ /etc/init.d/chronyd stop            # [On Init]
```
gpsd:
```
# Установка
$ sudo apt-get install gpsd
$ sudo apt-get install gpsd-clients

$ sudo gpscat -s 9600 /dev/ttyUSB0       # Просмотреть прямой вывод с устройства (9600 — скорость обмена)
$ sudo gpsmon /dev/ttyUSB0               # Форматный вывод с распарсиванием строки
$ sudo gpsd -S 2727 /dev/ttyUSB0 9600    # Запускаем GPSD daemon транслировать данные на localhost:2727
$ gpsmon localhost:2727                  # Проверяем приход данных на локальный порт

$ gpsd /dev/ttyUSB0                      # запуск демона
$ xgps                                   # запуск клиента GUI
$ cgps                                   # запуск клиента в консоли 

# В конфигурационном файле добавить для автозапуска:
$ nano /etc/default/gpsd

    DEVICES="/dev/ttyUSB0"
    GPSD_OPTIONS="-n"

# перезапуск gpsd
$ systemctl daemon-reload
$ systemctl restart gpsd

$ systemctl status gpsd                # узнать статус gpsd            
```
Эмулятор GPS-сигнала в tty:
```
$ sudo apt install socat

$ socat PIPE PTY,link=/tmp/my_pty,raw,echo=0
    # PIPE — создаёт неименованную трубу между входом и выходом, по сути работает как простой эхо-ответчик
    # PTY — создаёт псевдотерминальное устройство, к которому можно подключиться
    # link=/tmp/my_pty — создаёт ссылку на устройство, к которой можно подключаться, как к устройству, именно его можно указывать в open() при открытии порта.
    # raw,echo=0 — задаёт режим работы псевдотерминала, дабы исключить изменение данных ответа.

$ echo "Hello" > /tmp/my_pty
$ cat  /tmp/my_pty
```

```
# Wireshark - протокол NTP работает на UDP порт 123
udp.dstport == 123
```

