---
description: sortDefinitions -> sortDefinition
---

# Кастомные сортировки

* **`customSort`** - дополнительная (custom) сортировка. необходимо передать тип из **`sortDefinitions`** (опционально)
*   **`type`** - тип сортировки (идентификатор). Далее используется в тегах **`offer`** для указания сортировки

    * значение - название в интерфейсе выбора сортировки в мобильном приложении
    * **`direction`** - направление сортировки по переданной величине. **`asc`** - по возрастанию, **`desc`** - по убыванию
    * **`main`** - использовать для сортировки товаров на главном экране. Только одна сортировка может быть **`main`**&#x20;
    * **`hidden`** - видимость. **`true`** / **`false`** . используется для скрытия из интерфейса сортировки в мобильном приложении. Например чтобы использовать сортировку для главного экрана, но не давать выбрать эту сортировку в каталоге.



```markup
<sortDefinitions>
  <sortDefinition type="home" direction="asc" main="true" hidden="true">Главный экран</sortDefinition>
  <sortDefinition type="popular" direction="asc">По популярности</sortDefinition>
  <sortDefinition type="new" direction="desc">Новинки</sortDefinition>
</sortDefinitions>
<offers>
  <offer id="61b06345-c404-11e0-ad14-3c4a926c6ba4" available="true" uuid="a43c03a5-3d1d-5791-b9a5-1ef95438cd8e" group_id="6" sizeGridImage="">
    <barcode>4627077842287</barcode>
    <barcode>2680983579717</barcode>
    <sort>2</sort>
    <customSort type="new">1610623217147</customSort>
    <customSort type="home">18</customSort>
    <customSort type="popular">12</customSort>
    ...
  </offer>
  ...     
</offers>
```
