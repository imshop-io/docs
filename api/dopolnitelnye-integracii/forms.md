# Формы



{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../oformlenie-zakaza.-dostavki-oplaty/order.md)
* [Доставки](../oformlenie-zakaza.-dostavki-oplaty/deliveries.md)
* [Оплаты](../oformlenie-zakaza.-dostavki-oplaty/payments.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

{% hint style="info" %}
Вам необходимо предоставить:

* URL для подключения, по которому мы сможем отправлять данные формы в вашу систему
* API ключ
{% endhint %}

## Запрос

### Описание формата

* **`formId`** - id формы в системе imshop
* **`data`** - данные формы в формате ключ-значение

### Пример запроса

```javascript
{
    "formId": "form_123",
    "data": {
        "name": "ФИО",
        "email": "test@test.test",
        "phone": "79998887766"
    }
}
```

## Ответ

### Формата ответа

* **`success`** - флаг успеха

### Пример ответа

```javascript
{
    "success": true
}
```

