---
title: PassKit
description: Бумажника представляет собой систему iOS приложение хранит и отображает штрих-код и другие сведения для связи клиента транзакции на свой телефон с реальной жизни.
ms.prod: xamarin
ms.assetid: 74B9973B-C1E8-B727-3F6D-59C1F98BAB3A
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/20/2017
ms.openlocfilehash: f1c8ac92c5ff7eed5116587ed13755ddee74a877
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="passkit"></a>PassKit

_Бумажника представляет собой систему iOS приложение хранит и отображает штрих-код и другие сведения для связи клиента транзакции на свой телефон с реальной жизни._

Бумажника — это приложение для iPhone и iPod соприкасается с iOS 6. Он хранит и отображает штрих-код и другие сведения для связи клиента транзакции на свой телефон с реальной жизни. Передает создаются путем предпринимателей и отправки клиентам по электронной почте, URL-адреса или в корпорации Майкрософт собственные приложения iOS. Бумажника хранит и организует всех этапах на телефоне и отображает напоминания проход на экране блокировки в зависимости от даты и времени или местоположение устройства.

В этом документе представлены бумажника, с помощью API передачи пакета с помощью Xamarin.iOS и описывается реализация передает на сервере.

 [![](passkit-images/image1.png "Бумажника хранит и организует всех этапах на телефон")](passkit-images/image1.png#lightbox)


## <a name="requirements"></a>Требования

Набор магазина возможности, рассматриваемые в этом документе требуется iOS 6 и Xcode 4.5, а также Xamarin.iOS 6.0.


## <a name="introduction"></a>Вступление

Проблема ключа, решающего передать пакет является распространения и управления штрихкоды. Некоторые примеры реальных как штрихкоды в настоящее время используются:

-   **Приобретение через Интернет билетов фильма** — клиентов обычно уведомления по электронной почте штрих-код, представляющий их билетов. Этот штрихкод печатается и уделить кинофильмов сканирования для записи.
-   **Баллов** — клиентов содержат ряд различных карт конкретного хранилища в их бумажника или кошелек, для отображения и просмотра при совершении покупки товаров.
-   **Купоны** — купоны распространяются по электронной почте, как печати веб-страницы, через letterboxes и как штрихкодов в газеты и журналы. Клиенты их подключением к хранилищу для сканирования, для получения товаров, службы или скидки в ответ.
-   **Посадке передает** — аналогично приобретения билета фильма.


Комплект средств для этапа является альтернативной для каждого из этих сценариев:

-   **Билеты фильма** — после покупки, клиент добавляет проход билет событий (с помощью электронной почты или ссылки веб-сайта). Время для фильма подходы выполнение этапа, автоматически отобразятся на экране блокировки для напоминания, а при поступлении на кинофильмов проход легко извлекается и отображается в бумажника для сканирования.
-   **Баллов** — вместо (или в дополнение к) предоставление физических карт, хранилища может выдавать (по электронной почте или после входа веб-сайта) передаче карты хранилища. Хранилище можно предоставить дополнительные возможности, такие как обновление баланса счета при проходе через push-уведомления и с помощью служб geolocation проход может автоматически отображаются на экране блокировки когда клиент превышает это расположение хранилища.
-   **Купоны** — передает купона может легко создавать с уникальными характеристиками, чтобы помочь при отслеживании и распространяются с помощью ссылки по электронной почте или веб-сайта. Загруженный купоны автоматически могут отображаться на экране блокировки, если пользователь находится рядом с определенным элементом и/или в определенную дату (например, если приближается Дата окончания срока действия). Поскольку купоны хранятся на телефон пользователя, они всегда под рукой и не потерян. Купоны может предлагать клиентам скачать дополнительное приложений, поскольку ссылки на магазин приложений могут быть включены в проходе, увеличение взаимодействия с клиентом.
-   **Посадке передает** — после возврата процесс в сети, клиент получит их адаптации проход по электронной почте или ссылку. Вспомогательное приложение, предоставляемых поставщиком транспорта может включать в процессе возврата и также позволяют клиенту для выполнения дополнительных функций, таких как выбор своих рабочих мест или обед. Поставщик транспорта можно использовать push-уведомлений для обновления на этапе, если транспорт отложено или отменено. Посадки времени подходов этот этап будет отображаться на экране блокировки для напоминания и для обеспечения быстрого доступа для передачи.


По существу передать пакет содержит простой и удобный способ хранения и отображения штрих-кодов на устройстве iPhone или iPod touch. С экрана блокировки интеграция расположение и дополнительное время push-уведомлений и сопутствующих образцах приложений интегрировать предоставляет основу для очень сложных продажи билетов и выставления счетов службы.


## <a name="pass-kit-ecosystem"></a>Передайте экосистема Kit

Комплект средств для этапа не интерфейс API в пределах CocoaTouch, вместо этого он является частью большего экосистема приложений, данных и служб, предназначенных для упрощения безопасного совместного использования и управления штрих-кодов и другие данные. Этой верхнего уровня диаграмме показаны различные сущности, которые могут принимать участие в создании и использовании передает.

 [![](passkit-images/image2.png "Эта диаграмма верхнего уровня изображены сущностей в создании и использовании передает")](passkit-images/image2.png#lightbox)

Каждый фрагмент экосистемы имеет четко определенные роли:

-   **Бумажника** — Apple iOS встроенные приложения (для iPhone и iPod touch), хранит и отображает передает. Это единственное место, передает подготавливаются к просмотру для использования в реальном мире (ie штрихкод отображается, вместе с локализованные данные при прохождении).
-   **Приложения-компаньон** — приложений iOS 6, созданных поставщиками проход для расширения функциональности передает, выдачи, таких как добавление значения в карте магазина, изменение место в передаче посадки или других функций конкретного бизнеса. Помощник по поиску приложения не требуются для проход для использования.
-   **Сервер** — защищенный сервер, где передает могут возникать и подписи для распространения. Помощник по поиску приложения могут подключиться к серверу для создания нового передает или обновления существующих передает запрос. При необходимости может использовать API веб-службы, который бумажника нужно вызвать, чтобы обновить передает.
-   **Серверы APNS** — сервер имеет возможность уведомлять бумажника обновлений для передачи на данном устройстве с помощью APNS. Отправьте уведомление бумажника, который затем будет связаться с сервером для сведения об изменении. Помощник по поиску приложений необходимо реализовать APNS для этой функции (они могут прослушивать `PKPassLibraryDidChangeNotification` ).
-   **Каналом приложения** — приложения, не работают непосредственно передает (как и помощник по поиску приложений), но что может повысить свои программы, распознает передает и позволяет добавить бумажника. Почтовые клиенты, браузеры социальных сетей и других приложениях статистической обработки данных все возникающие вложения или ссылки на этапах.


Целая экосистема выглядит сложным, так стоит отметить, что некоторые компоненты являются необязательными, и гораздо проще передать комплект средств для реализации возможны.

## <a name="what-is-a-pass"></a>Что такое атака Pass?

Передача — это совокупность данных, представляющих билет, купона или карты. Может быть предназначен для однократного использования отдельное (и поэтому содержат сведения, например рейса номер и место размещения), или это может быть несколько использование маркера, который может использоваться совместно с любым числом пользователей (например, купона скидки). Подробное описание доступных в компании Apple [о передаче файлов](https://developer.apple.com/library/prerelease/ios/#documentation/UserExperience/Reference/PassKit_Bundle/Chapters/Introduction.html) документа.


### <a name="types"></a>Типы

В настоящее время пять поддерживаемых типов, которые можно классифицировать в приложении бумажника макет и верхней границе этапа:

-  **Событие билет** — небольшой Полукруглая обрезки.
-   **Передайте адаптации** — можно указать деления значок параллельно, относящуюся к транспорту (например) шины, обучение, "в самолете").
-   **Хранить карты** — скругленными сверху, например кредитной или дебетовой карт.
-  **Купона** — перфорированной вдоль верхней.
-  **Универсальный** — то же, что хранилище карты, закругленной вершиной.


На этом снимке экрана показаны проход пять типов (в порядке: хранения купона, generic, карт, передайте посадки и событие билета):

 [![](passkit-images/image3.png "На этом снимке экрана показаны проход пять типов")](passkit-images/image3.png#lightbox)

### <a name="file-structure"></a>Структура файла

Передайте файл является фактически ZIP-архив с **.pkpass** расширение, содержащее некоторые определенные файлы JSON (обязательно), различные изображения файлы (необязательно) и локализованные строки (обязательно).

-   **PASS.JSON** — требуется. Содержит все сведения для прохода.
-   **manifest.JSON** — требуется. Содержит хэш SHA1 для каждого файла в этап за исключением файл сигнатур и этот файл (manifest.json).
-   **подпись** — требуется. Созданные подписи `manifest.json` файла с помощью сертификата, созданного в портале подготовки iOS.
-  **Logo.PNG** — необязательно.
-  **Background.PNG** — необязательно.
-  **icon.PNG** — необязательно.
-  **Файлы локализуемые строки** — необязательно.


Ниже приведен файл проход структуры каталогов (это содержимое ZIP-архив):

 [![](passkit-images/image4.png "Здесь отображается структура каталогов файл pass")](passkit-images/image4.png#lightbox)

### <a name="passjson"></a>PASS.JSON

JSON является форматом, поскольку передает обычно создаются на сервере — это означает, что код создания зависящий от платформы на сервере. Ниже приведены три основных элемента информации при каждом проходе.

-   **teamIdentifier** — это связывает все этапы создания для учетной записи магазина приложений. Это значение отображается в портал Провизионирования iOS.
-   **passTypeIdentifier** — регистрация на портале подготовки группу передает друг с другом (если создать несколько типов). Например на примере кафе создать хранилище передать карточками позволяет клиентам получить лояльности кредиты, но отдельный купона передать тип для создания и распространения купоны скидки. Этот же кафе даже может хранить события динамической Музыка и выдачи билетов передает события для тех.
-   **серийный номер** — уникальную строку в это `passTypeidentifier` . Значение является непрозрачным для бумажника, но важна для отслеживания конкретных проходах при обмене данными с сервером.


Имеется большое количество других ключей JSON в каждом проходе, пример которых показан ниже:

``` 
{
   "passTypeIdentifier":"com.xamarin.passkitdoc.banana",  //Type Identifier (iOS Provisioning Portal)
   "formatVersion":1,                                     //Always 1 (for now)
   "organizationName":"Xamarin",                          //The name which appears on push notifications
   "serialNumber":"12345436XYZ",                          //A number for you to identify this pass
   "teamIdentifier":"XXXAAA1234",                         //Your Team ID
   "description":"Xamarin Demo",                          //
   "foregroundColor":"rgb(54,80,255)",                    //color of the data text (note the syntax)
   "backgroundColor":"rgb(209,255,247)",                  //color of the background
   "labelColor":"rgb(255,15,15)",                         //color of label text and icons
   "logoText":"Banana ",                                  //Text that appears next to logo on top
   "barcode":{                                            //Specification of the barcode (optional)
      "format":"PKBarcodeFormatQR",                       //Format can be QR, Text, Aztec, PDF417
      "message":"FREE-BANANA",                            //What to encode in barcode
      "messageEncoding":"iso-8859-1"                      //Encoding of the message
   },
   "relevantDate":"2012-09-15T15:15Z",                    //When to show pass on screen. ISO8601 formatted.
  /* The following fields are specific to which type of pass. The name of this object specifies the type, e.g., boardingPass below implies this is a boarding pass. Other options include storeCard, generic, coupon, and eventTicket */
   "boardingPass":{
/*headerFields, primaryFields, secondaryFields, and auxiliaryFields are arrays of field object. Each field has a key, label, and value*/
      "headerFields":[          //Header fields appear next to logoText
         {
            "key":"h1-label",   //Must be unique. Used by iOS apps to get the data.
            "label":"H1-label", //Label of the field
            "value":"H1"        //The actual data in the field
         },
         {
            "key":"h2-label",
            "label":"H2-label",
            "value":"H2"
         }
      ],
      "primaryFields":[       //Appearance differs based on pass type
         {
            "key":"p1-label",
            "label":"P1-label",
            "value":"P1"
         }
      ],
      "secondaryFields":[     //Typically appear below primaryFields
         {
            "key":"s1-label",
            "label":"S1-label",
            "value":"S1"
         }
      ],
      "auxiliaryFields":[    //Appear below secondary fields
         {
            "key":"a1-label",
            "label":"A1-label",
            "value":"A1"
         }
      ],
      "transitType":"PKTransitTypeAir"  //Only present in boradingPass type. Value can
                                        //Air, Bus, Boat, or Train. Impacts the picture
                                        //that shows in the middle of the pass.
   }
}
```

### <a name="barcodes"></a>Штрих-кодов

Поддерживаются только 2D форматы: PDF417, Aztec, QR. Apple утверждений, непригодна для сканирования на экране телефона подсветкой 1D штрихкоды.

Текст, отображаемый под ним необязателен – некоторые продавцы нужно иметь возможность чтения или тип вручную.

Кодировка ISO-8859-1 — наиболее распространенные проверка, какая кодировка используется сканирования системами, которые будут читать ваш передает.

### <a name="relevancy-lock-screen"></a>Релевантность (блокировка экрана)

Существует два типа данных, которая может привести к передаче, который будет отображаться на экране блокировки.

 **Расположение**

Проход, например хранилищ, которые часто посещает клиента или расположение кинофильмов или аэропорта, можно указать до 10 расположений. Клиент может задать эти расположения через вспомогательное приложение или поставщик может определить их по данным об использовании (если собираются с разрешением клиента).

При отображении на экране блокировки проход барьер вычисляется, когда он покидает область проход скрыта от на экран блокировки. Радиус привязывается к передаче стиля для предотвращения нарушений.

 **Дата и время**

В передаче можно указать только один даты и времени. Дата и время полезен для запуска экрана блокировки напоминания о посадки передает и билеты событий.

Можно обновить путем принудительной или с помощью PassKit API, чтобы дата и время, которые могут быть обновлены в случае билет многократного использования (например билет сезона режиме театра или спортивных сложным).

### <a name="localization"></a>Локализация

Перевод передаче на несколько языков аналогична локализация приложения iOS: создание языка определенные каталоги с `.lproj` расширения и поместите локализованные элементы внутри. Переводы текст должны вводиться в `pass.strings` файл, пока локализованного изображения должен иметь имя, совпадающее с именем образа, они заменяют в корне проход.

## <a name="security"></a>Безопасность

Передает подписанным сертификатом закрытого, которые созданы в портал Провизионирования iOS. Для входа на этапе необходимо:

1.  Вычислить хэш SHA1 для каждого файла в каталоге проход (не включайте `manifest.json` или `signature` файл, ни один из которых должны существовать все равно на этом этапе).
1.  Запись `manifest.json` как список ключей и значений JSON имени каждого файла с ее хэш-код.
1.  Использовать сертификат для подписи `manifest.json` файла и запись в файл с именем результат `signature` .
1.  АРХИВИРОВАТЬ все данные и предоставьте полученный файл `.pkpass` расширение имени файла.


Поскольку ваш закрытый ключ необходим для входа на этапе, этот процесс должно использоваться только на защищенном сервере, которым вы управляете. НЕ распространяйте ключи может попытаться создать передает в приложение.

 
## <a name="configuration-and-setup"></a>Установка и настройка

Этот раздел содержит инструкции для установки сведений о своей подготовки и создания вашего первого этапа.

### <a name="provisioning-passkit"></a>Подготовка PassKit

Чтобы передать в магазине приложений введите он должен быть связан с учетной записью разработчика. Это в два этапа:

1.  Этот этап должен быть зарегистрирован с помощью уникальный идентификатор, называемый идентификатор передачи типа
1.  Действительный сертификат должен быть создан для входа на этапе цифровой подписью для разработчиков.

Создание передать идентификатор типа do следующее.


<a name="create-passid"/>

#### <a name="create-a-pass-type-id"></a>Создать идентификатор типа Pass

Первым шагом является настройка передать идентификатор типа для каждая новая _тип_ этапа для поддержки. Передайте идентификатор (или идентификатор типа передачи) создает уникальный идентификатор этапа. Мы будем использовать этот идентификатор для связи с учетной записью разработчика, с помощью сертификата на передачи.

1. В [сертификаты, идентификаторы и профили раздел портал Провизионирования iOS](https://developer.apple.com/account/overview.action), перейдите к **идентификаторы** и выберите **передать идентификаторы типов** . Выберите **+** кнопку, чтобы создать новый тип этапа: [ ![ ] (passkit-images/passid.png "Создание типа pass")](passkit-images/passid.png#lightbox)

2.   Укажите **описание** (имя) и **идентификатор** (уникальная строка) для прохода. Обратите внимание, что все идентификаторы типов для передачи должна начинаться со строки `pass.` в этом примере мы используем `pass.com.xamarin.coupon.banana` : [ ![ ] (passkit-images/register.png "указать описание и идентификатор")](passkit-images/register.png#lightbox)


3.   Подтвердите ИД передачи, нажав клавишу **зарегистрировать** кнопки.


<a name="generate" />

#### <a name="generate-a-certificate"></a>Создание сертификата

Чтобы создать новый сертификат для этого передайте идентификатор типа, выполните следующие действия.

1.  Выберите только что созданный идентификатор передать из списка и нажмите кнопку **изменить** : [ ![ ] (passkit-images/pass-done.png "выберите новый идентификатор передать из списка")](passkit-images/pass-done.png#lightbox)

    Выберите **Создание сертификата...** :

    [![](passkit-images/cert-dist.png "Выберите Создание сертификата")](passkit-images/cert-dist.png#lightbox)


2.  Выполните шаги для создания подписи сертификата запроса (CSR).
  
3. Нажмите клавишу **Продолжить** кнопку на портале разработчиков и отправьте CSR создать сертификат.

4. Загрузите сертификат и дважды щелкните ее, чтобы установить его в цепочке ключей.


Теперь, когда мы создали сертификат для этого передайте идентификатор типа, в следующем разделе описывается, как построить обходной вручную.

Дополнительные сведения о подготовке для бумажника посвящены [работа с возможностями](~/ios/deploy-test/provisioning/capabilities/wallet-capabilities.md) руководства.

 <a name="Create_a_Pass_Manually" />

### <a name="create-a-pass-manually"></a>Создать транзитный вручную

Теперь, когда мы создали передать тип, можно вручную создать проход для тестирования на устройстве или симуляторе. Чтобы создать транзитный, необходимо:

-  Создайте каталог для хранения файлов проход.
-  Создайте файл pass.json, содержащий все требуемые данные.
-  Включайте изображения в папку (если это необходимо).
-  Вычислите хэш SHA1 для каждого файла в папке, а запись manifest.json.
-  Manifest.json входа с файлом .p12 загруженный сертификат.
-  ZIP-архив содержимое каталога и переименовать с .pkpass расширения.


В образце кода для данной статьи, который может использоваться для создания передаче существуют некоторые исходные файлы. Использовать файлы в `CouponBanana.raw` каталог CreateAPassManually каталога. Имеются следующие файлы:

 [![](passkit-images/image18.png "Эти файлы присутствуют")](passkit-images/image18.png#lightbox)

Pass.json открывать и редактировать JSON. По крайней мере, необходимо обновить `passTypeIdentifier` и `teamIdentifer` для сопоставления учетной записи разработчика Apple.

```csharp
"passTypeIdentifier" : "pass.com.xamarin.coupon.banana",
"teamIdentifier" : "?????????",
```

Затем необходимо вычислить хэш-коды для каждого файла и создать `manifest.json` файла. Он будет выглядеть примерно следующим образом после завершения:

```csharp
{
  "icon@2x.png" : "30806547dcc6ee084a90210e2dc042d5d7d92a41",
  "icon.png" : "87e9ffb203beb2cce5de76113f8e9503aeab6ecc",
  "pass.json" : "c83cd1441c17ecc6c5911bae530d54500f57d9eb",
  "logo.png" : "b3cd8a488b0674ef4e7d941d5edbb4b5b0e6823f",
  "logo@2x.png" : "3ccd214765507f9eab7244acc54cc4ac733baf87"
}
```

Далее подписи должен быть создан для этого файла с использованием сертификата (.p12-файл), созданный для данного этапа тип удостоверения.

 <a name="Signing_On_a_Mac" />


#### <a name="signing-on-a-mac"></a>Подписи на компьютере Mac

Загрузить **материалов бумажника начальное значение** из [загружает Apple](https://developer.apple.com/downloads/index.action?name=Passbook) сайта. Используйте `signpass` средство для преобразования папки в передаче (это также определит SHA1 хэширует и почтовый индекс выходные данные в файл .pkpass).

 <a name="Signing_On_a_PC" />


#### <a name="signing-on-a-pc"></a>Подписи на клиентском Компьютере

В примере кода для данной статьи существует — проект с именем `signpassnet` , работающий в .NET в Windows. Предпринимается попытка имитировать средство Apple, однако он включает существенно меньшим объемом кода проверки.

 <a name="Testing" />


#### <a name="testing"></a>Тестирование

Если для проверки выходные данные этих средств (Задание имени файла на ZIP и откройте его), которые появляются следующие файлы (Обратите внимание, добавление `manifest.json` и `signature` файлов):

 [![](passkit-images/image19.png "Анализ результатов этих средств")](passkit-images/image19.png#lightbox)

После подписи ZIPped и переименовать файл (например) Чтобы `BananaCoupon.pkpass`) можно перетащить его в симулятор для тестирования или отправить по электронной почте самому себе, чтобы получить на физическом устройстве. Вы увидите экран для **Add** pass, следующим образом:

 [![](passkit-images/image20.png "Добавить экран pass")](passkit-images/image20.png#lightbox)

Обычно этот процесс будет выполняться автоматически на сервере, однако вручную этап создания может быть параметр для малого бизнеса, которые создаются только купоны не требуется поддержка внутреннего сервера.

 <a name="Wallet" />

## <a name="wallet"></a>Wallet

Бумажника является центральной экосистемы передачи пакета. На этом снимке экрана демонстрирует пустой бумажника и внешний вид списка проход и отдельных этапов:

 [![](passkit-images/image21.png "На этом снимке экрана показано пустой бумажника и внешний вид списка проход и отдельных этапов")](passkit-images/image21.png#lightbox)

Функции бумажника:

-  Он является единственным местом, передает подготавливаются к просмотру с их штрих-код для сканирования.
-  Пользователь может изменить параметры для обновлений. Если параметр включен, push-уведомлений можно запускать обновления данных при передаче.
-  Пользователя можно включить или отключить интеграцию с экрана блокировки. Если параметр включен, это позволяет проход автоматически отображаться на экранах блокировки на основе соответствующие время и место данных внедренных в этот этап.
-  Обратной стороне этапа поддерживает запросу на обновление, если веб сервер-URL-адрес предоставляется в JSON передачи.
-  Помощник по поиску приложений можно открыть (или загрузить) при в JSON передать идентификатор приложения.
-  Передает могут быть удалены (с забавны физическое уничтожение анимации).


 <a name="Getting_Passes_into_Wallet" />

## <a name="adding-passes-into-wallet"></a>Добавление передает в бумажника

Передает добавляемыми бумажника одним из следующих способов:

* **Каналом приложения** — они не передает напрямую управлять, они просто загрузить файлы проход и предоставить пользователю возможность добавить их бумажника. 

* **Приложения-компаньон** — они записываются поставщиками для распространения передает и обеспечивают дополнительные функциональные возможности можно просматривать или редактировать их. Приложения Xamarin.iOS имеют полный доступ к API передачи комплект средств для создания и управления передает. Передает, можно добавить с помощью бумажника `PKAddPassesViewController`. Этот процесс описан более подробно в **приложений дополнительное** раздел этого документа.

### <a name="conduit-applications"></a>Каналом приложений

Приложения, каналом, промежуточного приложения, которые могут получать передает от имени пользователя и должны программироваться для распознавания типу содержимого и предоставляют функциональность добавления бумажника. Примеры приложений каналом.

-   **Mail** — распознает вложения в качестве передаче.
-   **Safari** — распознает передать тип содержимого при щелчке ссылки передать URL-адрес.
-   **Другие настраиваемые приложения** — любое приложение, получение вложениями или открытие ссылок (социальных сетей клиентов, средства чтения почты, и т. д).


На этом снимке экрана показано, как **Mail** в iOS 6 распознает вложения проход и (если затронутых) предлагает **добавить** его бумажника.

 [![](passkit-images/image22.png "На этом снимке экрана показано, как письма в iOS 6 распознает вложения Pass")](passkit-images/image22.png#lightbox)

 [![](passkit-images/image23.png "На этом снимке экрана показано, как почта предлагается добавить вложение проход для бумажника")](passkit-images/image23.png#lightbox)

При построении приложения, которое может быть каналом для передает их можно распознать.

-  **Расширение файла** -.pkpass
-  **Тип MIME** -application/vnd.apple.pkpass
-  **UTI** — com.apple.pkpass


Основные операции каналом приложения является получение передайте файл вызова передать пакет `PKAddPassesViewController` дать пользователю возможность добавить к этапу их бумажника. Реализация этого контроллера представления рассматривается в следующем разделе на **приложений дополнительное**.

Каналом приложения не обязательно должно быть подготовлено для конкретных передать идентификатор типа таким же образом, сопровождающий приложения.

## <a name="companion-applications"></a>Помощник по поиску приложений

Вспомогательное приложение предоставляет дополнительные функциональные возможности для работы с прохода, включая создание передаче, обновление сведений, связанных с передаче и других аспектов управления передает связанные с приложением.

Помощник по поиску приложения не должны пытаться функции бумажника. Они не предназначены для отображения проходов для сканирования.

В остальной части этого раздела описывает, как создать простое дополнительное приложение, взаимодействующее с набором для передачи.

### <a name="provisioning"></a>Подготовка

Поскольку бумажника технологии хранилища, приложение должно быть подготовлено отдельно и не могут использовать профиль подготовки команды или идентификатор шаблоны приложений. Ссылаться на [работа с возможностями](~/ios/deploy-test/provisioning/capabilities/wallet-capabilities.md) руководство для создания приложения бумажника уникальный идентификатор приложения и профиль подготовки.

### <a name="entitlements"></a>Объемы обслуживания

**Entitlements.plist** файла должны быть включены в проект все последние Xamarin.iOS. Чтобы добавить новый файл Entitlements.plist, выполните действия, описанные в [работа с данными](~/ios/deploy-test/provisioning/entitlements.md) руководства.

Чтобы задать права выполните следующие действия:

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

Дважды щелкните **Entitlements.plist** файл в решение прокладки, чтобы открыть редактор Entitlements.plist:

![](passkit-images/image31.png "Редактор Entitlements.plst")

В разделе бумажника выберите **включить бумажника** параметр

![](passkit-images/image32.png "Включить бумажника правах")


Значение по умолчанию — для вашего приложения разрешить все передачи типов. Тем не менее существует возможность ограничить приложения и допускают только подмножество типов проход team. Чтобы включить эту выберите **разрешить подмножества группы подстановки типов** и введите идентификатор типа pass подмножества, которые требуется разрешить.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Дважды щелкните **Entitlements.plist** файл, чтобы открыть исходный файл XML.

Чтобы добавить права бумажника, задайте **свойство** для `Passbook Identifiers` в раскрывающемся списке, который автоматически устанавливается **тип** `Array`. Затем задайте строку **значение** для `$(TeamIdentifierPrefix)*`:

![](passkit-images/image33.png "Включить бумажника правах")

Это позволит вашему приложение работать со всеми типами карт. Для ограничения приложения и допускают только подмножество проход типы групп, задайте значение строки:

`$(TeamIdentifierPrefix)pass.$(CFBundleIdentifier)`

Где `pass.$(CFBundleIdentifier)` передать идентификатор созданного [выше](~/ios/platform/passkit.md)

-----

### <a name="debugging"></a>Отладка

Если возникают проблемы с развертыванием приложения, проверьте, что вы используете правильный **профиль подготовки** и что `Entitlements.plist` выбран в качестве **пользовательские права** файла в **iPhone подписывание пакета** параметры.

Если возникают ошибки при развертывании.

```csharp
Installation failed: Your code signing/provisioning profiles are not correctly configured (error: 0xe8008016)
```

затем `pass-type-identifiers` неправильный прав массив (или не соответствует **профиль подготовки**). Проверьте правильность идентификаторов передать тип и идентификатор команды.

 <a name="Classes" />

## <a name="classes"></a>Классы

Следующие классы передачи пакета доступны для приложений для доступа к передает:

-  **PKPass** — экземпляр передаче.
-  **PKPassLibrary** — предоставляет API для доступа к передает на устройстве.
-  **PKAddPassesViewController** — используется для отображения прохода для пользователю сохранить в их бумажника.
-  **PKAddPassesViewControllerDelegate** — Xamarin.iOS разработчиков


## <a name="example"></a>Пример

Ссылаться на проект PassLibrary в образце кода для данной статьи. Он демонстрирует следующие общие функции, которые будут необходимы в приложении дополнительное бумажника:

### <a name="check-that-wallet-is-available"></a>Убедитесь, что бумажника доступно

Бумажника на iPad, недоступен, поэтому приложения должны проверять, прежде чем пытаться получить доступ к функциям передачи пакета.

```csharp
if (PKPassLibrary.IsAvailable) {
    // create an instance and do stuff...
}
```

### <a name="creating-a-pass-library-instance"></a>Создание экземпляра библиотеки Pass

Библиотека передать пакет не является Singleton-классом, приложения необходимо создать и хранить и экземпляр для доступа к API передачи пакета.

```csharp
if (PKPassLibrary.IsAvailable) {
    library = new PKPassLibrary ();
    // do stuff...
}
```

### <a name="get-a-list-of-passes"></a>Получить список этапов

Приложения могут запрашивать список передает из библиотеки. Этот список автоматически фильтруется по передать комплект средств для, чтобы будут отображаться только передает были созданы с помощью идентификатора команды и перечислены в прав.

```csharp
var passes = library.GetPasses ();  // returns PKPass[]
```

Обратите внимание, симулятор не фильтрации списка передает возвращен, поэтому этот метод следует всегда тестировать на реальном устройстве. Этот список может быть отображено в UITableView образец приложения выглядят следующим образом, после добавления двух купоны:

 [![](passkit-images/image29.png "Образец приложения вид, как в данном после добавления двух купонов")](passkit-images/image29.png#lightbox)


### <a name="displaying-passes"></a>Отображение передает

Для подготовки к просмотру передает в приложениях дополнительное доступен ограниченный набор информации.

Выберите из этого набора стандартных свойств для отображения списков пройден, как и в примере кода.

```csharp
string passInfo =
                "Desc:" + pass.LocalizedDescription
                + "\nOrg:" + pass.OrganizationName
                + "\nID:" + pass.PassTypeIdentifier
                + "\nDate:" + pass.RelevantDate
                + "\nWSUrl:" + pass.WebServiceUrl
                + "\n#" + pass.SerialNumber
                + "\nPassUrl:" + pass.PassUrl;
```

Эта строка отображается в виде предупреждения в образце:

 [![](passkit-images/image30.png "В образце предупреждения выбран купона")](passkit-images/image30.png#lightbox)

Можно также использовать `LocalizedValueForFieldKey()` метод для извлечения данных из поля этапов проектирования (так как вы будете знать, какие поля должны присутствовать). В примере кода это не отображается.

### <a name="loading-a-pass-from-a-file"></a>Загрузка передаче из файла

Поскольку передача могут добавляться только к бумажника с разрешениями пользователя, с помощью которых можно решить, должна быть представлена представление контроллер. Этот код используется в **добавить** кнопки в примере, для загрузки в передаче готовые, внедренных в приложение (необходимо заменить на тот, который вы выполнили):

```csharp
NSData nsdata;
using ( FileStream oStream = File.Open (newFilePath, FileMode.Open ) ) {
        nsdata = NSData.FromStream ( oStream );
}
var err = new NSError(new NSString("42"), -42);
var newPass = new PKPass(nsdata,out err);
var pkapvc = new PKAddPassesViewController(newPass);
NavigationController.PresentModalViewController (pkapvc, true);
```

Этот этап предоставляется **добавить** и **отменить** параметры:

 [![](passkit-images/image20.png "Передайте, выбрать один из режимов Установка и Отмена")](passkit-images/image20.png#lightbox)

### <a name="replace-an-existing-pass"></a>Замените существующий Pass

Замена существующего передать не требует разрешения пользователя, однако завершается ошибкой, если выполнение этапа еще не существует.

```csharp
if (library.Contains (newPass)) {
     library.Replace (newPass);
}
```

### <a name="editing-a-pass"></a>На этапе редактирования

PKPass не изменяемым, поэтому не удается обновить передайте объекты в коде. Для изменения данных в передаче, приложение должно иметь доступ к веб-сервера, можно хранить запись передает и создайте новый файл проход с обновленными значениями, которые можно загрузить приложение.

Этап создания файла необходимо сделать на сервере, поскольку передает должны быть подписаны сертификатом, который требуется обеспечить конфиденциальность и безопасность.

После создания передайте обновленный файл используйте `Replace` метод перезаписывает старые данные на устройстве.

### <a name="display-a-pass-for-scanning"></a>Отображать за проход для сканирования

Как уже отмечалось ранее, только бумажника можно отобразить успешного прохождения проверки. Передача может отображаться с использованием `OpenUrl` метода, как показано:

 `UIApplication.SharedApplication.OpenUrl (p.PassUrl);`

### <a name="receiving-notifications-of-changes"></a>Получение уведомлений об изменениях

Приложения могут прослушивать изменения, внесенные в библиотеку передать с помощью `PKPassLibraryDidChangeNotification`. Изменения может быть вызвано уведомления, активируя обновлений в фоновом режиме, поэтому рекомендуется для прослушивания их в приложении.

```csharp
noteCenter = NSNotificationCenter.DefaultCenter.AddObserver (PKPassLibrary.DidChangeNotification, (not) => {
    BeginInvokeOnMainThread (() => {
        new UIAlertView("Pass Library Changed", "Notification Received", null, "OK", null).Show();
        // refresh the list
        var passlist = library.GetPasses ();
        table.Source = new TableSource (passlist, library);
        table.ReloadData ();
    });
}, library);  // IMPORTANT: must pass the library in
```

Очень важно для передачи экземпляр библиотеки при регистрации для уведомления, так как PKPassLibrary не является Singleton-классом.

## <a name="server-processing"></a>Сервер обработки

Подробное рассмотрение построения серверного приложения для поддержки передачи пакета выходит за рамки данной статьи начального уровня.

Код .NET в *signpassnet* образец можно использовать в качестве основы для стороны сервера метод, который можно создать передает.

Представление [WWDC видео: введение в расчетной, часть 2](https://developer.apple.com/videos/wwdc/2012/?include=309#309) от 27: 00 минут для получения дополнительной информации.

### <a name="other-resources"></a>Другие источники

В разделе [dotnet расчетной](https://github.com/tomasmcguinness/dotnet-passbook) открыть серверный код исходного кода C#.

## <a name="push-notifications"></a>Push-уведомления

Подробное описание с помощью push-уведомлений для обновления передает выходит за рамки данной статьи начального уровня.

Будет необходимо реализовать в стиле REST API, определенный по Apple, чтобы реагировать на веб-запросы из бумажника установки обновлений. Код .NET в *signpassnet* образец можно использовать в качестве основы для создания нового передает в результате эти запросы.

Представление [WWDC видео: введение в расчетной, часть 2](https://developer.apple.com/videos/wwdc/2012/?include=309#309) от 27: 00 минут для получения дополнительной информации.

## <a name="summary"></a>Сводка

В этой статье появились передать пакет, описанные некоторые из причин, почему оно удобно и описано различных частей, которые должны быть реализованы для полнофункционального решения передачи пакета. Он описываются шаги, необходимые для настройки учетной записи разработчика Apple для создания этапы процесса, чтобы выполнить проход вручную, а также как получить доступ к API-интерфейсы комплект средств для передачи из приложения Xamarin.iOS.

## <a name="related-links"></a>Связанные ссылки

- [CreateAPassManually (пример)](https://developer.xamarin.com/samples/PassKit/)
- [Образец PassKit](https://developer.xamarin.com/samples/monotouch/PassKit/)
- [Введение в iOS 6](~/ios/platform/introduction-to-ios6/index.md)
- [Руководство по программированию расчетной](https://developer.apple.com/library/prerelease/ios/#documentation/UserExperience/Conceptual/PassKit_PG/Chapters/Introduction.html)
- [Расчетной для разработчиков](https://developer.apple.com/passbook/)
- [Сведения о файлах Pass](https://developer.apple.com/library/prerelease/ios/#documentation/UserExperience/Reference/PassKit_Bundle/Chapters/Introduction.html)
- [Передать ссылку Kit Framework](https://developer.apple.com/library/prerelease/ios/#documentation/UserExperience/Reference/PassKit_Framework/_index.html)
- [Передать ссылку Kit Framework](https://developer.apple.com/library/prerelease/ios/#documentation/UserExperience/Reference/PassKit_Framework/_index.html)
- [Ссылки расчетной веб-службу](https://developer.apple.com/library/prerelease/ios/#documentation/PassKit/Reference/PassKit_WebService/WebService.html)
