# Web Service

Предназначен для адаптации HTTP запросов в BUS сообщения.


#### Правила использования

* URL должен соответствовать [корректному виду](#Вид-url-запроса)
* Параметр `id` должен указываться единожды: в теле запроса или в URL.
* Тип тела запроса должен быть `JSON`.
* Название модели должно быть указано в
  [CamelCase](https://ru.wikipedia.org/wiki/CamelCase).
* Название сервиса, действия и т.д. в `lowerCamelCase`.


#### Вид URL запроса

```
{Domain}/{Service}/{Model}/{Action}/{?id}
```

Расшифровка URL запроса:

| Переменная |                                                           Значение                                                           | Обязательное? |
|:----------:|:----------------------------------------------------------------------------------------------------------------------------:|:-------------:|
|   Domain   |                                         Доменное имя на котором работает приложение                                          |      Да       |
|  Service   |                                      Название сервиса, к которому идет запрос действия                                       |      Да       |
|   Model    |                                       Название модели, к которому идет запрос действия                                       |      Да       |
|     id     | Идентификатор, который будет передан в параметры запроса действия.<br>Может принимать как числовые, так и строковые значения |      Нет      |

Примеры:
* example.com/auth/User/getItem/1
* example.com/notify/Message/getItems
* example.com/sms/Phone/create


#### Пример вызова действия:

Создадим действие `Example/testMessage`:

```php
namespace App\Models;

use Egal\Model\Model as EgalModel;

class Example extends EgalModel
{

    // ...

    /**
     * @param string $testMessage
     * @return string
     * @statuses-access guest,logged
     */
    public static function actionTestMessage(string $testMessage): string
    {
        return 'Message: ' . $testMessage;
    }

    // ...

}
```

Сформируем запрос:

```bash
curl --location --request GET 'domain/service/Example/testMessage' \
    --header 'Content-Type: application/json' \
    --data-raw '{
        "test_message": "Hello, John Doe!"
    }'
```

Получим ответ:

```json
{
    "action": {
        "type": "action",
        "service_name": "auth",
        "model_name": "User",
        "action_name": "testMessage",
        "parameters": {
            "test_message": "Hello, John Doe!"
        },
        "token": null,
        "uuid": "ebd0b008-e987-4e50-963e-8f115514a1fe"
    },
    "start_processing": {
        "type": "start_processing",
        "started_at": "2021-03-04T07:54:56.639985Z",
        "uuid": "6dcad2e2-dc03-4007-b787-2419ba8b25bd"
    },
    "action_result": {
        "type": "action_result",
        "data": "Message: Hello, John Doe!",
        "uuid": "33a055c7-065b-4596-8805-ff87eecdc7b7"
    },
    "action_error": null
}
```

