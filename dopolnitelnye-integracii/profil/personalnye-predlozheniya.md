# Персональные предложения

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](broken-reference)
* [Доставки](broken-reference)
* [Оплаты](broken-reference)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

## Описание

Данный метод позволяет получить персональные для пользователя промокоды (акции) для показа в виде шрихкода и считывания на кассе, например, Акция "Скачай приложение и получи скидку на кассе". Для того, чтобы акция отобразилась у пользователя нужно, чтобы:

* Пользователь авторизовался в приложении
* Вебхук вернул акцию с промокодом
* В админке imshop создан баннер акции с указанным id акции - именно этот баннер будет показан пользователю, в конце содержимого баннера будет показан штрихкод акции для считывания на кассе

## Получение списка индивидуальных предложений

### Формат запроса

* **`userId`** - идентификатор пользователя в системе продавца (на сайте / в CRM итд)
* **`segments`** - список сегментов, в которые добавлен пользователь на стороне IMSHOP
  * **`id`** - идентификатор сегмента
  * **`name`** - название сегмента

#### Пример запроса

```javascript
{
    "userId": "1234567890",
    "segments": [
        { "id": "PEREKRESTOR-BUYER", "name": "Пользователи, установившие приложение по флаеру в Перекрестке" },
        { "id": "SALES", "name": "Пользователи, покупающие только на распродажах" }
    ]
}
```

### Формат ответа

* **`offers`** - список предложений
  * **`id`** - идентификатор предложения
  * **`name`** - название
  * **`description`** - описание
  * **`promocode`** - промокод
  * **`barcodeType`** (опционально) - тип баркода, по-умолчанию `code128`
  * **`online`** - промокод может быть применен в приложении
  * **`offline`** - промокод может быть предъявлен в рознице
  * **`used`** (опционально) - **`true`** / **`false`** - предложение было использовано
  * **`expirationTimestamp`** - [таймштамп](https://www.unixtimestamp.com/), когда истекает срок действия предложения (**`null`** - если предложение не имеет срока действия)

#### Пример ответа

```javascript
{
    "offers": [
        {
            "id": "PROMO-1",
            "name": "Скидка 1000 рублей при покупке духов HUGO BOSS",
            "description": "Воспользуйтесь вашим персональным промокодом до 31 августа",
            "promocode": "HUGO1000",
            "barcodeType": "qr",
            "online": true,
            "offline": false,
            "expirationTimestamp": 1586459114
        }
    ]
}
```

### Список промокодов оффера (в разработке)

* **`promoList`**
  * **`promocode`** - промокод (строка)
  * **`value`** - номинал (число); в валюте, используемой в каталоге приложения
  * **`image`** (опционально) - ссылка на изображение (строка); по умолчанию отображается  QR-код со значением, заданным в `promocode`
  * **`expirationTimestamp`**(опционально) - [таймштамп](https://www.unixtimestamp.com/), когда истекает срок действия промокода

#### Пример ответа

```javascript
{
    "offers": [
        {
            "id": "PROMO-1",
            "name": "Ваши промокоды",
            "promoList": [
                {
                    "promocode": "code-1",
                    "value": 500,
                    "image": "https://media.url/promo-image.png",
                    "expirationTimestamp": 1586459114
                },
                {
                    "promocode": "code-2",
                    "value": 1000
                }
            ]
        }
    ]
}
```

