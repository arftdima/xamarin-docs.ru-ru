---
title: Введение в iOS 8
description: С iOS 8 Apple предоставляет множество новых платформ и API-интерфейсы для excite и порадовать разработчиков. В этом руководстве мы вводят эти новые интерфейсы API и разделе преимуществах iOS 8 разработчиков и пользователей.
ms.prod: xamarin
ms.assetid: 33AD66C0-3743-49FE-9DCE-88ED3A16BA63
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 06/14/2017
ms.openlocfilehash: 2f57547356adcbafd01851bc54e42a14454ccd6a
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="introduction-to-ios-8"></a>Введение в iOS 8

_С iOS 8 Apple предоставляет множество новых платформ и API-интерфейсы для excite и порадовать разработчиков. В этом руководстве мы вводят эти новые интерфейсы API и разделе преимуществах iOS 8 разработчиков и пользователей._

iOS 7 визуально изменить пользовательский интерфейс Всего операций ввода-вывода какие пользователи и разработчики имели ожидать, справа от первой iPhone ОС. IOS 8 продолжается с этим путем предоставления множество платформ для разработчиков, которая позволяет пользователям управлять практически любой аспект их жизненного цикла от их iPhone. Например можно проанализировать работоспособности продажи и применимости с *HealthKit*, секретные коды устаревшей с биометрической проверки подлинности с помощью *LocalAuthentication*, *расширений приложения*открыть канал связи между сторонних приложений, и *HomeKit* позволяет превратить ваш дом в домашней будущего. 

Если о delighting пользователи iOS 7, iOS 8 основное внимание уделяется delighting разработчикам целый ряд их tasty. 

В этом руководстве описаны новые интерфейсы API для разработчиков, Xamarin.iOS.  

Существует несколько интерфейсов API, которые являются устаревшими в iOS 8, приведены в конце этого документа.

## <a name="requirements"></a>Требования

Для создания приложений iOS 8 в Visual Studio для Mac необходимы следующие:

- **Xcode 7 и iOS 8 или более новой версии** — последние Xcode и iOS API-интерфейсы Apple необходимо установить и настроить на компьютере разработчика.
- **Visual Studio для Mac** — последнюю версию Visual Studio для Mac должен быть установлен и настроен на устройстве пользователя.
- **iOS 8 устройство или симулятор** — самая последняя версия iOS 8 для тестирования устройства iOS.

## <a name="home-and-leisure"></a>Дом и свободное время

iOS 8 позволило надежно завода прямо в лежит в основе дома с помощью HomeKit и HealthKit устройств iOS и Apple. В этом разделе мы рассмотрим работать как обе эти новые платформы, и как они могут интегрироваться в приложения Xamarin.iOS.

## <a name="homekit"></a>HomeKit

Управление вашего устройства с помощью iPhone не нового приложения технологии; Многие продукты подключен дома можно регулировать с помощью приложения iOS. Однако HomeKit теперь принимает это дальше переместив общий протокол для автоматизации дома устройств и предоставлении некоторых производителей, например iHome, Philips Компания Honeywell открытый API. Для пользователя, это означает, что они могут управлять практически любой аспект легко из дома внутри одного приложения. Он не имеет значения для них знать, что они используют лампочки Philips оттенка или сигнализации вложения. Пользователи также можно соединить в цепочку многочисленные смарт-домашней процессов друг с другом в «Автоматически».

С HomeKit приложения сторонних производителей и Siri может обнаружить стандартные и добавить их в их базу данных конфигурации домашней, редактировать и обрабатывают эти данные и взаимодействовать с стандартные и служб, чтобы выполнить действие.

### <a name="configuration"></a>Конфигурация

На приведенной ниже диаграмме показана иерархия основные конфигурации стандартные HomeKit:

![](introduction-to-ios8-images/image1.png "На этой диаграмме показаны основные иерархии конфигурации стандартные HomeKit")
 
Чтобы приступить к работе с HomeKit, разработчики должны оставалось выбранной службой HomeKit их подготовительный профиль. Apple также предоставил разработчикам HomeKit симулятор надстройки для Xcode. Его можно найти в [Центр разработчиков Apple](https://developer.apple.com/downloads/index.action)в разделе `Hardware IO Tools for Xcode`. 

Дополнительные сведения см. в разделе нашей [HomeKit](~/ios/platform/homekit.md) руководства.

## <a name="healthkit"></a>HealthKit

HealthKit — это платформа, представленные в iOS 8, обеспечивающий централизованное, координации и безопасного хранилища данных сведения о работоспособности. Операционная система гарантирует конфиденциальность и безопасность информации о состоянии и с помощью работоспособности приложения панели мониторинга для пользователя. С разрешения пользователя приложения могут читать и записывать различные сведения о работоспособности.

Дополнительные сведения об использовании этого приложения Xamarin.iOS посвящены [введение в HealthKit](~/ios/platform/healthkit.md) руководства.

## <a name="extending-iphone-functionality"></a>Расширение функциональности iPhone
С iOS8 разработчиков предоставляют больший контроль над кто может использовать свои приложения и повышения возможности для более открыта взаимодействие между приложениями сторонних производителей. Функции, такие как Выбор документа и расширения приложения откройте мир возможности использования приложений в экосистеме компании Apple.

### <a name="app-extensions"></a>Расширения приложения
Расширения приложения, чтобы чрезмерно упростить, представляют собой способ для приложений сторонних разработчиков для взаимодействия друг с другом. Для обеспечения высокого уровня безопасности стандартов и поддержанию целостности изолированных приложений, такая связь не происходит напрямую между приложениями. Вместо этого он выполняется *расширения* в середине.

Первым шагом при создании расширения приложения является правильным расширением точки — это важно для обеспечения поведения и доступности правильно API-интерфейсов. Для создания расширения приложения в Visual Studio для Mac, добавьте его к существующему приложению путем добавления нового проекта в решение.

В **новый проект** диалоговом окне перейдите к **C#** > **iOS** > **единой API**  >   **Расширения**, как показано на снимке экрана ниже:

![](introduction-to-ios8-images/image2.png "Создание нового расширения")
 
Диалоговое окно нового проекта предоставляет семь новых шаблонов проектов для создания расширений приложения и рассматриваются ниже. Обратите внимание, что многие из модулей, связаны с других новых API в iOS, такие как Выбор документа:

- **Действие** — это позволяет разработчикам создавать уникальные настраиваемое действие кнопки позволяет пользователям выполняет определенные задачи
- **Настраиваемые сочетания** — это позволяет разработчикам добавлять к диапазону созданных в Apple клавиатуры добавлять свои собственные пользовательские. Популярные клавиатуры Swype использует это для приведения их сочетания операций ввода-вывода.
- **Документирование выбора** — это содержит контроллер представление выбора документа, который позволяет пользователям получать доступ к файлам вне приложения "песочницы".
- **Документирование поставщика средства выбора файлов** — это обеспечивает безопасное хранение для файлов с помощью средства выбора документа.
- **Изменение фотографий** — этот расширяет фильтры и средства, уже обеспечиваемые Apple в приложении фотографии, чтобы предоставить пользователям дополнительные параметры и больший контроль при редактировании фотографий редактирования.
- **Сегодня** — это дает приложениям возможность отображать мини-приложения в разделе "сегодня" Центр уведомлений.

Дополнительные сведения об использовании расширений приложений в Xamarin см. [введение расширения приложения](~/ios/platform/extensions.md) руководства.

### <a name="touch-id"></a>Touch ID

Touch ID был введен в iOS 7, с точки зрения проверки подлинности пользователя — аналогично секретный код. Тем не менее он был ограничен разблокировки устройства, с помощью магазина приложений, с помощью iTunes и проверки подлинности только к цепочке ключей iCloud 

Сейчас существует два способа использовать Touch ID в качестве механизма проверки подлинности в приложениях iOS 8, с помощью API локальной проверки подлинности. Он в настоящее время не поддерживается для использования локальной проверки подлинности для проверки подлинности удаленного.

Во-первых он помогает существующие цепочки ключей службы за счет использования новых ключей списки управления доступом (ACL). Данные цепочки ключей может быть разблокировано с успешной проверки подлинности пользователей по отпечатку пальца.

Во-вторых LocalAuthentication предоставляет два метода для проверки подлинности приложения локально. Разработчикам следует проявлять `CanEvaluatePolicy` для определения, является ли устройство способное принимать Touch ID и затем `EvaluatePolicy` для запуска операции проверки подлинности.

Дополнительные сведения на Touch ID и узнайте, как интегрировать в приложения Xamarin.iOS [введение в TouchID](~/ios/platform/touchid.md) руководства.

### <a name="document-picker"></a>Выбор документа

Документ выбора работает с диска iCloud пользователей, чтобы разрешить пользователю открывать файлы, которые были созданы в другое приложение, импортировать и управлять ими и экспортировать их обратно еще раз. Это создает интуитивно рабочего процесса и поэтому гораздо удобнее работать, для пользователей. дальнейшей синхронизации iCloud делает этот шаг, любые изменения, внесенные в одном приложении также может быть отражать постоянно на всех устройствах.

Дополнительные сведения о средстве выбора документа более подробно и узнайте, как интегрировать в приложения Xamarin.iOS, относятся к [введение в средства выбора документа](~/ios/platform/document-picker.md) руководства.

### <a name="handoff"></a>Перемещение вручную

Перемещение вручную, который является частью большего функции обеспечения непрерывности, принимает этапом дальнейшей интеграции iOS и OS X. Сюда входят AirDrop между различными платформами, может принимать вызовы iPhone, SMS на iPad и Mac, а также улучшения в модем с помощью iPhone.

Перемещение вручную работает с iOS 8 и Yosemite и требуется учетная запись iCloud вход в систему на различных устройствах, вы хотите использовать. Он должен работать с предварительно установленные приложения Apple, включая Safari, iWork, карты, календари и контакты.

Дополнительные сведения см. в разделе нашей [сдачи](~/ios/platform/handoff.md) руководства.

## <a name="unified-storyboards"></a>Унифицированный раскадровки
включает в себя новый iOS 8 проще в использовании механизм для создания пользовательского интерфейса — унифицированной раскадровки. С помощью одного раскадровки, чтобы охватить все размеры экрана другое оборудование быстрых и отвечать на запросы представления могут создаваться в стиле «Проектируйте один раз, использовать многие» значение true.

До iOS8, разработчики использовали `UIInterfaceOrientation` для различия между режимами книжной и альбомной и `UIInterfaceIdiom` для различения устройства iOS. В iOS8 он больше не нужно создавать отдельные раскадровки для устройств iPhone и iPad, ориентацию и устройства, определяются с помощью *классы размер*.

Каждое устройство, определяется класс размер в вертикальной и горизонтальной оси, и существует два типа классов размер в iOS 8:

- **Регулярные** -это большой экран (таких как iPad) или мини-приложения, который создает впечатление большого размера (например, UIScrollView
- **Compact** -это для более мелких устройств (таких как iPhone). Этот размер учитывает ориентации устройства.

Если эти два понятия используются совместно, результатом является сетки 2 x 2, который определяет различные возможные размеры, которые могут использоваться в обоих разные ориентации, как показано на следующей схеме:

![](introduction-to-ios8-images/image3.png "Диаграммы, представляющие сетки 2 x 2, который определяет различные возможные размеры, которые можно использовать в различных ориентациях")
 
Дополнительные сведения о классах размер посвящены [введение в единой раскадровки](~/ios/user-interface/storyboards/unified-storyboards.md).

## <a name="photo-kit"></a>Комплект средств для фотографий
Набор фото — новую платформу, которая позволяет приложениям запрашивать библиотека изображений системы и создавать настраиваемые пользовательские интерфейсы для просмотра и изменения его содержимого. Он включает несколько классов, представляющих изображения и видео активы, а также коллекции средств, таких как диски и папки.

Дополнительные сведения см. в разделе нашей [PhotoKit](~/ios/platform/photokit.md) руководства.

## <a name="games"></a>Игры

<a name="scenekit" />

### <a name="scene-kit"></a>Комплект средств для сцены

Набор сцены — 3D-сцену graph API, который упрощает работу с трехмерной графикой. Впервые появившийся в OS X 10.8 и теперь пришло iOS 8. Комплект сцены Создание случайного трехмерных игр и впечатляющие трехмерной визуализации не требуется опыт в OpenGL. Основываясь на основные понятия граф сцены, комплект сцены устраняет сложности OpenGL и OpenGL ES, поскольку его легко добавить трехмерные содержимого в приложение. Тем не менее если вы не являетесь специалистом OpenGL, набор сцены имеет отличную поддержку для привязки непосредственно с также OpenGL. Также включает множество функций, которые дополняют трехмерной графики, такие как физический и хорошо интегрируется с несколькими другими средами Apple, как основной анимации, образ Core и Sprite Kit.

Дополнительные сведения см. в разделе нашей [SceneKit](~/ios/platform/gaming/scenekit.md) документации.

<a name="spritekit" />

### <a name="sprite-kit"></a>Комплект Sprite

Комплект Sprite, платформа игр 2D Apple, имеет некоторые интересные новые возможности в iOS 8 и OS X Yosemite. К ним относятся интеграция с Kit сцены, поддержка построителя текстуры, освещения, теней, ограничения, создания карты нормалей и улучшения физических. В частности новые возможности физических сделать очень легко включить реалистичных эффектов в игру.

Дополнительные сведения см. в разделе нашей [SpriteKit](~/ios/platform/gaming/spritekit.md) документации.

## <a name="other-changes"></a>Другие изменения
А также основные изменения в iOS 8, как описано выше Apple Дополнительно обновил многие существующие платформы. Они описаны ниже.

- **[Основной образ](https://developer.apple.com/library/prerelease/ios/documentation/GraphicsImaging/Reference/CoreImagingRef/index.html#//apple_ref/doc/uid/TP40001171)**  — Apple был расширен после его среда обработки изображения, добавив улучшенную поддержку обнаружения прямоугольной области, а также QR-коды в изображения. Майк Bluestein более подробно рассматривается это в своем блоге post под названием [образа обнаружения в iOS 8](http://blog.xamarin.com/image-detection-in-ios-8/)

## <a name="deprecated-apis"></a>Устаревшие интерфейсы API
Все улучшения, внесенные в iOS 8 устаревшими несколько API-интерфейсов. Ниже описаны некоторые из них.

- **[UIApplication](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIApplication_Class/index.html#//apple_ref/occ/cl/UIApplication)**  — методы и свойства, используемые для регистрации уведомлений удаленного устаревшими. Это registerForRemoteNotificationTypes и enabledRemoteNotificationTypes.
- **[UIViewController](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UIViewController_Class/index.html#//apple_ref/occ/cl/UIViewController)**  — признаки и размер классы заменили методы и свойства, используемые для описания интерфейса ориентации. Ссылаться на [введение в единой раскадровки](~/ios/user-interface/storyboards/unified-storyboards.md) Дополнительные сведения о том, как их использовать.

- **[UISearchDisplayController](https://developer.apple.com/library/prerelease/ios/documentation/UIKit/Reference/UISearchDisplayController_Class/index.html#//apple_ref/occ/cl/UISearchDisplayController)**  — это будет заменен UISearchController в iOS8.

## <a name="summary"></a>Сводка
В этой статье мы рассмотрели некоторые новые функции в Apple iOS 8.



## <a name="related-links"></a>Связанные ссылки

- [UIKitEnhancements (пример)](https://developer.xamarin.com/samples/monotouch/ios8/UIKitEnhancements)
- [Введение в расширения приложения](~/ios/platform/extensions.md)
- [Введение в CloudKit](~/ios/data-cloud/intro-to-cloudkit.md)
- [Общие сведения о средстве выбора документа](~/ios/platform/document-picker.md)
- [Общие сведения о HealthKit](~/ios/platform/healthkit.md)
- [Знакомство с элементами управления вручную камеры](~/ios/user-interface/controls/intro-to-manual-camera-controls.md)
- [Общие сведения о TouchID](~/ios/platform/touchid.md)
- [Общие сведения о единой раскадровки](~/ios/user-interface/storyboards/unified-storyboards.md)
