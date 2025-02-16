# Model: существующие методы

Модель предназначена не только для вызова действий, но и для хранения
полученной информации и включает в себя различные вспомогательные
методы, позволяющие разработчику получать только нужную ему информацию
(например, запрашивать только список отношений модели, список ее полей,
доступных ей действий, только нужные ему поля и т.д.)

Методы модели:
1. `actionGetMetadata`:
   
   Принимает параметры:
    - `microservice_name`: обязательный параметр, устанавливает название
      микросервиса
    - `connection_type`: устанавливает тип соединения (`axios` или `socket`)
    
2. `actionGetItems`:
   
   Принимает параметры:
    - `microservice_name`: обязательный параметр, устанавливает название
      сервиса
    - `connection_type`: устанавливает тип соединения (`axios` или `socket`)
    - `per_page`: устанавливает количество запрашиваемых записей. Если
      параметр не установлен, запрашивается весь список записей
    - `page`: устанавливает номер запрашиваемой страницы. Если параметр
      не установлен, запрашивается первая страница
    - `filter`: массив с данными для фильтрации
    - `withs`: массив с данными для получения with
    - `orders`: массив с данными для сортировки
    
3. `actionGetItem`:
   
   Принимает параметры:
    - `microservice_name`: обязательный параметр, устанавливает название
      сервиса
    - `connection_type`: устанавливает тип соединения (`axios` или `socket`)
    - `id`: обязательный параметр, устанавливает id запрашиваемой записи
    - `filter`: массив с данными для фильтрации
    - `withs`: массив с данными для получения with
    - `orders`: массив с данными для сортировки
    
4. `actionCreate`:
   
   Принимает параметры:
    - `microservice_name`: обязательный параметр, устанавливает название
      сервиса
    - `connection_type`: устанавливает тип соединения (`axios` или `socket`)
    - `action_params`: обязательный параметр, устанавливает параметры
      запроса (вся информация для создания сущности)
      
5. `actionUpdate`:
   
   Принимает параметры:
    - `microservice_name`: обязательный параметр, устанавливает название
      сервиса
    - `connection_type`: устанавливает тип соединения (`axios` или `socket`)
    - `action_params`: параметры запроса (вся информация для обновления
      сущности)
      
6. `actionDelete`:
   
   Принимает параметры:
    - `microservice_name`: обязательный параметр, устанавливает название
      сервиса
    - `connection_type`: устанавливает тип соединения (`axios` или `socket`)
    - `actionParams`: параметры запроса (id удаляемой сущности)
    
7. `actionUpdateManyWithFilter`:
   
   Принимает параметры:
    - `microservice_name`: обязательный параметр, устанавливает название
      сервиса
    - `connection_type`: устанавливает тип соединения (`axios` или `socket`)
    - `action_params`: параметры запроса (вся информация для обновления
      сущностей)
      
8. `actionDeleteManyWithFilter`:

   Принимает параметры:
    - `microservice_name`: обязательный параметр, устанавливает название
      сервиса
    - `connection_type`: устанавливает тип соединения (`axios` или `socket`)
    - `action_params`: параметры запроса (id удаляемых сущностей)

9. `actionCustom`: отправка запроса на любой кастомный endpoint.

    Принимает параметры:
    - `microservice_name`: обязательный параметр, устанавливает название
      сервиса
    - `action_name`: обязательный параметр, устанавливает название
      действия (в данном случае название endpoint)
    - `connection_type`: устанавливает тип соединения (`axios` или `socket`)
    - `request_type`: устанавливает тип запроса axios (get, post, put, delete)
      Если значение не задано, по умолчанию выставляется 'post'
    - `action_params`: параметры запроса
    
10. `getModelMetadata` - получение сохраненной metadata модели без
   дополнительного запроса к серверу
   
11. `getModelActionList` - получение списка всех действий доступных
    модели
    
12. `getModelValidationRules` - получение списка правил валидации для
    каждого поля
    
13. `getModelActionsMetaData` - получение полного описания всех действий
    доступных модели
    
14. `getModelFieldsWithTypes` - получение fields with types модели
    
15. `getSpecificFields` - получение выбранных пользователем полей
    
    принимает параметры:
    - `fields`: массив с названиями полей
    - `filterType`: ‘includes’ возвращает указанные в массиве fields
      поля, `excludes` возвращает все поля, кроме указанных в fields
    - `dataToFilter`: принимает массив записей для фильтрации

