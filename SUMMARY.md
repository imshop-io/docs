# Table of contents

* [Документация](README.md)

## Синхронизация каталога <a id="sync"></a>

* [YML \(фид каталога товаров\)](sync/yml/README.md)
  * [Для тарифов с Elasticsearch](sync/yml/elastic.md)
* [Фиды наличия товаров](sync/availability-feed.md)
* [Фиды наличия товаров \(для маркетплейсов\)](sync/availability-feed-for-marketplaces.md)
* [Передача наличия товара в YML фиде](sync/yml-availability.md)

## Интеграция \(API / webhooks\) <a id="api"></a>

* [Общая информация о подключении по API](api/general.md)
* [ОФОРМЛЕНИЕ ЗАКАЗА. Доставки, оплаты](api/oformlenie-zakaza.-dostavki-oplaty/README.md)
  * [Оформление заказа](api/oformlenie-zakaza.-dostavki-oplaty/order.md)
  * [Доставки](api/oformlenie-zakaza.-dostavki-oplaty/deliveries.md)
  * [Оплаты](api/oformlenie-zakaza.-dostavki-oplaty/payments.md)
* [Объект «Местоположение»](api/obekt-mestopolozhenie.md)
* [Дополнительные интеграции](api/dopolnitelnye-integracii/README.md)
  * [Проверка наличия товара](api/dopolnitelnye-integracii/availability.md)
  * [Расчет корзины, скидок, баллов](api/dopolnitelnye-integracii/calc.md)
  * [Синхронизация статусов заказов](api/dopolnitelnye-integracii/order-status-sync.md)
  * [Эквайринг через webhook](api/dopolnitelnye-integracii/acquiring-webhook.md)
  * [Поисковые подсказки](api/dopolnitelnye-integracii/search-suggestions.md)
  * [Отзывы на товары](api/dopolnitelnye-integracii/reviews.md)
  * [Учётная запись пользователя. Авторизация. История заказов](api/dopolnitelnye-integracii/users/README.md)
    * [Авторизация по номеру телефона + SMS \(предпочтительный способ авторизации\)](api/dopolnitelnye-integracii/users/otp.md)
    * [Авторизация через пару логин + пароль \(используйте только если авторизация по SMS невозможна\)](api/dopolnitelnye-integracii/users/email-auth.md)
    * [Получение и редактирование данных учётной записи](api/dopolnitelnye-integracii/users/user.md)
    * [История заказов](api/dopolnitelnye-integracii/users/order-history.md)
    * [Избранное \(вишлист\) пользователя \(в разработке\)](api/dopolnitelnye-integracii/users/wishlist.md)
  * [Персональные предложения](api/dopolnitelnye-integracii/personal-offers.md)
  * [Формы](api/dopolnitelnye-integracii/forms.md)
* [Приложение продавца](api/dss/README.md)
  * [Статистика](api/dss/sales-stats.md)

## Интеграция эквайринга <a id="payments"></a>

* [Яндекс.Касса](payments/yandex.kassa.md)
* [Сбербанк](payments/sberbank.md)
* [Apple Pay](payments/apple-pay.md)

## Интеграция в службы доставки

* [СДЭК](integraciya-v-sluzhby-dostavki/cdek.md)
* [Boxberry](integraciya-v-sluzhby-dostavki/boxberry.md)
* [Яндекс.Доставка](integraciya-v-sluzhby-dostavki/yandeks.delivery.md)
* [Грастин](integraciya-v-sluzhby-dostavki/grastin.md)

## Fulfillment

* [ESolutions](fulfillment/esolutions.md)
* [LaModa B2B](fulfillment/lamoda-b2b.md)

## Digital Store Solution \(интеграция OMS\) <a id="dss"></a>

* [Создание заявки](dss/new-order.md)
* [Уведомления об обновлении статуса заявки](dss/webhook-updates.md)

## Примерочные <a id="fitting"></a>

* [Список примерочных](fitting/rooms.md)
* [Уведомления об обновлении статуса примерочной](fitting/room-update.md)

## Инструменты <a id="tools"></a>

* [Создание диплинков](tools/deeplink-tool.md)
* [Universal ссылки](tools/universal-links.md)

