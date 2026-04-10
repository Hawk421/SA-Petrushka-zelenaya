## API: Партнерские магазины

## 1. Endpoint

GET /api/v1/partner-stores

---

## 2. Пример ответа

```json
{
  "stores": [
    {
      "id": "metro",
      "name": "METRO",
      "logoUrl": "https://cdn.petrushka.ru/logos/metro.png",
      "delivery": {
        "type": "scheduled",
        "label": "Ближайшая доставка",
        "timeRange": {
          "date": "2026-04-09",
          "from": "21:00",
          "to": "23:00"
        },
        "displayText": "сегодня 21:00–23:00"
      },
      "action": {
        "type": "external_link",
        "url": "https://metro.ru"
      }
    },
    {
      "id": "auchan",
      "name": "Ашан",
      "logoUrl": "https://cdn.petrushka.ru/logos/auchan.png",
      "delivery": {
        "type": "scheduled",
        "label": "Ближайшая доставка",
        "timeRange": {
          "date": "2026-04-09",
          "from": "18:00",
          "to": "20:00"
        },
        "displayText": "сегодня 18:00–20:00"
      },
      "action": {
        "type": "external_link",
        "url": "https://auchan.ru"
      }
    },
    {
      "id": "vkusvill",
      "name": "ВкусВилл",
      "logoUrl": "https://cdn.petrushka.ru/logos/vkusvill.png",
      "delivery": {
        "type": "express",
        "label": "Быстрая доставка",
        "timeRange": {
          "fromMinutes": 20,
          "toMinutes": 60
        },
        "displayText": "от 20 до 60 минут"
      },
      "action": {
        "type": "external_link",
        "url": "https://vkusvill.ru"
      }
    }
  ],
  "meta": {
    "total": 3,
    "generatedAt": "2026-04-09T18:00:00Z"
  }
}
```

## 3. Описание полей

### Store

| Поле    | Тип    | Описание                 |
| ------- | ------ | ------------------------ |
| id      | string | Уникальный идентификатор |
| name    | string | Название магазина        |
| logoUrl | string | Ссылка на логотип        |

---

### Delivery

| Поле        | Тип    | Описание                           |
| ----------- | ------ | ---------------------------------- |
| type        | string | Тип доставки (scheduled / express) |
| label       | string | Название блока                     |
| timeRange   | object | Интервал доставки                  |
| displayText | string | Готовый текст для UI               |

---

### Action

| Поле | Тип    | Описание                     |
| ---- | ------ | ---------------------------- |
| type | string | Тип действия (external_link) |
| url  | string | Ссылка для перехода          |

---
