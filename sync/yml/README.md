# YML (фид каталога товаров)

## Описание

Для того, чтобы товарный каталог отобразился в приложении, необходимо передать вашему менеджеру в IMSHOP.IO ссылку на актуальный фид в формате YML

{% hint style="info" %}
**YML** - [Yandex Market Language.](https://yandex.ru/support/partnermarket/export/yml.html) Формат, который использует Яндекс Маркет для получения товарного каталога. Если ваш магазин есть в Яндекс Маркете, или вы пользуетесь услугами сторонних облачных сервисов (например умный поиск товаров, системы рекомендаций, или программа лояльность), то скорее всего у вас уже есть YML фид.
{% endhint %}

Подробное описание формата можно [прочитать тут](https://yandex.ru/support/partnermarket/export/yml.html). Помимо стандартного функционала YML, IMSHOP.IO предлагает свой набор изменений для YML, которые позволяют передавать данные, не поддерживаемые в YML по стандарту Яндекса (например передача картинок для категорий, или передача флага доступности онлайн-оплаты для товара)

{% hint style="warning" %}
Пожалуйста, создавайте выгрузку товаров в соответствии с рекомендациями, указанными ниже!
{% endhint %}

## Подключение

Для настройки синхронизации каталога товаров на основе YML фида необходимо передать следующие данные вашему личному менеджеру в IMSHOP.IO:

* URL, по которому можно скачать каталог товаров в описанном формате
* Логин/пароль, если требуется HTTP-авторизация для доступа к выгрузке товаров
* Желаемое время обновления каталога товаров (например, раз в день в 01:00)

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

* **`id`** - _атрибут_, идентификатор товарного предложения - обязательна уникальность! в рамках каталога
* **`uuid`** - атрибут, дополнительный идентификатор товара (например, из 1С)
* **`group_id`** - атрибут, элемент объединяет все предложения, которые являются вариациями одной модели и должен иметь одинаковое значение
* **`available`** - атрибут, обязательный. Товары с **`available`** = **`false`** не будут отображаться в приложении вне зависимости от каких либо других факторов / апишек / остатков.
* **`sizeGridImage`** - атрибут, URL-ссылка на картинку с размерами для примерки
* **`itemPreviewUrl`** - атрибут, URL-ссылка на страницу с 3D-моделью товара (на саму страницу с 3D предпросмотром, не на карточку товара)
*   **`fraction`** - кратность товара, с которой можно добавлять его в корзину. Например, если fraction=0.2, то добавлять в корзину можно только 0.2, 0.4, 0.6 и т.д. единиц товара.

    fraction необходим для включения функционала. По умолчанию кратность всегда 1 к 1.

    Цена указывается за 1 (одну) полную единицу товара (не за 0.2, 0.3 и т.д.).

#### **offers -> offer (дочерные элементы)**

* **`barcode`** - штрихкод товара от производителя в одном из форматов: EAN-13, EAN-8, UPC-A, UPC-E. Элемент offer может содержать несколько элементов barcode, в этом случае каждый из штрихкодов передается в отдельном теге.
* **`name`** - полное название предложения, в которое входит: тип товара, производитель, модель и название товара, важные характеристики. Составляйте по схеме: что (тип товара) + кто (производитель) + товар (модель, название) + важные характеристики.
* **`url`** - URL страницы товара на сайте магазина
* **`sort`** - порядок сортировки по популярности
* **`vendor`** - производитель
* **`vendorCode`** - код производителя для данного товара
* **`model`** - модель и название товара
* **`typePrefix`** - тип / категория товара (например, «мобильный телефон», «стиральная машина», «угловой диван»)
* **`categoryId`** - идентификатор категории товара, присвоенный магазином. Элемент offer может содержать несколько элементов categoryId, в этом случае каждая из категорий передается в отдельном теге.
* **`googleProductCategory`** - google product category (GPC) taxonomy для товара.
* **`param`** - все важные характеристики товара — цвет, размер, объем, материал, вес, возраст, пол, и т. д. Элемент offer может содержать несколько элементов param (один элемент param — одна характеристика), в этом случае каждая характеристика передается в отдельном теге. (при использовании перелинковки цвета отдавать в hex формате )

```markup
<offer........>
...
    <param name="Артикул">CK7238-010</param>
            <param name="Размер">M</param>
            <param name="Цвет">Черный </param>
            <param name="Пол">Мужское </param>
            <param name="Страна">Вьетнам</param>
            <param name="Состав">100% нейлон</param>
            <param name="Рост на модели">176/М</param>
</offer>
...
```

* **`picture`** - URL-ссылка на картинку товара. Элемент offer может содержать несколько элементов picture, в этом случае каждая из картинок передается в отдельном теге.
* **`currencyId`** - валюта, в которой указана цена товара: RUR, USD, EUR, UAH, KZT, BYN.
* **`price`** - актуальная цена товара
* **`oldprice`** - старая цена товара, должна быть выше текущей
* **`parentVendorCode`** - по данному параметру объединяем товары для перелинковки (позволяет добавлять переключаемые параметры на карточку товара) **не должен пересекаться с group id, не используется вместе с othercolors**
* **`othercolors`**- блок товаров "еще в другом цвете", перечислить group Id товаров с альтернативными цветами. **Не используется вместе с parentVendorCode.**

```xml
<othercolors>352634_03,352634_75,352634_65,352634_66,352634_77</othercolors>
```

* **`retailPrice`** - РРЦ товара (цена товара в оффлайне в случае если отличается от price)
* **`deferPrice`** - цена на случай отсрочки получения, должна быть ниже `price`
* **`listPrice`** - необязательно, справочные цены, если нужно показать несколько цен, только для отображения, в расчетах не используются
  * **`title`** - атрибут, текстовое описание цены
  * **`city`** - (опционально), фиас города, только на тарифе с эластиком, если есть различия по городам
* **`description`** - описание предложения
* **`rec`** - идентификаторы товаров для блока рекомендаций через запятую (например, 11951,11860,11735)
  * Возможно передавать несколько блоков с подборками товаров, например "Похожие товары", "С этим покупают", "Дополни образ" итд. Для этого следует передать несколько тегов `rec` с атрибутом `title` (см пример)
* **`maxPromocodeDiscountPercent`** - максимальный процент скидки на данный товар, например, по купону. Используется для ограничения размера скидки, например, для товаров с низкой маржинальностью.
* **`vat`** - значение ставки НДС для товара. Для всех ставок НДС предусмотрены специальные значения.
  * НДС не облагается - `6` или `NO_VAT`
  * 0% - `5` или `VAT_0`
  * 10% - `2` или `VAT_10`
  * 20% - `7` или `VAT_20`
* **`useBonuses`** - возможность частичной или полной оплаты данного товара с бонусного счета при наличии программы лояльности
* **`overSized`** - крупногабаритный товар
* **`preorder`** -параметр для товаров по предзаказу
* **`badge`**- бейджик на картинке товара. Элемент offer может содержать несколько элементов badge, в этом случае каждый из бейджик передается в отдельном теге. **В одном бейдже может быть либо только текстовый вариант, либо только с картинкой. И текст и картинка в одной бейджике быть не могут.**
* текст, необязательно, указывается внутри тега
*   **`picture`**, атрибут, необязательно - картинка бейджика вместо текста, обязательно

    указание либо текста либо картинки
* **`textColor`**, атрибут, необязательно - цвет текста в формате #rrggbb
* **`bgColor`**, атрибут, необязательно - цвет фона для текстового бейджика в формате `#rrggbb`
* **`link`**, атрибут, необязательно - ссылка при нажатии на бейджик
* **`regionId`** - список виртуальных регионов через запятую, для тарифов с elasticsearch
* **`video`** - видео товара (можно передать несколько). Видео должны быть в формате H.264
  * **`main`** - если **`true`**, то видео будет отображаться в слайдере с фотографиями товара
  * **`title`** - опциональный заголовок видео
  * **`image`** - URL на картинку, которая отображается, пока грузится видео
* **`file`** - релевантные докумнеты
  * **`title`** - название
  * **`size`** (опционально) - вес файла для отображения на кнопке в приложении
  * **`icon`** (опционально) - иконка для отображения на кнопке в приложении
  * **`url`** - ссылка на скачивание

**categories -> category (атрибуты)**

* **`id`** - идентификатор категории
* **`parentId`** - идентификатор родительской категории
* **`picture`** - URL картинки категории
* **`textColor`** - цвет текста (опционально)
* **`backgroundColor`** - цвет фона (опционально)

### Сортировки&#x20;

#### Стандартная сортировка на витрине – желательно

* **`sort`** - порядок сортировки по популярности

{% hint style="info" %}
Цвет передается в hex формате. например **`FF1122`**
{% endhint %}

## Пример

```markup
<sortDefinitions>
  <sortDefinition type="home" direction="asc" main="true" hidden="true">Главный экран</sortDefinition>
  <sortDefinition type="popular" direction="asc">По популярности</sortDefinition>
  <sortDefinition type="new" direction="desc">Новинки</sortDefinition>
</sortDefinitions>
<categories>
  <category id="1" picture="https://www.respublica.ru/uploads/01/00/00/00/01/large_6b02643c12e57081.jpg">Книги</category>
  <category id="1742" parentId="1" picture="https://www.respublica.ru/uploads/00/00/00/01/ce/large_e8eb9fa0f2ec9362.jpg">Бестселлеры</category>
  <category id="6" parentId="1" picture="https://www.respublica.ru/uploads/00/00/00/00/06/large_a8dce8d4628022ee.jpg">Искусство, дизайн и мода</category>
  <category id="35" parentId="6" picture="https://www.respublica.ru/uploads/01/00/00/00/0z/large_654bfb4b1cc1c58a.jpg">Дизайн</category>
  ...
</categories>
<offers>
  <offer id="61b06345-c404-11e0-ad14-3c4a926c6ba4" available="true" uuid="a43c03a5-3d1d-5791-b9a5-1ef95438cd8e" group_id="6" sizeGridImage="">
    <barcode>4627077842287</barcode>
    <barcode>2680983579717</barcode>
    <sort>2</sort>
    <preorder>true</preorder>
    <customSort type="new">1610623217147</customSort>
    <customSort type="home">18</customSort>
    <customSort type="popular">12</customSort>
    <url>https://www.respublica.ru/knigi/iskusstvo-dizayn-i-moda/arhitektura/A001617-antonio-gaudi</url>
    <vendor>Caramella</vendor>
    <vendorCode>A001617</vendorCode>
    <model>V198605N-1568C68</model>
    <typePrefix>Книга</typePrefix>
    <price>450</price>
    <oldprice>650</oldprice>
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
    <parentVendorCode>37-edinorogov</parentVendorCode>
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
  ...     
</offers>
```

## Конфигурации по размерам внутри офера (делается по согласованию с менеджером)

Если по одной модели есть несколько товарных предложений (отличия по размеру), необходимо в каждый такой параметр добавить атрибут **`configurationID`** с уникальным идентификатором в качестве значения - он будет использоваться при проверке наличия.

```xml
<offer........>
...
    <param name="Размер" configurationId="a8974b77-c662-11e4-80c1-40f2e9a197bc#17">17</param>
    <param name="Размер" configurationId="a8974b77-c662-11e4-80c1-40f2e9a197bc#19">19</param>
</offer>
```

## Рекомендации (что важно клиенту)

### **Категории**

* Важно наличие отдельной картинки для категорий, иначе картинка берется из первого товара, что не всегда релевантно.
* Избегайте сильной вложенности категорий.
* Отсутствие или малое количество категорий при большом количестве товаров - это плохо.

### **Товары**

* Важно наличие не одной, а нескольких картинок товара, чем больше тем лучше!
* Поле **`param`** имеет значение, на основе параметров. Мобильное приложение автоматически формирует фильтр по возможным значениям параметра, поэтому важно избегать параметров с огромным количеством значений, или параметров, не описывающих характеристик товаров (например, не указывать модель товара, штрих-код или инструкцию по уходу / стирке в качестве параметра).
* Заполнять и передавать поле barcode, так как мобильное приложение имеет сканер штрих-кодов, по которому покупатель может быстро найти товар в каталоге.
* Заполнять поле **`sort`**, иначе сортировка товаров по популярности работать не будет
* Cоблюдать уникальность **`id`** товара в рамках выгрузки, товары с одинаковым **`id`** не попадут в каталог!
