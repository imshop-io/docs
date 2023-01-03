# Apple pay

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

* Пользователь находится на корзине / на карточке товара и видит кнопку "купить с Apple Pay"
* Пользователь нажимает кнопку Apple Pay, проверяет контакт, адрес доставки и стоимость, и подтверждает оплату
* Заказ оформляется и выгружается в систему клиента через webhook. Заказу присваивается номер
* IMSHOP.IO делает запрос в webhook управления оплатами на создание платежа через Apple Pay. В теле запроса передается криптограмма Apple Pay
* Система клиента передает криптограмму в процессор платежей и инициирует списание средств. Если оплата прошла, то webhook передает идентификатор платежа и статус. Если заказ не прошел, webhook должен вернуть ошибку
* IMSHOP.IO помечает заказ как оплаченный

## Создание платежа ApplePay

### Пример запроса

```json
{
    "command": "applepay",
    "paymentMethodId": "sberbank/applepay",
    "orderUuid": "cbc85e53-8067-4f13-a708-11d9aea71bf3",
    "orderId": "12345",
    "applePayData": "xxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

* **`command`** - запрос на создание оплаты Apple Pay (**`applepay`**)
* **`paymentMethodId`** - выбранный покупателем способ оплаты. Берется из ответа [webhook получения способов оплат](https://developer.imshop.io/developers/deliveries-and-payments/payments)
* **`orderUuid`** - внутренний номер заказа в IMSHOP.IO
* **`orderId`** - внешний номер заказа в системе клиента
* **`applePayData`** - криптограмма Apple Pay, в формате base64

### Пример ответа

```json
{
    "success": true,
    "paymentId": "7d0567f9-bf37-4e84-9580-86b68b8a0e81",
    "paymentCaptured": true
}
```

* **`success`** - флаг успеха **`true`** / **`false`**
* **`paymentId`** - идентификатор платежа
* **`paymentCaptured`** - деньги успешно списаны
* **`error`** - текст ошибки если **`success`** = **`false`**
