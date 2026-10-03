# Node-RED Lab 2 API

## Общая информация

API реализован в Node-RED с использованием узлов `HTTP In`, `Function` и `HTTP Response`.

Базовый адрес при локальном запуске:

```text
http://localhost:1880
```

Все endpoints используют HTTP-метод `GET`.

---

## GET /api/text

Возвращает простой текстовый ответ.

### Request

```http
GET /api/text
```

### Response

```text
Node-RED Lab 2: GET endpoint works
```

### Status

```text
200 OK
```

---

## GET /api/info

Возвращает информацию о студенте и лабораторной работе в формате JSON.

### Request

```http
GET /api/info
```

### Response

```json
{
    "student": "Zheleznyi",
    "group": "DL2026"
}
```

### Status

```text
200 OK
```

---

## GET /api/items

Возвращает элемент по его идентификатору.

### Request

```http
GET /api/items?id=1
```

Параметр:

| Parameter | Type    | Required | Description            |
| --------- | ------- | -------- | ---------------------- |
| `id`      | integer | Yes      | Идентификатор элемента |

### Успешный ответ

Для запроса:

```http
GET /api/items?id=1
```

возвращается:

```json
{
    "id": 1,
    "name": "Node-RED"
}
```

Статус:

```text
200 OK
```

### Ошибка: параметр не указан

Запрос:

```http
GET /api/items
```

Ответ:

```json
{
    "error": "Parameter id is required"
}
```

Статус:

```text
400 Bad Request
```

### Ошибка: элемент не найден

Запрос:

```http
GET /api/items?id=99
```

Ответ:

```json
{
    "error": "Item not found"
}
```

Статус:

```text
404 Not Found
```

---

## Реализация

Endpoints реализованы в отдельном Node-RED flow:

```text
HTTP In → Function → HTTP Response
```

Для `/api/items` используется параметр запроса `id`, который получается через:

```javascript
msg.req.query.id
```

HTTP-код ответа устанавливается через:

```javascript
msg.statusCode
```
