#### gpsd

```bash
# Просмотреть распарсиный вывод NMEA
$ gpsmon /dev/ttyUSB0

# Запускаем GPSD daemon транслировать данные на localhost:2727
$ gpsd -S 2727 /dev/ttyUSB0 9600

# Проверяем приход данных на локальный порт
$ gpsmon localhost:2727
```
