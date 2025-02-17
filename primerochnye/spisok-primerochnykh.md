---
icon: list-ol
---

# Список примерочных

{% hint style="danger" %}
**IMSHOP Retail Protocol (IRP)** является объектом интеллектуальной собственности ООО «АЙ ЭМ СОЛЮШНЗ» (IMSHOP) и защищён как объект авторского права. Свидетельство о депонировании произведения № 023-014461 от 16 января 2023 г. подтверждает исключительные права ООО «АЙ ЭМ СОЛЮШНЗ» на данные технологии.

IMSHOP Retail Protocol создан по заказу ООО «АЙ ЭМ СОЛЮШНЗ». Использование IMSHOP Retail Protocol допустимо только при взаимодействии с ООО "АЙ ЭМ СОЛЮШНЗ" и наличии действующего лицензионного договора. Более подробно можно ознакомиться [здесь](../api-license.md).
{% endhint %}

## Подключение

{% hint style="info" %}
Для подключения обратитесь к личному менеджеру в IMSHOP.IO\
Вам необходимо получить:

* URL для подключения, по которому вы сможете получать список примерочных
* API ключ
{% endhint %}

{% hint style="info" %}
Ключ передается как **`Bearer`** токен в HTTP заголовке **`Authorization`**
{% endhint %}

{% hint style="info" %}
Запросы передаются методом **POST** c типом данных `application/json` в теле запроса
{% endhint %}

### Формат запроса

* **`all`** - (опционально), true, если нужно получить список всех примерочных, по-умолчанию в ответе будут только свободные
* **`type`** - (опционально), тип примерочной, может иметь любое значение, о котором договоримся, например couch (диван) или room (комната)

### Пример запроса

```javascript
{
    "all": true,
    "type": "couch"
}
```

### Формат ответа

* **`success`** - флаг успеха
* **`data`** - список примерочных&#x20;
  * **`privateId`** - id/номер примерочной понятный для вашей системы
  * **`available`** - статус доступности
  * **`type`** - тип примерочной

### Пример ответа

```javascript
{
    "success": true,
    "data": [
        {
            "privateId": "Room_1",
            "available": false,
            "type": "room"
        },
        {
            "privateId": "Couch_2",
            "available": true,
            "type": "couch"
        }
    ]
}
```
