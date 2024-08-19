# Ивенты и расшифровка

* **account\_personal\_data\_submitted** -юзер заполнил личные данные
* **add\_to\_cart** - юзер добавил товар в корзину
* **add\_to\_wishlist** - юзер добавил товар в вишлист
* **add\_to\_cart\_from\_navigation\_history** - добавление в корзину из "Ранее вы смотрели"
* **app\_clear\_data** - удаление аккаунта/очистил личные данные
* **app\_open** - запуск приложения
* **app\_remove** - удаление приложения (only android)
* **app\_review\_modal\_closed** - юзер закрыл модалку оценки
* **app\_review\_modal\_user\_response\_no** - юзер сказал что приложение не нравится
* **app\_review\_modal\_user\_response\_yes** - юзер сказал что приложение нравится
* **app\_review\_modal\_review\_submitted**
* **app\_update** - обновление приложения
* **appsflyer\_error** - артефакт/ со временем исчезнет из аналитики
* **barcode\_scanner\_opened** - запуск баркод/qr сканера
* **begin\_checkout** - запуск чекаута
* **cart\_items\_nav\_history\_add\_to\_cart** - юзер добавил товар в корзину из раннее просмотренных товаров в корзине
* **cart\_items\_nav\_history\_wishlist** - юзер добавил товар в вишлист из ранее просмотренных товаров в корзине
* **category\_selected** - переход в категорию
* **cancel\_order\_from\_order\_history -** отмена заказа из истории заказов
* **choosing\_delivery\_method** - смена способа доставки
* **choosing\_payment\_method** - смена способа оплаты
* **completed\_registration** - успешная регистрация юзера (создание пользователя)
* **dynamic\_link\_app\_open** - записывается, когда пользователь повторно открывает приложение через динамическую ссылку
* **dynamic\_link\_first\_open -** записывается, когда пользователь впервые открывает приложение через динамическую ссылку.
* **delivery\_address\_selection\_confirmed** - юзер заполнил адрес доставки
* **delivery\_address\_selection\_started** - юзер начал заполнять адрес доставки
* **filters\_applied** - применение фильтра
* **filters\_requested** - выдан список товаров соответсвующий фильтрам
* **first\_open** - первый запуск приложения
* **get\_presents\_tap\_after\_purchase** - нажали на кнопку Получить подарок на экране Спасибо за покупку
* get\_presents\_tap\_on\_order\_history - нажали на кнопку Подарки на экране история заказов
* **install\_on\_promotion** - отображает сколько раз установили ваше приложение из других приложений. Это показатель входящего трафика от сторонних приложений к нам. Т.е. число установок вашего приложения
* **item\_3d\_model\_tap** - переход в 3д модель с карточки товара
* **item\_badge\_tap** - клик на бейджик (шильдик) карточки товара
* **item\_images\_carousel\_in\_cell\_swiped** - просмотр фото в листинге каталога
* **jump\_from\_search** - переход в поиск согласно запросу
* **navigate\_to\_order\_history** переход в историю заказов (с какого экрана перешли)
* **navigate\_to\_presents** - с какого экрана перешли на экран списка подарков
* **notification\_history\_opened** - открытие истории уведомлений в профиле
* **open\_search\_screen** - начал заполнять поиск
* **on\_customer\_choice\_item\_open** - открытие товара с раздела "Выбор покупателей"
* **on\_press\_listing\_banner**
* **on\_tab\_tap** - отображает нажатие пользователя на какой-либо таб в приложении (например Витрина/Каталог/Корзина/Избранное/Профиль)
* **on\_today\_navigation\_panel\_tag\_tap -** нажатие на панель навигации под поиском (напр. Каталог/Скидки)
* **on\_today\_search\_tag\_tap -** нажатие на поисковой тег в разделе "Сейчас ищут"
* **onboarding\_started** - начало прохождения онбординга
* **onboarding\_disabled\_push** - пропуск соглашения на приход уведомлений с онбординга
* **onboarding\_done** - завершение прохождения онбординга
* **onboarding\_enabled\_push** - соглашение на приход уведомлений с онбординга
* **onboarding\_gender\_selected** - выбор пола в онбординге
* **onboarding\_sizes\_selected** - выбор размера в онбординге
* **open\_banner\_on\_promotion** - отображает переход пользователей из трафикообмена на посадочный лендинг
* **open\_item\_from\_navigation\_history** - открытие товара из раздела "Ранее вы смотрели"
* **open\_order\_history\_after\_purchase** - открытие истории заказа после оформления заказа
* **open\_order\_processing\_screen** - открытие экрана Спасибо за покупку (TYP)
* **open\_promotion -** отображает какое из предложений на экране трафикообмена пользуется наибольшей популярностью в вашем приложении
* **os\_update** -системный дубль **app\_update**
* **payment\_by\_card** - выбран способ оплаты картой
* **payment\_in\_cash** -выбран способ оплаты наличкой
* **payment\_accepted** - платеж принят
* **payment\_method\_initiated** - список оплат получен
* **pickup\_location\_selection\_confirmed** - выбран локация доставки пвз
* **pickup\_location\_selection\_started** - получен список локаций пвз
* **product\_photo\_swiped** - юзер свайпает фото на карточке товара
* **promocode\_active** - применен промокод
* **profile\_button\_clicked** - пользователь кликает по кнопке экрана профиля
* **purchase** - покупка
* **push\_notification\_opened** - открыт пуш
* **registration\_authorization** - авторизация юзера (вход в свой аккаунт)
* **remove\_from\_cart** - товар удален из корзины
* **screen\_view** - просмотр экрана (любого)
* **search** - применен поиск
* **session\_start** - начал сессию (новая сессия начинается через 10 минут если приложение было неактивно)
* **share\_item** - пользователь делится карточкой товара
* **size\_grid\_opened -** открыта таблица размеров
* **quick\_menu\_tap** - "Быстрое меню", при нажатии на пункт меню трекается эвент quick\_menu\_tap с аттрибутами url и title
* **sort\_event** - применил сортировку
* **today\_screen\_city\_selected** - сменил город на главной
* **today\_screen\_deep\_link\_tap** - юзер перешел в баннер
* **transition\_to\_recommended\_item** - перешел в рекомендованный товар
* **quick\_checkout\_started** - начат быстрые чекаут
* **view\_item** - просмотр товара
* **view\_item\_list** - просмотр списка товаров
* **wishlist\_items\_nav\_history\_add\_to\_cart** - добавил товар в корзину из списка ранее просмотренных в корзину
* **wishlist\_items\_nav\_history\_wishlist** - добавил товар в вишлист из списка ранее просмотренных в вишлисте
* **item\_pay\_now\_checkout\_started** - старт быстрого чекаута с карточки товара
* **app\_clear\_data -** удаление данных юзера
* **on\_today\_search\_tag\_tap** - запуск поиска с тудея
* **story\_url\_open** - нажатие на кнопку в сториз
* **open\_story** - открытие сториз
* **today\_screen\_external\_link\_tap** - переход на внешнюю ссылку с экрана витрины
