---
title: Значок App Store
description: Это статье рассматриваются включая и управлении ресурса изображения в приложении Xamarin.iOS для использования в качестве значка приложения магазина.
ms.prod: xamarin
ms.assetid: BFB5665A-F557-46E1-B35E-870CC2026AD9
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 09/26/2017
ms.openlocfilehash: f8d993ccb23817e237b9cef8074b881f3ea4b3a2
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="app-store-icon"></a>Значок App Store

_Это статье рассматриваются включая и управлении ресурса изображения в приложении Xamarin.iOS для использования в качестве значка приложения магазина._

Прежде чем Xcode 9 все значки магазина были добавлены через iTunes Connect. Однако это не так. Значки магазина приложений теперь должен быть включен как часть вашего проекта пакета и добавляются в каталоге активов. Приложения, которые не содержат значок App Store, будут отклонены Apple.

Значок хранилища, приложения, приложения для пользователей, поэтому он должен быть запоминающимися и отображает их также в небольшой размер циферблата. Чтобы хорошо запоминаться, значок должен быть понятным, простым и легко узнаваемым.

При разработке значка приложения компания Apple рекомендует придерживаться указанных ниже правил:

- Значок должен соответствовать приложению.
- Создайте простой значок, который согласуется с оформлением приложения.
- Не используйте слова на значке.
- Мыслите глобально: один и тот же значок приложения будет использоваться во всех странах, где распространяется приложение.

В качестве значка приложения, отображаемого в App Store, требуется изображение размером 1024 x 1024 пикселей.  В соответствии с требованиями Apple значок App Store в каталоге ресурсов не может быть прозрачным и не должен содержать альфа-канал.

Дополнительные сведения см. в разделе Apple [iOS рекомендациям по интерфейсам](https://developer.apple.com/ios/human-interface-guidelines/icons-and-images/image-size-and-resolution/).

## <a name="adding-an-app-store-icon"></a>Добавление значка App Store

Значки приложения Store на данный момент предоставляются в каталоге ресурсов. 

Чтобы добавить значок магазина выполните следующее:

1. Найдите **AppIcon** задание изображения в **Assets.xcassets** файла проекта. 
    - Должен содержать все новые проекты **Assets.xcassets** файл, содержащий набор AppIcon изображения.
    - Чтобы добавить новый каталог активов, щелкните правой кнопкой мыши проект и выберите пункт **Добавить > новый файл > каталога активов**.
    - Чтобы добавить новый набор изображение значка приложения, щелкните правой кнопкой мыши в области набор значок и выберите **значки приложений & запуска изображений > новый значок приложения**:
    
    ![Добавьте новый параметр set изображения](app-store-icon-images/image1.png)

2. Перейдите к пункту **App Store** значка в списке:

    ![Значок App Store](app-store-icon-images/image2.png)

3. Щелкните значок и найдите изображение 1024 x 1024 пикселей. Сохраните каталога активов.




## <a name="related-links"></a>Связанные ссылки

- [Управление значки с каталогами активов](~/ios/app-fundamentals/images-icons/app-icons.md#managing)
