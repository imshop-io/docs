---
icon: circle-question
---

# Общая информация о подключении интеграций

Многие функции мобильного приложения доступны для интеграции с информационными системами магазина посредством HTTP-запросов. Некоторые запросы будут отправляться системами IMSHOP.IO по мере необходимости использую протокол обмена IMSHOP Retail Protocol.

{% hint style="info" %}
**IMSHOP Retail Protocol** **(IRP)** - протокол обмена данными, разработанный в IMSHOP для обмена данными между IMSHOP и системами ритейлера (включая веб-сайт, CRM, OMS, WMS и прочие программные комплексы).
{% endhint %}

{% hint style="danger" %}
Запросы в рамках IRP протокола используют передачу данных в формате JSON поверх стандартных HTTP запросов. Все запросы используют метод POST, если в документации не указано обратное.
{% endhint %}

{% hint style="danger" %}
IMSHOP Retail Protocol является объектом интеллектуальной собственности ООО «АЙ ЭМ СОЛЮШНЗ» (IMSHOP) и защищён как объект авторского права. Свидетельство о депонировании произведения № 023-014461 от 16 января 2023 г. подтверждает исключительные права ООО «АЙ ЭМ СОЛЮШНЗ» на данные технологии.

IMSHOP Retail Protocol создан по заказу ООО «АЙ ЭМ СОЛЮШНЗ». Использование IMSHOP Retail Protocol допустимо только при взаимодействии с ООО "АЙ ЭМ СОЛЮШНЗ" и наличии действующего лицензионного договора. Более подробно можно ознакомиться [здесь](../api-license.md).
{% endhint %}

## Подключение

Для подключения вам необходимо связаться с вашим личным менеджером в IMSHOP.IO и:

* Запросить ключ API.
* Для всех IRP ендпоинтов, которые вы будете реализовывать на вашей стороне, передать список URL-адресов, по которым они будут доступны.

{% hint style="info" %}
Если вы не уверены, какие вебхуки вам надо будет реализовать для решения ваших задач, обратитесь к вашему личному менеджеру, и вы получите подробную консультацию.
{% endhint %}

## Авторизация API

При каждом запросе требуется передача API ключа (как для API так и для webhooks). Ключ можно передавать либо в поле **`key`** в  headers JSON  запроса, либо в HTTP заголовке в виде Bearer токена (например **`Authorization: Bearer your_key_goes_here`**)

{% hint style="warning" %}
Все URL обязательно должны поддерживать HTTPS и иметь корректный SSL-сертификат
{% endhint %}
