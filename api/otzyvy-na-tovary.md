# Отзывы на товары

## Получение списка отзывов

{% hint style="info" %}
Для подключения обратитесь к вашему личному менеджеру в IMSHOP
{% endhint %}

### Формат запроса

* `id` - идентификатор товара в системе продавца \(на сайте / в CRM итд\)

```
{
    "id": "1234567890"
}
```

### Формат ответа

* `rating` - суммарный рейтинг отзывов по товару, от 1 до 5
* `reviews` - список отзывов
  * `text` - текст отзыва, обязательно наличие либо текста либо картинок
  * `author` - автор, обязательное поле
  * `date` - дата отзыва, в формате YYYY-MM-DDTHH:MM, обязательное поле
  * `title` - \(опционально\), заголовок отзывы
  * `rating` - \(опционально\), рейтинг отзыва по шкале от 1 до 5
  * `pictures` \(опционально\) - массив картинок отзыва
    * `src` - веб-ссылка на картинку

#### Пример ответа

```javascript
{
    "rating": "1.7",
    "reviews": [
      {
        "author": 'Jake',
        "date": '2020-04-25T08:30',
        "title": 'Lorem ipsum',
        "text": 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
        "pictures": [
          { "src": 'https://pmdn.sokolov.io/pics/F7/A5/84C379E76E8EE97A3B23EBE39DE4.jpg' },
        ],
        "rating": 3
      }
    ]
}
```



