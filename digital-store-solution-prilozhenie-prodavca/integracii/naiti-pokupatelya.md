# Найти покупателя

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

## Получение информации о Покупателе

{% hint style="info" %}
Для подключения обратитесь к вашему личному менеджеру в IMSHOP
{% endhint %}

### Формат запроса

* **`clientVersion`** - версия мобильного приложения
* **`userIdentifier`** - идентификатор пользователя (обязательное поле), полученный от системы клиента на этапе авторизации (как правило, это телефон)

#### Пример запроса

```javascript
{
	"clientVersion": "6.55.1",
	"userIdentifier": "79058138138"
}
```

### Формат ответа

* **`user`** - полная информация о покупателе
  * **`name`** - имя покупателя
  * **`email`** - адрес электронной почты
  * **`smsNotification`** - согласие на получение SMS-уведомлений
  * **`emailNotification`** - согласие на получение уведомлений на электронную почту
  * **`id`** - идентификатор учетной записи покупателя
  * **`bonuses`** - количество бонусных баллов у покупателя
  * **`cardNumber`** - номер карты лояльности

#### Пример ответа

<pre class="language-javascript"><code class="lang-javascript">    {
        "user": {
            "name": "Ted Lasso",
            "email": "ted@lasso.com",
            "smsNotification": true,
            "emailNotification": false,
            "bonuses": 10000,
            "cardNumber": "777696969",
            "id": "79058138138"
        }
<strong>    }
</strong></code></pre>
