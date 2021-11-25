# Информация о ПВЗ



## Запрос

### Описание формата

* **`locationId`** - str, id ПВЗ
* **`address`** - информация о локации пользователя
* **`items`** - arr, корзина:
* id: str, id товара
* quantity: number, количество

### Пример запроса

```javascript
{
  locationId: 'MSK123',
  address: {
    location: {
      region: 'Москва',
      regionWithType: 'г Москва',
      area: null,
      areaWithType: null,
      city: 'Москва',
      cityWithType: 'г Москва',
      settlement: null,
      settlementWithType: null,
      street: null,
      streetType: null,
      house: null,
      block: null,
      apt: null,
      lat: '55.75396',
      lon: '37.620393',
      streetWithType: null,
      areaFiasId: null,
      cityFiasId: '0c5b2444-70a0-4932-980c-b4dc0d3f02b5',
      regionFiasId: '0c5b2444-70a0-4932-980c-b4dc0d3f02b5',
      settlementFiasId: null,
      streetFiasId: null,
      houseFiasId: null,
      regionKladrId: '7700000000000',
      cityKladrId: '7700000000000',
      areaKladrId: null,
      settlementKladrId: null,
      streetKladrId: null,
      houseKladrId: null,
      federalDistrict: 'Центральный',
      fiasId: '0c5b2444-70a0-4932-980c-b4dc0d3f02b5',
      fiasCode: '7700000000000000000',
      kladrId: '7700000000000',
      postalCode: '101000',
      valueCity: 'Москва',
      valueCityFull: 'Москва',
      valueAddress: null,
      valueAddressFull: null
    }
  },
  items: [
    { 
      id: '29891',
      quantity: 1
    }
  ],
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
    "locationId": "MSK123",
    "deliveryTerm": "от 3-х дней",
    "timetable": "пн-пт: 9:00–19:00, сб: 10:00–15:00",
    "images": [
      "https://image.com/image1.jpg",
      "https://image.com/image2.jpg",
      "https://image.com/image3.jpg",
    ]
}
```
