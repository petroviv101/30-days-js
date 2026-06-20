
Node.js - среда выполнения js на сервере
https://nodejs.org/en/download

## Команды для консоли

node - команда для запуска кода js
npm - менджер пакетов Node.js, чтобы устанавливать библиотеки
git - команда для использования git

-v , флаг который показывает версию программы 
--version, узнать версию программы

## Плагины для VS Code

| Плагин                | Назначение                          |
| --------------------- | ----------------------------------- |
| **ESLint**            | Проверка ошибок в коде              |
| **Prettier**          | Автоматическое форматирование       |
| **Thunder Client**    | Тестирование API (позже пригодится) |
| **npm Intellisense**  | Автодополнение для npm              |
| **Path Intellisense** | Автодополнение путей к файлам       |
| **GitLens**           | Удобная работа с Git                |
# Первый день
## Введение

Node.js - позволяет js работать на сервере, это позволяет создавать:

- Читать и создавать файлы на компьютере
- Работать с базами данных
- Слушать запросы от пользователей в интернете
- Отправлять email
- Всё, что обычно делают серверные языки (Python, PHP, Java)

### Первая программа
1. консоль
``` cmd
C:\Users\123ho>node C:\Users\123ho\Downloads\test\hello.js
Привет, мир! Я начинаю изучать Node.js!
Сегодня мой первый день!
Я учусь писать серверные программы!
```
2. js
``` js
console.log("Привет, мир! Я начинаю изучать Node.js!");
console.log("Сегодня мой первый день!");
console.log("Я учусь писать серверные программы!");
```

### REPL - Интерактивный режим для консоли

нужно просто написать, node без path и нажать enter, после чего появится 
``` cmd
C:\Users\123ho>node
Welcome to Node.js v24.17.0.
Type ".help" for more information.
> 2 + 2
> 4
```

### Аргументы командной строки
Ниже код, когда мы вызываем команду Node + path
то он передаёт аргументы 2 автоматически это путь к node.exe, а так же сам файл
+мои аргументы, сколько можно
``` js
process.argv[] //массив для хранения аргументов
```
Пример программы, которая выводит основные 2 аргумента с путями к node.exe и самому файлу, а так же двумя дополнительными аргументами, в данном случае имя и выводит привет + имя
``` js
// process.argv — это массив со всеми аргументами
// argv = argument values (значения аргументов)

console.log("=== ВСЕ АРГУМЕНТЫ ===");
console.log(process.argv);
console.log("");

// Разберём по частям:

console.log("process.argv[0] = " + process.argv[0]);  // путь к node.exe
console.log("process.argv[1] = " + process.argv[1]);  // путь к вашему файлу
console.log("process.argv[2] = " + process.argv[2]);  // ваш первый аргумент
console.log("process.argv[3] = " + process.argv[3]);  // ваш второй аргумент

console.log("");

// slice(2) — отрезает первые два элемента (нам они не нужны)
// Получаем только наши аргументы
const args = process.argv.slice(2);
console.log("Мои аргументы (без первых двух):", args);
console.log("");

// Практическое применение:
if (args.length > 0) {

    console.log("Привет, " + args[0] + "!");

} else {

    console.log("Передайте имя! Пример: node args-demo.js Анна");

}
```

Что выводится в консоль:

``` js
C:\Users\123ho>
C:\Users\123ho>node C:\Users\123ho\Downloads\test\hello.js Олег
=== ВСЕ АРГУМЕНТЫ ===
[
  'C:\\Program Files\\nodejs\\node.exe',
  'C:\\Users\\123ho\\Downloads\\test\\hello.js',
  'Олег'
]

process.argv[0] = C:\Program Files\nodejs\node.exe
process.argv[1] = C:\Users\123ho\Downloads\test\hello.js
process.argv[2] = Олег
process.argv[3] = undefined

Мои аргументы (без первых двух): [ 'Олег' ]

Привет, Олег!

C:\Users\123ho>
```

### slice()
slice() - метод, чтобы обрезать массив, если передать аргумент 2, то обрежет первые 2 аргумента

## Практика 1

### Задание 1

1. Создаёт переменную `city` с названием вашего города
2. Создаёт переменную `population` с населением (число)
3. Создаёт переменную `isCapital` с `true` или `false`
4. Выводит всё это в консоль

``` js
console.log("______Программа привествие!!!______");
console.log(process.argv);

let city = process.argv[2];
let count = process.argv[3];
let mid = false;

if(city != undefined && count != undefined){
    if(city == 'Москва' || city == 'москва') mid = true;
    console.log("Ваш город: " + process.argv[3]);
    console.log("Население: " + process.argv[4]);
    console.log("Столица: " + mid);

}else{
    console.log("Введите агументы, свой город, население своего города");
}
```

Тест: 

``` cmd
C:\Users\123ho>node C:\Users\123ho\Downloads\test\hello.js Москва 12000000
______Программа привествие!!!______
[
  'C:\\Program Files\\nodejs\\node.exe',
  'C:\\Users\\123ho\\Downloads\\test\\hello.js',
  'Москва',
  '12000000'
]
Ваш город: 12000000
Население: undefined
Столица: true

C:\Users\123ho>node C:\Users\123ho\Downloads\test\hello.js Ярославль 512000
______Программа привествие!!!______
[
  'C:\\Program Files\\nodejs\\node.exe',
  'C:\\Users\\123ho\\Downloads\\test\\hello.js',
  'Ярославль',
  '512000'
]
Ваш город: 512000
Население: undefined
Столица: false

C:\Users\123ho>
```

### Задание 2 - калькулятор

``` js
console.log("______Калькулятор______");

let first = +(process.argv[2]);
let znak = process.argv[3];
let second = +(process.argv[4]);

if(second == undefined){
    console.log("Введите 3 аргумент, первое число, операцию( + , / , - , * ), второе число");
}else{
    if(znak == '+'){
        console.log(first + second);
    }else if(znak == '-'){
        console.log(first - second);
    }else if(znak == '*'){
        console.log(first * second);
    }else if(znak == '/'){
        if(second != 0){
            console.log(first / second);
        }else{
            console.log("Нельзя делить на 0");
        }
    }else{
        console.log('Введена неверная операция');
    }
}
```

``` cmd
C:\Users\123ho>node C:\Users\123ho\Downloads\test\hello.js 2 + 12
______Калькулятор______
14

C:\Users\123ho>node C:\Users\123ho\Downloads\test\hello.js 2 + 0
______Калькулятор______
2

C:\Users\123ho>node C:\Users\123ho\Downloads\test\hello.js 24 / 0
______Калькулятор______
Нельзя делить на 0

C:\Users\123ho>node C:\Users\123ho\Downloads\test\hello.js 12 + 12
______Калькулятор______
24

C:\Users\123ho>
```

# Git

План на первый день: 
1. **Создадим репозиторий** (хранилище для кода) на GitHub
2. **Подключим** его к вашему компьютеру
3. **Отправим** (зальём) все ваши программы в облако

### git config 

Настройка моего ноутбука для работы с гитом(моим личным кабинетом)

```
C:\Users\123ho>git config --global user.name "petroviv101"
C:\Users\123ho>git config --global user.email "dm.snyatkov@edu.mubint.ru"
C:\Users\123ho>
```

###  Разбор флага `--global`

|Флаг|Что значит|Где сохраняется|
|---|---|---|
|`--global`|Настройки для **всех** проектов на вашем компьютере|Файл `~/.gitconfig`|
|`--system`|Настройки для **всех пользователей** компьютера|Файл `/etc/gitconfig`|
|`--local`|Настройки **только для текущего** проекта|Файл `.git/config` в папке проекта|
### git init

``` git
git init
```

**Что делает:** Создаёт в вашей папке скрытую папку `.git` — это «сердце» репозитория.

### .gitignore

Данные, которые не стоит сохранять в репозитории, временные файлы, файлы для работы компилятора или иной программы. Так же файлы, которые в целом не хочется сохранять, фотографии и тд

пример: 

```
# Временные файлы
*.log
*.tmp
# Настройки редактора (ваши личные)
.vscode/
.idea/
# Пароли и секреты
.env
config/secrets.json
# Библиотеки (их можно скачать заново)
# Системные файлы
.DS_Store  # Mac
Thumbs.db  # Windows
```
###  git add 

git add - подготовка файлов к комиту, смотрит .gitignore и отсекает ненужные файлы

### git status

Показывает какие файлы еще не были запушены в репозиторий

### git commit

git commit -m
сохраняет все файлы из зоны подготовки(git add)

### git remote

указываем адрес нашего репозитория
git branch -M main
git push -u origin main

# 2 часть первого дня

## Решение задач

Задача: Ваш код должен возвращать true или false (а не 'true' и 'false') в зависимости от того, является ли заданное число нарциссическим числом в системе счисления с основанием 10. В вашем языке, например в PHP, это могут быть значения True и False. Проверка на наличие текстовых строк или других недопустимых входных данных не требуется, в функцию будут передаваться только корректные положительные ненулевые целые числа.
Пример, число 153

``` js
    1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 153
```

``` js
let value = process.argv[2];

if (value === undefined) {
  console.log('Пожалуйста, передайте число как аргумент');
  process.exit(1);
}

let valueString = String(value);
let n = valueString.length;
let sum = 0; // отдельная переменная для результата

while (n > 0) {
  n--;
  const digit = Number(valueString[n]);
  if (Number.isNaN(digit)) {
    console.error(`Ошибка: символ "${valueString[n]}" не является цифрой`);
    process.exit(1);
  }
  sum += digit * digit * digit;
}

console.log(sum);
```

Обычно при покупке у вас спрашивают, верны ли номер кредитной карты, номер телефона или ответ на ваш самый секретный вопрос. Однако кто‑то может заглянуть вам через плечо, поэтому не хочется, чтобы эти данные отображались на экране. Вместо этого их нужно скрыть.

Ваша задача — написать функцию `maskify`, которая заменяет все символы, кроме последних четырёх, на `#`.

``` js
let value = process.argv[2];
let size = 0;
let newValue = '';
const len = value.length;

while (size < len) {
  if (len - size <= 4) {
    newValue += value[size];
  } else {
    newValue += '#';
  }
  size++;
}

console.log(newValue);
```

# Переменные

## Типы данных

| Тип         | Описание                     | Пример                             |
| ----------- | ---------------------------- | ---------------------------------- |
| `number`    | Числа (целые и дробные)      | `42`, `3.14`, `-10`                |
| `string`    | Строки (текст)               | `"Привет"`, `'Hello'`, `` `Мир` `` |
| `boolean`   | Логический (правда/ложь)     | `true`, `false`                    |
| `undefined` | Значение не определено       | `let x;` → `undefined`             |
| `null`      | Пустое значение (специально) | `let x = null;`                    |
| `bigint`    | Очень большие числа          | `9007199254740991n`                |
| `symbol`    | Уникальные идентификаторы    | `Symbol('id')`                     |
## Преобразование типов

``` js
Number("42")      // → 42
String(123)       // → "123"
Boolean(0)        // → false
Boolean("hello")  // → true

// Неявное преобразование
"5" - 3           // → 2 (строка стала числом)
"5" + 3           // → "53" (число стало строкой)
```

## Ложные значения

- `false`
- `0`, `-0`
- `""` (пустая строка)
- `null`
- `undefined`
- `NaN`

``` js
let a = true //Все остальные значения, это true
```

## Ввод данных readline

### Подключение readline

``` js
const readline = require('readline');
```

requier('readline') - подключает встроенный модуль, местный аналог inuclude из с++
const readline - сохраняем модуль в переменную

### Базовая структура

``` js
const readline = require('readline');
const rl = readline.createInterface({
	input: process.stdin,
	output: process.stdout
});
```

Пример использования

``` js
const readline = require('readline'); //подключаем модуль

const rl = readline.createInterface({ //создаём интерфейс 
    input: process.stdin, //получаем данные с вода
    output: process.stdout  //получаем куда выводить
});

rl.question('Сколько тебе лет? ', (age)=>{ //реализация интерфейса, функцией вопрос
    console.log('\nТебе ' + age + ' лет'); 
    rl.close();
})
```

### Задачи с readline

Калькулятор

``` js
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
})

let oper1="";
let first1 = 0;
let second1 = 0;

rl.question('Какую операцию будем использовать?\n', (oper)=>{
    oper1 = oper;
    rl.question('Введите первое число?\n', (first)=>{
        first1 = Number(first);
        rl.question('Введите второе число?\n', (second)=>{
            second1 = Number(second);
            if(oper1 == '+'){
                console.log(first1 + second1);
            }else if(oper1 == '-'){
                console.log(first1 - second1);
            }else if(oper1 == '*'){
                console.log(first1 * second1);
            }else if(oper1 == '/'){
                if(second1 == 0){
                    console.log("Нельзя делить на 0");
                }else{
                    console.log(first1 / second1);
                }
            }
            rl.close();
    })
})
})
```
