---
title: Независимая публикация
ms.prod: xamarin
ms.assetid: 6FB4DEF2-01AD-C5FE-0950-CE1BF088A9C6
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/21/2017
ms.openlocfilehash: 6d278f3ae046a31be6e4335119572fb509672a66
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="publishing-independently"></a>Независимая публикация

Приложение можно опубликовать, не обращаясь в существующие Магазины Android. В этом разделе рассматриваются альтернативные методы публикации и уровни лицензирования Xamarin.Android.


## <a name="xamarin-licensing"></a>Лицензирование Xamarin

Для разработки, развертывания и распространения приложений Xamarin.Android доступны четыре лицензии:

-   **Visual Studio Community** &ndash; для учащихся, небольших команд и разработчиков OSS, использующих Windows.

-   **Visual Studio Professional** &ndash; для индивидуальных разработчиков или небольших команд (только для Windows). Эта лицензия предлагает стандартную подписку или подписку на облачную службу, доступ к дополнительным материалам Xamarin University и не накладывает ограничения на использование.

-   **Visual Studio Enterprise** &ndash; для команд любого размера (только для Windows). Эта лицензия предлагает возможности уровня предприятия, стандартную подписку или подписку на облачную службу и скидку 25 % на Xamarin Test Cloud.

Посетите веб-сайт [visualstudio.com](https://www.visualstudio.com/xamarin/), чтобы скачать Community Edition или получить дополнительные сведения о приобретении выпусков Professional и Enterprise.


## <a name="allow-installation-from-unknown-sources"></a>Разрешение установки из неизвестных источников

По умолчанию Android запрещает пользователям скачивать и устанавливать приложения из расположений, отличных от Google Play. Чтобы разрешить установку не из Marketplace, перед установкой приложения пользователь должен выбрать на устройстве параметр *Неизвестные источники*. Он находится в разделе **Параметры > Безопасность**, как показано на следующем изображении:

[![Экран параметров безопасности](publishing-independently-images/settings.png)](publishing-independently-images/settings.png#lightbox)


> [!IMPORTANT]
> Некоторые поставщики сети могут запрещать установку приложений из неизвестных источников независимо от этого параметра.



## <a name="publishing-by-e-mail"></a>Публикация по электронной почте

Вложение пакета APK для выпуска в сообщение электронной почты является быстрым и простым способом распространения приложения пользователям. Когда пользователь открывает сообщение на устройстве на платформе Android, Android распознает вложение APK и отображает кнопку **Установить**, как показано на следующем изображении:

[![Кнопка "Установить" для вложения](publishing-independently-images/publishing-via-email.png)](publishing-independently-images/publishing-via-email.png#lightbox)

Несмотря на простоту, распространение по электронной почте располагает незначительным количеством механизмов защиты от пиратства или несанкционированного распространения. Этот вариант лучше всего подходит для небольших групп получателей приложения, которые не будут распространять приложение самостоятельно.


## <a name="publishing-by-web"></a>Публикация через Интернет

Приложения можно распространять через веб-сервер. Для этого нужно отправить приложение на веб-сервер, а затем предоставить пользователям ссылку для скачивания. Когда пользователь устройства на платформе Android переходит по ссылке, а затем скачивает приложение, оно устанавливается автоматически.


## <a name="manually-installing-an-apk"></a>Установка пакета APK вручную

Установка вручную является третьим вариантом установки приложений. Далее приводятся действия по установке приложения вручную:

1.   **Распространение копии пакета APK пользователю** &ndash; Например, эта копия может распространяться на компакт-диске или USB-устройстве флэш-памяти.
1.   **(Пользователь) устанавливает приложение на устройство Android** &ndash; с помощью средства командной строки *Android Debug Bridge* (**adb**). **adb** — это универсальное средство командной строки для взаимодействия с экземпляром эмулятора или устройства на платформе Android. **adb** входит в состав пакета SDK для Android и находится в каталоге **<sdk>/platform-tools/**.

Устройство Android должно быть подключено к компьютеру с помощью USB-кабеля.
Чтобы средство **adb** распознавало компьютеры Windows, для них могут потребоваться дополнительные драйверы USB от производителя телефонов. Инструкции по установке этих дополнительных драйверов USB выходят за рамки настоящего документа.

Перед выполнением команд **adb** нужно знать, какие экземпляры эмулятора или устройства подключены (если таковые имеются). Список подключенных устройств можно просмотреть с помощью команды `devices`, как показано в следующем фрагменте:

```shell
$ adb devices
List of devices attached
        0149B2EC03012005device
```

После подтверждения подключенных устройств можно установить приложение, выполнив команду `install` с **adb**:

```shell
$ adb install <path-to-apk>
```

Следующий фрагмент является примером установки приложения на подключенное устройство.

```shell
$ adb install helloworld.apk
3772 KB/s (3013594 bytes in 0.780s)
        pkg: /data/local/tmp/helloworld.apk
Success
```

Если приложение уже установлено, `adb install` не сможет установить пакет APK и сообщит об ошибке, как показано в следующем примере:

```shell
$ adb install helloworld.apk
4037 KB/s (3013594 bytes in 0.728s)
        pkg: /data/local/tmp/helloworld.apk
Failure [INSTALL_FAILED_ALREADY_EXISTS]
```

Потребуется удалить приложение с устройства. Сначала выполните команду `adb uninstall`:

```shell
adb uninstall <package_name>
```

Во фрагменте ниже приведен пример удаления приложения:

```shell
$ adb uninstall mono.samples.helloworld
Success
```
