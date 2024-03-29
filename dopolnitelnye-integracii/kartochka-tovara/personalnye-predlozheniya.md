# Персональные предложения

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../../osnovnye-integracii/oformlenie-zakaza.md)
* [Доставки](../../osnovnye-integracii/dostavki.md)
* [Оплаты](../../osnovnye-integracii/oplaty.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

## Запрос

* **`externalUserId`** - идентификатор покупателя
* **`itemId`** - идентификатор товара из фида (**`group_id`**, если есть группировка, или **`id`** если группировок нет)

### Пример запроса

```javascript
{
    "externalUserId": "123456789",
    "itemId": "17888999"
}
```

## Ответ

* **`personalInStorePrice`** - персональная цена в данном магазине

{% hint style="info" %}
При отсутствии предложений на данный товар необходимо ответить пустым телом с HTTP кодом 204
{% endhint %}

### Пример ответа

```json
{
    "personalInStorePrice": 499.00   
}
```
