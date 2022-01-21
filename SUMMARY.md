# Table of contents

* [Документация](README.md)

## Синхронизация каталога <a href="#sync" id="sync"></a>

* [YML (фид каталога товаров)](sync/yml/README.md)
  * [Для тарифов с Elasticsearch](sync/yml/elastic.md)
* [Фиды наличия товаров](sync/availability-feed.md)
* [Фиды наличия товаров (для маркетплейсов)](sync/availability-feed-for-marketplaces.md)
* [Передача наличия товара в YML фиде](sync/yml-availability.md)

## Интеграция (API / webhooks) <a href="#api" id="api"></a>

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
  * [Поиск. Поисковая выдача](api/dopolnitelnye-integracii/poisk.-poiskovaya-vydacha.md)
  * [Отзывы на товары](api/dopolnitelnye-integracii/reviews.md)
  * [Учётная запись пользователя. Авторизация. История заказов](api/dopolnitelnye-integracii/users/README.md)
    * [Авторизация по номеру телефона + SMS](api/dopolnitelnye-integracii/users/otp.md)
    * [Получение и редактирование данных учётной записи](api/dopolnitelnye-integracii/users/user.md)
    * [История заказов](api/dopolnitelnye-integracii/users/order-history.md)
    * [Оценка качества обслуживания (в разработке)](api/dopolnitelnye-integracii/users/ocenka-kachestva-obsluzhivaniya-v-razrabotke.md)
    * [Избранное (вишлист) пользователя (в разработке)](api/dopolnitelnye-integracii/users/wishlist.md)
    * [Объект «Учётная запись пользователя»](api/dopolnitelnye-integracii/users/obekt-uchyotnaya-zapis-polzovatelya.md)
  * [Персональные предложения](api/dopolnitelnye-integracii/personal-offers.md)
  * [Персональные предложения в розничном магазине](api/dopolnitelnye-integracii/personal-offers-instore.md)
  * [Рейтинг качества обслуживания](api/dopolnitelnye-integracii/reiting-kachestva-obsluzhivaniya.md)
  * [История бонусов](api/dopolnitelnye-integracii/bonuses-history.md)
  * [Формы](api/dopolnitelnye-integracii/forms.md)
  * [Допы (в  разработке)](api/dopolnitelnye-integracii/addons.md)
  * [Информация о ПВЗ](api/dopolnitelnye-integracii/informaciya-o-pvz-v-razrabotke.md)
  * [Лайки/дизлайки отзывов (в разработке)](api/dopolnitelnye-integracii/laiki-dizlaiki-otzyvov-v-razrabotke.md)
  * [Баннеры на главном экране (в разработке)](api/dopolnitelnye-integracii/bannery-na-glavnom-ekrane-v-razrabotke/README.md)
    * [Создание/обновление баннера (в разработке)](api/dopolnitelnye-integracii/bannery-na-glavnom-ekrane-v-razrabotke/sozdanie-obnovlenie-bannera-v-razrabotke.md)
    * [Удаление баннера](api/dopolnitelnye-integracii/bannery-na-glavnom-ekrane-v-razrabotke/udalenie-bannera.md)
* [Приложение продавца](api/dss/README.md)
  * [Статистика](api/dss/sales-stats.md)

## Интеграция эквайринга <a href="#payments" id="payments"></a>

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

## Digital Store Solution (интеграция OMS) <a href="#dss" id="dss"></a>

* [Создание заявки](dss/new-order.md)
* [Уведомления об обновлении статуса заявки](dss/webhook-updates.md)

## Примерочные <a href="#fitting" id="fitting"></a>

* [Список примерочных](fitting/rooms.md)
* [Уведомления об обновлении статуса примерочной](fitting/room-update.md)

## Инструменты <a href="#tools" id="tools"></a>

* [Создание диплинков](tools/deeplink-tool.md)
* [Universal ссылки](tools/universal-links.md)
