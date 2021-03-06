---
title: Сжатие макета
description: Макет сжатия удаляет указанный макеты из визуального дерева с целью повышения производительности отрисовки страницы. В этой статье объясняется, как включить сжатие макета и преимуществах, которые можно было подключить его.
ms.prod: xamarin
ms.assetid: da9e1b26-9d31-4762-94c3-4039f306b7f2
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 12/13/2017
ms.openlocfilehash: 9c698d539ab671ee2a033ae5943a46e0cc870f76
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="layout-compression"></a>Сжатие макета

_Макет сжатия удаляет указанный макеты из визуального дерева с целью повышения производительности отрисовки страницы. В этой статье объясняется, как включить сжатие макета и преимуществах, которые можно было подключить его._

## <a name="overview"></a>Обзор

Xamarin.Forms выполняет макета с помощью двух рядов рекурсивных вызовов метода.

- Макет начинается в верхней части визуального дерева, страница, и он проходит через все ветви визуального дерева для охвата каждого визуального элемента на странице. Для изменения размеров и положения их дочерние элементы относительно сами отвечают элементы, которые являются родительскими для других элементов.
- Недействительность — это процесс, с помощью которого изменения в элемент на странице запускает новый цикл макета. Элементы считаются недопустимыми, если они больше не имеют неподходящий размер или положение. Каждого элемента в визуальное дерево дочерних элементов является оповещение при изменении одного из его дочерних элементов размеры. Таким образом изменения в размере элемента в визуальное дерево может привести к изменения, которые ripple вверх по дереву.

Дополнительные сведения о Xamarin.Forms выполнение макета. в разделе [Создание пользовательский макет](~/xamarin-forms/user-interface/layouts/custom.md).

В результате процесса макет — это иерархия собственные элементы управления. Тем не менее эта иерархия включает контейнер дополнительные модули подготовки отчетов и оболочки для модулей подготовки отчетов платформы, дальнейшей дало бы ошибку представление иерархии вложенности. Чем выше уровень вложенности, тем больший объем работы, Xamarin.Forms должен выполнить для отображения страницы. Для сложных макетов Просмотр иерархии может быть глубокие и широкие с несколькими уровнями вложенности.

Например рассмотрим следующую кнопку из образца приложения для входа в Facebook.

![](layout-compression-images/facebook-button.png "Кнопка Facebook")

Эта кнопка указывается как пользовательский элемент управления со следующей иерархии представление XAML:

```xaml
<ContentView ...>
    <StackLayout>
        <StackLayout ...>
            <AbsoluteLayout ...>
                <Button ... />    
                <Image ... />
                <Image ... />
                <BoxView ... />
                <Label ... />
                <Button ... />
            </AbsoluteLayout>
        </StackLayout>
        <Label ... />
    </StackLayout>    
</ContentView>
```

Можно проверить в итоге иерархия вложенное представление с [Xamarin инспектора](~/tools/inspector/index.md). В Android вложенное представление иерархии содержит 17 представления:

![](layout-compression-images/no-compression.png "Просмотр иерархии для кнопки Facebook")

Сжатие макета, которая доступна для Xamarin.Forms приложений для iOS и Android платформ, стремится одноуровневые вложение, удалив указанный макеты из визуального дерева, что может повысить производительность отрисовки страницы представления. Выигрыш в производительности, который доставляется зависит от сложности страницы, версию используемой операционной системы и устройства, на котором выполняется приложение. Однако наиболее заметное повышение производительности будет наблюдаться на старых устройствах.

> [!NOTE]
> Хотя данная статья посвящена результаты применения сжатия макета на Android, равной мере применимы к iOS.

## <a name="layout-compression"></a>Сжатие макета

В языке XAML, можно включить сжатие макета, задав `CompressedLayout.IsHeadless` присоединенному свойству `true` макет класса:

```xaml
<StackLayout CompressedLayout.IsHeadless="true">
  ...
</StackLayout>   
```

Кроме того, его можно включить в C#, указав в качестве первого аргумента экземпляр макета `CompressedLayout.SetIsHeadless` метод:

```csharp
CompressedLayout.SetIsHeadless(stackLayout, true);
```

> [!IMPORTANT]
> Поскольку макет сжатия удаляет макет из визуального дерева, не подходит для макеты, имеют внешний вид, или, получите сенсорный ввод. Таким образом, макеты, задать [ `VisualElement` ](https://developer.xamarin.com/api/type/Xamarin.Forms.VisualElement/) свойства (такие как [ `BackgroundColor` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.BackgroundColor/), [ `IsVisible` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.IsVisible/), [ `Rotation` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.Rotation/), [ `Scale` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.Scale/), [ `TranslationX` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.TranslationX/) и [ `TranslationY` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.TranslationY/)) или, которые принимают жесты, не подходят для макета сжатие. Тем не менее Включение сжатия макета в макете, задает свойства внешнего вида или которая принимает жесты, не приведет к ошибке построения или выполнения. Вместо этого применяется сжатие макет и внешний вид свойства и распознавания жестов, выполняться не будут.

Для кнопки Facebook сжатие макета можно включить классы три макета:

```xaml
<StackLayout CompressedLayout.IsHeadless="true">
    <StackLayout CompressedLayout.IsHeadless="true" ...>
        <AbsoluteLayout CompressedLayout.IsHeadless="true" ...>
            ...
        </AbsoluteLayout>
    </StackLayout>
    ...
</StackLayout>  
```

На Android это приведет к вложенное представление иерархии 14 представлений:

![](layout-compression-images/layout-compression.png "Просмотр иерархии для Facebook кнопки со сжатием макета")

По сравнению с исходной иерархии вложенное представление 17 представлений, это значение представляет уменьшение число просмотров % 17. Уменьшение может показаться незначащие, снижая представления по всей страницы может быть более существенным.

### <a name="fast-renderers"></a>Быстрые отрисовщики

Быстрый модулей подготовки отчетов снизить расширению и затраты на отрисовку элементов управления Xamarin.Forms на Android, выравнивание в итоге иерархия собственного представления. Это еще больше повышает производительность, создав меньше объектов, который в свою очередь приводит к менее сложные визуального дерева, а также сократить использование памяти. Дополнительные сведения о быстрой модулей подготовки отчетов см. в разделе [быстрого модулей подготовки отчетов](~/xamarin-forms/internals/fast-renderers.md).

Для кнопки Facebook в демонстрационном приложении объединение макета сжатия и быстро модулей подготовки отчетов выводит вложенное представление иерархии 8 представлений:

![](layout-compression-images/layout-compression-with-fast-renderers.png "Просмотр иерархии для Facebook кнопки со сжатием макета и быстро модулей подготовки отчетов")

По сравнению с исходной иерархии вложенное представление 17 представлений, это значение представляет сокращение % 52.

Образец приложения содержит страницы, извлеченные из реальных приложений. Без сжатия макета и быстро модулей подготовки отчетов страницы выводятся вложенное представление иерархии 130 представлений на Android. Включение быстрого модулей подготовки отчетов и сжатие макета в классах соответствующий макет уменьшает вложенное представление иерархии 70 представлениям, снижая 46%.

## <a name="summary"></a>Сводка

Макет сжатия удаляет указанный макеты из визуального дерева с целью повышения производительности отрисовки страницы. В этом случае рост производительности зависит от сложности страницы, версии используемой операционной системы и устройства, на котором выполняется приложение. Однако наиболее заметное повышение производительности будет наблюдаться на старых устройствах.


## <a name="related-links"></a>Связанные ссылки

- [Создание пользовательского макета](~/xamarin-forms/user-interface/layouts/custom.md)
- [Быстрые отрисовщики](~/xamarin-forms/internals/fast-renderers.md)
- [LayoutCompression (пример)](https://developer.xamarin.com/samples/xamarin-forms/userinterface/layoutcompression/)
