# Товары в прямом эфире

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

### Пример запроса:

```json
{

    “country”: “RU”

}
```

* **`country`** - национальный домен страны, в которой идет трансляция

### Пример ответа:

```json
{

    "items": ["789887", "961551", "55598192"]

}
```

* **`items`** - список ID товаров из фида

<figure><img src="../../.gitbook/assets/Simulator Screen Shot - iPhone 14 - 2022-12-20 at 10.34.26.png" alt=""><figcaption><p><strong>В массиве Items отдан один товар</strong></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Simulator Screen Shot - iPhone 14 - 2022-12-20 at 10.35.08.png" alt=""><figcaption><p><strong>В массиве Items отданы несколько товаров</strong></p></figcaption></figure>

Цвет бейджика можно задать в файле цветов под тегом liveBadgeColor
