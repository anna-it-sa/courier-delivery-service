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
  <details>
  <summary>Авторизация курьера в приложении</summary>

  ```mermaid
  sequenceDiagram
      actor user as Пользователь
      participant app as Мобильное приложение
      participant auth_service as Сервис аутентификации
      participant user_service as Сервис пользователей
      participant jwt as JWT-сервер
  
      user ->> app: Ввод логина и пароля
      app ->> +auth_service: Отправка данных авторизации
      auth_service ->> +user_service: Запрос данных пользователя
  
      alt Пользователь не найден
      user_service -->> auth_service: Пользователь не найден
      auth_service ->> app: Ошибка 404 Not Found 
      app ->> user: Необходима регистрация
      else Введен неправильный пароль
      user_service -->> auth_service: Неправильный пароль
      auth_service ->> app: Ошибка 401 Unauthorized 
      app ->> user: Введите верный пароль
      else Пользователь авторизован
      user_service -->> -auth_service: Возврат данных пользователя
      auth_service ->> +jwt: Запрос генерации токена
      jwt ->> jwt: Генерация токена
      jwt ->> -auth_service: JWT токен
      auth_service ->> -app: 200 Успешная авторизация. Возврат токена    
      app ->> app: Токен сохранён в БД
      app ->> user: Авторизация успешна
      end
  ```
  </details>
  <details>
  <summary>Получение списка заказов</summary>
    
  ```mermaid
  sequenceDiagram
      actor user as Курьер    
      participant app as Мобильное приложение
      participant db_mobile as БД устройства
      participant order_service as Сервис заказов
      participant notification_service as Сервис уведомлений 
  
      notification_service -->> app : Уведомление о новых заказах
      app -->> user : Есть новые заказы
      user ->> +app : Посмотреть новые заказы 
      
      par Загрузка сохраненных заказов из локальной базы
          app ->> +db_mobile :Запрос сохраненных заказов из локальной базы
          db_mobile ->> -app : Список сохраненных заказов
          app ->> user : Отображение списка сохраненных заказов
      and Загрузка новых заказов из сервиса заказов
          app ->> +order_service : Запрос новых заказов
      alt Новых заказов нет
          order_service -->> app : Пустой список
          app ->> user : Отображение списка сохраненных заказов из БД
      else Есть новые заказы
          order_service -->> app : Список новых заказов
          app ->> db_mobile : Сохранение новых заказов в локальной базе  
          app ->> user : Отображение обновленного списка всех заказов
      else Ошибка при выполнении запроса
          order_service -->> -app : Ошибка
          app ->> db_mobile : Логирование ошибки
          app ->> -user : Сообщение об ошибке    
      end
      end
  ```
  </details>  
 
- API спецификации:
  - Курьер REST API (OpenAPI 3.0) [.md](https://github.com/anna-it-sa/courier-delivery-service/blob/main/rest_api_courier.md)  [.yaml](https://github.com/anna-it-sa/courier-delivery-service/blob/main/rest_api_courier.yml)
  - AsyncAPI Сервис заказов [v2.md](https://github.com/anna-it-sa/courier-delivery-service/blob/main/kafka_api_order_v2.md)  [v2.yaml](https://github.com/anna-it-sa/courier-delivery-service/blob/main/kafka_api_order_v2.yaml)  [v3.yaml](https://github.com/anna-it-sa/courier-delivery-service/blob/main/kafka_api_order_v3.yaml)
  - AsyncAPI Сервис доставки [v3.yaml](https://github.com/anna-it-sa/courier-delivery-service/blob/main/kafka_api_delivery_v3.yaml) 

