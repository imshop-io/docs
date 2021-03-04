# Оплаты

{% hint style="info" %}
Для подключения webhook расчета оплат, обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

IMSHOP.IO позволяет при помощи webhook выводить доступные способы оплат при оформлении заказа.

## Формата запроса и пример

### Пример

```javascript
{
    "externalUserId": "XXXXXX",
    "country": "RU",
    "city": "Москва",
    "promocode": null,
    "deliveryId": "14",
    "pickupLocationId": "100",
    "items": [
        {
            "name": "Тестовый товар 1",
            "id": "00a03026-412a-54fe-a9df-dcf9325f8618",
            "privateId": "3464",
            "configurationId": "3464",
            "price": 3735,
            "quantity": 1,
            "discount": 0,
            "subtotal": 3735
        },
        {
            "name": "Тестовый товар 2",
            "id": "605e0108-dc95-5dab-95a2-7f459da6aade",
            "privateId": "29117",
            "configurationId": "29117",
            "price": 14540,
            "quantity": 1,
            "discount": 0,
            "subtotal": 14540
        },
        {
            "name": "Тестовый товар 3",
            "id": "3ccd380e-1f40-5056-8a7a-ef6e8a9582b5",
            "privateId": "34607",
            "configurationId": "34607",
            "price": 5723,
            "quantity": 2,
            "discount": 0,
            "subtotal": 11446
        },
        {
            "name": "Тестовый товар 4",
            "id": "523036eb-b776-5795-b24b-0f224f2d8b17",
            "privateId": "6527",
            "configurationId": "6527",
            "price": 29336,
            "quantity": 1,
            "discount": 0,
            "subtotal": 29336
        }
    ]
}
```

### Описание формата

* **`externalUserId`** - идентификатор покупателя на стороне клиента \(`null` если не известен, или новый покупатель\)
* **`country`** - ISO код страны
* **`city`** - стандартизированное имя города из системы ФИАС
* **`promocode`** - прикрепленный промокод в виде строки. `null` если промокод не был применен
* **`deliveryId`** - идентификатор выбранного способа доставки
* **`pickupLocationId`** - выбранный пункт получения заказа \(`null` если доставка или не подразумевает выбора пвз\)
* **`items`** - список товаров в корзине
  * **`id`** - идентификатор товара в IMSHOP.IO
  * **`configurationId`** - идентификатор товарного предложения в IMSHOP.IO
  * **`privateId`** - идентификатор товарного предложения в системе клиента
  * **`name`** - наименование,
  * **`price`** - цена товара за 1 позицию
  * **`quantity`** - количество
  * **`discount`** - скидка на всю позицию
  * **`subtotal`** - итого за позицию \(`subtotal` = \(`price` \* `quantity`\) - `discount`\)

## Ответ

### Описание формата

* **`payments`** - список доступных способов оплаты
  * **`id`** - идентификатор
  * **`title`** - название
  * **`description`** - описание
  * **`type`** - тип 
    * `cash` - оплата наличнами
    * `card_on_delivery` - картой курьеру или при получении
    * `card` - картой в приложении
    * `iOS` - Apple Pay

### Пример

```javascript
{
    "payments": [
        {
            "id": "cash",
            "title": "Оплата наличными при получении",
            "description": "Оплата наличными курьеру при получении заказа",
            "type": "cash"
        },
        {
            "id": "card",
            "title": "Картой в приложении",
            "description": "Оплата картой visa или mastercard в приложении",
            "type": "card"
        }]
    ]
}
```

