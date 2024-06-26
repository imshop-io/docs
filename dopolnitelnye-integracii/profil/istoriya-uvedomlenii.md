# История уведомлений

{% hint style="danger" %}
**IMSHOP Retail Protocol (IRP)** является объектом интеллектуальной собственности ООО «АЙ ЭМ СОЛЮШНЗ» (IMSHOP) и защищён как объект авторского права. Свидетельство о депонировании произведения № 023-014461 от 16 января 2023 г. подтверждает исключительные права ООО «АЙ ЭМ СОЛЮШНЗ» на данные технологии.

IMSHOP Retail Protocol создан по заказу ООО «АЙ ЭМ СОЛЮШНЗ». Использование IMSHOP Retail Protocol допустимо только при взаимодействии с ООО "АЙ ЭМ СОЛЮШНЗ" и наличии действующего лицензионного договора. Более подробно можно ознакомиться [здесь](../../api-license.md).
{% endhint %}

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../../osnovnye-integracii/oformlenie-zakaza.md)
* [Доставки](../../osnovnye-integracii/dostavki.md)
* [Оплаты](../../osnovnye-integracii/oplaty.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

## Запрос

`APP SERVER → INFRASTRUCTURE`

В вашу систему будут приходить вот такие данные:

```javascript
{
    "userId": "12345"
}
```

* **`userId`** — идентификатор пользователя (обязательное поле), полученный от системы клиента на этапе авторизации

#### Ответ

```javascript
{
  "history": [
    {
      "id": "aksdhj-asdhj1i2jo3-asldasdn",
      "title": "Ваш персональный промокод!",
      "createdOn": 1659982792971,
      "updatedOn": 1659982792971,
      "text": "На некоторые товары",
      "promocode": "JAH12DASD"
    }
  ]
}
```

* **`history`** - список уведомлений
  * **`id`** - уникальный идентификатор
  * **`title`** - название для уведомления
  * **`createdOn`** - (number) [timestamp](https://www.unixtimestamp.com/) создания уведомления (format Milliseconds (1/1,000 second))
  * **`updatedOn`** - (number) [timestamp](https://www.unixtimestamp.com/) последнего обновления уведомления (format Milliseconds (1/1,000 second))
  * **`text`** - текст сообщения (опционально)
  * **`url`** - ссылка (опционально)
  * **`deepLink`** - диплинк (опционально)
  * **`promocode`** - промокод (опционально)

{% hint style="info" %}
Следует помнить, что этот запрос будет приходить из нашего доверенного, [авторизованного](broken-reference) сервера; это — не публичный API.
{% endhint %}

Любой другой ответ API будет расцениваться как отсутствие истории уведомлений.



### Ендпоинт на прочтение уведомлений (опционально)

#### Запрос

`APP SERVER → INFRASTRUCTURE`

В вашу систему будут приходить вот такие данные:

```javascript
{
    "userId": "12345",
    "ids": ["id1", "id2", "id3"]
}
```

* **`userId`** — идентификатор пользователя (обязательное поле), полученный от системы клиента на этапе авторизации
* **`ids`** - список уникальных идентификаторов уведомлений которые были прочитаны

