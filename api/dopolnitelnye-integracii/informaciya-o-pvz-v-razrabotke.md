# Информация о ПВЗ (в разработке)



## Запрос

### Описание формата

* **`locationId`** - str, id ПВЗ

### Пример запроса

```javascript
{
    "locationId": "PVZ_123"
}
```

## Ответ

### Формата ответа

* **`price`** - number, цена
* **`address`** - string, адрес
* **`lat`** - str, широта
* **`lon`** - str, долгота
* **`locationDescription`** - str, описание нахождения ПВЗ
* **`title`** - str, название ПВЗ
* **`deliveryTerm`** - str, срок доставки в свободной форме
* **`timetable`** - str, расписание в свободной форме
* **`images`** - str\[], URL изображений

### Пример ответа

```javascript
"pickup_info": {
    "price": 100,
    "address": "ул. Пушкина, дом 1",
    "lat": "55.654295",
    "lon": "37.578029",
    "locationDescription": "Обойти здание, за поворотом направо."",
    "title": "Пункт выдачи заказов №123",
    "locationId": "PVZ-123",
    "deliveryTerm": "от 3-х дней",
    "timetable": "пн-пт: 9:00–19:00, сб: 10:00–15:00",
    "images": [
      "https://image.com/image1.jpg",
      "https://image.com/image2.jpg",
      "https://image.com/image3.jpg",
    ]
}
```
