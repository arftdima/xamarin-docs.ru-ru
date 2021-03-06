---
title: Стили устройства
description: Xamarin.Forms включает шесть динамические стили, известный как стили устройства, в классе Device.Styles.
ms.prod: xamarin
ms.assetid: 7FF19ED1-0822-4238-9435-AD970317A2F8
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/17/2016
ms.openlocfilehash: c52de431faa8e6d17b281ece87c862a49d30e886
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="device-styles"></a>Стили устройства

_Xamarin.Forms включает шесть динамические стили, известный как стили устройства, в классе Device.Styles._

*Устройства* стили:

- [`BodyStyle`](https://developer.xamarin.com/api/field/Xamarin.Forms.Device+Styles.BodyStyle/)
- [`CaptionStyle`](https://developer.xamarin.com/api/field/Xamarin.Forms.Device+Styles.CaptionStyle/)
- [`ListItemDetailTextStyle`](https://developer.xamarin.com/api/field/Xamarin.Forms.Device+Styles.ListItemDetailTextStyle/)
- [`ListItemTextStyle`](https://developer.xamarin.com/api/field/Xamarin.Forms.Device+Styles.ListItemTextStyle/)
- [`SubtitleStyle`](https://developer.xamarin.com/api/field/Xamarin.Forms.Device+Styles.SubtitleStyle/)
- [`TitleStyle`](https://developer.xamarin.com/api/field/Xamarin.Forms.Device+Styles.TitleStyle/)

Все шесть стили могут применяться только к [ `Label` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Label/) экземпляров. Например `Label` , отображается текст абзаца может установить его [ `Style` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.Style/) свойства [ `BodyStyle` ](https://developer.xamarin.com/api/field/Xamarin.Forms.Device+Styles.BodyStyle/).

В следующем примере кода показано использование *устройства* стили в XAML-страницы:

```xaml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms" xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml" x:Class="Styles.DeviceStylesPage" Title="Device" Icon="xaml.png">
    <ContentPage.Resources>
        <ResourceDictionary>
            <Style x:Key="myBodyStyle" TargetType="Label"
              BaseResourceKey="BodyStyle">
                <Setter Property="TextColor" Value="Accent" />
            </Style>
        </ResourceDictionary>
    </ContentPage.Resources>
    <ContentPage.Content>
        <StackLayout Padding="0,20,0,0">
            <Label Text="Title style"
              Style="{DynamicResource TitleStyle}" />
            <Label Text="Subtitle text style"
              Style="{DynamicResource SubtitleStyle}" />
            <Label Text="Body style"
              Style="{DynamicResource BodyStyle}" />
            <Label Text="Caption style"
              Style="{DynamicResource CaptionStyle}" />
            <Label Text="List item detail text style"
              Style="{DynamicResource ListItemDetailTextStyle}" />
            <Label Text="List item text style"
              Style="{DynamicResource ListItemTextStyle}" />
            <Label Text="No style" />
            <Label Text="My body style"
              Style="{StaticResource myBodyStyle}" />
        </StackLayout>
    </ContentPage.Content>
</ContentPage>
```

Стили устройства связаны с помощью `DynamicResource` расширения разметки. Динамическая природа стилей можно увидеть в iOS, изменив **специальных возможностей** параметры для размера текста. Внешний вид *устройства* стили отличается для каждой платформы, как показано на следующем снимке экрана:

![](device-images/device-styles.png "Стили устройства для каждой платформы")

*Устройство* стили также могут быть производными от, задав [ `BaseResourceKey` ](https://developer.xamarin.com/api/property/Xamarin.Forms.Style.BaseResourceKey/) свойства имени ключа для стиля устройства. В приведенном выше примере кода `myBodyStyle` наследует от [ `BodyStyle` ](https://developer.xamarin.com/api/field/Xamarin.Forms.Device+Styles.BodyStyle/) и задает цвет текста с диакритическими знаками. Дополнительные сведения о наследовании динамического стиля см [динамического наследования стиля](~/xamarin-forms/user-interface/styles/dynamic.md#dynamic-style-inheritance).

В следующем примере кода показаны в эквивалентную страницу в C#:

```csharp
public class DeviceStylesPageCS : ContentPage
{
    public DeviceStylesPageCS ()
    {
        var myBodyStyle = new Style (typeof(Label)) {
            BaseResourceKey = Device.Styles.BodyStyleKey,
            Setters = {
                new Setter {
                    Property = Label.TextColorProperty,
                    Value = Color.Accent
                }
            }
        };

        Title = "Device";
        Icon = "csharp.png";
        Padding = new Thickness (0, 20, 0, 0);

        Content = new StackLayout {
            Children = {
                new Label { Text = "Title style", Style = Device.Styles.TitleStyle },
                new Label { Text = "Subtitle style", Style = Device.Styles.SubtitleStyle },
                new Label { Text = "Body style", Style = Device.Styles.BodyStyle },
                new Label { Text = "Caption style", Style = Device.Styles.CaptionStyle },
                new Label { Text = "List item detail text style",
                  Style = Device.Styles.ListItemDetailTextStyle },
                new Label { Text = "List item text style", Style = Device.Styles.ListItemTextStyle },
                new Label { Text = "No style" },
                new Label { Text = "My body style", Style = myBodyStyle }
            }
        };
    }
}
```

[ `Style` ](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.Style/) Каждого экземпляра [ `Label` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Label/) экземпляр имеет значение соответствующего свойства из [ `Devices.Styles` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Device+Styles/) класса.

## <a name="accessibility"></a>Специальные возможности

*Устройства* стили учитывают параметры расширенного доступа и размеры шрифтов меняется, как изменяются параметры расширенного доступа для каждой платформы. Таким образом, чтобы обеспечить поддержку текста, доступен, убедитесь, что *устройства* стили используются в качестве основы для любой стили текста в приложении.

Следующих снимках экрана демонстрируют стили устройства на каждой платформе с наименьшим размером доступного шрифта.

[![](device-images/minimum-size.png "Стили доступны небольшое устройство на каждой платформе")](device-images/minimum-size-large.png#lightbox "стили доступны небольшое устройство на каждой платформе")

Следующих снимках экрана показано стили устройства на каждой платформе с максимальный размер шрифта доступны:

![](device-images/maximum-size.png "Стили доступного больших устройства для каждой платформы")

## <a name="summary"></a>Сводка

Xamarin.Forms включает шесть *динамическое* стили, известный как *устройства* стили в [ `Devices.Styles` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Device+Styles/) класса. Все шесть стили могут применяться только к [ `Label` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Label/) экземпляров.


## <a name="related-links"></a>Связанные ссылки

- [Стили текста](~/xamarin-forms/user-interface/text/styles.md)
- [Расширения разметки XAML](~/xamarin-forms/xaml/xaml-basics/xaml-markup-extensions.md)
- [Динамические стили (пример)](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Styles/DynamicStyles/)
- [Работа со стилями (пример)](https://developer.xamarin.com/samples/xamarin-forms/WorkingWithStyles/)
- [Device.Styles](https://developer.xamarin.com/api/type/Xamarin.Forms.Device+Styles/)
- [ResourceDictionary](https://developer.xamarin.com/api/type/Xamarin.Forms.ResourceDictionary/)
- [Style](https://developer.xamarin.com/api/type/Xamarin.Forms.Style/)
- [Setter](https://developer.xamarin.com/api/type/Xamarin.Forms.Setter/)
