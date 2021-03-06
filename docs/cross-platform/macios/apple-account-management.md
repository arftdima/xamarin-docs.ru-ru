---
title: Управление учетной записью Apple
ms.prod: xamarin
ms.assetid: 71388B83-699B-4E42-8CBF-8557A4A3CABF
ms.technology: xamarin-cross-platform
author: asb3993
ms.author: amburns
ms.date: 04/05/2017
ms.openlocfilehash: 21af0ef09644f39f9be42788b3d8f4977a2143d3
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="apple-account-management"></a>Управление учетной записью Apple

Интерфейс управления Apple учетной записи позволяет просматривать все команды разработчиков, связанных с идентификатор Apple ID. Он также позволяет просмотреть дополнительные сведения о каждой команды, отображая список _удостоверений подписи_ и _профили подготовки_ , установленных на компьютере.

Проверка подлинности своего идентификатора Apple выполняется в командной строке с [fastlane](https://fastlane.tools/). fastlane должны быть установлены на компьютере необходимо успешно пройти проверку подлинности. Дополнительные сведения о fastlane и его установке, описанные в [fastlane](~/ios/deploy-test/provisioning/fastlane/index.md) руководства.

Учетная запись Apple диалогового окна в Visual Studio для Mac позволяет сделать следующее:

* **Создание и управление сертификатами** 
* **Создание и управление ими профили подготовки** 

Сведения о том, как это сделать, описанные в этом руководстве.

Также можно использовать средства, подписывание пакета iOS для выполнения следующих:

* **Добавить новое удостоверение подписи для существующего профиля** 
* **Подготовка новых устройств** 

Дополнительные сведения об использовании этих функций см. [подготовки устройства](~/ios/get-started/installation/device-provisioning/index.md) руководства.
️
## <a name="requirements"></a>Требования

Управление учетной записью Apple можно найти в Visual Studio для Mac. Он недоступен в Visual Studio для Windows.

Необходимо иметь учетную запись разработчика Apple для использования этой функции. Дополнительные сведения об учетных записях разработчика Apple доступна в [подготовки устройства](~/ios/get-started/installation/device-provisioning/index.md) руководства.

- Убедитесь, что вы подключены к Интернету. Это происходит потому fastlane взаимодействует непосредственно с портала разработчиков Apple.
- Убедитесь в наличии [установлены инструменты fastlane](~/ios/deploy-test/provisioning/fastlane/index.md#Installation).
- Убедитесь, имеются новейшие средства fastlane из [ https://download.fastlane.tools ](https://download.fastlane.tools).
- Прежде чем начать, убедитесь в том принять все лицензионные соглашения в [портал разработчиков](https://developer.apple.com/account/).

## <a name="adding-an-apple-developer-account"></a>Добавление учетной записи разработчика Apple

1. Чтобы открыть диалоговое окно управления учетной записи перейдите на **Visual Studio > Параметры > учетную запись разработчика Apple**:

    ![Параметры учетной записи разработчика Apple](apple-account-management-images/image1.png)

2. Нажмите клавишу **+** кнопки для отображения знака в диалоговом окне, как показано ниже: 

    ![диалоговое окно fastlane.](apple-account-management-images/image2.png)

4. Введите идентификатор Apple ID и пароль и нажмите кнопку **входа** кнопки. Учетные данные будут сохранены в цепочке ключей безопасности на этом компьютере. [fastlane](~/ios/deploy-test/provisioning/fastlane/index.md) позволяет безопасно обрабатывать свои учетные данные и передавать их в портале для разработчиков Apple.
 
5. Выберите **всегда разрешать** на предупреждения диалогового окна, чтобы разрешить Visual Studio используйте свои учетные данные:

    ![](apple-account-management-images/image4.png)

6. После успешного добавления учетной записи, вы увидите идентификатор Apple и командам, идентификатор Apple.

    ![](apple-account-management-images/image5.png)

7. Выберите все группы и нажмите клавишу **подробности...** . Отобразится список всех удостоверений подписи и профили подготовки, которые установлены на компьютере.

    ![](apple-account-management-images/image6.png)


<a name="managing" />


## <a name="managing-signing-identities-and-provisioning-profiles"></a>Управление удостоверениями подписи и профили подготовки

Сведения о диалоговом окне team список удостоверений подписи, упорядоченных по типам. **Состояние** столбец будет указано, является ли сертификат: 

* **Допустимые** — удостоверение подписывания (сертификат и закрытый ключ), установлены на компьютере и не истек.

* **Не в цепочке ключей** — отсутствует допустимое удостоверение подписи на сервере Apple. Для установки на компьютере, его необходимо экспортировать с другого компьютера. Не удается загрузить удостоверение подписи с портала разработчиков Apple, как она не содержит закрытый ключ.

* **Отсутствует закрытый ключ** — в цепочке ключей установлен сертификат без закрытого ключа.

* **Истек срок действия** — истек срок действия сертификата. Вы должны удалить с цепочке ключей.

  ![](apple-account-management-images/image7.png)

## <a name="create-a-signing-identities"></a>Создание удостоверений подписи

Чтобы создать новое удостоверение подписи, выберите **создать новый сертификат** кнопку раскрывающегося списка и выберите нужный тип, который потребуется. При наличии необходимых разрешений новой подписи удостоверений появится через несколько секунд.

Если параметра в раскрывающемся списке серым цветом, а не выбрано, как показано ниже, это означает, что у вас соответствующей команде разрешения на создание такого типа.

![](apple-account-management-images/image8.png)

## <a name="download-provisioning-profiles"></a>Загрузить профили подготовки

Сведения о диалоговом окне team также отображает список всех профилей подготовки, связанных с учетной записью разработчика. Все профили подготовки можно загрузить на локальный компьютер, нажав клавишу **загрузить все профили** кнопки

![](apple-account-management-images/image9.png)

## <a name="ios-bundle-signing"></a>Подписывание пакета iOS

Сведения о развертывании приложения на устройство [подготовки устройства](~/ios/get-started/installation/device-provisioning/index.md) руководства.

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="view-details-dialog-is-empty"></a>Открыть диалоговое окно сведений пуст

В настоящее время это известная проблема, связанная с ошибкой [#53906](https://bugzilla.xamarin.com/show_bug.cgi?id=53906). Убедитесь, что используется последняя стабильная версия Visual Studio для Mac

### <a name="if-you-are-experiencing-issues-logging-in-your-account-please-try-the-following"></a>Если вы испытываете проблемы ведения журналов в учетной записи, попробуйте выполнить следующие:

* Откройте приложение цепочки ключей и в списке категории выберите *пароли*. Поиск `deliver.`и удалите все записи.

### <a name="error-adding-account-please-sign-in-with-an-app-specific-password"></a>«Ошибка при добавлении учетной записи. Выполните вход в систему с паролем конкретного приложения»

Это происходит потому 2 многофакторной проверки подлинности включена в вашей учетной записи. Убедитесь, что используется последняя стабильная версия Visual Studio для Mac

### <a name="failed-to-create-new-certificate"></a>Не удалось создать новый сертификат
«Достигнут предел для сертификатов этого типа»

![](apple-account-management-images/image10.png)

Максимальное допустимое число сертификатов созданы. Чтобы устранить эту проблему, перейдите к [Центр разработчиков Apple](https://developer.apple.com/account/ios/certificate/distribution) и отзовите один из рабочих сертификатов.

## <a name="known-issues"></a>Известные проблемы

* Иногда сведения о представлении диалогового окна может занять слишком много времени для получения удостоверения подписи и профили.
* Часто фокус может не вернуться в Visual Studio для Mac после ввода сведений о своей, вызывая вашей учетной записи не для добавления. Если это так, повторите процесс.
* Профили подготовки, созданные в Visual Studio для Mac, не будут учитывать объемы обслуживания, выбранные в проектах (Entitlements.plist). Эта возможность будет добавлена в будущих версиях интегрированной среды разработки.
* Распространение профилей подготовки будет по умолчанию предназначено для магазина приложений. Собственные или специализированные профили необходимо создавать вручную.
