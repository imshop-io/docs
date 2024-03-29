# Допы (в  разработке)

{% hint style="info" %}
Доп. товары - это такие же товары как и остальные, только в корзину они попадают в поле `addons` родительского товара.

Доп. товары должны быть обязательно преставлены в фиде, если товара нет в фиде, то он не будет показан покупателю, даже если его id будет передан в данном вебхуке.
{% endhint %}

## Формат запроса и пример <a href="format-zaprosa-i-primer" id="format-zaprosa-i-primer"></a>

### Пример <a href="primer" id="primer"></a>

```javascript
[{
  "configurationId": "12345",
  "selected": ["1_1", "1_2"]
},
{...}
]
```

### Описание формата <a href="opisanie-formata" id="opisanie-formata"></a>

* **`configurationId`** - идентификатор торгового предложения, для которого нужно получить доп. товары (**`id`** из YML фида)
* **`selected`** - список ид выбранных пользователем доп. товаров

‌

## Формат ответа и пример <a href="format-otveta-i-primer" id="format-otveta-i-primer"></a>

### Пример <a href="primer-1" id="primer-1"></a>

```javascript
[{  
  price: 1999,
	oldprice: 2999,
	groups: [
		{
			title: "Только один на выбор",
			type: "single",
			required: true,
			items: [
			{
				configurationId: "1_1",
				price: 999
			},
			{...}
		},
		{
			title: "Можно выбрать несколько",
			type: "multi",
			required: false,
			items: [
			{
				configurationId: "1_1",
				price: 999
			},
			{...}
		}
	]
},
{...}
]
```

### Описание формата <a href="opisanie-formata-2" id="opisanie-formata-2"></a>

* **`price`** - итоговая цена товара вместе с допами
* **`oldprice`** - опционально,  цена вместе с допами до скидки
* **`groups`** - группы доп. товаров
  * **`title`** - заголовок группы,  например, _Основание для кровати_
  * **`type`** - тип группы, `single` - можно выбрать только один товар,  `multi` - можно выбрать несколько  товаров
  * **`required`** - (опционально), если true, то покупатель обязательно должен выбрать доп. товар перед тем как положить в корзину
  * **`items`** - список доп. товаров
    * **`configurationId`** - ид товара, должно совпадать с ид товара из фида
    *   **`price`** - цена доп товара для отображения при выборе

