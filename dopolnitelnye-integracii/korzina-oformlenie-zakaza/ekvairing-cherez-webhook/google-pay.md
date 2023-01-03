# Google pay

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

### Google Pay

* Пользователь находится на корзине / на карточке товара и видит кнопку "купить с Google Pay"
* Пользователь нажимает кнопку Google Pay, адрес доставки и стоимость, и подтверждает оплату
* Заказ оформляется и выгружается в систему клиента через webhook. Заказу присваивается номер
* IMSHOP.IO делает запрос в webhook управления оплатами на создание платежа через Google Pay. В теле запроса передается криптограмма Google Pay
* Система клиента передает криптограмму в процессор платежей и инициирует списание средств. Если оплата прошла, то webhook передает идентификатор платежа и статус. Если заказ не прошел, webhook должен вернуть ошибку
* IMSHOP.IO помечает заказ как оплаченный

### Создание платежа Google Pay

### **Пример запроса**

```json
{
    "command": "androidpay",
    "paymentMethodId": "sberbank/androidpay",
    "orderUuid": "cbc85e53-8067-4f13-a708-11d9aea71bf3",
    "orderId": "12345",
    "androidPayData": "xxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

* **`command`** - запрос на создание оплаты Google Pay (**`androidpay`**)
* **`paymentMethodId`** - выбранный покупателем способ оплаты. Берется из ответа [webhook получения способов оплат](../../../osnovnye-integracii/oplaty.md)
* **`orderUuid`** - внутренний номер заказа в IMSHOP.IO
* **`orderId`** - публичный номер заказа в системе клиента
* **`android`** - криптограмма Android Pay, в формате base64

### **Пример ответа**

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
