# Передача наличия товара в YML фиде

Наличие товаров можно также передать непосредственно в YML фиде при отсутствии возможности сформировать отдельный фид наличия.

## Описание формата

Внутри тега `<shop>` \(на одном уровне с тегами `<categories>` и `<offers>`\) необходимо передать два новых блока \(тега\): `<outlets>` \(список магазинов и складов\) и `<availability>` \(наличие\). Рекомендуем передавать эти теги в самом начале фида, перед категориями и товарами.

### Магазины / склады

* **`outlets`** - Cписок магазинов
  * **`outlet`** - Магазин
    * **`id`** \(аттрибут\) - идентификатор магазина
    * **`name`** - Название
    * **`online`** - Является складом интернет магазина
    * **`city`** - Город
    * **`address`** - Адрес
    * **`subway`** - Станция метро
    * **`lat`** - Широта
    * **`lon`** - Долгота
    * **`role`** - Тип \(может быть передано несколько тегов **`role`**\). Возможные значения:
      * **`store`** - магазин
      * **`warehouse`** - склад
      * **`distributionCenter`** - распределительный центр

### Наличие

* **`availability`** - Список остатков
  * **`product`** - Товар
    * **`id`** \(аттрибут\) - идентификатор товарного предложения
    * **`outlet`** \(аттрибут\) - идентификатор магазина
    * **`quantity`** \(аттрибут\) - количество

## Пример

```markup
<?xml version="1.0" encoding="UTF-8"?>
<yml_catalog date="2020-07-21 19:31">
<shop>
	<outlets>
		<outlet id="ЦБ-000002">
			<name>Охотный Ряд</name>
			<online>false</online>
			<city>Москва</city>
			<address>Манежная площадь  дом 1 стр 2</address>
			<subway>Охотный ряд</subway>
			<lat>55.75497137</lat>
			<lon>37.614063</lon>
			<role>store</role>
			<role>warehouse</role>
		</outlet>
		<outlet id="CB-000009">
			<name>Хорошо</name>
			<online>false</online>
			<city>Москва</city>
			<address>Хорошёвское ш. 27</address>
			<subway>ЦСКА</subway>
			<lat>55.66365837</lat>
			<lon>37.510536</lon>
			<role>store</role>
			<role>warehouse</role>
		</outlet>
	</outlets>
	<availability>
		<product id="ec311960-add0-11e4-80e3-00505680614f" outlet="ЦБ-000002" quantity="1"/>
		<product id="8766dd99-be58-11e4-80e3-00505680614f" outlet="CB-000009" quantity="1"/>
	</availability>
	<categories>
		....
	</categories>
	<offers>
		....
	</offers>
</shop>
```

