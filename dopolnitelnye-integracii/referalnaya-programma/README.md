---
icon: link
---

# Реферальная программа

![](<../../.gitbook/assets/Screenshot 2022-10-14 at 12.22.14.png>)

{% hint style="danger" %}
Дополнительные интеграции вводятся в эксплуатацию после завершения основных интеграций:

* [Оформление заказа](../../osnovnye-integracii/oformlenie-zakaza.md)
* [Доставки](../../osnovnye-integracii/dostavki.md)
* [Оплаты](../../osnovnye-integracii/oplaty.md)

Для подключения дополнительных интеграций обратитесь к вашему менеджеру в IMSHOP.IO
{% endhint %}

Firebase сам генерит эту ссылку исходя из того что мы туда вшили, а туда мы вшиваем:

1\) ID баннера на который перейдет пользователь перейдя по этой ссылке (после установки приложения)

2\) реферальный код пользователя кто приглашает (берем ID пользователя из вашей системы).

Далее, как понять что по этой ссылке перешел клиент и нужно начислять бонусы, при переходе по ссылке и в дальнейшем первом открытии приложении, приложение запоминает реферальный код который был зашит в этой ссылке, и при регистрации в приложении, мы отправляем в webhook поле referralCode с этим кодом.

## Запрос

`APP SERVER → INFRASTRUCTURE`

{% hint style="warning" %}
От вас потребуется URL, на который наш сервер будет слать **POST**-запрос. Да, мы _запрашиваем_ данные через _POST_, а не через _GET_.
{% endhint %}

В вашу систему будут приходить вот такие данные:

```json
{
    "userId": "12345"
}
```

* **`userId`** — идентификатор пользователя (обязательное поле), полученный от системы клиента на этапе авторизации

#### Ответ

```json
{
  "stats": [
    {
      "title": "Бонус (руб)",
      "value": 4250
    },
    {
      "title": "Кол-во приглашенных друзей",
      "value": 2
    }
  ]
}
```

**`stats`** - список статистики

* **`title`**  - название для раздела статистики
* **`value`** - значение

{% hint style="info" %}
Следует помнить, что этот запрос будет приходить из нашего доверенного, [авторизованного](broken-reference) сервера; это — не публичный API.
{% endhint %}

Любой другой ответ API будет расцениваться как отсутствие истории уведомлений.
