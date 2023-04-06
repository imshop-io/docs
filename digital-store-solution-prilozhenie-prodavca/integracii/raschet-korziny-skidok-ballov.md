# Расчет корзины, скидок, баллов

Мы работаем только через **POST**-запросы.

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../../osnovnye-integracii/oformlenie-zakaza.md)
* [Доставки](../../osnovnye-integracii/dostavki.md)
* [Оплаты](../../osnovnye-integracii/oplaty.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

{% hint style="info" %}
Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO​
{% endhint %}

IMSHOP.IO позволяет при помощи webhook подключить уже существующую на вашей стороне систему пересчета корзины с учетом акций, предложений, бонусных баллов итд.

{% hint style="info" %}
Пересчет корзины через webhook означает, что для каждого изменения состава корзины IMSHOP.IO будет отправлять данные о заказе в систему клиента и ожидать в ответ данные об итоговой стоимости заказа и примененных маркетинговых акциях.
{% endhint %}

## Формат запроса и примеры <a href="#format-zaprosa-i-primery" id="format-zaprosa-i-primery"></a>

### Пример запроса <a href="#primer-zaprosa" id="primer-zaprosa"></a>

```json
{
            "userData": null,
            "staffId": "1111111",
            "authorizedBonuses": 0,
            "items": [
              {
                "privateId": "7619426049232",
                "subtotal": 320,
                "quantity": 1,
                "appliedDiscounts": [],
                "addons": [],
                "name": "Название Товара",
                "discount": 0,
                "price": 320,
                "id": "7619426",
                "configurationId": "426049232"
              }
            ],
            "deliveryId": null,
            "installId": "efef3134-825f-41f6-9827-76dae5fa6527",
            "preferredPickupId": null,
            "promocode": null,
            "fiasCode": null,
            "externalUserId": null,
            "outletId": "0120383",
            "cityKladr": "7700000000000",
            "addressData": {
              "lon": null,
              "building": null,
              "house": null,
              "beltwayDistance": null,
              "houseKladr": null,
              "cityFias": "0c5b2444-70a0-4932-980c-b4dc0d3f02b5",
              "settlement": null,
              "streetType": null,
              "city": "Москва",
              "fiasCode": null,
              "streetKladr": null,
              "settlementWithType": null,
              "beltwayHit": null,
              "capitalMarker": null,
              "streetFias": null,
              "areaFias": null,
              "settlementKladr": null,
              "street": null,
              "value": null,
              "zip": null,
              "apt": null,
              "region": "Москва",
              "fias": "0c5b2444-70a0-4932-980c-b4dc0d3f02b5",
              "area": null,
              "regionKladr": "7700000000000",
              "lat": null,
              "kladr": null,
              "houseFias": null,
              "cityKladr": "7700000000000",
              "settlementFias": null,
              "areaKladr": null,
              "regionFias": "0c5b2444-70a0-4932-980c-b4dc0d3f02b5"
            },
            "customSectionValues": {},
            "user": {
              "phone": "none",
              "name": "none",
              "email": "none"
            },
            "loyaltyCard": "",
            "city": "Москва",
            "paymentId": null
          }
```

### Описание формата запроса

* **`outletId`** — идентификатор магазина
* **`staffId`** — идентификатор сотрудника
* **`deliveryId`** - идентификатор выбранной службы доставки в IMSHOP.IO (**`null`** если доставка еще не выбрана)
* **`paymentId`** - идентификатор выбранной службы оплаты в IMSHOP.IO (**`null`** если оплата еще не выбрана)
* **`deliveryPickupId`** - (опционально) выбранный желаемый пункт выдачи / магазин для получения заказа
* **`preferredPickupId`** - (опционально) id любимого пункта самовывоза (если есть),  выбранный в списке любимых магазинов, например на этапе корзины
* **`addressData`** — полная информация о адресе, прошедшая валидацию [DaData](https://dadata.ru/)
  * **`kladr`** — [Классификатор адресов Российской Федерации](https://www.alta.ru/fias/), определяющий  город и улицу
  * **`apt`**— номер квартиры
  * **`houseKladr`**— **не ориентируйтесь на это поле** [Классификатор адресов Российской Федерации](https://www.alta.ru/fias/), определяющий конкретный дом, по умолчанию **`null`**, ситуативно [DaData ](https://dadata.ru/)может передавать данное поле заполненным
  * **`region`**— регион
  * **`fias`**— [ФИАС](https://www.alta.ru/fias) города и улицы
  * **`value`**— адрес полностью
  * **`cityFias`**— [ФИАС](https://www.alta.ru/fias) города&#x20;
  * **`areaFias`** — [ФИАС](https://www.alta.ru/fias)-код района
  * **`streetKladr`**— [Классификатор адресов Российской Федерации](https://www.alta.ru/fias/), определяющий  улицу
  * **`regionKladr`**— [Классификатор адресов Российской Федерации](https://www.alta.ru/fias/), определяющий регион
  * **`regionFias`**— [ФИАС](https://www.alta.ru/fias) определяющий регион
  * **`city_kladr`**— [Классификатор адресов Российской Федерации](https://www.alta.ru/fias/), определяющий город
  * **`streetFias`**— [ФИАС](https://www.alta.ru/fias) определяющий улицу
  * **`zip`**— индекс дома
  * **`settlement`** — населенный пункт
  * **`settlementFias`** — [ФИАС](https://www.alta.ru/fias)-код населенного пункта
  * **`beltwayDistance`** — расстояние от кольцевой в км (только если заполнен **`beltwayHit`**)
  * **`lat`**— широта&#x20;
  * **`lon`**— долгота
  * **`settlementKladr`** — [Классификатор адресов Российской Федерации](https://www.alta.ru/fias/), определяющий населенный пункт
  * **`house`**— номер дома
  * **`city`**— название города
  * **`cityKladr`**— [Классификатор адресов Российской Федерации](https://www.alta.ru/fias/), определяющий город
  * **`houseFias`**— **не ориентируйтесь на это поле** [ФИАС](https://www.alta.ru/fias), определяющий конкретный дом, по умолчанию **`null`**, ситуативно [DaData ](https://dadata.ru/)может передавать данное поле заполненным
  * **`beltwayHit`** — внутри кольцевой ( IN_MKAD - на территории МКАД, OUT\__MKAD - за территорией МКАД)
  * **`area`** — район в регионе
  * **`fias_code`** — не заполняется, используйте **`fias_id`**
  * **`street`**— название улицы
  * **`areaKladr`** — [Классификатор адресов Российской Федерации](https://www.alta.ru/fias/), определяющий район
  * **`settlementWithType`** — улица с типом
  * **`fias_id`** — [ФИАС](https://www.alta.ru/fias)-код адреса (идентификатор адреса)
* **`items`** - состав корзины
  * **`name`** - наименование
  * **`id`** - идентификатор товара в IMSHOP.IO
  * **`privateId`** - идентификатор товарного предложения в системе клиента
  * **`configurationId`** - идентификатор товарного предложения в IMSHOP.IO
  * **`price`** - цена товара на момент добавления в корзину (если товар - это подарок на выбор, то тут передается **`0`**)
  * **`quantity`** - количество
  * **`subtotal`** - итого по позиции (**`subtotal`** = **`price`** \* **`quantity`**)
  * **`appliedDiscounts`** - если предыдущий расчет показал наличие маркетинговой акции, или это - подарок на выбор, то передаем идентификатор акции из прошлого ответа от API
  * **`deliveryGroup`** - (опционально) выбранная группа доставки товара, при разбиении корзины
  * **`addons`** - (опционально, в разработке) доп. товары, например "Основание для кровати"
* **`externalUserId`** - идентификатор покупателя в системе клиента, если известен
* **`configurationId`** - идентификатор товарного предложения из фида
* **`promocode`** - промокод, введенный покупателем
* **`installId`** - идентификатор установки приложения
* **`loyaltyCard`** - номер карты лояльности&#x20;
* **`customSectionValues`** - индивидуальные секции в оформлении заказа (к примеру добавить открытку, если пользователь приобретает товар в подарок)
