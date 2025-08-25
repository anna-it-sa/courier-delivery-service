# Мобильное приложение Курьер OpenAPI 3.0 спецификация
API для мобильного приложения сотрудников службы доставки. Предоставляет методы работы с профилем пользователя и методы для работы с заказами.

## Version: 1.0.0

**License:** [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0.html)

### /user/login

#### POST
##### Summary:

Вход пользователя в систему

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Успешная авторизация |
| 400 | Неверные имя пользователя/пароль |
| default | Непредвиденная ошибка |

### /user/logout

#### POST
##### Summary:

Выход пользователя из системы

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Успешный выход из системы |
| 401 | Токен доступа отсутствует или недействителен |
| default | Непредвиденная ошибка |

##### Security

| Security Schema | Scopes |
| --- | --- |
| bearerAuth | |

### /user/{userId}

#### PUT
##### Summary:

Обновление данных пользователя

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | path | UUID пользователя | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Данные пользователя успешно обновлены |
| 400 | Неверный запрос |
| 401 | Токен доступа отсутствует или недействителен |
| 404 | Пользователь не найден |
| default | Непредвиденная ошибка |

##### Security

| Security Schema | Scopes |
| --- | --- |
| bearerAuth | |

### /orders

#### GET
##### Summary:

Получение списка заказов, назначенных на пользователя

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| userId | query | UUID пользователя | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Успешный ответ со списком заказов |
| 401 | Токен доступа отсутствует или недействителен |
| 404 | Пользователь не найден |
| default | Непредвиденная ошибка |

##### Security

| Security Schema | Scopes |
| --- | --- |
| bearerAuth | |

### /orders/{orderId}

#### GET
##### Summary:

Получение данных одного заказа

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| orderId | path | UUID заказа | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Успешный ответ с одним заказом |
| 401 | Токен доступа отсутствует или недействителен |
| 404 | Пользователь не найден |
| default | Непредвиденная ошибка |

##### Security

| Security Schema | Scopes |
| --- | --- |
| bearerAuth | |

#### PUT
##### Summary:

Обновление данных одного заказа

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| orderId | path | UUID заказа | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Успешное обновление заказа |
| 401 | Токен доступа отсутствует или недействителен |
| 404 | Пользователь не найден |
| default | Непредвиденная ошибка |

##### Security

| Security Schema | Scopes |
| --- | --- |
| bearerAuth | |
