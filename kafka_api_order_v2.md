# API Сервис заказов 1.0.0 documentation

* Specification ID: `https://github.com/anna-it-sa/courier-delivery-service`
* License: [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)
* Default content type: [application/json](https://www.iana.org/assignments/media-types/application/json)
* Support: [author](https://github.com/anna-it-sa)
* Email support: [email@gmail.com](mailto:email@gmail.com)

Получение сообщений о новом заказе. Отправка сообщений об изменении статуса заказа.
##### Specification tags

| Name | Description | Documentation |
|---|---|---|
| orders | - | - |
| asyncapi v2.6.0 | - | - |


## Table of Contents

* [Servers](#servers)
  * [eventstreams](#eventstreams-server)
* [Operations](#operations)
  * [SUB orderCreated](#sub-ordercreated-operation)
  * [PUB orderStatusChanged](#pub-orderstatuschanged-operation)

## Servers

### `eventstreams` Server

* URL: `es-kafka-bootstrap-eventstreams.com:443`
* Protocol: `kafka-secure 3.3.0`

Кафка кластер

#### Security

##### Security Requirement 1

* Type: `ScramSha512`
  * security.protocol: SASL_SSL
  * sasl.mechanism: SCRAM-SHA-512

  Учетные данные потоков событий






## Operations

### SUB `orderCreated` Operation

* Operation ID: `onOrderCreated`

В этот канал поступают сообщения о новых заказах

##### Operation tags

| Name | Description | Documentation |
|---|---|---|
| orders | - | - |

#### Message Сообщение о создании нового заказа `orderCreatedMessage`

*Сообщение содержит детали нового заказа*

* Message ID: `orderCreatedMessage`
* Content type: [application/json](https://www.iana.org/assignments/media-types/application/json)

##### Payload

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| (root) | object | - | - | - | **additional properties are allowed** |
| orderId | string | UUID заказа | examples (`"8edea954-ee3c-471a-9f02-fc6aa9d67e70"`) | - | - |
| customerId | string | UUID покупателя | examples (`"251931ca-f4be-409c-beb8-be003b65e309"`) | - | - |
| orderDetails | object | Детали заказа | - | - | **additional properties are allowed** |
| orderDetails.orderNumber | integer | Номер заказа | examples (`741`) | - | - |
| orderDetails.address | string | Адрес доставки | examples (`"г. Москва, Ленинский проспект 37, кв. 11"`) | - | - |
| orderDetails.customerName | string | Имя покупателя | examples (`"Иван Петров"`) | - | - |
| orderDetails.customerPhone | string | Телефон покупателя | examples (`"+7(910)564-88-77"`) | - | - |
| orderDetails.comment | string | Комментарий покупателя | examples (`"Позвоните за 30 минут до приезда"`) | - | - |
| createdAt | string | Дата и время создания заказа | examples (`"2025-08-19T12:17:34Z"`) | - | - |

> Examples of payload _(generated)_

```json
{
  "orderId": "8edea954-ee3c-471a-9f02-fc6aa9d67e70",
  "customerId": "251931ca-f4be-409c-beb8-be003b65e309",
  "orderDetails": {
    "orderNumber": 741,
    "address": "г. Москва, Ленинский проспект 37, кв. 11",
    "customerName": "Иван Петров",
    "customerPhone": "+7(910)564-88-77",
    "comment": "Позвоните за 30 минут до приезда"
  },
  "createdAt": "2025-08-19T12:17:34Z"
}
```



### PUB `orderStatusChanged` Operation

* Operation ID: `onOrderStatusChanged`

В этот канал отправляются сообщения об изменении статуса заказа

##### Operation tags

| Name | Description | Documentation |
|---|---|---|
| orders | - | - |

#### Message Cообщение об изменении статуса заказа `orderStatusChangedMessage`

*Сообщение содержит детали измененного заказа*

* Message ID: `orderStatusChangedMessage`
* Content type: [application/json](https://www.iana.org/assignments/media-types/application/json)

##### Payload

| Name | Type | Description | Value | Constraints | Notes |
|---|---|---|---|---|---|
| (root) | object | - | - | - | **additional properties are allowed** |
| orderId | string | UUID заказа | examples (`"8edea954-ee3c-471a-9f02-fc6aa9d67e70"`) | - | - |
| customerId | string | UUID покупателя | examples (`"251931ca-f4be-409c-beb8-be003b65e309"`) | - | - |
| statusId | integer | Id cтатуса заказа | examples (`3`) | - | - |
| status | string | Статус заказа | examples (`"Возврат на склад"`) | - | - |
| comment | string | Комментарий курьера | examples (`"Покупатель не отвечает на звонки"`) | - | - |
| orderDetails | object | Детали заказа | - | - | **additional properties are allowed** |
| orderDetails.orderNumber | integer | Номер заказа | examples (`741`) | - | - |
| orderDetails.address | string | Адрес доставки | examples (`"г. Москва, Ленинский проспект 37, кв. 11"`) | - | - |
| orderDetails.customerName | string | Имя покупателя | examples (`"Иван Петров"`) | - | - |
| orderDetails.customerPhone | string | Телефон покупателя | examples (`"+7(910)564-88-77"`) | - | - |
| orderDetails.comment | string | Комментарий покупателя | examples (`"Позвоните за 30 минут до приезда"`) | - | - |
| createdAt | string | Дата и время создания заказа | examples (`"2025-08-19T12:17:34Z"`) | - | - |

> Examples of payload _(generated)_

```json
{
  "orderId": "8edea954-ee3c-471a-9f02-fc6aa9d67e70",
  "customerId": "251931ca-f4be-409c-beb8-be003b65e309",
  "statusId": 3,
  "status": "Возврат на склад",
  "comment": "Покупатель не отвечает на звонки",
  "orderDetails": {
    "orderNumber": 741,
    "address": "г. Москва, Ленинский проспект 37, кв. 11",
    "customerName": "Иван Петров",
    "customerPhone": "+7(910)564-88-77",
    "comment": "Позвоните за 30 минут до приезда"
  },
  "createdAt": "2025-08-19T12:17:34Z"
}
```



