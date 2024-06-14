# Виджет описания рассрочки

{% hint style="danger" %}
**IMSHOP Retail Protocol (IRP)** является объектом интеллектуальной собственности ООО «АЙ ЭМ СОЛЮШНЗ» (IMSHOP) и защищён как объект авторского права. Свидетельство о депонировании произведения № 023-014461 от 16 января 2023 г. подтверждает исключительные права ООО «АЙ ЭМ СОЛЮШНЗ» на данные технологии.

IMSHOP Retail Protocol создан по заказу ООО «АЙ ЭМ СОЛЮШНЗ». Использование IMSHOP Retail Protocol допустимо только при взаимодействии с ООО "АЙ ЭМ СОЛЮШНЗ" и наличии действующего лицензионного договора. Более подробно можно ознакомиться [здесь](../../api-license.md).
{% endhint %}

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../../osnovnye-integracii/oformlenie-zakaza.md)
* [Доставки](../../osnovnye-integracii/dostavki.md)
* [Оплаты](../../osnovnye-integracii/oplaty.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

IMSHOP.IO позволяет вывести виджет рассрочки на карточке товара для информирования покупателей о том что на этот товар есть рассрочка и увидеть предполагаемый график платежей.

## Формат запроса и пример

### Пример

```javascript
{
  "itemId": "12345",
  "itemPrice": 12345,
}
```

### Описание формата

* **`itemId`** - ID товара в системе клиента
* **`itemPrice`** - цена товара из фида

## Формат ответа и пример

### Описание формата

### Пример

```javascript
{
    "installment":
    {
        "itemWidgetButton":
        {
            "buttonText": "asd",
            "buttonIconSrc": "imshop.io/icons/1.png",
            "buttonIconWidth": 60,
            "buttonIconHeight": 20
        },
        "widgetPages":
        [
            {
                "tabName": "Долями",
                "title": "asd",
                "description": "asd asd asd",
                "topImageSrc": "imshop.io/icons/1.png",
                "topImageWidth": 120,
                "topImageHeight": 40,
                "paymentsGraphic":
                [
                    {
                        "periodPrice": "2200 $",
                        "periodDescription": "asd",
                        "progress": 25
                    }
                ],
                "additionalTextes":
                [
                    "asd asd asd"
                ],
                "footerText": "asdasdasdasd imshop.io"
            },
            {
                "tabName": "Подели",
                "title": "asd2",
                "description": "asd asd asd",
                "topImageSrc": "imshop.io/icons/1.png",
                "topImageWidth": 120,
                "topImageHeight": 40,
                "paymentsGraphic":
                [
                    {
                        "periodPrice": "2200 $",
                        "periodDescription": "asd",
                        "progress": 25
                    }
                ],
                "additionalTextes":
                [
                    "asd asd asd"
                ],
                "footerText": "asdasdasdasd imshop.io"
            }
        ]
    }
}
```

### Описание формата

* **`itemWidgetButton`** - описание кнопки на карточке товара
  * **`buttonText`** - текст кнопки
  * **`buttonIconSrc`** - иконка кнопки
  * **`buttonIconWidth`** - ширина иконки кнопки
  * **`buttonIconHeight`** - высота иконки кнопки
* **`widgetPages`** - описание экранов виджета (массив)
  * **`title`** - заголовок экрана виджета&#x20;
  * **`tabName`** - наазвания в переключателе между экранами&#x20;
  * **`description`** - основное описание экрана виджета
  * **`topImageSrc`** - иконка вверху экрана виджета
  * **`topImageWidth`** - ширина иконки вверху экрана виджета
  * **`topImageHeight`** - высота иконки вверху экрана виджета
  * **`paymentsGraphic`** - описание графика платежей (массив)
    * **`periodPrice`** - текст цены за период
    * **`periodDescription`** - описание, например дата платежа
    * **`progress`** - процент платежа от основной цены
  * **`additionalTextes`** - дополнительные пункты описания, например преимущества или выдержка из описания (массив)
  * **`footerText`** - текст колонтитула, поддерживает url например на детальное описание программы рассрочки
