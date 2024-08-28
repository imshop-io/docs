# YML (фид каталога товаров)

## Описание дополнений формата от IMSHOP.IO и примеры

### Общая структура фида (пример)

```markup
<?xml version="1.0" encoding="UTF-8"?>
<yml_catalog date="2017-02-05 17:22">
  <shop>
    <categories>
      <category.........>...</category>
      ...
    </categories>
    <offers>
      <offer........>
        ...
      </offer>
      ...
    </offers>
  </shop>
</yml_catalog>
```

### Описание формата

#### **offers -> offer (атрибуты)**

* **`available`** - обязательный атрибут. Товары с **`available`** = **`false`** не будут отображаться в приложении вне зависимости от каких либо других факторов api / остатков.
* **`publishedOn`** - дата релиза товара для подключения автоматической сортировки по старым/новым товарам
* **`id`** - атрибут, идентификатор **товарного предложения** - _**обязательна уникальность**_ в рамках каталога.
* **`itemPreviewUrl`** - атрибут, URL-ссылка на страницу с 3D-моделью товара (на страницу с 3D предпросмотром, не на карточку товара).
*   **`fraction`** - кратность товара, с которой можно добавлять его в корзину. Например, если fraction=0.2, то добавлять в корзину можно только 0.2, 0.4, 0.6 и т.д. единиц товара.

    fraction необходим для включения функционала. По умолчанию кратность всегда 1 к 1.

    Цена указывается за 1 (одну) полную единицу товара (не за 0.2, 0.3 и т.д).
* **`group_id`** - атрибут, элемент объединяет все предложения, которые являются вариациями одной модели и должен иметь одинаковое значение. Это идентификатор карточки товара в каталоге.
* **`uuid`** - атрибут, дополнительный идентификатор товара (например, из 1С).
* **`sizeGridImage`** - атрибут, URL-ссылка на картинку с размерами для примерки.

```xml
<offer id="700996" available="true" uuid="a43c03a5-3d1d-5791-b9a5-1ef95438cd8e" group_id="111111">
</offer>
<offer id="998822" publishedOn="2014-11-12 00-00-00" available="true" group_id="222222" sizeGridImage="https://https://xxx.ru/upload/xxx.jpg">
</offer>
<offer id="898822" available="true" group_id="222222" sizeGridImage="https://https://xxx.ru/upload/xxx.jpg">
</offer>
<offer id="198820" available="true" fraction="5">
</offer>
```

#### **offers -> offer (дочерные элементы)**

* **`barcode`** - штрихкод товара от производителя в одном из форматов: EAN-13, EAN-8, UPC-A, UPC-E. Элемент offer может содержать несколько элементов barcode, в этом случае каждый из штрихкодов передается в отдельном теге.
* **`name`** - полное название предложения, в которое входит: тип товара, производитель, модель и название товара, важные характеристики. Составляйте по схеме: что (тип товара) + кто (производитель) + товар (модель, название) + важные характеристики.
* **`url`** - URL страницы товара на сайте магазина
* **`sort`** - порядок сортировки по популярности
* **`guid`** - параметр необходимый при прямой интеграции mindbox чтобы определять какой товар смотрел юзер. Значение должно быть то же которое настроено в mindbox
* **`vendor`** - производитель.
* **`vendorCode`** - код производителя для данного товара.
* **`model`** - модель и название товара.
* **`typePrefix`** - тип / категория товара (например, «мобильный телефон», «стиральная машина», «угловой диван»).
* **`categoryId`** - идентификатор категории товара, присвоенный магазином. Элемент offer может содержать несколько элементов categoryId, в этом случае каждая из категорий передается в отдельном теге.
* **`googleProductCategory`** - google product category (GPC) taxonomy для товара.
* **`param`** - все важные характеристики товара — цвет, размер, объем, материал, вес, возраст, пол, и т. д. Элемент offer может содержать несколько элементов param (один элемент **`param`** — одна характеристика), в этом случае каждая характеристика передается в отдельном теге. (при использовании перелинковки цвета отдавать в hex формате или указывать URL изображения в атрибуте **`itemImage`**).
* **`picture`** - URL-ссылка на картинку товара. Элемент offer может содержать несколько элементов picture, в этом случае каждая из картинок передается в отдельном теге.
* **`currencyId`** - валюта, в которой указана цена товара: RUR, USD, EUR, UAH, KZT, BYN.
* **`price`** - актуальная цена товара.
* **`priceByCard`** - цена товара по скидочной карте (в разработке), должна быть ниже обычной цены. Несовместимо с **`oldrice`**.
* **`priceUnits`** - единица измерения.
* **`oldprice`** - старая цена товара, должна быть выше текущей.
* **`saleEndsDateIso`** - Дата время до окончания акции по аналогии с датой фида у яндекса.
* **`retailPrice`** - РРЦ товара (цена товара в оффлайне в случае если отличается от price).
* **`deferPrice`** - цена на случай отсрочки получения, должна быть ниже **`price`**.
* **`listPrice`** - необязательно, справочные цены, если нужно показать несколько цен, только для отображения, в расчетах не используются.
  * **`title`** - атрибут, текстовое описание цены.
* **`priceLabel`** - текст вместо цены товара для кейса когда товара нет в наличии но есть возможность подписаться на него **только для клиентов с elassticSearch**&#x20;

```xml
<priceLabel>Скоро в продаже</priceLabel>
```

* **`description`** - описание предложения.
* **`collapsibleDescription`** - описание со сворачивающимися блоками
  * **collapsibleDescription -> section (дочерние элементы)**
    * **section (атрибуты)**
      * **`lang`** – локализация (необязательно)
      * **`expanded`** – укажите expanded="true", чтобы секция была развернута по умолчанию. Опционально.
    * **`title`** – заголовок
    * **`text`** – описание (поддерживается markdown)

{% code overflow="wrap" %}
```xml
<collapsibleDescription>
  <section>
    <title>Title</title>
    <text>Text</text>
  </section>
  <section lang="ru" expanded="true">
    <title>TitleRU1</title>
    <text>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis congue metus, non vestibulum dui. Vivamus cursus orci vel sem tristique, a dictum quam aliquam.</text>
  </section>
  <section lang="ru">
    <title>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis congue metus, non vestibulum dui. Vivamus cursus orci vel sem tristique, a dictum quam aliquam.</title>
    <text>* Первый пункт
    
    * Второй пункт
     
    * Третий пункт</text>
  </section>
  <section lang="ru">
    <title>TitleRU3</title>
    <text>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis quis congue metus, non vestibulum dui. Vivamus cursus orci vel sem tristique, a dictum quam aliquam.</text>
  </section>
  <section lang="en">
    <title>TitleEN</title>
    <text>TextEN</text>
  </section>
</collapsibleDescription>
```
{% endcode %}

* **`rec`** - идентификаторы товаров для блока рекомендаций через запятую. Возможно передавать несколько блоков с подборками товаров, например "Похожие товары", "С этим покупают", "Дополни образ" итд. Для этого следует передать несколько тегов **`rec`** с атрибутом **`title`** (см пример).&#x20;

{% hint style="info" %}
Для товаров из списка рекомендаций, объединённых в группы (см. атрибут**`group_id`**), необходимо указывать их идентификатор группы вместо товарного предложения, т.е. значение из group\_id="\*\*\*", а не offer id="\*\*\*".
{% endhint %}

* **`maxPromocodeDiscountPercent`** - максимальный процент скидки на данный товар, например, по купону. Используется для ограничения размера скидки, например, для товаров с низкой маржинальностью.
* **`vat`** - значение ставки НДС для товара. Для всех ставок НДС предусмотрены специальные значения.
  * НДС не облагается - **`6`** или **`NO_VAT`**
  * 0% - **`5`** или **`VAT_0`**
  * 10% - **`2`** или **`VAT_10`**
  * 20% - **`7`** или **`VAT_20`**
* **`useBonuses`** - возможность частичной или полной оплаты данного товара с бонусного счета при наличии программы лояльности.
* **`overSized`** - крупногабаритный товар.
* **`preorder`** -параметр для товаров по предзаказу.
* **`badge`**- бейджик на картинке товара. Элемент offer может содержать несколько элементов badge, в этом случае каждый из бейджик передается в отдельном теге. **В одном бейдже может быть либо только текстовый вариант, либо только с картинкой. И текст и картинка в одной бейдже быть не могут.**
  * **`textColor`**, атрибут, необязательно - цвет текста в формате **`#rrggbb`**
  * **`bgColor`**, атрибут, необязательно - цвет фона для текстового бейджа в формате **`#rrggbb`**
  * **`link`**, атрибут, необязательно - ссылка при нажатии на бейджик
  * **`position`** атрибут, необязательно - задает позицию бейджа на карточке товара. Возможные значения: top-right, top-left, bottom-left, bottom-right
  * **`type`**, атрибут, необязательно – позволяет задать дополнительный тип бейджа:
    * **`wideImage`** – бейдж с бóльшим ограничением по ширине (для широких картинок)
* **`video`** - видео товара (можно передать несколько). Видео должны быть в формате H.264.
  * **`main`** - если **`true`**, то видео будет отображаться в слайдере с фотографиями товара
  * **`title`** - опциональный заголовок видео
  * **`image`** - URL на картинку, которая отображается, пока грузится видео
* **`file`** - релевантные документы.
  * **`title`** - название
  * **`size`** (опционально) - вес файла для отображения на кнопке в приложении
  * **`icon`** (опционально) - иконка для отображения на кнопке в приложении
  * **`url`** - ссылка на скачивание
* **`rating`** - рейтинг товара для отображения на карточке товара сверху (не путать с [хуком отзывов на товары](../../dopolnitelnye-integracii/kartochka-tovara/otzyvy-na-tovary.md)).
* **`reviews_count`** - количество отзывов для отображения в ячейке и на карточке товара сверху (не путать с [хуком отзывов на товары](../../dopolnitelnye-integracii/kartochka-tovara/otzyvy-na-tovary.md)).
* **`sizeGridPageUrl`** -  URL-ссылка на HTML с таблицей размеров (отобразится, если не задан в атрибутах sizeGridImage и нет sizeGridImgUrl в settings)
* **`othercolors`**- блок товаров "еще в другом цвете", перечислить group Id товаров с альтернативными цветами. **Не используется вместе с parentVendorCode.**
* **`parentVendorCode`** - по данному параметру объединяем товары для перелинковки (позволяет добавлять переключаемые параметры на карточку товара) **не должен пересекаться с group id, не используется вместе с othercolors**
* **`showMultipleFractionsCounter`** - показывать для этого товара двойной пикер: один по единице измерения, который передан **`priceUnits`**,  а второй пикер по упаковкам. **`fraction`** отвечает за количество единиц в упаковке, купить товар можно будет только по упаковкам (в разработке)

```xml
<offer id="998822" available="true" group_id="222222">
<guid configurationId="998822">819bc1b1-af54-4317-bbff-5fb476ffcb12#123eeb8f-f19e-4ba3-a423-c1cc9e50a23b</guid>
<barcode>4627077842287</barcode>
<name>Ботинки кожаные</name>
<url>https://xxx.ru/xxx./</url>
<sort>8</sort>
<price>450</price>
<oldprice>650</oldprice>
<priceByCard>390</priceByCard>
<retailPrice>790</retailPrice>
<deferPrice>550</deferPrice>
<priceUnits>м²</priceUnits>
<currencyId>RUB</currencyId>
<saleEndsDateIso>2020-11-22T14:37:38</saleEndsDateIso>
<vendor>BrandName</vendor>
<vendorCode>0000-667838</vendorCode>
<categoryId>1728</categoryId>
<model>V198605N-1568C68</model>
<typePrefix>Ботинки</typePrefix>
<param name="Размер">39</param>
<param name="Цвет" hex="#0000FF">Синий</param>
<param name="Материал подошвы">Каучук</param>
<param name="Материал верха">Кожа</param>
<param name="Обложка" noFilter="true">Мягкая</param>
<description>Прекрасные ботинки известного бренда</description>
<googleProductCategory>Apparel &amp; Accessories > Clothing > Shirts &amp; Tops</googleProductCategory>
<rec title="Похожие товары">213741,1899435,1630074</rec>
<rec title="Дополни образ">666000,777000</rec>
<badge textColor="#000" bgColor="#CCFF33">НОВИНКА</badge>
<badge picture="https://xxxxx/xxxxxx.png"</badge>
<maxPromocodeDiscountPercent>0</maxPromocodeDiscountPercent>
<vat>vat_20</vat>
<picture>https://xxxx/xxxx/image1.jpg</picture>
<picture>https://xxxx/xxxx/image2.jpg</picture>
<useBonuses>true</useBonuses>
<preorder>true</preorder>
<showMultipleFractionsCounter>true</showMultipleFractionsCounter>
<rating>4.5</rating>
<reviews_count>130</reviews_count>
<video main="true" image="https://xxxxxx">https://xxx.ru/xxx.mp4</video>
<video title="Видео-инструкция" image="https://xxx.ru/xxx.mp4</video>
<file title="Руководство пользователя" size="24mb" icon="https://xxx.ru/xxx.png" url="https://xxxxxxx/x.pdf" />
```

**categories -> category (атрибуты)**

* **`id`** - идентификатор категории
* **`parentId`** - идентификатор родительской категории
* **`picture`** - URL картинки категории
* **`textColor`** - цвет текста (опционально)
* **`backgroundColor`** - цвет фона (опционально)
* **`universalLink`** - URL страницы категории на сайте магазина (опционально)
* **`name`** - имя категории (обязательно _при использовании сегментов в категории, только на тарифах с ElasticSearch_)

```xml
<categories>
<category id="6323" picture="https://xxx/xxx/xxx.jpg">Смартфоны и гаджеты</category>
<category id="183" parentId="6323" picture="https://xxx/xxx/xxx.jpg">Смартфоны</category>
</categories> 
```

### Размеры с дополнительными юнитами

В случае, если у вас товар имеет размерную сетку с несколькими значениями (US, RU, UK, EUR), можно добавить эти значения в фид, чтобы юзер мог использовать размерную сетку, удобную для себя. Поле не является обязательным.

<div align="left">

<figure><img src="../../.gitbook/assets/IMAGE 2024-03-04 160924.jpg" alt="" width="148"><figcaption><p>Фильтры с unit размерами</p></figcaption></figure>

</div>

<pre class="language-xml"><code class="lang-xml">&#x3C;offer>
&#x3C;param name="Размер" unit="US">10&#x3C;/param>
&#x3C;param name="Размер" unit="RU">40&#x3C;/param>
<strong>&#x3C;/offer>
</strong></code></pre>

### Вывод таба "Бренды" в приложении

В фиде создается категория бренды, в нее вкладываются подкатегории-бренды. **Если какие-то бренды не вложены в основную категорию-они не отобразятся во вкладке.**

Если во вкладке с брендами необходимо сделать разделение на сегменты (например: мужчинам, женщинам, детям).

```xml
<category id="1">Бренды</category>
<category id="brands_679" parentId="1" picture="https://xxx.ru/xxx.jpg">Дети</category>
<category id="brands_678" parentId="1" picture="https://xxx.ru/xxx.jpg">Женщины</category>
<category id="brands_677" parentId="1" picture="https://xxx.ru/xxx.jpg">Мужчинам</category>
```

Для вывода "Топ брендов" нужно передать бренды в том порядке, в котором они должны быть отображены:

```xml
<category id="1">Бренды</category>
<category id="brands_679" parentId="1" picture="https://xxx.ru/xxx.jpg">Дети</category>
 <category id="brands_679455" parentId="brands_6799" picture="https://xxx.ru/xxx.jpg">Balmain</category>
 <category id="brands_679456" parentId="brands_6799" picture="https://xxx.ru/xxx.jpg">Burberry</category>
 ...
<category id="brands_678" parentId="1" picture="https://xxx.ru/xxx.jpg">Женщины</category>
<category id="brands_679457" parentId="brands_6798" picture="https://xxx.ru/xxx.jpg">>Relaxsan</category>
<category id="brands_679458" parentId="brands_6798" picture="https://xxx.ru/xxx.jpg">>Anita</category>
...
```

{% hint style="warning" %}
В чем отличие **`group_id`** и **`id`**?

**`group_id`** - это идентификатор **модели товара**. Например _"Белые Nike Air Max 95"_. Модель товара представлена в каталоге одной карточкой товара.

**`id`** - идентификатор товарного предложения (конкретного размера / варианта товара). Например _"Белые Nike Air Max 95, размер 43"_ будут иметь свой уникальный `id`

\
**`id`** обязательно уникален на весь каталог. _"Белые Nike Air Max 95, размер 43"_ и _"Белые Nike Air Max 95, размер 44"_ будут иметь разные id.

**`group_id`** объединяет (группирует) товарные предложения в одну карточку товара, и является ее идентификатором. _"Белые Nike Air Max 95, размер 43"_ и _"Белые Nike Air Max 95, размер 44"_ будут иметь одинаковый **`group_id`**.\
\
\-----\
\
**id** используется, например, в API пересчета корзины и оформления заказа, так как в этом случае необходимо передавать идентификатор конкретного размера товара, который добавлен в корзину\
\
**group\_id** используется, в API рекомендаций похожих товаров, поиска и подсказок, а также при перелинковке между товарами ("еще в другом цвете"), так как в этом случае мы ссылкаемся не на конкретный размер, а на идентификатор модели товара (карточки товара)\
\
Если у товара отсутствуют товарные предложения (всегда доступен в одном варианте), то group\_id можно пропустить. В этом случае **`group_id`** будет совпадать с **`id`**.\
\
Если вы все-таки передаете **`group_id`** в фиде, то он не должен совпадать с **`id`** товара

\
[Подробнее можно прочитать в документации Яндекса](https://yandex.ru/support/market-distr/product-feed.html?lang=ru)
{% endhint %}
