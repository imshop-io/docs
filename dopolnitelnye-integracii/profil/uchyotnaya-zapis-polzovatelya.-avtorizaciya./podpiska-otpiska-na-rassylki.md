# Подписка/отписка на рассылки



{% hint style="danger" %}
**IMSHOP Retail Protocol (IRP)** является объектом интеллектуальной собственности ООО «АЙ ЭМ СОЛЮШНЗ» (IMSHOP) и защищён как объект авторского права. Свидетельство о депонировании произведения № 023-014461 от 16 января 2023 г. подтверждает исключительные права ООО «АЙ ЭМ СОЛЮШНЗ» на данные технологии.

IMSHOP Retail Protocol создан по заказу ООО «АЙ ЭМ СОЛЮШНЗ». Использование IMSHOP Retail Protocol допустимо только при взаимодействии с ООО "АЙ ЭМ СОЛЮШНЗ" и наличии действующего лицензионного договора. Более подробно можно ознакомиться [здесь](../../../api-license.md).
{% endhint %}

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../../../osnovnye-integracii/oformlenie-zakaza.md)
* [Доставки](../../../osnovnye-integracii/dostavki.md)
* [Оплаты](../../../osnovnye-integracii/oplaty.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

IMSHOP.IO получает данные о доступных пользователю рассылках

## Формат ответа и пример

### Пример

```javascript
{
  "notifications": [
    {
      "id": "sms",
      "title": "СМС уведомления"
    },
    {
      "id": "email",
      "title": "EMAIL уведомления"
    }
  ]
}
```

### Описание формата

* **`notifications`** - список доступных уведомлений
  * **`id`** - идентификатор. Используется в ендпоинте [редактирования информации пользователя](obekt-uchyotnaya-zapis-polzovatelya.md)&#x20;
  * **`title`** - наименование уведомление, которое будет отображаться пользователю
