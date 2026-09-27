# API Endpoints

Базовый URL: `http://localhost:1880`

## GET /api/text

Возвращает простой текст.

**Параметры:** нет.

**Успешный ответ (200 OK):**

```
Hello from Node-RED! This is a plain text response.
```

**Пример:**

```bash
curl http://localhost:1880/api/text
```

---

## GET /api/info

Возвращает JSON с двумя полями.

**Параметры:** нет.

**Успешный ответ (200 OK):**

```json
{
  "service": "Node-RED Lab 2",
  "author": "Dubrovshchik"
}
```

**Пример:**

```bash
curl http://localhost:1880/api/info
```

---

## GET /api/items/:id

Возвращает элемент по его id. Поддерживает query-параметры (пробрасываются в ответ для демонстрации).

**Path-параметры:**
- `id` (integer, обязательный) — идентификатор элемента.

**Query-параметры:**
- любые — пробрасываются в поле `query` ответа.

**Успешный ответ (200 OK):**

```json
{
  "item": { "id": 2, "name": "Mouse", "price": 25 },
  "query": {},
  "requested_at": "2026-09-27T13:00:00.000Z"
}
```

**Пример успешного запроса:**

```bash
curl http://localhost:1880/api/items/2
curl "http://localhost:1880/api/items/2?verbose=true"
```

**Ошибка 404 Not Found:**

Возвращается, если элемента с таким id нет.

```json
{
  "error": "Not Found",
  "message": "Элемент с таким id не найден",
  "id": 999
}
```

```bash
curl -i http://localhost:1880/api/items/999
```

**Ошибка 400 Bad Request:**

Возвращается, если id не является положительным целым числом.

```json
{
  "error": "Bad Request",
  "message": "Параметр id должен быть положительным целым числом",
  "received": "abc"
}
```

```bash
curl -i http://localhost:1880/api/items/abc
```