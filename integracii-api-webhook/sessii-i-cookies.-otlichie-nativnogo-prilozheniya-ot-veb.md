# 🍪 Сессии и Cookies. Отличие нативного приложения от веб

{% hint style="info" %}
**IMSHOP Retail Protocol** **(IRP)** - протокол обмена данными, разработанный в IMSHOP для обмена данными между IMSHOP и системами ритейлера (включая веб-сайт, CRM, OMS, WMS и прочие программные комплексы).
{% endhint %}

{% hint style="danger" %}
IMSHOP Retail Protocol является объектом интеллектуальной собственности ООО «АЙ ЭМ СОЛЮШНЗ» (IMSHOP) и защищён как объект авторского права. Свидетельство о депонировании произведения № 023-014461 от 16 января 2023 г. подтверждает исключительные права ООО «АЙ ЭМ СОЛЮШНЗ» на данные технологии.

IMSHOP Retail Protocol создан по заказу ООО «АЙ ЭМ СОЛЮШНЗ». Использование IMSHOP Retail Protocol допустимо только при взаимодействии с ООО "АЙ ЭМ СОЛЮШНЗ" и наличии действующего лицензионного договора. Более подробно можно ознакомиться [здесь](../api-license.md).
{% endhint %}

## Основные отличия

Нативные мобильные приложения радикально отличаются от веб-приложений и сайтов. Из самых очевидных отличий:

* Платфора IMSHOP является stateless и не хранит серверное состояние ни в мобильном приложении, ни на бекенде.
* Приложение не поддерживает Cookies в стандартном понимании веб-разработки и не совместимо со стандартным механизмом веб-сессий.
* В мобильных приложениях технически невозможно использовать JS библиотеки и SDK, предназначенные для веба
* Трекинг установок через UTM метки невозможен. Для отслеживания источника установок необходимо использовать специальные MMP сервисы.

***

## Что означает "stateless API и приложение"?

Stateless API платформы IMSHOP и stateless приложение означает, что ни бекенд IMSHOP, ни приложение не хранят никаких флагов, "признаков", cookies и прочих данных, которые могут влиять на результат выполнения последующих запросов.

Каждый запрос включает в себя исчерпывающий набор данных, достаточный для получения ответа на конкретно этот запрос. Каждый запрос может быть выполнен независимо.

Этот подход несет в себе следующие плюсы:

* Каждый запрос может быть выполнен независимо от остальных. Ритейлеры, обслуживающие большое количество онлайн посетителей могут легко масштабировать обработку запросов от IMSHOP горизонтально
* Каждый запрос может быть идемпотентным[^1] и может быть кеширован на стороне ритейлера для радикального снижения нагрузки
* При масштабировании системы горизонтально, асинхронность запросов перестает быть проблемой со stateless запросами, так как порядок выполнения stateless запросов не важен

## Почему нет cookies? Как управлять сессиями, если бекенд ритейлера имеет состояние?

Cookies - это веб механизм, позволяющий хранить состояние, определенное сервером на стороне клиента. Очень часто Cookies хранят в себе только идентификатор сессии, а сами данные хранятся на бекенде ритейлера. Так как набор Cookies может меняться (и очень часто меняется) от запроса к запросу, то это нарушает принцип stateless api:

* Запрос невозможно повторить как есть. Тело/заголовки запросов могут зависеть от результата других нерелевантных запросов
* Результаты невозможно кешировать на стороне IMSHOP
* Кеширование на стороне ритейлера становится сложнее
* Порядок выполнения запросов теперь важен
* Проблемы с механизмом хранения сессий на стороне сервера могут вызывать сайд-эффекты на стороне приложения (де-авторизация/разлогин пользователей, потеря данных итд)

### Я понимаю минусы, но что делать если фреймфорк/CMS/OMS/CRM имеет состояние для пользователя/корзины/прочих данных и использует сессии для управления состоянием?

В момент установки приложения устройству выдается `Install ID`. Это случайный уникальный идентификатор. Он присваивается устройству до выполнения первого запроса и никогда не меняется. Единственный способ изменить `Install ID` - это переустановить приложение.

`Install ID` передается во всех запросах от IMSHOP к инфраструктуре ритейлера. Если инфраструктура ритейлера имеет состояние, которое хранится в веб-сессии (например текущий состав корзины с примененными промокодами и выбранной доставкой), то ритейлер должен на своей стороне связывать `Install ID` с сессией пользователя, либо использовать `Install ID` как идентификатор сессии.

{% hint style="info" %}
Пример:

* OMS обслуживающая сайт и приложение хранит состояние корзины в сессии. Не использовать сессии невозможно, так как любое изменение будет создавать в систему новую анонимную корзину, а процесс оформления заказа сильно усложнится.
* У каждой сессии есть идентификатор, которым нельзя управлять. OMS генерирует случайный идентификатор, который нельзя указать вручную при создании сессии

**Решение:**

* Ритейлер на стороне использует кеш-решение на свое усмотрение (например Redis или Memcached)
* Ритейлер получает от IMSHOP `Install ID` в каждом запросе
* Ритейлер не может создать сессию с `Install ID` в качестве идентификатора, но может хранить в кеше соответствие `Install ID` и идентификатора сессии:
  * Сначала проверяем есть ли в кеше идентификатор сессии для этого `Install ID`
  * Если его нет, то OMS создает новую сессию. Берем идентификатор только что созданной сессии и сохраняем его в кеше для `Install ID` с которого пришел запрос
  * При последующем запросе, находим в кеше уже существующую связку `Install Id` + идентификатора сессии и продолжаем сессию с найденным идентификатором
{% endhint %}

{% hint style="info" %}
Допускается также хранить `install id` и идентификаторы сессии в БД или даже профиле пользователя (для авторизованных пользователей), но использование key-value решений (redis / memcached) является более гибким и более простым
{% endhint %}



[^1]: Запросы, имеющие одни и те же данные в параметрах/теле запроса порождают один и тот же результат.&#x20;



    **Например:**&#x20;

    рассчет скидок для одной и той же корзины у одного и того же пользователя вызванный несколько раз подряд с одними и теми же условиями возвращает одни и те же цены. Проверка наличия одного и того же товара в одном и том же городе вернет один и тот же результат.