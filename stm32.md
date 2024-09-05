#### STM32

```
# Установка ARM GCC Toolchain
$ sudo apt install gcc-arm-none-eabi

# Установка OpenOCD: Это инструмент для прошивки микроконтроллеров STM32 через отладочные интерфейсы (например, ST-Link).
$ sudo apt install openocd

# Установка st-link: для взаимодействия с программой ST-Link, используемой для загрузки прошивки
$ sudo apt install stlink-tools

# Библиотеки STM32 и HAL: 
# Библиотеки аппаратной абстракции (HAL) для работы с периферией микроконтроллера. 
# Их можно найти на официальном сайте STM32CubeF4 или установить с помощью STM32CubeMX.
# 

```

```
# Сборка прошивки
$ make

# Прошивка
$ st-flash write blink.bin 0x8000000
```
Makefile:
```
# Binary firmware name
FW_NAME = blinky

# Source code file
SRCS = main.c

# Libraries
STM32F4_LIB_DIR = ./STM32F4_DISC_LIB

# Compilers
CC = arm-none-eabi-gcc
OBJCOPY = arm-none-eabi-objcopy

# Config file and startup script
SRCS += $(STM32F4_LIB_DIR)/system_stm32f4xx.c
SRCS += $(STM32F4_LIB_DIR)/Libraries/CMSIS/ST/STM32F4xx/Source/Templates/TrueSTUDIO/startup_stm32f4xx.s

# Compiler flags
CFLAGS = -g -O2 -Wall
CFLAGS += -mlittle-endian -mthumb -mcpu=cortex-m4 -mthumb-interwork
CFLAGS += -mfloat-abi=hard -mfpu=fpv4-sp-d16
CFLAGS += -T $(STM32F4_LIB_DIR)/stm32f4xx_flash.ld
CFLAGS += -I $(STM32F4_LIB_DIR)/.

# Include libraries
CFLAGS += -I $(STM32F4_LIB_DIR)/Utilities/STM32F4-Discovery
CFLAGS += -I $(STM32F4_LIB_DIR)/Libraries/CMSIS/Include
CFLAGS += -I $(STM32F4_LIB_DIR)/Libraries/CMSIS/ST/STM32F4xx/Include
CFLAGS += -I $(STM32F4_LIB_DIR)/Libraries/STM32F4xx_StdPeriph_Driver/inc

# Default make target
all: build_fw

# Build firmware
.PHONY: firmware
build_fw: $(SRCS)
	$(CC) $(CFLAGS) $^ -o $(FW_NAME).elf
	$(OBJCOPY) -O ihex $(FW_NAME).elf $(FW_NAME).hex
	$(OBJCOPY) -O binary $(FW_NAME).elf $(FW_NAME).bin

# Upload firmware
.PHONY: upload
upload: build_fw
	st-flash write $(FW_NAME).bin 0x8000000

# Clean
.PHONY: clean
clean:
	rm -f *.o $(FW_NAME).elf $(FW_NAME).hex $(FW_NAME).bin
```
Проверка подключения платы STM32F4-Discovery
```
$ lsusb

$ st-info --probe
```

[Blink Tutorial](https://hmchung.gitbooks.io/stm32-tutorials/content/bare-metal/blink/blink-stm32disc.html)
