#### AVR
Программа на C, котора мигает светодиодом
```
#include <avr/io.h>
#include <util/delay.h>

int main(void) {
    // Устанавливаем PB5 (пин 13 на Arduino Uno) как выход
    DDRB |= (1 << PB5);

    while (1) {
        // Включаем светодиод
        PORTB |= (1 << PB5);
        _delay_ms(500);

        // Выключаем светодиод
        PORTB &= ~(1 << PB5);
        _delay_ms(500);
    }

    return 0;
}
```

Makefile
```
# Название проекта (имя выходного .hex файла)
PROJECT = blink

# Путь к исходным файлам
SRC = $(PROJECT).c

# Модель микроконтроллера
MCU = atmega328p

# Тактовая частота микроконтроллера (Гц)
F_CPU = 16000000UL

# Флаги компиляции
CFLAGS = -mmcu=$(MCU) -DF_CPU=$(F_CPU) -Os

# Флаги линковщика
LDFLAGS = -mmcu=$(MCU)

# Порт и программатор для avrdude
PORT = /dev/ttyACM0
PROGRAMMER = arduino
BAUD = 115200

# Цели сборки

all: $(PROJECT).hex

# Компиляция
$(PROJECT).elf: $(SRC)
	avr-gcc $(CFLAGS) -o $@ $^

# Создание .hex файла
$(PROJECT).hex: $(PROJECT).elf
	avr-objcopy -O ihex -R .eeprom $< $@

# Загрузка прошивки в микроконтроллер
flash: $(PROJECT).hex
	avrdude -c $(PROGRAMMER) -p $(MCU) -P $(PORT) -b $(BAUD) -U flash:w:$(PROJECT).hex

# Очистка временных файлов
clean:
	rm -f $(PROJECT).elf $(PROJECT).hex

# Файлы зависимостей
.PHONY: all flash clean
```

```
# Подключить расширенный репозиторий
$ sudo add-apt-repository universe
$ sudo apt-get update

# Установить пакет avr-gcc 
$ sudo apt-get install avr-gcc avr-libc

# Установить avrdude, чтобы загрузить прошивку на микроконтроллер
$ sudo apt-get install avrdude
```

```
# Компиляция
$ avr-gcc -mmcu=atmega328p -Os -o blink.elf blink.c

# Создайте файл в формате Intel HEX, который будет загружен в микроконтроллер
$ avr-objcopy -O ihex -R .eeprom blink.elf blink.hex

# Используйте avrdude для загрузки программы
$ avrdude -c arduino -p m328p -P /dev/ttyACM0 -b 115200 -U flash:w:blink.hex
```
