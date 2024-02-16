# Подтверждение email

{% hint style="danger" %}
Мы работаем только через **POST**-запросы
{% endhint %}

{% hint style="info" %}
Перед тем как подключить хук подтверждения email, необходимо для хуков авторизации и получения профиля добавить поле `emailConfirmed`см.[obekt-uchyotnaya-zapis-polzovatelya.md](uchyotnaya-zapis-polzovatelya.-avtorizaciya./obekt-uchyotnaya-zapis-polzovatelya.md "mention")&#x20;
{% endhint %}

## Описание хука "Подтверждение email"

После добавлении поля `emailConfirmed`, до подключения хука подтверждения email, **Профиль** клиента будет выглядеть следующим образом, если поле `emailConfirmed` имеет значение `false`.

<div align="center" data-full-width="false">

<figure><img src="../../.gitbook/assets/image (11).png" alt="" width="188"><figcaption><p>Неподтвержденный email без хука подтверждения</p></figcaption></figure>

</div>

После подключения хука бэйдж будет автоматически заменен на кнопку, отправляющую с бекенда imshop запрос на адрес хука (подробнее в описании запроса). Выглядит следующим образом

<figure><img src="../../.gitbook/assets/image (12).png" alt="" width="188"><figcaption><p>Неподтвержденный email с подключенным хуком подтверждения</p></figcaption></figure>

После пользователем совершения действий для подтверждения и получения в хуке профиля значения поля `emailConfirmed` информация о статусе email исчезнет из профиля и пользователь увидит следующее

<figure><img src="../../.gitbook/assets/image (13).png" alt="" width="188"><figcaption><p>Подтвержденный email</p></figcaption></figure>

## Описание запроса

При нажатии на кнопку **"Подтвердить email"** из бекенда imshop в бекенд клиента будет уходить POST запрос со следующим содержанием

```json
 {
    "userIdentifier":"12345",
    "userEmail":"test@test.test"
 } 
```

* **`userIdentifier`** — идентификатор пользователя, полученный от системы клиента на этапе авторизации
* **`userEmail`** — email пользователя, указанный им при регистрации или в личном кабинете мобильного приложения

## Описание ответа

В ответ бекенд imshop ожидает следующие поля

```json
{
  "success": true,
  "message": "Ссылка для подтверждения отправлена на указанный email"
}
```

* **`success`** — boolean (обязательное поле), статус получения и обработки запроса&#x20;
* &#x20;**`message`**  — string (обязательное поле), сообщение, которое будет показано пользователю после нажатия на кнопку
