# Рекомендации товаров

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../../osnovnye-integracii/oformlenie-zakaza.md)
* [Доставки](../../osnovnye-integracii/dostavki.md)
* [Оплаты](../../osnovnye-integracii/oplaty.md)

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
      "privateId": "12345",
      "userIdentifier": "qwerty12345"
}
```

* **`privateId`** — id товара \*
* **`userIdentifier`** — external id  (идентификатор пользователя в системе клиента)

### Ответ

Массив с объектами

**`ids`** - массив с id товарами

**`title`** - Название для отдела с товарами

#### Пример ответа

```javascript
[{ ids: ["12345"], title: "Покупают вместе с этим" }]
```
