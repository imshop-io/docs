# Авторизация в телеграм-приложении

{% hint style="danger" %}
**IMSHOP Retail Protocol (IRP)** является объектом интеллектуальной собственности ООО «АЙ ЭМ СОЛЮШНЗ» (IMSHOP) и защищён как объект авторского права. Свидетельство о депонировании произведения № 023-014461 от 16 января 2023 г. подтверждает исключительные права ООО «АЙ ЭМ СОЛЮШНЗ» на данные технологии.

IMSHOP Retail Protocol создан по заказу ООО «АЙ ЭМ СОЛЮШНЗ». Использование IMSHOP Retail Protocol допустимо только при взаимодействии с ООО "АЙ ЭМ СОЛЮШНЗ" и наличии действующего лицензионного договора. Более подробно можно ознакомиться [здесь](../../../api-license.md).
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

«Золотой» сценарий:

1. Пользователь видит кнопку "авторизоваться" в телеграм приложении
2. Пользователь нажимает кнопку и видит запрос на разрешение поделиться номером телефона
3. Телеграм приложение отправляет запрос с верифицированным номером телефона через чат в сервер IMSHOP.IO
4. Сервер IMSHOP.IO получает запрос от Telegram и проверяет запрос на фрод, убеждается что номер телефона подтвержден и действительно принадлежит пользователю.
5. Сервер IMSHOP.IO отправляет в бекенд ритейлера подписанный запрос с номером телефона покупателя и его ID в телеграм
6. Бекенд ритейлера также возвращает данные пользователя

## Запрос профиля из бекенда ритейлера

`APP SERVER → INFRASTRUCTURE`

{% hint style="info" %}
От вас потребуется URL, на который наш сервер будет слать **POST**-запрос.
{% endhint %}

В вашу систему будут приходить вот такие данные:

```json
{
    "identityProviderUserIdentifier": "12345|71234567890",
    "identityProvider": "telegram",
    "payload": {
        "tma": "XXX"
    }
}
```

* **`userIdentifier`** — идентификатор пользователя в формате `<telegram_id>|<телефон>`
* **`payload`** - данные о пользователе, и подпись запроса, полученные из telegram

### Аккаунт существует

Если запрошенный аккаунт существует, вы должны ответить профилем пользователя в системе

**Пример ответа:**

```json
{
    "user": {
        "id": "123",
        "name": "Иванов Иван",
        "phone": "71234567890",
        "email": "ivanov@mail.com",
        "bonuses": 10000,
        "pendingBonusesTitle": "Будет накоплено",
        "pendingBonuses": 1000,
        "exressBonusesTitle": "Экспресс-бонусы",
        "expressBonuses": 500,
        "loyaltyProgram": {
            "currentLevelTitle": "Золотой уровень",
            "progress": 60,
            "profitDescription": "Cashback до 20% с каждой покупки",
            "nextLevelDescription": "Совершите покупку на 1000 рублей до уровня Платиновый",
            "backgroundColor": "gold",
            "progressBarColor": "black",
            "progressBarBackroundColor": "white",
            "textColor": "black"
        },
        "segments": ["registered", "loyal"],
        "age": 35,
        "gender": "male",
        "cardNumber": "456123789"
    }
}
```

Формат ответа описан в [документации получения профиля пользователя](poluchenie-dannykh-uchyotnoi-zapisi.md)

### **Регистрация**

Если данный номер телефона не зарегистрирован, вы можете **не отправлять профиль,** а сначала запросить дополнительные данные для регистраци.

Для этого необходимо ответить на запрос в следующем формате:

```javascript
{
    "dataRequired": ["email", "fullName"]
}
```

* **`dataRequired`** - список полей для запроса дополнительных данных\
  возможные значения:
  * **`email`** - e-mail
  * **`fullName`** - ФИО
  * **`birthday`** - день рождения
  * **`gender`** - пол
  * **`allowSms`** - запрос на разрешение отправки рекламных смс
  * **`allowEmail`** - запрос на разрешение отправки рекламных e-mail
  * **`allowMarketing`** - запрос на разрешение отправки рекламных акций (без уточнения канала)
  * **`referralCode`** - поле для реферального кода
  * **`legalEntities`** - возможность добавить юридическое лицо в профиль
* **`dataOptional`** - список необязательных для заполнения полей. Обратите внимание, что указанные в этом поле идентификаторы полей должны быть прописаны и в **`dataRequired`**

После сбора дополнительных данных, запрос на получение OTP будет повторен, но в запрос будут приложены все запрошенные данные. Пример:

```json
{
    "identityProviderUserIdentifier": "12345|71234567890",
    "identityProvider": "telegram",
    "payload": {
        "tma": "XXX"
    },
    "email": "some@mail.com",
    "fullName": "Николай Иванов",
    "birthday": "1980-01-31",
    "gender": "f"
}
```

В ответ на этот запрос вы должны зарегистрировать пользователя, и ответить полным профилем пользователя.

### Идентификаторы пользователя

* **`identityProviderUserIdentifier`** - идентификатор пользователя, полученный из внешнего сервиса авторизации и подтверждения (в данном случае - telegram)
* **`userIdentifier`** - идентификатор пользователя в вашей CRM / CDP / сайте. Будет использоваться во всех запросах, когда пользователь авторизован

### Подпись запросов, антифрод, безопасность

В telegram, при запросе номера телефона, покупатель может поделиться только телефоном, подтвержденным по СМС. Сервера IMSHOP проверяют запрос от telegram на аутентичность.

IMSHOP пересылает в бекенд ритейлера **`tma`** параметр из телеграм приложения. Описание этого параметра.

Бекенд ритейлера может использовать **`tma`** для

* Валидации запроса на свой стороне (опционально, так как IMSHOP уже верифицирует запросы от телеграм приложения)
* Получения данных пользователя в telegram (например имя, фамилию и фото)

Подробнее про верификацию запросов и получению профиля пользователя из payload можно прочитать [в официальной документации telegram](https://docs.telegram-mini-apps.com/platform/init-data#validating).