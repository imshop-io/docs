# Персональные предложения в розничном магазине

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../oformlenie-zakaza.-dostavki-oplaty/order.md)
* [Доставки](../oformlenie-zakaza.-dostavki-oplaty/deliveries.md)
* [Оплаты](../oformlenie-zakaza.-dostavki-oplaty/payments.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

## Описание

Данный метод вызывается при сканировании QR кода в розничных магазинах, для получения индивидуального предложения для зарегистрированного покупателя на товар в магазине

## Запрос

* **`externalUserId`** - идентификатор покупателя
* **`locationId`** - идентификатор магазина
* **`itemId`** - идентификатор товара из фида \(**`group_id`**, если есть группировка, или **`id`** если группировок нет\)

### Пример запроса

```javascript
{
    "externalUserId": "123456789",
    "locationId": "0240",
    "itemId": "17888999"
}
```

## Ответ

* personalInStorePrice - персональная цена в данном магазине
* code - код для отображения на экране телефона для считывания на кассе
  * type - тип кода. поддерживаемые стандарты: code128, qr
  * value - значение, которое надо передать в коде

{% hint style="info" %}
При отсутствии предложений на данный товар необходимо ответить пустым телом с HTTP кодом 204
{% endhint %}

### Пример ответа

```javascript
{
    "personalInStorePrice": 499.00,
    "code": {
        "type": "qr",
        "value": "aaa-b-cc-d-88888"
    }    
}
```



