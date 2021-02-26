---
description: Опции на выбор
---

# Товар: цвета, размеры и другие характеристики

{% hint style="warning" %}
Перед прочтением и реализацией согласуйте детали с вашим менеджером в IMSHOP.IO
{% endhint %}

### Ограничения

На этой странице описан формат передачи характеристик товара, который несовместим с примером из [основной спецификации фида](./).

* `group_id` и `offerId` не поддерживаются
* фильтрация по характеристикам не поддерживается \(функциональность находится в разработке\)

### Задача

У одной и той же модели товара могут существовать вариации, различающиеся по ключевым характеристикам. Например, у кроссовок могут быть размеры от 38го до 44го.

Если ключевых характеристик одна или две — следует использовать метод, описанный в [основной спецификации фида](./), см. `group_id`, `offerId`. Например, это сработает для товаров, у которых варьируются только размеры и цвета.

Если характеристик **три и более**, используется метод ниже.

### Описание формата

```markup
<?xml version="1.0" encoding="UTF-8"?>
<yml_catalog date="2017-02-05 17:22">
  <shop>
    <categories>
      <category …>…</category>
    </categories>
    <offers>
      <offer …>
        <variableParam name="Ширина" id="width">
          <!-- Ширина 30 см. -->
          <value id="30" name="30 см.">
            <variableParam name="Высота" id="height">
              <value id="10" name="10 см."><!-- 30×10×? -->
                <variableParam name="Длина" id="length">
                  <value id="60" name="60 см." /><!-- 30×10×60, значение по умолчанию -->
                  <value id="70" name="70 см." />
                  <value id="80" name="80 см." />                  
                </variableParam>
              </value>
              <value id="20" name="20 см."><!-- 30×20×? -->
                <variableParam name="Длина" id="length">
                  <value id="60" name="60 см." />
                  <value id="70" name="70 см." /><!-- 30×20×70 -->
                  <value id="80" name="80 см." />                  
                </variableParam>
              </value>
              <value id="25" name="25 см."><!-- 30×25×? -->
                <variableParam name="Длина" id="length">
                  <value id="60" name="60 см." />
                  <value id="70" name="70 см." />
                  <value id="80" name="80 см." />                  
                </variableParam>
              </value>
            </variableParam>
          </value>
          <!-- Ширина 40 см. -->
          <value id="40" name="40 см.">
            <variableParam name="Высота" id="height">
              <value id="10" name="10 см."><!-- 40×10×? -->
                <variableParam name="Длина" id="length">
                  <value id="60" name="60 см." />
                  <value id="70" name="70 см." />
                </variableParam>
              </value>
              <value id="20" name="20 см."><!-- 40×20×? -->
                <variableParam name="Длина" id="length">
                  <value id="60" name="60 см." /><!-- 40×20×60, единственное значение -->
                </variableParam>
              </value>
            </variableParam>
          </value>
        </variableParam>
      </offer>
    </offers>
  </shop>
</yml_catalog>
```

{% hint style="warning" %}
Все параметры — обязательные
{% endhint %}

#### offer → variableParam

* **`name`** — отображаемое название \(например, «Ширина»\)
* **`id`** — идентификатор, используемый в интеграциях корзины, доставок, оплат, оформления заказа и т.д. \(например, «width»\)

#### offer → variableParam → value 

* **`id`** — идентификатор, используемый в интеграциях корзины, доставок, оплат, оформления заказа и т.д.
* **`name`** — отображаемое значение

