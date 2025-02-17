---
icon: earth-africa
---

# Передача наличия и цен по регионам, персональные цены, cashback

{% hint style="danger" %}
Если у вас редко (менее 3х раз в день) изменяется подборка товаров в фиде, или необходимо часто обновлять наличие товаров (чаще чем 3 раза в день) - используйте для передачи наличия и разных цен [**фид наличия для ElasticSearch.**](../fid-nalichiya-dlya-elasticsearch.md)



Данный функционал **не должен** использоваться совместно с отдельным фидом наличия.
{% endhint %}

Чтобы передать различное наличие товаров и цен по регионам, необходимо передать следующие дочерние теги внутри тега **`<offer>`** :

* **`available`** - наличие в городе / регионе
* **`price`** - цена в регионе
* **`oldprice`** - цена до скидки в регионе

Для каждого из заданных тегов необходимо передать атрибут **`city`** с [ФИАС](https://www.alta.ru/fias/) GUID города или региона, к которому будет применено данное наличие / цена.

Также можно передать один тег без атрибута **`city`**. Его значение будет использовано по умолчанию для городов, не подходящих ни под одно правило.

### Персональные цены в зависимости сегмента пользователя

Также можно передать тег **`priceTier`**&#x441;о значением сегмента пользователя для которого применится цена

```xml
<price>472</price>
<price priceTier="silver">380</price>
<price priceTier="gold">375</price>
<price priceTier="platina">340</price>
<price priceTier="vip">200</price>
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

### Пример

В данном примере товар доступен везде, кроме Москвы и Московской области.\
Цена товара 400 руб во Владимирской области, и 450 рублей в остальных регионах.

```xml
<offer id="61b06345-c404-11e0-ad14-3c4a926c6ba4" available="true" uuid="a43c03a5-3d1d-5791-b9a5-1ef95438cd8e" group_id="6" sizeGridImage="">
    <available>true</available>
    <available city="0c5b2444-70a0-4932-980c-b4dc0d3f02b5">false<available>
    <available city="29251dcf-00a1-4e34-98d4-5c47484a36d4">false<available>
    
    <price>450</price>
    <price city="b8837188-39ee-4ff9-bc91-fcc9ed451bb3">400<price>
    <oldprice>650</oldprice>
    
    <barcode>4627077842287</barcode>
    <barcode>2680983579717</barcode>
    <sort>2</sort>
    <customSort type="new">1610623217147</customSort>
    <customSort type="home">18</customSort>
    <customSort type="popular">12</customSort>
    <url>https://www.respublica.ru/knigi/iskusstvo-dizayn-i-moda/arhitektura/A001617-antonio-gaudi</url>
    <vendor>Caramella</vendor>
    <vendorCode>A001617</vendorCode>
    <model>V198605N-1568C68</model>
    <typePrefix>Книга</typePrefix>
    <currencyId>RUR</currencyId>
    <retailPrice>790</retailPrice>
    <categoryId>31</categoryId>
    <categoryId>1956</categoryId>
    <googleProductCategory>Apparel &amp; Accessories > Clothing > Shirts &amp; Tops</googleProductCategory>
    <picture>https://www.respublica.ru/uploads/00/00/00/1i/50/large_05dcba0a72595c8e.jpg</picture>
    <picture>https://www.respublica.ru/uploads/01/00/00/1i/51/large_64d78b626ef2e2c9.jpg</picture>
    <store>true</store>
    <pickup>true</pickup>
    <delivery>false</delivery>
    <name>Книга Антонио Гауди</name>
    <description>Текст этой книги, которую с полным правом можно назвать маленьким исследованием, начинается со слов, что биографию А.Гауди лучше анализировать, &amp;quot;внимательно изучая его работы&amp;quot;. Это справедливо. И такую возможность читатели получают, так как повествование сопровождается прекрасными фотографиями.</description>
    <sales_notes>40 городов с магазинами, 750 точек самовывоза</sales_notes>
    <barcode>9785956100455</barcode>
    <barcode>2680001191891</barcode>
    <param name="Обложка">Мягкая</param>
    <param name="Язык">Русский</param>
    <param name="Количество страниц">96</param>
    <param name="Год издания">2008</param>
    <param name="Формат">18 х 23</param>
    <param name="Раздел">Зарубежные</param>
    <param name="Направление">История архитектуры</param>
    <param name="Стили">Модерн</param>
    <param name="Объект архитектуры">Здания</param>
    <maxPromocodeDiscountPercent>0</maxPromocodeDiscountPercent>
    <useBonuses>false</useBonuses>
    <rec>16277,88167</rec>
    <rec title="С этим покупают">11951,11860,11735</rec>
    <rec title="Другие цвета">74826,83900,11155</rec>
    <rec title="Дополни образ">84629,83466,99998</rec>
    <vat>vat_20</vat>
    <badge textColor="#fff" bgColor="#bba267">Акция -30%</badge>
    <badge regionId="33,34" textColor="#fff" bgColor="#bba267">Акция -30%</badge>
    <badge picture="https://xxxxx/xxxxxx.png" />
    <video main="true" image="https://xxxxxx">https://xxxxxxxxx/xxx.mp4</video>
    <video title="Видео-инструкция" image="https://xxxxxx">https://xxxxxxxxx/xxx.mp4</video>
    <file title="Руководство пользователя" size="24mb" icon="https://xxxxxxx/x.png" url="https://xxxxxxx/x.ppdf" />
</offer>
```

## Cashback

Чтобы показать кешбек в зависимости от `priceTier` пользователя, необходимо передать тек `cashback` внутри `offer`:

```xml
<cashback>100</cashback>
<cashback priceTier="silver">110</cashback>
<cashback priceTier="gold">120</cashback>
<cashback priceTier="platina">130</cashback>
<cashback priceTier="vip">140</cashback>
```

Тег `cashback` без `priceTier` будет использоваться по умолчанию (для пользователей без `priceTier` или если текущий `priceTier` пользователя не найдет в теге `offer` для данного товара)

## Сегменты в категориях

#### category -> segment (функционал сегментов в категориях)

* **`id`** - идентификатор сегмента (`_all` – системный сегмент, обозначающий всех пользователей)
* **`enabled`** - `"true"`/`"false"`, опционально, отключение сегмента (в примере ниже указано, как отключить системный сегмент `_all` и оставить отображение категории только для пользователей с сегментами выше)

```xml
<categories>
    <category id="6323" picture="https://xxx/xxx/xxx.jpg" name="Смартфоны и гаджеты">
        <segment id="test" />
        <segment id="test2" />
        <segment id="_all" enabled="false" />
    </category>
</categories> 
```
