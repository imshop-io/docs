# Лайки/дизлайки отзывов

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

## Запрос

### Описание формата

* **`commentId`** - str, id комментария
* **`value`**
  * **`true`**- лайк (отзыв понравился)
  * **`false`**- дизлайк (отзыв не понравился)&#x20;

### Пример запроса

```json
{
    "commentId": "123",
    "value": true
}
```

## Ответ

### Формата ответа

* **`success`** - boolean, успех/неуспех операции

### Пример ответа

```javascript
{
    "success": true
}
```
