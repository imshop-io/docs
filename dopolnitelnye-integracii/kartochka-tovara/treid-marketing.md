---
description: Комплекты
---

# Трейд-маркетинг

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

## Описание

Данный метод позволяет получить список разных маркетинговых предложений для конкретного товара.\
\
Список возможных маркетинговых предложений**:**\
1\) Комплекты (Kits). Это список товаров в дополнение к текущему, чтобы появилась возможность купить вместо какого-то товара целый комплект по сниженной стоимости. Можно передать несколько комплектов к товару.

## Как работает

При переходе на экран товара отправляется запрос на получения списка маркетинговых предложений. После успешного получения списка маркетинговых предложений, они отобразятся на экране товара.

Порядок действий:

* Пользователь зашел на экран товара
* Ушел запрос на получение маркетинговых предложений для этого товара
* Пришел ответ со всеми маркетинговыми предложениями
* Маркетинговые предложения отобразились на экране товара

## Получение маркетинговых предложений

### Формат запроса

* **`itemId`** (required, тип: string)- идентификатор товара, на экран которого зашел пользователя. К этому товару получаем список маркетинговых предложений.

#### Пример запроса

```javascript
{
    "itemId": "ad221bac-5ea1",
}
```

### Формат ответа

* **`kits`** (optional, тип: `array<object>`) - комплекты. У каждого комплекта есть следующие параметры:
  * **`id`** (required, тип: `string`) - уникальный идентификатор комплекта
  * **`fullPrice`** (required, тип: `number`) - полная цена - цена, если бы каждый товар покупался отдельно
  * **`kitPrice`** (required, тип: `number`) - цена комплекта - выгодная цена за весь комплект
  * **`benefit`** (required, тип: `number`) - выгода от приобретения комплекта (**`fullPrice - kitPrice`**)
  * **`title`** (optional, тип: `string`)- описание комплекта (выводится под товарами комплекта)
  * **`kitItems`** (required, тип: `array<object>`) - товары, входящие в комплект. Для товара передаются следующие параметры:
    * **`id`** (required, тип: `string`) - идентификатор товара - должен быть такой же, как и в каталоге всего приложения (**`group_id`** для каталога с вариантами товаров, или **`id`** для остальных случаев)
    * **`image`** (required, тип: `string`) - uri картинки товара
    * **`price`** (required, тип: `number`) - полная цена - цена за товар, если покупать без комплекта
    * **`kitPrice`** (required, тип: `number`) - цена за товар в комплекте
    * **`title`** (required, тип: `string`) - название товара

#### Пример комплекта

```javascript
{
    "id": "asdf-asdf-ljkasdf",
    "fullPrice": 15990,
    "kitPrice": 14990,
    "benefit": 1000,
    "kitItems": [
        {
            "id": "91fe51cc-1bac-5ea1-ad22",
            "image": "https://someImageUriForItem1",
            "price": 5990,
            "kitPrice": 5590,
            "title": "Item 1 title"
        },
        {
            "id": "fbc15b04b429-1bac-5ea1-ad22-91fe51cc",
            "image": "https://someImageUriForItem2",
            "price": 6000,
            "kitPrice": 5600,
            "title": "Item 2 title"
        },
        {
            "id": "1bac-fbc15b04b4291bac-5ea1-ad22-91fe51cc",
            "image": "https://someImageUriForItem3",
            "price": 4000,
            "kitPrice": 3800,
            "title": "Item 3 title"
        }
    ]
}
```



#### Пример ответа всего запроса:

```javascript
{
    "kits": [
        {
            "id": "asdf-asdf-ljkasdf",
            "fullPrice": 15990,
            "kitPrice": 14990,
            "benefit": 1000,
            "title": "описание первого комплекта товара",
            "kitItems": [
                {
                    "id": "91fe51cc-1bac-5ea1-ad22",
                    "image": "https://someImageUriForItem1",
                    "price": 5990,
                    "kitPrice": 5590,
                    "title": "Item 1 title"
                },
                {
                    "id": "fbc15b04b429-1bac-5ea1-ad22-91fe51cc",
                    "image": "https://someImageUriForItem2",
                    "price": 6000,
                    "kitPrice": 5600,
                    "title": "Item 2 title"
                },
                {
                    "id": "1bac-fbc15b04b4291bac-5ea1-ad22-91fe51cc",
                    "image": "https://someImageUriForItem3",
                    "price": 4000,
                    "kitPrice": 3800,
                    "title": "Item 3 title"
                }
            ]
        },
        {
            "id": "qqqq-asdf-asdf-",
            "fullPrice": 2000,
            "kitPrice": 1100,
            "benefit": 900,
            "title": "описание второго комплекта товара",
            "kitItems": [
                {
                    "id": "91fe51cc-1bac-5ea1-ad22",
                    "image": "https://someImageUriForItem1",
                    "price": 1000,
                    "kitPrice": 1000,
                    "title": "Item 1 title"
                },
                {
                    "id": "fbc15b04b429-1bac-5ea1-ad22-91fe51cc",
                    "image": "https://someImageUriForItem2",
                    "price": 1000,
                    "kitPrice": 100,
                    "title": "Item 2 title"
                }
            ]
        }
    ]
}
```

