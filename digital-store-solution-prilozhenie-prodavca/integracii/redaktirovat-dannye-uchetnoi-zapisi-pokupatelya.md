# Редактировать данные учетной записи Покупателя

{% hint style="danger" %}
**IMSHOP Retail Protocol© (IRP)** является объектом интеллектуальной собственности ООО «АЙ ЭМ СОЛЮШНЗ» (Imshop) и защищён законом об авторском праве как ноу-хау. Использование Imshop Retail Protocol допустимо только при взаимодействии с ООО "АЙ ЭМ СОЛЮШНЗ" и наличии действующего лицензионного договора. Более подробно можно ознакомиться [здесь](../../api-license.md).
{% endhint %}

{% hint style="danger" %}
Используется **PATCH**-запрос
{% endhint %}

## Обновление данных пользователя по идентификатору

{% hint style="info" %}
Для подключения обратитесь к вашему личному менеджеру в IMSHOP
{% endhint %}

### Формат запроса

`APP SERVER → INFRASTRUCTURE`

* **`email`** - адрес электронной почты
* **`emailNotification`** - согласие на получение уведомлений на электронную почту
* **`name`** - имя покупателя
* **`phone`** - телефон покупателя
* **`smsNotification`** - согласие на получение SMS-уведомлений
* **`userIdentifier`** - идентификатор учетной записи покупателя

Если то или иное поле в запросе отсутствует — соответствующую информацию обновлять не нужно.

#### Пример запроса

<pre class="language-javascript"><code class="lang-javascript"><strong>    {
</strong>        "email": "arthur@morgan.com",
<strong>        "emailNotification": true,
</strong>        "name": "Arthur Morgan",
        "phone": "79619619619",
        "smsNotification": true,
        "userIdentifier": "79619619619",
    }
</code></pre>

### Формат ответа

* **`user`** - полная информация о покупателе
  * **`name`** - имя покупателя
  * **`email`** - адрес электронной почты
  * **`smsNotification`** - согласие на получение SMS-уведомлений
  * **`emailNotification`** - согласие на получение уведомлений на электронную почту
  * **`bonuses`** - количество бонусных баллов у покупателя
  * **`cardNumber`** - номер карты лояльности
  * **`id`** - идентификатор учетной записи покупателя

#### Пример ответа

<pre class="language-javascript"><code class="lang-javascript">    {
        "user": {
            "name": "Arthur Morgan",
            "email": "arthur@morgan.com",
            "smsNotification": true,
            "emailNotification": true,
            "bonuses": 777,
            "cardNumber": "777696969",
            "id": "79619619619"
        }
<strong>    }
</strong></code></pre>
