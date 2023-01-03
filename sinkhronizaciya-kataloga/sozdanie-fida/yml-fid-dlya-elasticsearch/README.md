# YML фид для ElasticSearch

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
* **`id`** - атрибут, идентификатор товарного предложения - _**обязательна уникальность**_ в рамках каталога.
* **`itemPreviewUrl`** - атрибут, URL-ссылка на страницу с 3D-моделью товара (на страницу с 3D предпросмотром, не на карточку товара).
*   **`fraction`** - кратность товара, с которой можно добавлять его в корзину. Например, если fraction=0.2, то добавлять в корзину можно только 0.2, 0.4, 0.6 и т.д. единиц товара.

    fraction необходим для включения функционала. По умолчанию кратность всегда 1 к 1.

    Цена указывается за 1 (одну) полную единицу товара (не за 0.2, 0.3 и т.д).
* **`group_id`** - атрибут, элемент объединяет все предложения, которые являются вариациями одной модели и должен иметь одинаковое значение.
* **`uuid`** - атрибут, дополнительный идентификатор товара (например, из 1С).
* **`sizeGridImage`** - атрибут, URL-ссылка на картинку с размерами для примерки.

```xml
</offer>
<offer id="700996" available="true" uuid="a43c03a5-3d1d-5791-b9a5-1ef95438cd8e" group_id="111111">
</offer>
<offer id="998822" publishedOn="2014-11-12 00-00-00" available="true" group_id="222222" sizeGridImage="https://https://xxx.ru/upload/xxx.jpg">
</offer>
<offer id="898822" available="true" group_id="222222" sizeGridImage="https://https://xxx.ru/upload/xxx.jpg">
```

#### **offers -> offer (дочерные элементы)**

* **`barcode`** - штрихкод товара от производителя в одном из форматов: EAN-13, EAN-8, UPC-A, UPC-E. Элемент offer может содержать несколько элементов barcode, в этом случае каждый из штрихкодов передается в отдельном теге.
* **`name`** - полное название предложения, в которое входит: тип товара, производитель, модель и название товара, важные характеристики. Составляйте по схеме: что (тип товара) + кто (производитель) + товар (модель, название) + важные характеристики.
* **`url`** - URL страницы товара на сайте магазина
* **`sort`** - порядок сортировки по популярности
* **`guid` ** - параметр необходимый при прямой интеграции mindbox чтобы определять какой товар смотрел юзер. Значение должно быть то же которое настроено в mindbox
* **`vendor`** - производитель.
* **`vendorCode`** - код производителя для данного товара.
* **`model`** - модель и название товара.
* **`typePrefix`** - тип / категория товара (например, «мобильный телефон», «стиральная машина», «угловой диван»).
* **`categoryId`** - идентификатор категории товара, присвоенный магазином. Элемент offer может содержать несколько элементов categoryId, в этом случае каждая из категорий передается в отдельном теге.
* **`googleProductCategory`** - google product category (GPC) taxonomy для товара.
* **`param`** - все важные характеристики товара — цвет, размер, объем, материал, вес, возраст, пол, и т. д. Элемент offer может содержать несколько элементов param (один элемент **`param`** — одна характеристика), в этом случае каждая характеристика передается в отдельном теге. (при использовании перелинковки цвета отдавать в hex формате или указывать URL изображения в атрибуте **`itemImage`**).
  * **`noFilter="true"`** - скрыть параметр из фильтров
  * **`noDetails="true"`** - скрыть параметр на карточке товара
  * **`numeric="true"`** - сделать фильтр слайдером
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
* **`description`** - описание предложения.
* **`rec`** - идентификаторы товаров для блока рекомендаций через запятую. Возможно передавать несколько блоков с подборками товаров, например "Похожие товары", "С этим покупают", "Дополни образ" итд. Для этого следует передать несколько тегов **`rec`** с атрибутом **`title`** (см пример).
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
  * **`type`** , необязательно атрибут - тип бейджа - строка (**text**, **color**,**smallImage**) по умолчанию тип text
  * **`textColor`**, атрибут, необязательно - цвет текста в формате **`#rrggbb`**
  * **`bgColor`**, атрибут, необязательно - цвет фона для текстового бейджа в формате **`#rrggbb`** , в случае если тип бейджа **color** - используется как цвет заполнения и становится обязательным полем
  * **`link`**, атрибут, необязательно - ссылка при нажатии на бейджик
  * **`picture`**, атрибут, необязательно - используется для передачи картинки типа бейджа **smallImage**, ссылка на картинку
  * **`position`** - атрибут, необязательно - строка, может быть одним из 4 типов (**top-left**, **top-right**, **bottom-left**, **bottom-right**), управляет положением бейджа относительно угла, по умолчанию **top-left**(либо значение из настроек), также нужно обратиться к продукту что вы хотите сами управлять положением бейджей на товаре
* **`video`** - видео товара (можно передать несколько). Видео должны быть в формате H.264.
  * **`main`** - если **`true`**, то видео будет отображаться в слайдере с фотографиями товара
  * **`title`** - опциональный заголовок видео
  * **`image`** - URL на картинку, которая отображается, пока грузится видео
* **`file`** - релевантные документы.
  * **`title`** - название
  * **`size`** (опционально) - вес файла для отображения на кнопке в приложении
  * **`icon`** (опционально) - иконка для отображения на кнопке в приложении
  * **`url`** - ссылка на скачивание
* **`rating`** - рейтинг товара для отображения на карточке товара сверху (не путать с [хуком отзывов на товары](../../../dopolnitelnye-integracii/kartochka-tovara/otzyvy-na-tovary.md)).
* **`reviews_count`** - количество отзывов для отображения в ячейке и на карточке товара сверху (не путать с [хуком отзывов на товары](../../../dopolnitelnye-integracii/kartochka-tovara/otzyvy-na-tovary.md)).

```xml
<offer id="998822" available="true" group_id="222222">
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
<guid configurationId="3573311">
<vendor>BrandName</vendor>
<vendorCode>0000-667838</vendorCode>
<categoryId>1728</categoryId>
<model>V198605N-1568C68</model>
<typePrefix>Ботинки</typePrefix>
<param name="Размер">39</param>
<param name="Цвет" hex="#0000FF">Синий</param>
<param name="Материал подошвы">Каучук</param>
<param name="Материал верха">Кожа</param>
<description>Прекрасные ботинки известного бренда</description>
<googleProductCategory>Apparel &amp; Accessories > Clothing > Shirts &amp; Tops</googleProductCategory>
<rec title="Похожие товары">213741,1899435,1630074</rec>
<rec title="Дополни образ">666000,777000</rec>
<badge textColor="#000" bgColor="#CCFF33">НОВИНКА</badge>
<badge picture="https://xxxxx/xxxxxx.png"></badge>
<badge type="smallImage" picture="https://xxxxx/xxxxxx.png" position="top-left"></badge>
<badge type="color" bgColor="#02d3b4" position="bottom-right"></badge>
<maxPromocodeDiscountPercent>0</maxPromocodeDiscountPercent>
<vat>vat_20</vat>
<picture>https://xxxx/xxxx/image1.jpg</picture>
<picture>https://xxxx/xxxx/image2.jpg</picture>
<useBonuses>true</useBonuses>
<preorder>true</preorder>
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

```xml
<categories>
<category id="6323" picture="https://xxx/xxx/xxx.jpg">Смартфоны и гаджеты</category>
<category id="183" parentId="6323" picture="https://xxx/xxx/xxx.jpg">Смартфоны</category>
</categories> 
```

### **Синонимы (поиск по ключевым словам, которых нет в названии/модели оффера):**

```markup
<offers>
  <offer id="61b06345-c404-11e0-ad14-3c4a926c6ba4" available="true">
    ...
    <name>Harry Potter™ Hogwarts™ Crests</name>
    <alias>Гарри поттер</alias>
    <alias>Хогвартс</alias>
  </offer>
  ...     
</offers>
```

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
