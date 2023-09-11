#### WebAssembly


Без Emscripten
```bash
# Установка LLVM и clang
$ sudo apt install llvm
$ sudo apt install clang
$ sudo apt install lld

# Проверка установки
$ llc --version

# Компиляция в Wasm
$ clang \
  --target=wasm32 \ # Target WebAssembly
  -emit-llvm \ # Emit LLVM IR (instead of host machine code)
  -c \ # Only compile, no linking just yet
  -S \ # Emit human-readable assembly rather than binary
  add.c

# Делает IR внутренее представление LLVM
$ clang --target=wasm32 -emit-llvm -c -S add.c

# Делает ассемблерный файл Wasm
$ llc add.ll

# Делает объектный файл Wasm
$ llc -filetype=obj add.ll

# Дизассемблирование объектного файла
$ wasm-objdump -x add.o

# Компоновка
$ wasm-ld \
  --no-entry \ # We don’t have an entry function
  --export-all \ # Export everything (for now)
  -o add.wasm \
  add.o

$ wasm-ld --no-entry --export-all -o add.wasm add.o

# Компиляция и компоновка одной командой
$ clang \
  --target=wasm32 \
  -nostdlib \ # Don’t try and link against a standard library
  -Wl,--no-entry \ # Flags passed to the linker
  -Wl,--export-all \
  -o add.wasm \
  add.c

$ clang --target=wasm32 -nostdlib -Wl,--no-entry -Wl,--export-all -o add.wasm add.c

# Преобразует wasm файл в wat
$ wasm2wat add.wasm

# Преобразует wasm файл в wat
$ wat2wasm add.wat

# Применяем оптимизацию
$ clang \
   --target=wasm32 \
+  -O3 \ # Agressive optimizations
+  -flto \ # Add metadata for link-time optimizations
   -nostdlib \
   -Wl,--no-entry \
   -Wl,--export-all \
+  -Wl,--lto-O3 \ # Aggressive link-time optimizations
   -o add.wasm \
   add.c

$ clang --target=wasm32 -O3 -flto -nostdlib -Wl,--no-entry -Wl,--export-all -Wl,--lto-O3 -o add.wasm add.c

# Изменить размер стека при компоновке
$ clang \
   --target=wasm32 \
   -O3 \
   -flto \
   -nostdlib \
   -Wl,--no-entry \
   -Wl,--export-all \
   -Wl,--lto-O3 \
+  -Wl,-z,stack-size=$[8 * 1024 * 1024] \ # Set maximum stack size to 8MiB
   -o add.wasm \
   add.c

$ clang --target=wasm32 -O3 -flto -nostdlib -Wl,--no-entry -Wl,--export-all -Wl,--lto-O3 -Wl,-z,stack-size=$[8 * 1024 * 1024] -o add.wasm add.c


```
Emscripten

```bash
# Установка Emscripten
$ sudo apt install emscripten

# Компиляция с созданием .html, .js, .wasm
$ emcc *.c -o index.html

# Компиляция с созданием .js, .wasm
$ emcc *.c -o index.js

# Компиляция только стороннего модуля .wasm
$ emcc *.c -s SIDE_MODULE=2 -O1 -s EXPORTED_FUNCTIONS=['_Increment'] -o index.wasm

```
