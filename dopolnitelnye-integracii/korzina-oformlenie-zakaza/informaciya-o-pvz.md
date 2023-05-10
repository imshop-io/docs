# Информация о пвз

## Запрос

### Описание формата

* **`locationId`** - str, id ПВЗ
* **`address`** - информация о локации пользователя
* **`items`** - arr, корзина
* **`id`**: configurationId товара
* **`quantity`**: number, количество

### Пример запроса

```json
{
    "address":
    {
        "location":
        {
            "apt": null,
            "area": null,
            "areaFiasId": null,
            "areaKladrId": null,
            "areaWithType": null,
            "block": null,
            "city": "Москва",
            "cityFiasId": "0c5b2444-70a0-4932-980c-b4dc0d3f02b5",
            "cityKladrId": "7700000000000",
            "cityWithType": "г Москва",
            "federalDistrict": "Центральный",
            "fiasCode": "7700000000000000000",
            "fiasId": "0c5b2444-70a0-4932-980c-b4dc0d3f02b5",
            "house": null,
            "houseFiasId": null,
            "houseKladrId": null,
            "kladrId": "7700000000000",
            "lat": "55.75396",
            "lon": "37.620393",
            "postalCode": "101000",
            "region": "Москва",
            "regionFiasId": "0c5b2444-70a0-4932-980c-b4dc0d3f02b5",
            "regionKladrId": "7700000000000",
            "regionWithType": "г Москва",
            "settlement": null,
            "settlementFiasId": null,
            "settlementKladrId": null,
            "settlementWithType": null,
            "street": null,
            "streetFiasId": null,
            "streetKladrId": null,
            "streetType": null,
            "streetWithType": null,
            "valueAddress": null,
            "valueAddressFull": null,
            "valueCity": "Москва",
            "valueCityFull": "Москва"
        }
    },
    "items":
    [
        {
            "id": "29891",
            "quantity": 1
        }
    ],
    "locationId": "MSK582"
}
```

## Ответ

### Формата ответа

* **`pickupInfo`**
  * **`price`** - number, цена
  * **`address`** - string, адрес
  * **`priceDescription`** - string, текстовое описание стоимости доставки. Исползуется вместо price на экране информации о ПВЗ
  * **`lat`** - str, широта
  * **`lon`** - str, долгота
  * **`locationDescription`** - str, описание нахождения ПВЗ
  * **`title`** - str, название ПВЗ
  * **`deliveryTerm`** - str, срок доставки в свободной форме
  * **`timetable`** - str, расписание в свободной форме
  * **`images`** - str\[], URL изображений

### Пример ответа

```javascript
"pickupInfo": {
    "price": 100,
    "address": "ул. Пушкина, дом 1",
    "priceDescription": "от 100 до 500 рублей",
    "lat": "55.654295",
    "lon": "37.578029",
    "locationDescription": "Обойти здание, за поворотом направо.",
    "title": "Пункт выдачи заказов №123",
    "locationId": "MSK123",
    "deliveryTerm": "от 3-х дней",
    "timetable": "пн-пт: 9:00–19:00, сб: 10:00–15:00",
    "images": [
      "https://image.com/image1.jpg",
      "https://image.com/image2.jpg",
      "https://image.com/image3.jpg"
    ]
}
```
