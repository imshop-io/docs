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
* [Дополнительные интеграции](api/extra-integrations/README.md)
  * [Проверка наличия товара](api/extra-integrations/availability.md)
  * [Расчет корзины, скидок, баллов](api/extra-integrations/calc.md)
  * [Синхронизация статусов заказов](api/extra-integrations/order-status-sync.md)
  * [Отправка уведомлений пользователям](api/extra-integrations/otpravka-uvedomlenii-polzovatelyam.md)
  * [Эквайринг через webhook](api/extra-integrations/acquiring-webhook.md)
  * [Поисковые подсказки](api/extra-integrations/search-suggestions.md)
  * [Поиск. Поисковая выдача](api/extra-integrations/poisk.-poiskovaya-vydacha.md)
  * [Отзывы на товары](api/extra-integrations/reviews.md)
  * [Учётная запись пользователя. Авторизация. История заказов](api/extra-integrations/users/README.md)
    * [Авторизация по номеру телефона + SMS](api/extra-integrations/users/otp.md)
    * [Получение и редактирование данных учётной записи](api/extra-integrations/users/user.md)
    * [История заказов](api/extra-integrations/users/order-history.md)
    * [Оценка качества обслуживания (в разработке)](api/extra-integrations/users/ocenka-kachestva-obsluzhivaniya-v-razrabotke.md)
    * [Избранное (вишлист) пользователя (в разработке)](api/extra-integrations/users/wishlist.md)
    * [Объект «Учётная запись пользователя»](api/extra-integrations/users/obekt-uchyotnaya-zapis-polzovatelya.md)
  * [Персональные предложения](api/extra-integrations/personal-offers.md)
  * [Персональные предложения в розничном магазине](api/extra-integrations/personal-offers-instore.md)
  * [Рейтинг качества обслуживания](api/extra-integrations/reiting-kachestva-obsluzhivaniya.md)
  * [История бонусов](api/extra-integrations/bonuses-history.md)
  * [Формы](api/extra-integrations/forms.md)
  * [Допы (в  разработке)](api/extra-integrations/addons.md)
  * [Информация о ПВЗ](api/extra-integrations/informaciya-o-pvz.md)
  * [Лайки/дизлайки отзывов (в разработке)](api/extra-integrations/laiki-dizlaiki-otzyvov-v-razrabotke.md)
  * [Рекомендация товаров](api/extra-integrations/rekomendaciya-tovarov.md)
  * [Баннеры на главном экране (в разработке)](api/extra-integrations/bannery-na-glavnom-ekrane-v-razrabotke/README.md)
    * [Создание/обновление баннера (в разработке)](api/extra-integrations/bannery-na-glavnom-ekrane-v-razrabotke/sozdanie-obnovlenie-bannera-v-razrabotke.md)
    * [Удаление баннера](api/extra-integrations/bannery-na-glavnom-ekrane-v-razrabotke/udalenie-bannera.md)
  * [Синхронизация избранного с сайтом (в разработке)](api/extra-integrations/wishlist-sync.md)
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
