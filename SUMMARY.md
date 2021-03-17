# Table of contents

* [Документация](README.md)

## Синхронизация каталога <a id="sync"></a>

* [YML \(фид каталога товаров\)](sync/yml.md)
* [Фиды наличия товаров](sync/availability-feed.md)
* [Фиды наличия товаров \(для маркетплейсов\)](sync/availability-feed-for-marketplaces.md)
* [Передача наличия товара в YML фиде](sync/yml-availability.md)

## Интеграция \(API / webhooks\) <a id="api"></a>

* [Общая информация о подключении по API](api/general.md)
* [Расчет корзины, скидок, баллов](api/calc.md)
* [Доставки](api/deliveries.md)
* [Оплаты](api/payments.md)
* [Эквайринг через webhook](api/acquiring-webhook.md)
* [Проверка наличия товара](api/availability.md)
* [Оформление заказа](api/order.md)
* [Синхронизация статусов заказов](api/order-status-sync.md)
* [Персональные предложения](api/personal-offers.md)
* [Отзывы на товары](api/reviews.md)
* [Учётная запись пользователя. Авторизация. История заказов](api/users/README.md)
  * [Авторизация по номеру телефона + SMS \(предпочтительный способ авторизации\)](api/users/otp.md)
  * [Авторизация через пару логин + пароль \(используйте только если авторизация по SMS невозможна\)](api/users/email-auth.md)
  * [Получение и редактирование данных учётной записи](api/users/user.md)
  * [История заказов](api/users/order-history.md)
  * [Избранное \(вишлист\) пользователя \(в разработке\)](api/users/wishlist.md)
* [Поисковые подсказки](api/search-suggestions.md)
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

