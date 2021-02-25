# Оформление заказа

{% hint style="info" %}
Для подключения webhook передачи заказа, обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

## Формат запроса и пример

### Пример

```javascript
{
    "device": {
        "platform": "ios"
    },
    "installId": "9e201bab-1ccf-47d1-82e0-90d71ee5fd2c",
    "orders": [{
        "uuid": "2d81f6e5-01cb-44ca-abb0-ded88c1fc982",
        "externalUserId": "XXXXXX",
        "groupId": "2d81f6e5-01cb-44ca-abb0-ded88c1fc982",
        "createdOn": "2018-10-15 12:54:18.356089",
        "updatedOn": "2018-10-15 12:54:18.356089",
        "status": "placed",
        "name": "Дмитрий",
        "phone": "+7 (999) 999-9999",
        "email": "some@mail.com",
        "country": "RU",
        "city": "Москва",
        "address": "ул Тестовая, д 1",
        "addressData": {
            "city": "Москва",
            "region": "Москва",
            "street": "Тестовая",
            "house": "1",
            "building": null,
            "apt": null,
            "zip": "127001",
            "kladr": "7700000000000",
            "city_kladr": "7700000000000",
            "fias_code": "77000000000000000000000",
            "fias_id": "0c5b2444-70a0-4932-980c-b4dc0d3f02b5"
        },
        "addressComponents": {
            "city": "Москва",
            "street": "Тестовая",
            "house": "1",
            "building": null,
            "apt": null,
        },
        "price": 28065.00,
        "deliveryPrice": 250.00,
        "authorizedBonuses": 300,
        "promocode": null,
        "appliedDiscount": 0,
        "loyaltyCard": null,
        "delivery": "boxberry/pickup",
        "deliveryDate": "2019-10-25",
        "deliveryName": "Доставка в пункт самовывоза Боксберри",
        "pickupLocationId": "db30c598-2717-4adc-8e0c-9341786ba1f4",
        "pickupLoactionSnapshot": {},
        "payment": "internal/4",
        "paymentName": "Наличными курьеру",
        "paymentProcessed": false,
        "paymentId": "87da77a2-de03-40a0-91b7-eadabce5db22",
        "paymentGateway": "yandex",
        "externalIds": { "webhook": "66510", "retailcrm": "1456AA", "bitrix": "614" },
        "deliveryComment": "Домофон не работает",
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
              "subtotal": 29336,
              "variableParams": {
                "width": "30",
                "height": "10",
                "length": "60"
              }
            }
        ]
    }]
}
```

### Описание формата

* **`device`** - информация об устройстве пользователя
  * **`platform`**- ios или android 
* **`installId`** - идентификатор установки приложения
* **`orders`** - список заказов \(за 1 запрос может выгружаться более 1 заказа\)
  * **`uuid`** - идентификатор заказа на стороне IMSHOP.IO
  * **`externalUserId`** - идентификатор покупателя на стороне клиента \(`null` если не известен, или новый покупатель\)
  * **`groupId`** - идентификатор группировки заказа \(Если один заказ был разбит на несколько дочерних заказов, они будут иметь одинаковый `groupId` и всегда будут отправлены в одном запросе. Если это одиночный заказ, то значение этого поля будет `null`\)
  * **`createdOn`** - время создания заказа
  * **`updatedOn`** - время изменения заказа
  * **`status`** - статус заказа в IMSHOP.IO. Возможные значения:
    * `placed` - создан
    * `processing` - в обработке
    * `ready_to_dispatch` - готов к отправке
    * `dispatched` - отправлен в доставку
    * `ready_for_pickup` - готов к выдаче
    * `delivered` - доставлен
    * `closed` - завершен без выкупа
    * `canceled` - отменен
    * `done` - выполнен. выкуплен.
  * **`name`** - имя покупателя
  * **`phone`** - телефон
  * **`email`** - электронная почта
  * **`country`** - ISO код страны
  * **`city`** - стандартизированное имя города из системы ФИАС
  * **`address`** - адрес в виде текста
  * **`addressData`** - подробные данные об адресе доставки, включая идентификаторы из КЛАДР и ФИАС
  * **`addressComponents`** - данные об адресе доставки по полям как ввел пользователь
  * **`price`** - цена корзины
  * **`deliveryPrice`** - рассчитанная цена доставки
  * **`authorizedBonuses`** - запрос на списание баллов \(если у клиента есть бонусная ПЛ\)
  * **`promocode`** - прикрепленный промокод в виде строки. `null` если промокод не был применен
  * **`appliedDiscount`** - общая скидка на заказ включая промокод и все маркетинговые акции
  * **`loyaltyCard`** - идентификатор или номер карты лояльности \(если есть, иначе `null`\)
  * **`delivery`** - идентификатор способа доставки в формате **`<источник>/<идентификатор>`**. Например: **`webhook/a1`** для доставки с идентификатором **`a1`**, полученной из вебхук-интеграции доставок
  * **`deliveryDate`** - желаемая дата доставки
  * **`deliveryName`** - название способа доставки
  * **`pickupLocationId`** - идентификатор выбранного пункта самовывоза \(ПВЗ, постамат или магазин, в зависимости от `delivery`\)
  * **`pickupLoactionSnapshot`** - снимок метадаты о пункте самовывоза на момент заказа \(берется из API службы доставки\)
  * **`payment`** - выбранный способ оплаты
  * **`paymentName`** - название способа оплаты
  * **`paymentProcessed`** - флаг того, что заказ оплачен
  * **`paymentId`** - идентификатор платежа
  * **`paymentGateway`** - использованный эквайринг
  * **`externalIds`** - список идентификаторов этого же заказа в других системах
  * **`deliveryComment`** - комментарий к заказу
  * **`items`** - список товаров в корзине
    * `id` - идентификатор товара в IMSHOP.IO
    * `configurationId` - идентификатор товарного предложения в IMSHOP.IO
    * `privateId` - идентификатор товарного предложения в системе клиента
    * `name` - наименование,
    * `price` - цена товара за 1 позицию
    * `quantity` - количество
    * `discount` - скидка на всю позицию
    * `subtotal` - итого за позицию \(`subtotal` = \(`price` \* `quantity`\) - `discount`\)
    * `variableParams` - параметры товара, выбранные пользователем \(см. [Товар: цвета, размеры и другие характеристики](../sync/yml/tovar-cveta-razmery-i-drugie-kharakteristiki.md)\)

## Формат ответа и пример

### Описание формата

* **`message`** - \(опционально\) Кастомное сообщение для клиента, отображаемое на странице "спасибо за заказ" после оформления заказа
* **`orders`** - cписок принятых / не принятых заказов
  * **`success`** - `true` или `false` \(`boolean`\). флаг успеха. `true` если заказ принят
  * **`errorCode`** - код ошибки если `success` = `false`
  * **`errorMessage`** - описание ошибки если `success` = `false`
  * **`id`** - идентификатор созданного заказа в системе клиента
  * **`publicId`** - отображаемый публичный номер заказа \(опционально, если не совпадает с `id`\)
  * **`uuid`** - идентификатор заказа в IMSHOP.IO, полученный в запросе
  * **`price`** - \(опционально\) цена заказа
  * **`deliveryPrice`** - \(опционально\) цена доставки
  * **`items`** - список товаров в корзине **\(опционально, но обязательно, если возвращается больше одного заказа\)**
    * **`id`** - идентификатор товара в IMSHOP.IO
    * **`configurationId`** - идентификатор товарного предложения в IMSHOP.IO
    * **`privateId`** - идентификатор товарного предложения в системе клиента
    * **`name`** - наименование,
    * **`price`** - цена товара за 1 позицию
    * **`quantity`** - количество
    * **`discount`** - скидка на всю позицию
    * **`subtotal`** - итого за позицию \(`subtotal` = \(`price` \* `quantity`\) - `discount`\)

### Пример ответа

```javascript
{
  "message": "Ваш заказ принят.\nЗаказ будет готов к выдаче сегодня после 14:00",
  "orders": [
    {
      "success": true,
      "id": "12345",
      "publicId": "ЗКЗ445566",
      "uuid": "2d81f6e5-01cb-44ca-abb0-ded88c1fc982",
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
  ]
}
```

