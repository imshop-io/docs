# Рейтинг качества обслуживания

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../oformlenie-zakaza.-dostavki-oplaty/order.md)
* [Доставки](../oformlenie-zakaza.-dostavki-oplaty/deliveries.md)
* [Оплаты](../oformlenie-zakaza.-dostavki-oplaty/payments.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

## Запрос

`APP SERVER → INFRASTRUCTURE`

{% hint style="info" %}
От вас потребуется URL, на который наш сервер будет слать **POST**-запрос. Да, мы _запрашиваем_ данные через _POST_, а не через _GET_.
{% endhint %}

В вашу систему будут приходить вот такие данные:

```javascript
{
      "orderId": "1230"
      "rating": 5,
      "comment": "Все хорошо",
}
```

* `orderId` — номер заказа (строка)
* `rating` — значение от 1 до 5 (число)
* `comment` — комментарий (строка)
