# Universal ссылки

Universal ссылки позволяют при переходе по обычной ссылке на сайт открывать товар сразу в приложении, если оно установлено.

Universal links работают в мессенджерах \(whatsapp, telegram, facebook, vk, imessage\), SMS и даже в браузере и поисковой выдаче. Например, если ваш покупатель найдет товар в Google, то при нажатии на ссылку в выдаче откроется сразу товар в приложении. Если приложении не установлено, то откроется вебсайт в обычном режиме со смарт-баннером на установку приложения

## Установка

### Передайте ссылки на товары в фиде

В товарном YML-фиде должны быть переданы корректные ссылки на товары внутри тега `<url>` 

Ссылки не должны содержать лишних GET  / query параметров \(например недопустимо передавать utm метки, идентификаторы сессий итд в фиде\).

### Загрузите файлы подтверждения на сайт

#### iOS

* Получите у вашего менеджера в IMSHOP.IO идентификатор приложения для Universal ссылок \(appID\)
* В следующем шаблоне замените appID, на полученный от менеджера IMSHOP.IO и сделайте этот файл доступным по адресу https://www.вашсайт.ru/.well-known/apple-app-site-association

```javascript
{
  "applinks": {
    "apps": [],
    "details": [
      {
        "appID": "XXXXXXXXXX.ru.yourapp.ios",
        "paths": [
          "*"
        ]
      }
    ]
  }
}
```

#### Android

* Получите у вашего менеджера в IMSHOP.IO идентификатор android приложения для universal links \(package\_name\) и sha256 подпись \(sha256\_cert\_fingerprints\)
* В следующем шаблоне замените package\_name и sha256\_cert\_fingerprints, на полученные от менеджера IMSHOP.IO и сделайте этот файл доступным по адресу https://www.вашсайт.ru/.well-known/assetlinks.json

  ```javascript
  [{
    "relation": ["delegate_permission/common.handle_all_urls"],
    "target": {
      "namespace": "android_app",
      "package_name": "ru.yourapp.android",
      "sha256_cert_fingerprints":
      ["00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00"]
    }
  }]
  ```

{% hint style="warning" %}
Внимание! файлы обязательно должны быть доступны именно по следующим URL, другие URL не поддерживаются iOS / Android

iOS: https://www.вашсайт.ru/.well-known/apple-app-site-association

Android: https://www.вашсайт.ru/.well-known/assetlinks.json
{% endhint %}

