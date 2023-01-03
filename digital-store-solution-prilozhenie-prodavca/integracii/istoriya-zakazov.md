# История заказов

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

{% hint style="info" %}
Для подключения обратитесь к вашему личному менеджеру в IMSHOP
{% endhint %}

### Формат запроса

{% hint style="success" %}
Полная спецификация описана [здесь](../../dopolnitelnye-integracii/profil/istoriya-zakazov.md) для приложения покупателя. Ниже перечислены только отличия для приложения продавца.
{% endhint %}

* **`staffId`** - идентификатор сотрудника в системе продавца (на сайте / в CRM итд)
* **`outletId`** - идентификатор магазина/аутлета сотрудника в системе продавца (на сайте / в CRM итд)

{% hint style="warning" %}
Поле **`userIdentifier`** приходить в запросе _не будет_.
{% endhint %}

#### Пример запроса

```javascript
{
	"staffId": "4321",
	"outletId": "1234567890"
}
```

### Формат ответа

{% hint style="success" %}
Полная спецификация описана [здесь](../../dopolnitelnye-integracii/profil/istoriya-zakazov.md) для приложения покупателя. Отличий для приложения продавца нет.
{% endhint %}
