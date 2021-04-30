# Поиск. Поисковая выдача

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../oformlenie-zakaza.-dostavki-oplaty/order.md)
* [Доставки](../oformlenie-zakaza.-dostavki-oplaty/deliveries.md)
* [Оплаты](../oformlenie-zakaza.-dostavki-oplaty/payments.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

## Формат запроса

* `term` — поисковый запрос
* `location` — локация пользователя, объект «[Местоположение](../obekt-mestopolozhenie.md)»
* `page` — страница выдачи; размер страницы по умолчанию — 10 товаров

```javascript
{
    "term": "Стиральн",
    "location": {
        "city": "Москва",
        "cityFiasId": "0c5b2444-70a0-4932-980c-b4dc0d3f02b5",
        "region": "Москва",
        "regionFiasId": "0c5b2444-70a0-4932-980c-b4dc0d3f02b5"
    },
    "page": 1
}
```

## Формат ответа

* `items` - список ID товаров из фида \(`group_id` если есть, иначе `id`\)

```javascript
{
    "items": ["789887", "961551", "55598192"]
}
```

