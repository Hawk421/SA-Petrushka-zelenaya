## Архитектура PUSH-уведомлений

## 1. Общая идея

Для реализации PUSH-уведомлений используется событийно-ориентированная архитектура (event-driven).

Микросервисы не отправляют PUSH напрямую, а публикуют события.

---

## 2. Общая схема

```
flowchart TD
    A[Cart Service] --> B[Event Bus]
    C[Order Service] --> B
    D[Marketing Service] --> B

    B --> E[Notification Service]

    E --> F[Template Engine]
    E --> G[User Preferences]
    E --> H[Scheduler]

    E --> I[Push Gateway]

    I --> J[FCM (Android)]
    I --> K[APNs (iOS)]

    J --> L[Mobile App]
    K --> L
```

---

## 3. Компоненты системы

### Микросервисы

* Cart Service
* Order Service
* Marketing Service

Генерируют события:

* cart_abandoned
* order_cancelled
* marketing_campaign

---

### Event Bus

Используется Kafka или RabbitMQ

Назначение:

* асинхронное взаимодействие
* масштабируемость
* отказоустойчивость

---

### Notification Service

Центральный сервис уведомлений.

Функции:

* обработка событий
* принятие решения об отправке
* выбор шаблона

---

### Template Engine

Формирует текст PUSH-уведомления.

Пример:
"Ваш заказ №123 отменен"

---

### Scheduler

Отвечает за отложенные уведомления.

Пример:

* PUSH через 2 часа после события

---

### User Preferences

Хранит настройки пользователя:

* включены ли уведомления
* отключена ли реклама

---

### Push Gateway

Отправка уведомлений во внешние сервисы:

* Firebase Cloud Messaging (Android)
* Apple Push Notification Service (iOS)

---

### Mobile App

Получает и отображает PUSH-уведомления.

---

## 4. Сценарий: брошенная корзина

1. Пользователь добавил товар
2. Нет активности 2 часа
3. Cart Service отправляет событие `cart_abandoned`
4. Notification Service обрабатывает событие
5. Уведомление ставится в очередь
6. Через 2 часа отправляется PUSH

---

## 5. Нефункциональные требования

* масштабируемость
* отказоустойчивость
* retry механизм
* rate limiting

---
