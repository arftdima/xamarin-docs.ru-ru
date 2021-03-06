---
title: Публикация в Магазине приложений
description: В этой статье демонстрируется настройка, сборка и публикация приложения Xamarin.iOS для распространения через App Store. Здесь приводятся пошаговые инструкции по тому, как подготовить приложение к распространению, отправить его на проверку с помощью средств Apple, а также опубликовать в App Store.
ms.prod: xamarin
ms.assetid: DFBCC0BA-D233-4DC4-8545-AFBD3768C3B9
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 08/23/2017
ms.openlocfilehash: 5d78cb81f27ce7478719ff9f11f4eb38fddc3981
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="publishing-to-the-app-store"></a>Публикация в Магазине приложений

_В этой статье описано, как выполнять настройку, сборку и публикацию приложения Xamarin.iOS для распространения через App Store. Здесь приводятся пошаговые инструкции по подготовке приложения к распространению, отправке его на проверку с помощью средств Apple, а также публикации в App Store._

Согласно требованиям компании Apple, для распространения на всех устройствах с iOS приложения должны быть опубликованы в магазине *App Store*, который является единым центром, в котором можно приобрести приложения для iOS. В этом магазине представлено более 500 000 приложений, благодаря чему разработчики программ самых разных видов могут успешно зарабатывать на результатах своего труда. Магазин App Store представляет собой готовое решение для разработчиков приложений, в котором одновременно реализованы системы распространения и оплаты.

Процесс отправки приложения в App Store состоит из следующих этапов:

1. Создание **идентификатора приложения** и выбор **прав**.
2. Создание профиля **подготовки распространения**.
3. Построение приложения с использованием этого профиля.
4. Отправка приложения через **iTunes Connect**.


В этой статье описываются все действия, которые необходимо выполнить для подготовки, построения и отправки приложения для распространения через App Store.

## <a name="before-you-submit-an-application"></a>Действия перед отправкой приложения

Приложение, отправленное для публикации в App Store, проходит установленный компанией Apple процесс проверки на соответствие правилам Apple в отношении качества и содержимого. Если ваше приложение не соответствует этим правилам, компания Apple отклоняет его. В таком случае вам следует устранить указанные компанией Apple несоответствия и отправить приложение на проверку повторно.
Таким образом, чтобы максимально повысить шансы успешно пройти проверку Apple, ознакомьтесь с приведенными ниже рекомендациями и постарайтесь адаптировать свое приложение к ним. Требования Apple можно найти в разделе [Правила проверки для App Store](https://developer.apple.com/appstore/resources/approval/guidelines.html).

Прежде чем отправлять приложение, проверьте некоторые моменты:

1. Убедитесь, что описание приложения соответствует его функциональным возможностям.
2. Протестируйте приложение на отсутствие сбоев при обычном использовании. Необходимо проверить приложение на любых устройствах с iOS, которые оно поддерживает.


Кроме того, компания Apple предлагает ряд советов, с которыми рекомендуется ознакомиться перед отправкой приложения в App Store. Вы можете ознакомиться с ними на странице [Распространение через App Store](https://developer.apple.com/appstore/resources/submission/tips.html).

## <a name="configuring-your-application-in-itunes-connect"></a>Настройка приложения в iTunes Connect

[iTunes Connect](https://itunesconnect.apple.com/WebObjects/iTunesConnect.woa) — это набор веб-средств, обеспечивающих, помимо прочего, управление приложениями для iOS в App Store. Приложение Xamarin.iOS должно быть правильно настроено в iTunes Connect, прежде чем вы отправите его на проверку в Apple или в конечном итоге начнете его коммерческое или бесплатное распространение через App Store.

Выполните следующие действия:

1. Убедитесь, что в разделе **Соглашения, налоги и банковские операции** iTunes Connect установлены актуальные соглашения, относящиеся к коммерческому или бесплатному распространению приложений iOS.
2. Создайте новую **запись iTunes Connect** для приложения и укажите ее **отображаемое имя**, которое будут видеть пользователи App Store.
3. Установите **цену продажи** или укажите, что приложение будет распространяться на бесплатной основе.
5. Приведите краткое и лаконичное **описание** приложения с указанием его функциональных возможностей и преимуществ для конечного пользователя.
6. Укажите **категории**, **подкатегории** и **ключевые слова**, по которым пользователям будет проще найти ваше приложение в App Store.
7. Укажите URL-адреса для **связи** и **получения поддержки** на вашем веб-сайте в соответствии с требованиями Apple.
8. Укажите **возрастной рейтинг** приложения, который используется системой родительского контроля App Store.
9. Настройте дополнительные технологии App Store, такие как **Game Center** и **покупки в приложении**.

Дополнительные сведения см. в нашей документации по [настройке приложений в iTunes Connect](~/ios/deploy-test/app-distribution/app-store-distribution/itunesconnect.md).

## <a name="preparing-for-app-store-distribution"></a>Подготовка к распространению через App Store

Чтобы опубликовать приложение в App Store, сначала необходимо выполнить многоэтапный процесс его построения для распространения. В следующих разделах описывается все, что необходимо для подготовки приложения Xamarin.iOS к построению и отправке в App Store для проверки и распространения.

### <a name="provisioning-for-application-services"></a>Подготовка служб приложений

Apple предоставляет ряд специальных служб приложений, также называемых правами, которые можно активировать для приложения iOS при создании его уникального идентификатора. Независимо от того, используете вы настраиваемые права или нет, вам по-прежнему необходимо создать уникальный идентификатор приложения Xamarin.iOS, который требуется для его публикации в App Store.

Чтобы создать идентификатор приложения и при необходимости выбрать права для него с помощью веб-портала подготовки для iOS компании Apple, выполните следующие действия:

1. В разделе **Certificates, Identifiers & Profiles** (Сертификаты, идентификаторы и профили) выберите **Identifiers** > **App ID** (Идентификаторы > Идентификатор приложения).
2. Нажмите кнопку **+** и заполните поля **Name** (Имя) и **Bundle ID** (Идентификатор пакета) для нового приложения.
3. Прокрутите экран вниз и выберите в списке **App Services** (Службы приложений) службы, которые будут использоваться вашим приложением Xamarin.iOS.
4. Нажмите кнопку **Continue** (Продолжить) и создайте новый идентификатор приложения, следуя инструкциям на экране.

Помимо выбора и настройки необходимых служб приложений при определении идентификатора приложения, вам также необходимо настроить идентификатор приложения и права в проекте Xamarin.iOS, внеся необходимые изменения в файлы `Info.plist` и `Entitlements.plist`.

Выполните следующие действия:

1. В **обозревателе решений** дважды щелкните файл `Info.plist`, чтобы открыть его для редактирования.
2. В разделе **Целевая платформа приложения iOS** укажите имя приложения и введите **идентификатор пакета**, который был создан при определении идентификатора приложения.
3. Сохраните изменения в файле `Info.plist`.
4. В **обозревателе решений** дважды щелкните файл `Entitlements.plist`, чтобы открыть его для редактирования.
5. Выберите и настройте права для своего приложения Xamarin.iOS в соответствии с настройками, установленными ранее при определении идентификатора приложения.
6. Сохраните изменения в файле `Entitlements.plist`.

Подробные инструкции см. в нашей документации по [подготовке служб приложений](~/ios/get-started/installation/device-provisioning/manual-provisioning.md#appservices).

### <a name="setting-the-store-icons"></a>Настройка значка Store

Значки приложения Store на данный момент предоставляются в каталоге ресурсов. Чтобы добавить значок App Store, сначала найдите набор изображений **AppIcon** в файле **Assets.xcassets** своего проекта.

Нужный вам значок в каталоге ресурсов называется **App Store** и должен иметь размер **1024 x 1024**. В соответствии с требованиями Apple значок App Store в каталоге ресурсов не может быть прозрачным и не должен содержать альфа-канал.

Дополнительные сведения о настройке значка App Store см. в руководстве [Значок App Store](~/ios/app-fundamentals/images-icons/app-store-icon.md).

### <a name="setting-the-apps-icons-and-launch-screens"></a>Настройка значков приложений и экранов запуска

Компания Apple разрешает добавлять в App Store только те приложения для iOS, в которых используются соответствующие значки и экраны запуска для всех устройств iOS, на которых они будут выполняться. Значки приложений добавляются в проекты посредством каталога ресурсов с помощью набора изображений **AppIcon** в файле **Assets.xcassets**. Для добавления экранов запуска используется раскадровка.

Подробные инструкции по созданию значков приложений и экранов запуска см. в руководствах [Значок приложения](~/ios/app-fundamentals/images-icons/app-icons.md) и [Экраны запуска](~/ios/app-fundamentals/images-icons/launch-screens.md).

### <a name="creating-and-installing-a-distribution-profile"></a>Создание и установка профиля распространения

Для управления развертыванием определенных сборок приложений в iOS используются *профили подготовки*. Эти файлы содержат информацию о сертификате, который используется для подписывания приложения, *идентификатор приложения*, а также сведения о том, где можно устанавливать приложение. Для разработки и динамического распространения в профиль подготовки также включается список разрешенных устройств, на которых можно развертывать приложение. Тем не менее для публичного распространения через App Store включаются только сертификат и идентификатор приложения, поскольку другие механизмы не требуются.

Чтобы выполнить подготовку на портале подготовки для iOS компании Apple, выполните следующие действия:

1.  Выберите **Provisioning** > **Distribution** (Подготовка > Распространение).
2.  Нажмите кнопку **+** и выберите тип профиля распространения, который необходимо создать для **App Store**.
3.  Выберите в раскрывающемся списке **App ID** (Идентификатор приложения), для которого требуется создать профиль распространения.
4.  Выберите действительный рабочий сертификат (сертификат распространения), с помощью которого будет подписано приложение.
5.  Заполните поле **Name** (Имя) для нового элемента **Distribution Profile** (Профиль распространения) и создайте профиль.
6.  На компьютере Mac откройте средство Xcode и выберите **Preferences > [select your Apple ID]> View Details** (Настройки > [идентификатор_приложения]> Сведения). Скачивание всех доступных профилей в Xcode на компьютере Mac.
7.  Вернитесь в интегрированную среду разработки и в разделе **iOS Bundle Signing** (Подписывание пакета iOS) выберите профиль подготовки распространения для соответствующего типа _Build Configuration_ (Конфигурация сборки) (**App Store** или **Release** (Выпуск)).

Подробные инструкции см. в разделах [Создание профиля распространения](~/ios/get-started/installation/device-provisioning/manual-provisioning.md#provisioningprofile) и [Выбор профиля распространения в проекте Xamarin.iOS](~/ios/deploy-test/app-distribution/app-store-distribution/index.md#selectprofile).

## <a name="setting-the-build-configuration-for-your-application"></a>Настройка конфигурации сборки для приложения

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

Выполните следующие действия:

1. Щелкните правой кнопкой мыши **имя проекта** на **Панели решения** и выберите пункт **Параметры**, чтобы открыть параметры для редактирования.
2. Выберите **Сборка iOS** и **Выпуск | iPhone** в раскрывающемся списке **Конфигурация**:

    ![](publishing-to-the-app-store-images/configurevs01.png "Выбор пункта "AppStore" в раскрывающемся списке "Конфигурация"")

3. Если приложение предназначено для конкретной версии iOS, выберите ее в раскрывающемся списке **Версия пакета SDK**, в противоположном случае оставьте заданное по умолчанию значение.
4. Компоновка позволяет уменьшить общий размер распространяемых файлов приложений за счет исключения неиспользуемых методов, свойств, классов и т. д. Поэтому в большинстве случаев рекомендуется оставлять значение по умолчанию **Компоновать только сборки пакета SDK**. В некоторых случаях, например при использовании определенных сторонних библиотек, для сохранения нужных элементов может потребоваться выбор значения **Не компоновать**. Дополнительные сведения см. в руководстве [Механизм построения iOS](~/ios/deploy-test/ios-build-mechanics.md).
5. Следует установить флажок **Оптимизировать файлы изображений PNG для iOS**, поскольку это позволит дополнительно уменьшить размер конечных файлов приложения.
6. Включать отладку _не следует_, поскольку это приведет к неоправданному увеличению размеров сборки.
8. Для устройств iOS 11 необходимо выбрать одну из архитектур, которые поддерживают **ARM64**. Дополнительные сведения о построении для 64-разрядных устройств iOS см. в разделе **Поддержка 64-разрядных сборок приложений Xamarin.iOS** в документации по [сравнению 32- и 64-разрядных платформ](~/cross-platform/macios/32-and-64/index.md).
9. При необходимости вы можете использовать компилятор **LLVM**, который за счет более продолжительного процесса компиляции позволяет создавать более быстрый и компактный код.
10. Исходя из потребностей вашего приложения, вы также можете настроить тип **сборки мусора** и конфигурацию **интернационализации**.
11. Сохраните изменения в конфигурации сборки.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

По умолчанию при создании нового приложения Xamarin.iOS в Visual Studio автоматически создаются _конфигурации сборки_ для развертываний типа **Прямое соединение** и **App Store**. Прежде чем выполнить окончательную сборку приложения, которое будет отправлено в Apple, необходимо внести определенные изменения в базовую конфигурацию.

Выполните следующие действия:

1. Щелкните проект правой кнопкой мыши в поле **Имя проекта** в **обозревателе решений** и выберите пункт **Свойства**, чтобы открыть проект для редактирования.
2. Выберите **Сборка iOS** и **AppStore** (или **Выпуск**, если пункт "AppStore" недоступен) в раскрывающемся списке **Конфигурация**:

    ![](publishing-to-the-app-store-images/configurevs01.png "Выбор пункта "AppStore" в раскрывающемся списке "Конфигурация"")

3. Если приложение предназначено для конкретной версии iOS, выберите ее в раскрывающемся списке **Версия пакета SDK**, в противоположном случае оставьте заданное по умолчанию значение.
4. Компоновка позволяет уменьшить общий размер распространяемых файлов приложений за счет исключения неиспользуемых методов, свойств, классов и т. д. Поэтому в большинстве случаев рекомендуется оставлять значение по умолчанию **Компоновать только сборки пакета SDK**. В некоторых случаях, например при использовании определенных сторонних библиотек, для сохранения нужных элементов может потребоваться выбор значения **Не компоновать**. Дополнительные сведения см. в руководстве [Механизм построения iOS](~/ios/deploy-test/ios-build-mechanics.md).
5. Следует установить флажок **Оптимизировать файлы изображений PNG для iOS**, поскольку это позволит дополнительно уменьшить размер конечных файлов приложения.
6. Включать отладку _не следует_, поскольку это приведет к неоправданному увеличению размеров сборки.
7. Откройте вкладку **Дополнительно**:

    ![](publishing-to-the-app-store-images/configurevs02.png "Вкладка "Дополнительно"")

8. Если ваше приложение Xamarin.iOS предназначено для iOS 8 и 64-разрядных устройств iOS, необходимо выбрать одну из архитектур, которые поддерживают **ARM64**. Дополнительные сведения о построении для 64-разрядных устройств iOS см. в разделе **Поддержка 64-разрядных сборок приложений Xamarin.iOS** в документации по [сравнению 32- и 64-разрядных платформ](~/cross-platform/macios/32-and-64/index.md).
9. При необходимости вы можете использовать компилятор **LLVM**, который за счет более продолжительного процесса компиляции позволяет создавать более быстрый и компактный код.
10. Исходя из потребностей вашего приложения, вы также можете настроить тип **сборки мусора** и конфигурацию **интернационализации**.
11. Сохраните изменения в конфигурации сборки.

-----

## <a name="building-and-submitting-the-distributable"></a>Построение и отправка распространяемых файлов

После соответствующей настройки приложения Xamarin.iOS вы можете создать сборку для окончательного распространения, которая будет отправлена для проверки и выпуска в компанию Apple.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

### <a name="build-your-archive"></a>Построение архива

1. Выберите конфигурацию **Выпуск | Устройство** в Visual Studio для Mac:

    ![](publishing-to-the-app-store-images/buildxs01new.png "Выбор конфигурации "Выпуск | Устройство"")
1. В меню **Сборка** выберите **Архивировать для публикации**:

    ![](publishing-to-the-app-store-images/buildxs02new.png "Выбор элемента "Архивировать для публикации"")

1. После создания архива появится представление **Архивы**:

    ![](publishing-to-the-app-store-images/buildxs03new.png "Отображается представление "Архивы"")


> [!NOTE]
> Хотя старые конфигурации _App Store_ и _Специальный_ удаляются из всех проектов шаблонов Visual Studio для Mac, они по-прежнему могут присутствовать в некоторых предшествующих проектах. В таких случаях вы можете продолжать использовать конфигурацию **App Store | Устройство** на шаге 1 приведенного выше списка.

### <a name="sign-and-distribute-your-app"></a>Подписывание и распространение приложения

 Каждый раз при сборке приложения для архивирования автоматически открывается представление **Архивы**, где отображаются все заархивированные проекты, сгруппированные по решениям. По умолчанию в этом представлении отображаются только открытые на данный момент решения. Чтобы просмотреть все решения с архивами, выберите параметр **Показать все архивы**.

 Рекомендуется хранить архивы, которые были развернуты для клиентов (развертывания App Store или корпоративные развертывания), чтобы при необходимости впоследствии отображать любую получаемую отладочную информации.

 Чтобы подписать приложение и подготовить его к распространению, выполните следующие действия:


1. Выберите **Подписать и распространить...**, как показано ниже:

    ![](publishing-to-the-app-store-images/buildxs04new.png "Выбор команды "Подписать и распространить"")

1. Откроется мастер публикации. Выберите **App Store** в качестве канала распространения, чтобы создать пакет, и откройте загрузчик приложений:

    ![](publishing-to-the-app-store-images/distribute01.png "Запуск загрузчика приложений")

1. На экране профиля подготовки выберите удостоверение для подписывания и соответствующий профиль подготовки или подпишите повторно другим удостоверением:

    ![](publishing-to-the-app-store-images/distribute02.png "Выбор удостоверения для подписи и соответствующего профиля подготовки")

1. Проверьте сведения о пакете и затем нажмите кнопку **Опубликовать**, чтобы сохранить пакет `.ipa`:

    ![](publishing-to-the-app-store-images/distribute03.png "Проверка сведений о пакете")

1. После сохранения файла `.ipa` ваше приложение готово для загрузки в iTunes Connect с помощью загрузчика приложений:

    ![](publishing-to-the-app-store-images/distribute04.png "Экран успешного завершения публикация")

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

На данный момент подключаемый модуль Xamarin для Visual Studio не поддерживает рабочий процесс архивации для публикации приложений iOS в App Store. Соответственно, вам необходимо загрузить созданные IPA-файлы с помощью команды **Build Ad hoc IPA** (Построить динамический IPA-файл), которая описывается ниже.


## <a name="build-an-ipa"></a>Построение IPA-файла

 В этом разделе описывается процесс построения IPA-файла, который схож с процедурой подготовки к динамическому или корпоративному распространению. Тем не менее для его подписывания будет использоваться профиль подготовки App Store, который был создан выше.

 Выполните следующие действия:

1. В **обозревателе решений** щелкните имя проекта Xamarin.iOS правой кнопкой мыши и выберите **Свойства**, чтобы открыть его для редактирования:

    ![](publishing-to-the-app-store-images/imagevs01.png "Выбор пункта "Свойства"")
1. Щелкните **Подписывание пакета iOS** и выберите профиль подготовки App Store:

    ![](publishing-to-the-app-store-images/ipa01.png "Выбор пункта "Подписывание пакета iOS" и изменение профиля подготовки на профиль App Store")
1. Щелкните **Параметры IPA iOS** и выберите **Прямое соединение** в раскрывающемся списке **Конфигурация** (если этот пункт отсутствует, выберите вместо него элемент **Выпуск**):

    ![](publishing-to-the-app-store-images/imagevs02.png "Выбор пункта "Специальный" в раскрывающемся списке "Конфигурация"")

1. При необходимости заполните поле **Имя пакета** для IPA-файла, иначе оно будет совпадать с именем проекта Xamarin.iOS.
1. Сохраните изменения в свойствах проекта.
1. Выберите **Прямое соединение**  в раскрывающемся списке **Конфигурация сборки** в Visual Studio для Mac:

    ![](publishing-to-the-app-store-images/imagevs05.png "Выбор пункта "Специальный" в раскрывающемся списке "Конфигурация сборки"")
1. Выполните сборку проекта для создания пакета IPA.
1. IPA-файл будет располагаться в папке `Bin` > _Устройство iOS_ > `Ad Hoc`:

    ![](publishing-to-the-app-store-images/imagevs06.png "IPA-файл в проводнике")

-----


## <a name="customizing-the-ipa-location"></a>Настройка расположения файла IPA

Новое свойство **MSBuild** `IpaPackageDir` позволяет упростить настройку расположения для вывода файла `.ipa`. Если в параметре `IpaPackageDir` задано настраиваемое расположение, файл `.ipa` будет помещен в указанную папку, а не в установленный по умолчанию подкаталог с меткой времени. Это может быть полезно при создании автоматизированных сборок, для работы которых требуется конкретный путь к каталогу (например, это могут быть сборки непрерывной интеграции).

Использовать новое свойство можно несколькими способами:

Например, чтобы выводить файл `.ipa` в старый каталог по умолчанию (как в Xamarin.iOS 9.6 и более ранних версиях), присвойте свойству `IpaPackageDir` значение `$(OutputPath)` одним из следующих способов. Оба подхода совместимы со всеми сборками Unified API Xamarin.iOS, включая сборки интегрированной среды разработки и сборки командной строки, которые используют `xbuild`, `msbuild` или `mdtool`:

  - Первый способ подразумевает установку свойства `IpaPackageDir` в элементе `<PropertyGroup>` в файле **MSBuild**. Например, можно добавить следующий элемент `<PropertyGroup>` в конец файла `.csproj` проекта приложения iOS (непосредственно перед закрывающим тегом `</Project>`):

      ```xml
        <PropertyGroup>
            <IpaPackageDir>$(OutputPath)</IpaPackageDir>
        </PropertyGroup>
      ```
  - Более эффективный подход заключается в добавлении элемента `<IpaPackageDir>` в конец существующего элемента `<PropertyGroup>`, который соответствует конфигурации, используемой при построении файла `.ipa`. Это способ является рекомендуемым, поскольку он позволяет обеспечить дальнейшую совместимость с запланированными настройками на странице параметров IPA-файла для iOS в свойствах проекта. Если вы в данный момент используете конфигурацию `Release|iPhone` для построения файла `.ipa`, полностью обновленная группа свойств может иметь следующий вид:

      ```xml
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|iPhone' )
        <Optimize>true</Optimize>
        <OutputPath>bin\iPhone\Release</OutputPath>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
        <ConsolePause>false</ConsolePause>
        <CodesignKey>iPhone Developer</CodesignKey>
        <MtouchUseSGen>true</MtouchUseSGen>
        <MtouchUseRefCounting>true</MtouchUseRefCounting>
        <MtouchFloat32>true</MtouchFloat32>
        <CodesignEntitlements>Entitlements.plist</CodesignEntitlements>
        <MtouchLink>SdkOnly</MtouchLink>
        <MtouchArch>;ARMv7, ARM64</MtouchArch>
        <MtouchHttpClientHandler>HttpClientHandler</MtouchHttpClientHandler>
        <MtouchTlsProvider>Default</MtouchTlsProvider>
        <PlatformTarget>x86&</PlatformTarget>
        <BuildIpa>true</BuildIpa>
        <IpaPackageDir>$(OutputPath</IpaPackageDir>
      </PropertyGroup>
      ```
Альтернативный способ для сборок командной строки `msbuild` или `xbuild` заключается в добавлении аргумента командной строки `/p:` для установки свойства `IpaPackageDir`. В этом случае обратите внимание, что `msbuild` не развертывает выражения `$()`, передаваемые в командную строку, поэтому использовать синтаксис `$(OutputPath)` нельзя. Вместо этого необходимо предоставить полный путь. Команда Mono `xbuild` развертывает выражения `$()`, однако по-прежнему рекомендуется использовать полный путь к файлу, поскольку в конечном итоге в последующих выпусках `xbuild` устареет и уступит место [кроссплатформенной версии `msbuild`](http://www.mono-project.com/docs/about-mono/releases/4.4.0/#msbuild-preview-for-os-x). Полный пример, в котором используется этот подход, в ОС Windows может выглядеть следующим образом:

```bash
msbuild /p:Configuration="Release" /p:Platform="iPhone" /p:ServerAddress="192.168.1.3" /p:ServerUser="macuser" /p:IpaPackageDir="%USERPROFILE%\Builds" /t:Build SingleViewIphone1.sln
```

В Mac он будет иметь следующий вид:

```bash
xbuild /p:Configuration="Release" /p:Platform="iPhone" /p:IpaPackageDir="$HOME/Builds" /t:Build SingleViewIphone1.sln
```

После того как была создана и архивирована сборка для распространения, все готово для отправки приложения в iTunes Connect.

### <a name="automatically-copy-app-bundles-back-to-windows"></a>Автоматическое обратное копирование пакетов приложений в Windows

[!include[](~/ios/includes/copy-app-bundle-to-windows.md)]

## <a name="submitting-your-app-to-apple"></a>Отправка приложения в Apple

> [!NOTE]
> Недавно компания Apple изменила процесс проверки приложений для iOS. Теперь приложения, в IPA-файл которых входит `iTunesMetadata.plist`, могут отклоняться. Если вы столкнулись с ошибкой `ERROR: ERROR ITMS-90047: "Disallowed paths ( "iTunesMetadata.plist" ) found at: Payload/iPhoneApp1.app"`, для ее устранения можно попробовать обходной способ, описанный [здесь](https://forums.xamarin.com/discussion/40388/disallowed-paths-itunesmetadata-plist-found-at-when-submitting-to-app-store/p1).

После создания сборки для распространения все готово к тому, чтобы отправить ваше приложение для iOS на проверку в Apple и выпустить его в App Store.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio для Mac](#tab/vsmac)

 Выполните следующие действия:

1. Запустите **Xcode**.
2. В меню **Window** (Окно) выберите **Organizer** (Организатор).
3. Перейдите на вкладку **Archives** (Архивы) и выберите архив, который был построен ранее:

    ![](publishing-to-the-app-store-images/publishxs01.png "Выбор архива для отправки")
4. Нажмите кнопку **Validate** (Проверить).
5. Выберите учетную запись, для которой будет проведена проверка, и нажмите кнопку **Choose** (Выбрать):

    ![](publishing-to-the-app-store-images/publishxs02.png "Выбор учетной записи для проверки")
6. Нажмите кнопку **Validate** (Проверить):

    ![](publishing-to-the-app-store-images/publishxs03.png "Диалоговое окно сведений о файле")
7. Будут показаны любые возникшие проблемы с пакетом.
8. Исправьте все ошибки и снова постройте архив в Visual Studio для Mac.
9. Нажмите кнопку **Submit** (Отправить).
10. Выберите учетную запись, для которой будет проведена проверка, и нажмите кнопку **Choose** (Выбрать):

    ![](publishing-to-the-app-store-images/publishxs04.png "Выбор учетной записи для проверки")
11. Нажмите кнопку **Submit** (Отправить):

    ![](publishing-to-the-app-store-images/publishxs05.png "Диалоговое окно сведений о файле")
12. По завершении загрузки файла в iTunes Connect в Xcode появится соответствующее сообщение.


Рабочий процесс архивирования в Visual Studio для Mac автоматически откроет загрузчик приложений после сохранения _IPA_-файла:

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Для отправки приложений на проверку в Apple используется загрузчик приложений. Выполните следующие действия на узле сборки Mac. Копию загрузчика приложений можно скачать [здесь](https://itunesconnect.apple.com/apploader/ApplicationLoader_3.0.dmg).

-----

1. Щелкните *Deliver Your App* (Доставить приложение) и нажмите кнопку *Choose* (Выбрать):

    [![](publishing-to-the-app-store-images/publishvs01.png "Выбор команды "Доставить приложение"")](publishing-to-the-app-store-images/publishvs01.png#lightbox)

2. Выберите ранее созданный ZIP- или IPA-файл и нажмите кнопку **OK**.

3. Загрузчик приложения выполнит проверку файла:

    [![](publishing-to-the-app-store-images/publishvs02.png "Экран проверки")](publishing-to-the-app-store-images/publishvs02.png#lightbox)
4. Нажмите кнопку *Next* (Далее). Приложение будет проверено на соответствие требованиям App Store:

    [![](publishing-to-the-app-store-images/publishvs03.png "Проверка на соответствие требованиям App Store")](publishing-to-the-app-store-images/publishvs03.png#lightbox)
5. Нажмите кнопку **Send** (Отправить), чтобы отправить приложение на проверку в компанию Apple.
6. После успешной загрузки появится соответствующее сообщение загрузчика приложений.

## <a name="itunes-connect-status"></a>Статус iTunes Connect

Если вы войдете в iTunes Connect и выберете свое приложение в списке доступных, в iTunes Connect должен отображаться статус **Waiting for Review** (Ожидается проверка) или временный статус **Upload Received** (Файлы загружены) на время обработки:

[![](publishing-to-the-app-store-images/image21.png "Состояние ожидания проверки в iTunes Connect")](publishing-to-the-app-store-images/image21.png#lightbox)

## <a name="summary"></a>Сводка

В этой статье приводятся пошаговые инструкции по настройке, построению и отправке приложения для публикации в App Store. Сначала рассматриваются действия по созданию и установке профиля подготовки распространения. Затем описывается создание сборки для распространения с помощью Visual Studio и Visual Studio для Mac. В заключение рассказывается о том, как использовать iTunes Connect и средство для отправки приложения в App Store.


## <a name="related-links"></a>Связанные ссылки

- [Работа с образами](~/ios/app-fundamentals/images-icons/index.md)
- [Руководство по разработке приложений iOS. Распространение приложений](http://developer.apple.com/library/ios/#documentation/Xcode/Conceptual/ios_development_workflow/35-Distributing_Applications/distributing_applications.html)
- [Советы по отправке в App Store](https://developer.apple.com/appstore/resources/submission/tips.html)
- [Частые причины отклонения приложений](https://developer.apple.com/app-store/review/rejections/)
- [Руководство по оценке приложений App Store](https://developer.apple.com/appstore/resources/approval/guidelines.html)
