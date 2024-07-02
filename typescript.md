#### TypeScript

```
# Сначала установите Node.js и npm (если еще не установлены)
# Проверка установки
$ node -v
$ npm -v

# Установка TypeScript
$ npm install -g typescript

# Компиляция
$ tsc index.ts

# Создать tsconfig.json
# Этот файл позволяет настроить компилятор TypeScript
$ tsc --init

# Компиляция с файлом настройки tsconfig.json
$ tsc

# Запуск скомпилированного файла
$ node dist/index.js
```
Пример tsconfig.json
```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "outDir": "./dist"
  },
  "include": ["src"]
}

```
