# Документация для приложения Курьер
Мобильное приложение для курьеров службы доставки.

**Основные возможности приложения:** 
- Получение уведомления о новом назначенном заказе
- Просмотр списка всех текущих и новых заказов
- Просмотр деталей заказа: контакты и адрес покупателя, описание заказа, статус заказа
- Изменение статуса заказа в процессе выполнения
- Авторизация/выход из системы
- Изменение данных профиля курьера



**Список документации** (в разработке, будет пополняться):
- Диаграммы последовательности:
  - [Авторизация курьера в приложении](https://github.com/anna-it-sa/courier-delivery-service/blob/main/sequence_jwt_auth.md)
  - [Получение списка заказов](https://github.com/anna-it-sa/courier-delivery-service/blob/main/sequence_get_orders.md)
- API спецификации:
  - Курьер REST API (OpenAPI 3.0) [.md](https://github.com/anna-it-sa/courier-delivery-service/blob/main/rest_api_courier.md)  [.yaml](https://github.com/anna-it-sa/courier-delivery-service/blob/main/rest_api_courier.yml)
  - AsyncAPI Сервис заказов [v2.md](https://github.com/anna-it-sa/courier-delivery-service/blob/main/kafka_api_order_v2.md)  [v2.yaml](https://github.com/anna-it-sa/courier-delivery-service/blob/main/kafka_api_order_v2.yaml)  [v3.yaml](https://github.com/anna-it-sa/courier-delivery-service/blob/main/kafka_api_order_v3.yaml)
  - AsyncAPI Сервис доставки [v3.yaml](https://github.com/anna-it-sa/courier-delivery-service/blob/main/kafka_api_delivery_v3.yaml) 
