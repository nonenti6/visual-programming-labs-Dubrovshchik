## Часть 1. Установка и запуск Node-RED

**Способ установки:** Docker Desktop (образ `nodered/node-red:latest-22`)

**Версии:**
- Node-RED: v4.1.15
- Node.js: v22.23.2

**Команда запуска:**
\```bash
docker run -d --name mynodered -p 1880:1880 -v /d/node-red-data:/data --restart unless-stopped nodered/node-red:latest-22
\```

**URL редактора:** http://localhost:1880
**URL dashboard:** http://localhost:1880/ui

## Краткое описание выполненного

В ходе работы были собраны и задеплоены следующие потоки:

| № | Файл | Что демонстрирует |
|---|---|---|
| 2.1 | flow-01-inject-debug.json | Inject → Debug: базовый поток |
| 2.2 | flow-02-function.json | Function node: JS-логика (let/const, if/else, for, массивы, объекты) |
| 2.3 | flow-03-switch.json | Switch node: ветвление по msg.payload |
| 2.4 | flow-04-change.json | Change node: Set msg.topic, msg.timestamp, msg.payload |
| 2.5 | flow-05-template.json | Template node: Mustache-шаблон, JSON-вывод |
| 2.6 | flow-06-http-request.json | HTTP Request: запрос к публичному API (chucknorris.io) |
| 2.7 | flow-07-mqtt.json | MQTT: publish/subscribe через broker.hivemq.com |
| 2.8 | flow-08-endpoints.json | 3 GET-эндпоинта: /api/text, /api/info, /api/items/:id с обработкой 400/404 |
| 2.9 | flow-09-dashboard.json | Dashboard: ui_gauge + ui_chart |
| 2.10 | flow-10-telegram.json | Telegram-бот: /start, /sixseven (фото), echo |
| 2.11 | flow-11-files.json | Чтение и запись файла в /data (сохраняется между перезапусками) |
| 2.12 | flow-12-context.json | Flow context: счётчик между сообщениями |
| A11 | flow-achievement-11-telegram.json | Ачивка 11: Telegram inline keyboard, callback_query, меню заказа |

## Использованные AI-промпты (ключевые примеры)

1. **Генерация кода function node для 2.2:**
   > «Напиши код для function node в Node-RED, который использует let/const, if/else, цикл for, массив и объект. Функция должна принимать объект с полем numbers (массив чисел) и возвращать объект с полями sum, status и выше.»

2. **Mustache-шаблон для 2.5:**
   > «Составь Mustache-шаблон для Node-RED template node, который формирует JSON с полями student, group, year, greeting. Данные берутся из msg.payload.name, msg.payload.group, msg.payload.year.»

3. **Код эндпоинта /api/items/:id для 2.8:**
   > «Напиши код для function node в Node-RED, который обрабатывает GET /api/items/:id. Должен читать path-param id и query-параметры. Если id не положительное целое число — вернуть 400. Если элемента нет в "базе" — 404. Иначе — 200 с найденным элементом.»

4. **Inline-клавиатура для ачивки 11:**
   > «Сделай код function node для Node-RED telegram sender, который отправляет inline keyboard с тремя кнопками: Пицца, Суши, Бургер. callback_data = order:pizza и т.д.»

5. **Отладка структуры callback_query:**
   > «В node-red-contrib-telegrambot v19.0.3 при нажатии inline-кнопки выдаёт TypeError: Cannot read properties of undefined (reading 'data'). Покажи, в каком поле msg.payload лежит callback_data.»

## Освоенные ноды

**Базовые (common):**
- `inject` — источник сообщений (по клику, по расписанию)
- `debug` — вывод в панель отладки
- `complete` — узел-заглушка
- `catch` — обработка ошибок
- `status` — статус узла

**Функциональные (function):**
- `function` — выполнение произвольного JS-кода
- `switch` — ветвление по правилам
- `change` — установка/изменение свойств msg
- `template` — Mustache-шаблоны, JSON/текст
- `delay` — задержка
- `trigger` — управление временными интервалами

**Сетевые (network):**
- `http in` — приём HTTP-запросов
- `http response` — ответ на HTTP-запрос
- `http request` — исходящий HTTP-запрос
- `mqtt in` — подписка MQTT
- `mqtt out` — публикация MQTT

**Хранилище:**
- `write file` — запись в файл
- `read file` — чтение из файла

**Dashboard (пакет node-red-dashboard):**
- `ui_gauge` — круговой индикатор числового значения
- `ui_chart` — график истории значений

**Telegram (пакет node-red-contrib-telegrambot):**
- `telegram receiver` — приём сообщений от Telegram
- `telegram command` — фильтр по команде
- `telegram event` — обработка событий (callback_query и т.д.)
- `telegram sender` — отправка сообщений (текст, фото, клавиатура)

## Скриншоты

### Часть 1. Установка и версии

- ![Версия Node.js](screenshots/nodejs-version.png)
- ![Версия Node-RED](screenshots/node-red-version.png)

### 2.1. Inject → Debug

- ![flow-01](screenshots/01-inject-debug.png)

### 2.2. Function

- ![flow-02](screenshots/02-function.png)

### 2.3. Switch

- ![flow-03](screenshots/03-switch.png)

### 2.4. Change

- ![flow-04](screenshots/04-change.png)

### 2.5. Template

- ![flow-05](screenshots/05-template.png)

### 2.6. HTTP Request

- ![flow-06](screenshots/06-http-request.png)

### 2.7. MQTT

- ![flow-07](screenshots/07-mqtt.png)

### 2.8. Endpoints

- ![flow-08 общий](screenshots/08-endpoints.png)
- ![08a text](screenshots/08a-text.png)
- ![08b info](screenshots/08b-info.png)
- ![08c items success](screenshots/08c-items-success.png)
- ![08d items 404](screenshots/08d-items-404.png)
- ![08e items 400](screenshots/08e-items-400.png)

### 2.9. Dashboard

- ![flow-09](screenshots/09-dashboard.png)
- ![flow-09a dashboard UI](screenshots/09a-dashboard.png)

### 2.10. Telegram

- ![flow-10](screenshots/10-telegram.png)
- ![10a BotFather](screenshots/10a-telegram-father.png)
- ![10b chat](screenshots/10b-telegram-chat.png)

### 2.11. Файлы

- ![flow-11](screenshots/11-files.png)
- ![11a read](screenshots/11a-files-read.png)
- ![11a write](screenshots/11a-files-write.png)

### 2.12. Контекст

- ![flow-12](screenshots/12-context.png)
- ![12a counter flow](screenshots/12a-counter.png)
- ![12b counter](screenshots/12b-counter.png)

### Ачивка 11. Telegram Inline Keyboard

- ![achievement-11](screenshots/achievement-11-telegram.png)

## Выводы

Работать с docker, node-red интересно. Углубляясь, столько информации узнаешь. Благодаря node-red можно упрощать себе жизнь. Только с такой проблемой на начальных порах сталкиваешься, как синтаксис js, поскольку в предыдущих семестрах его не проходили.
Но самое интересное было создание telegram бота) и ачивку было увлекательно выполнять. Опыт в написании бота был на питоне, а теперь с помощью нод, поэтому знаю уже несколько подходов по созданию ботов в телеграме. 