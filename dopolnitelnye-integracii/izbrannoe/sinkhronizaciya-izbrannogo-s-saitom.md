# Синхронизация избранного с сайтом

{% hint style="info" %}
Чтобы подключить синхронизацию избранного, обратитесь к product менеджеру в IMSHOP.IO и **получите API ключ** интеграции
{% endhint %}

## Синхронизация при обновлении избранного в приложении

При обновлении избранного в приложении, IMSHOP.IO сделает запрос с полным текущим содержимым избранного в приложении. В ответ IMSHOP.IO ожидает новый полный актуальный список избранного.

### Формат запроса

* **`userId`** - идентификатор пользователя
* **`wishlist`** - список товаров
  * **`id`** - идентификатор товара
  * **`hidden`** - товар скрыт (soft-deleted) из избранного
  * **`syncedOn`** - [таймштамп](https://www.unixtimestamp.com/) последнего обновления записи
  * **`pricedropPrice`** - цена товара на момент добавления в вишлись
  * **`notify`**
    * **`pricedrop`** - **true** / **false**. Уведомить покупателя через push - уведомление при снижении цены на товар

### Пример запроса

```json
{
    "userId": "userId123",
    "wishlist": [
        {
            "id": "itemId1",
            "hidden": false,
            "syncedOn": 1649878707
        },
        {
            "id": "itemId1",
            "hidden": false,
            "syncedOn": 1649878707,
            "notify": {
                "pricedrop": true
            },
            "pricedropPrice": 10999
        }
    ]
}
```

### Формат ответа

В ответ необходимо отдать новый полный список товаров вишлиста

* **`id`** - идентификатор товара
* **`hidden`** - товар скрыт (soft-deleted) из избранного
* **`syncedOn`** - [таймштамп](https://www.unixtimestamp.com/) последнего обновления записи
* **`pricedropPrice`** - цена товара на момент добавления в вишлись
* **`notify`**
  * **`pricedrop`** - **`true`**/ **`false`**. Уведомить покупателя через push - уведомление при снижении цены на товар

### Пример ответа

```json
[
    {
        "id": "itemId1",
        "hidden": false,
        "syncedOn": 1649878707
    },
    {
        "id": "itemId1",
        "hidden": false,
        "syncedOn": 1649878707,
        "notify": {
            "pricedrop": true
        },
        "pricedropPrice": 10999
    }
]
```

## Синхронизация при обновлении избранного на сайте

При обновлении избранного на сайте необходимо сделать запрос по URL, который передаст вам ваш product manager.

### Формат запроса

* **`userId`** - идентификатор пользователя
* **`wishlist`** - полный состав избранного
  * **`id`** - идентификатор товара
  * **`hidden`** - товар скрыт (soft-deleted) из избранного
  * **`syncedOn`** - [таймштамп](https://www.unixtimestamp.com/) последнего обновления записи
  * **`pricedropPrice`** - цена товара на момент добавления в избранное
  * **`notify`**
    * **`pricedrop`** - **true** / **false**. Уведомить покупателя через push - уведомление при снижении цены на товар

### Пример запроса

```json
{
    "userId": "userId123",
    "wishlist": [
        {
            "id": "itemId1",
            "hidden": false,
            "syncedOn": 1649878707
        },
        {
            "id": "itemId1",
            "hidden": false,
            "syncedOn": 1649878707,
            "notify": {
                "pricedrop": true
            },
            "pricedropPrice": 10999
        }
    ]
}
```

### Формат ответа

Ответ будет иметь HTTP статус **200**, если синхронизация прошла успешно

Ответ будет иметь статус **404**, если пользователь с заданным userId не пользовался приложением и никогда не авторизовывался в приложении

## Полная синхронизация избранного