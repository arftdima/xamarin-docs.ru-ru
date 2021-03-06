---
title: Общие сведения о эффекты
description: Эффекты позволяют собственные элементы управления на каждой платформе, которую нужно изменить и обычно используются для изменения небольшой стилей. В этой статье содержатся вводные эффекты, описаны границу между эффекты и пользовательские модули подготовки отчетов и описывает класс PlatformEffect.
ms.prod: xamarin
ms.assetid: 30CB8615-8F39-4762-BDB7-333D2B57D112
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 03/08/2016
ms.openlocfilehash: 598136f43a23070d8bab04c18106738c9e6b0a52
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="introduction-to-effects"></a>Общие сведения о эффекты

_Эффекты позволяют собственные элементы управления на каждой платформе, которую нужно изменить и обычно используются для изменения небольшой стилей. В этой статье содержатся вводные эффекты, описаны границу между эффекты и пользовательские модули подготовки отчетов и описывает класс PlatformEffect._

Xamarin.Forms [страниц, макеты и элементы управления](~/xamarin-forms/user-interface/controls/index.md) предоставляет общий API для описания кросс платформенных мобильных пользовательских интерфейсов. Каждой страницы, макет и элемента управления по-разному отображается на каждой платформе, используя `Renderer` класс, который в свою очередь, создает собственный элемент управления (соответствующий представление Xamarin.Forms), упорядочивает таким образом, на экране и добавляет поведение, заданное в общий код.

Разработчики могут реализовывать пользовательские классы `Renderer` для настройки внешнего вида или работы элемента управления. Однако реализация класса пользовательского средства визуализации для выполнения настройки простого элемента управления чаще всего доступная ответа. Эффекты упростить этот процесс, позволяя собственные элементы управления на каждой платформе проще настраивать.

Эффекты создаются в проекты под конкретные платформы путем создания подкласса `PlatformEffect` элемента управления, а также влияние потребляются присоединив соответствующий элемент управления в проекте Xamarin.Forms Переносимая библиотека классов (PCL) или общую библиотеку.

## <a name="why-use-an-effect-over-a-custom-renderer"></a>Зачем использовать эффект через пользовательское средство отрисовки?

Влияние упростить настройку элемента управления, для повторного использования и могут быть параметризованы для дальнейшего повторного использования.

Все, что может осуществляться с эффектом также может осуществляться с помощью пользовательского средства отрисовки. Однако пользовательские модули подготовки отчетов обеспечивают большую гибкость и настроек, чем эффекты. Приведенный ниже список рекомендаций ситуации, в которой делается Выбор эффекта на пользовательское средство отрисовки:

- При изменении свойств элемента управления платформой достижения нужного результата рекомендуется эффект.
- Пользовательское средство отрисовки является обязательным при необходимости для переопределения методов элемента управления от платформы.
- Пользовательское средство отрисовки является обязательным при необходимости заменить специфический для платформы управления, который реализует элемент управления Xamarin.Forms.

## <a name="subclassing-the-platformeffect-class"></a>Создание подклассов класса PlatformEffect

В следующей таблице перечислены пространства имен для `PlatformEffect` класса для каждой платформы и типов свойств:

|Platform|Пространство имен|Контейнер|Элемент управления|
|--- |--- |--- |--- |
|iOS|Xamarin.Forms.Platform.iOS|UIView|UIView|
|Android|Xamarin.Forms.Platform.Android|Группе ViewGroup|Просмотр|
|Windows Phone 8.1|Xamarin.Forms.Platform.WinRT|FrameworkElement|FrameworkElement|
|Универсальная платформа Windows (UWP)|Xamarin.Forms.Platform.UWP|FrameworkElement|FrameworkElement|

Каждый платформой `PlatformEffect` класс предоставляет следующие свойства:

- `Container` — ссылается на конкретную платформу управления используется для реализации макета.
- `Control` — ссылается на конкретную платформу управления используется для реализации управления Xamarin.Forms.
- `Element` — ссылается на элемент управления Xamarin.Forms, который готовится к просмотру.

Эффекты не имеют тип сведений о контейнера, элемент управления или элемент, которым они присоединены, так как они можно прикрепить к любому элементу. Таким образом при присоединении эффекта на элемент, он не поддерживает должна завершаться или исключение. Тем не менее `Container`, `Control`, и `Element` свойства может быть приведен к типу реализации. Дополнительные сведения об этих типах см. в разделе [подготовки базовых классов и собственные элементы управления](~/xamarin-forms/app-fundamentals/custom-renderer/renderers.md).

Каждый платформой `PlatformEffect` класс предоставляет следующие методы, которые должны быть переопределены для реализации эффект:

- [`OnAttached`](https://developer.xamarin.com/api/member/Xamarin.Forms.Effect.OnAttached()/) — вызывается, когда влияние присоединяется к элементу управления Xamarin.Forms. Переопределения этого метода в каждом классе конкретного платформенный эффект служит для выполнения настройки элемента управления, а также обработка исключений в случае, если результат не может применяться к указанному элементу управления Xamarin.Forms.
- [`OnDetached`](https://developer.xamarin.com/api/member/Xamarin.Forms.Effect.OnDetached()/) — вызывается, когда эффект отсоединяется от управления Xamarin.Forms. Переопределения этого метода в каждом классе эффект от платформы — это место, чтобы выполнить очистку эффект, например Отмена регистрации обработчика событий.

Кроме того `PlatformEffect` предоставляет [ `OnElementPropertyChanged` ](https://developer.xamarin.com/api/member/Xamarin.Forms.PlatformEffect%3CTContainer,TControl%3E.OnElementPropertyChanged/p/System.ComponentModel.PropertyChangedEventArgs/) метод, который может быть переопределен. Этот метод вызывается при изменении свойства элемента. Переопределения этого метода в каждом классе эффект от платформы — это место для реагирования на изменения привязываемые свойства элемента управления Xamarin.Forms. Проверяет наличие измененного свойства должны быть выполнены, как это переопределение может быть вызван несколько раз.


## <a name="related-links"></a>Связанные ссылки

- [Пользовательские отрисовщики](~/xamarin-forms/app-fundamentals/custom-renderer/index.md)
