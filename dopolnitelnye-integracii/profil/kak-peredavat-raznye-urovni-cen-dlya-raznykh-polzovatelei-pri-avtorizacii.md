---
description: (в разработке)
---

# Как передавать разные уровни цен (для разных пользователей) при авторизации

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](broken-reference)
* [Доставки](broken-reference)
* [Оплаты](broken-reference)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

## Описание

При создании фида внутри тега **`offer`** нужно передать тег **`price`** или **`oldPrice`** с параметром **`priceTier`**со значением сегмента пользователя для которого изменится цена в каталоге

```xml
<oldprice>950</oldprice>
<price>750</price>
<price priceTier="vip">640</price>
<oldprice priceTier="vip">800</oldprice>
```

**Также** для поддержки функционала необходимо добавить расшифровки пример ниже:

```xml
...
</offers>
<priceTiers>
  <priceTier id="silver">Серебряный</priceTier>
  <priceTier id="gold">Золотой</priceTier>
  <priceTier id="platina">Платиновый</priceTier>
  <priceTier id="vip">Бриллиантовый</priceTier>
</priceTiers>
...
</shop>
```

А также при ответе на запрос авторизации или получения профиля в [объекте "Учетная запись пользователя"](uchyotnaya-zapis-polzovatelya.-avtorizaciya./obekt-uchyotnaya-zapis-polzovatelya.md) необходимо передать поле

```
{
    "user":
    {
        ...,
        "priceTier": "vip"
    }
}
```

После этих действий авторизированный пользователь которому присвоен данный **`priceTier`** увидит следующую картину в каталоге&#x20;

![](<../../.gitbook/assets/image (9).png>)

А неавторизированный пользователь или авторизированный, но которому не присвоен данный **`priceTier`** увидит такие цены

![](<../../.gitbook/assets/image (8).png>)
