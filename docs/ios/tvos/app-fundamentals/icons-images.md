---
title: Работа со значками и изображений
description: В этой статье описывается проектирование и работы со значками и изображений в приложении Xamarin.tvOS.
ms.prod: xamarin
ms.assetid: A2DA4347-0563-4C72-A8D7-5B9DE9E28712
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/16/2017
ms.openlocfilehash: c888ecf3d7e0f21734f2b89176eed56bf778dbf9
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="working-with-icons-and-images"></a>Работа со значками и изображений

_В этой статье описывается проектирование и работы со значками и изображений в приложении Xamarin.tvOS._

Создание зрительными значки и изображения являются важной частью разработки впечатляющие опыта для Apple TV приложений. В этом руководстве мы рассмотрим шаги, необходимые для создания и включения необходимых графических ресурсов для приложений Xamarin.tvOS:

- [Запустите изображения](#Launch-Image) -запуск изображение при первом запуске приложения и заменяется на первом экране приложения после запуска.
- [Многоуровневая изображений](#Layered-Images) — для Apple TV, Apple новой работы многоуровневая изображений с эффект фокусировки, чтобы создать объемные эффекты для выбранных элементов. Существует несколько способов [создания образов многоуровневая](#Creating-Layered-Images).
- [Значок приложения](#App-Icons) -значки требуются для экрана не только Apple TV Home, но на App Store. Их должно быть указано как изображение деления.
- [Верхняя Полка изображения](#Top-Shelf-Image) -приложения, помещенного в верхней строке домашний экран, он должен быть образ Полка Top, чтобы ознакомиться с функциями приложения. При необходимости можно предоставить [динамическое содержимое верхнего Полка](#Dynamic-Top-Shelf-Content) для выделения содержимого в приложении.
- [Игры Center изображения](#Game-Center-Images) -Если ваше приложение игры и использует Game Center, требуется несколько дополнительных образов.
- [Установка изображений проекта Xamarin.tvOS](#Setting-Xamarin.tvOS-Project-Images) -рассматриваются действия, необходимые для приложения Xamarin.tvOS установки запустите изображения и значка приложения.

> [!IMPORTANT]
> Все изображения на Apple TV, разрешением 1 x (`@1x`), поэтому вам необходимо _только_ использовать изображения такого размера. В том числе большего размера, более высоким разрешением графика принимать не только время загрузки и использовать больше памяти и хранилища, но они должны быть динамически масштабируется повторно во время выполнения и отрицательно повлиять на производительность отрисовки.

<a name="Launch-Image" />

## <a name="launch-image"></a>Запустите изображения

Изображение запуска первое, что отображается изначально при запуске приложения Xamarin.tvOS Apple TV, и таким образом, каждое приложение tvOS должны предоставить образ запуска. 

Запустите изображения отображается быстро и создает впечатление, что приложение будет быстро и отвечать на запросы. Apple TV заменяет изображение запуска на первом экране приложения вскоре существует после.

Запуск изображения имеют возможность для рекламы или художественного выражения, они существуют только для того, чтобы создать впечатление, что приложение будет быстро запущен и готов для использования.

|Запустите размер изображения|Примечания|
|---|---|
|1920x1080px|Только несколько уровней не PNG-файлы|

Apple вносит следующие рекомендации по проектированию образа запуска приложения:

- **Практически аналогично первый экран** -вашего экрана запуска должно быть как можно ближе к первый экран приложения можно. Включая различных графических или элемента может привести к раздражающих «flash» при первом появлении.
- **Избегайте текста с помощью** -запуска образы являются статическими и таким образом, не будет локализовано до их отображения.
- **Downplay запуска** -Apple TV, так как пользователи часто переключения приложений, не следует обратить внимание на процесс запуска приложения.
- **Без рекламы или продвижения** -ваш образ запуска не должны использоваться как экране или включать любые фирменная символика применяется в статической части первый экран приложения. Реклама запрещено.

<a name="Setting-the-Launch-Image" />

### <a name="setting-the-launch-image"></a>Задание рисунка, запуск

Для установки образа запуска проекта tvOS, выполните следующие действия.

1. В **обозревателе решений**, дважды щелкните `Assets.xcassets` чтобы открыть его для редактирования: 

    [![](icons-images-images/asset01.png "Файл Assets.xcassets")](icons-images-images/asset01.png#lightbox)
2. В **активов редактор**, щелкните на `LaunchImages` активов: 

    [![](icons-images-images/asset02.png "LaunchImages активов")](icons-images-images/asset02.png#lightbox)
3. Щелкните **1 x Apple TV** запись и выберите образ запуска или при необходимости перетащите новый образ из файловой системы: 

    [![](icons-images-images/asset03.png "Выберите образ запуска")](icons-images-images/asset03.png#lightbox)
4. Сохраните изменения.

<a name="Layered-Images" />

## <a name="layered-images"></a>Слоев изображения

Новый для Apple TV, работа многоуровневая изображений с эффект фокусировки, чтобы создать объемные эффекты, помогает сохранить пользователя на диване уме подключенные к содержимому на экране в комнате.

Многоуровневый образы содержат из двух (2) для пяти (5) отдельные слои, которые вместе составляют создания образа. За исключением фон каждый уровень использует его Z-порядка, а также прозрачности для создания иллюзии глубины. Когда пользователь взаимодействует с помощью слоев образа, более высокого уровня, упорядоченные Z масштабируются и overlapped, чтобы создать этот эффект.

[![](icons-images-images/layered01.png "Многоуровневый упорядоченные Z изображений диаграммы")](icons-images-images/layered01.png#lightbox)

> [!IMPORTANT]
> Слоев изображения являются обязательными для приложения значки и не являются обязательными для других [может иметь фокус элементы](~/ios/tvos/app-fundamentals/navigation-focus.md#Focus-and-Selection) (например, изображение Полка верхней). Тем не менее Apple предполагает использование многоуровневая изображений для изображения, можно получить фокус, в приложении.




Apple вносит следующие рекомендации по проектированию многоуровневая изображений:

- **Преобразование непрозрачный фон слой** -уровень фона (уровень 1) **должен** быть непрозрачным или при попытке использовать образ располагаются на Apple TV приведет к ошибке. Другие слои могут содержать несколько уровней прозрачности для улучшения объемные эффекты.
- **Изолировать переднего плана, среднего и фон элементов** -Показательным элементы (например, игры символов) на переднем плане, используйте середины получателей элементов или тени. Наконец включают нейтральный фон для обеспечения этап на верхние уровни.
- **Сохранить текст на переднем плане** — Если не требуется для скрывается более высокие уровни текста обычно он должен быть в верхнего уровня.
- **Использовать простой иерархическое представление** -эффект фокусировки был разработан в качестве слабая поэтому сохраните слоев для минимальной во избежание резать глаз, нереалистичная эффекты.
- **Включать в зону надежный** -так, как верхние уровни может обрезаться во время эффект фокусировки, необходимое для создания границы зоны безопасности в каждом слое. При получении содержимого слишком закрытие края слои, он может стать обрезанные. Верхние уровни могут возникнуть дополнительные масштабирование и кадрирование чем нижних слоев. В разделе [слои изменения размера изображения](#Sizing-Image-Layers) разделе ниже.
- **Предварительный просмотр часто** -многоуровневая изображения для просмотра часто, чтобы убедиться, что желаемого эффекта 3D происходит и что ни один из содержимого на отдельные слои обрезается. Его следует просмотреть многоуровневая изображений на реальном оборудовании Apple TV убедитесь, что они так, как ожидается.

Когда это возможно, следует всегда использовать встроенные `UIKit` элементы управления для отображения изображений многоуровневая, как они автоматически получают эффект фокусировки приходящих фокуса в.

<a name="Sizing-Image-Layers" />

### <a name="sizing-image-layers"></a>Слои изменения размера изображения

Очень важно не забудьте включить _зоны Safe_ границы в каждый слой, на котором намерены многоуровневая изображения. Поскольку отдельные слои можно масштабировать и обрезку во время эффект фокусировки, содержимое слоев могут быть обрезанные при слишком близко к краю слоя:

[![](icons-images-images/layered02.png "границы 35 пикселей")](icons-images-images/layered02.png#lightbox)

<a name="Creating-Layered-Images" />

### <a name="creating-layered-images"></a>Создание слоев изображения

tvOS работает с изображениями, располагаются в следующих форматах:

- **Файлы CAR** -это собственный формат каталога активов, созданная компанией Apple. Не создаются непосредственно файлы АВТОМОБИЛЯ, они создаются во время компиляции из любых файлов LSR и включаются в набора приложений.
- **Образы LSR** -это формат собственный образ, созданная компанией Apple. Используйте [фокусировки экспорта Adobe Photoshop Plugin](https://itunespartner.apple.com/assets/downloads/ParallaxExporter_Apps.zip) или [средство предварительного просмотра фокусировки](http://itunespartner.apple.com/assets/downloads/Parallax%20Previewer.dmg) для создания и предварительного просмотра многоуровневая изображений в формате LSR.
- **Assets.xcassets** — из двух (2) для пяти (5) стандартная `.png` форматированные изображений, включенных в каталоге активов, будут скомпилированы в автомобиль или LSR в формате изображения располагаются во время компиляции.
- **Файлы LCR** -это собственный формат, созданная компанией Apple. LCR файлы предназначены для использования в качестве дополнительного содержимого, загруженные из одного из серверов содержимого. LCR файл никогда не должен включаться в набора приложений. LCR файлы, создаваемые файлы LSR или Photoshop с помощью `layerutil` средства командной строки, включенная в Xcode.

<a name="The-Parallax-Previewer" />

### <a name="the-parallax-previewer"></a>Средство предварительного просмотра фокусировки

Apple создан [средство предварительного просмотра фокусировки](http://itunespartner.apple.com/assets/downloads/Parallax%20Previewer.dmg) для предварительного просмотра и созданный многоуровневая изображения, необходимые для приложения значков и дополнительных элементов может иметь фокус. Средство предварительного просмотра показывает каждый слой, формирующая завершенного образа многоуровневая:

[![](icons-images-images/layered03.png "Средство предварительного просмотра фокусировки")](icons-images-images/layered03.png#lightbox)

В режиме предварительного просмотра многоуровневая изображения, можно использовать мышь Поворот изображения и просмотреть эффект фокусировки. Используйте **+** (плюс) и **-** (кнопки для добавления и удаления слои минус).

При создании нового образа многоуровневая, его можно экспортируются в формате LSR и включенные в пакет приложения.

Дополнительные сведения о создании и предварительного просмотра многоуровневая образов см. в разделе Apple [Создание иллюстрации фокусировки](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/CreatingParallaxArtwork.html#//apple_ref/doc/uid/TP40015241-CH19-SW1) раздел [приложения руководство по программированию для tvOS](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/).

<a name="App-Icons" />

## <a name="app-icons"></a>Значки приложений

Приложение Xamarin.tvOS потребует не только значка приложения для Apple TV начального экрана, но и значок для магазина приложений. Значок приложения — первого измените значительные впечатление на потенциальных пользователей и необходимо связаться цели приложения с одного взгляда.

[![](icons-images-images/icon01.png "Значок приложения")](icons-images-images/icon01.png#lightbox)

Все приложения должны предоставить небольшого и большой версии его значка приложения. Мелкий значок будет использоваться для Apple TV начального экрана при установке приложения. Большой версии используется App Store. Большой значок приложения должен имитировать внешний вид версии маленького значка.

|Маленький значок||Крупные значки||
|---|---|---|---|
|Фактический размер|400x240px|Размер|1280x768px|
|Размер зоны безопасности|370x222px|||
|Размер без фокуса ввода|300x180px|||
|Размер фокусом ввода|370x222px|||

> [!IMPORTANT]
> Значки приложения должно быть предоставлено как **многоуровневая изображения**. См. в разделе [многоуровневая изображения](#Layered-Images) Дополнительные сведения см в разделе выше.




Компания Apple предоставляет следующие рекомендации по созданию значки приложения:

- **Укажите одну точку фокус** — значка с точкой фокуса одного конструктора, расположенного непосредственно в центре значка.
- **Простой фон** — усложнять фон значка, чтобы выделить верхние уровни. Рекомендуется использовать простые цвета или слабая градиента.
- **Ограничить объем текста** — так как имя приложения появится под значком, при этом пользователь, необходимо включать только текст при очень важно для проектирования значка.
- **Не используйте снимки экрана** — снимки экрана слишком сложны для значка и запретить пользователю видеть намерение приложения с одного взгляда.
- **Квадратные значки Keep** — tvOS автоматически применяет маску, которая слегка округление углов значки. Не включайте округление самостоятельно.
- **Тщательно Your слои разделения** — текст должен быть в правом верхнем большинство слой, вторичный элементов в середине и нейтральный фон, позволяющий на верхние уровни для освещения.
- **Используйте градиенты и Shadows тщательно** — градиенты и тени может пересекаться с эффект фокусировки, их следует использовать осторожно. Простой сверху вниз, лучше всего работают градиента стили светлого к темному. Shadows обычно работают лучше всего, как оттенки острый, с.
- **Изменять прозрачность слоя** — использование различных уровней прозрачности на верхние уровни значка вашего приложения для увеличения объемные эффекты. Фон должен быть непрозрачным или процесс завершится ошибкой.

<a name="Setting-the-App-Icons" />

### <a name="setting-the-app-icons"></a>Настройка значков приложения

Задаваемое значков приложения, необходимые для проекта tvOS, выполните следующие действия.

1. В **обозревателе решений**, дважды щелкните `Assets.xcassets` чтобы открыть его для редактирования: 

    [![](icons-images-images/asset01.png "Assets.xcassets fileg")](icons-images-images/asset01.png#lightbox)
2. В **активов редактор**, разверните `App Icon & Top Shelf Image` активов: 

    [![](icons-images-images/asset04.png "Разверните узел ресурса изображения Полка Top")](icons-images-images/asset04.png#lightbox)
3. Далее разверните `App Icon - Small` активов: 

    [![](icons-images-images/asset05.png "Разверните значок приложения — небольшой активов")](icons-images-images/asset05.png#lightbox)
4. Разверните `Back` активов и нажмите кнопку `Contents` входа: 

    [![](icons-images-images/asset06.png "Разверните активов назад")](icons-images-images/asset06.png#lightbox)
5. Щелкните **1 x Apple TV запись** и выберите файл изображения.
6. Повторите описанные выше шаги для `Front` и `Middle` активы.
7. Повторите эти шаги, чтобы определить `App Icon - Large` активов.
4. Сохраните изменения.

<a name="Top-Shelf-Image" />

## <a name="top-shelf-image"></a>Изображение верхняя Полка

Если отправки Xamarin.tvOS приложения в верхней строке на Apple TV начального экрана, при выборе пользователем приложения будет отображаться большое изображение Полка верхней. Этот образ необходимо ознакомиться с функциями приложения или прямых ссылок на содержимое.

[![](icons-images-images/topshelf01.png "Пример верхнего изображения Полка")](icons-images-images/topshelf01.png#lightbox)

Изображение сверху Полка либо могут быть предоставлены как один статический `.png` или `.lsr` файл (см. [создание образов многоуровневая](#Creating-Layered-Images)) или его можно создать динамически во время выполнения как одна строка может иметь фокус элементов (см. [ Содержимое динамического верхняя Полка](#Dynamic-Top-Shelf-Content) ниже).

|Размер образа верхняя Полка|Примечания|
|---|---|
|1920x720px|Статические PNG или многоуровневый .lsr файла|

Apple предоставляет следующие рекомендации по созданию изображений Полка верхней.

- **Используйте статические изображения Rich** — Если приложение не предоставляет динамическое содержимое, его верхней Полка изображение будет иметь не может иметь фокус. Используйте это изображение, чтобы ознакомиться с функциями приложения или фирменного стиля.
- **Ссылку на содержимое приложения** — динамических макетов Полка верхней обеспечивают быструю ссылку на содержимое, которое пользователь находит наиболее важных для вашего приложения. Используйте эту область для предоставления быструю ссылку, чтобы запустить приложение и немедленно переход заданного содержимого.
- **Продемонстрировать последнее содержимое** — Полка верхней Rich содержимое можно нарисовать пользователя в приложение и сделать их требуется использовать дополнительные. Используется как область для демонстрации высокий рейтингом или новейшие содержимого.
- **Содержимое с общими** — их наиболее часто используемые месте пользователей или избранных приложений в верхней строке экрана домашней страницы. Полка Top используется для отображения содержимого, которые могли бы быть всего его интересуют.
- **Реклама запрещено** — рекламы запрещено не будет отображаться в верхней полках. Может показать последние предлагаемые для продажи содержимое, но не сведения о ценах должны отображаться.

### <a name="setting-the-top-shelf-image"></a>Изображение верхняя Полка

Для установки образа Полка верхней, необходимые для проекта tvOS, выполните следующие действия.

1. В **обозревателе решений**, дважды щелкните `Assets.xcassets` чтобы открыть его для редактирования: 

    [![](icons-images-images/asset01.png "Файл Assets.xcassets")](icons-images-images/asset01.png#lightbox)
2. В **активов редактор**, разверните `App Icon & Top Shelf Image` активов: 

    [![](icons-images-images/asset04.png "Разверните узел ресурса изображения Полка Top")](icons-images-images/asset04.png#lightbox)
3. Щелкните `Top Shelf Image` активов: 

    [![](icons-images-images/asset07.png "Изображение сверху Полка")](icons-images-images/asset07.png#lightbox)
5. Щелкните **1 x Apple TV запись** и выберите файл изображения.
6. Сохраните изменения.

<a name="Dynamic-Top-Shelf-Content" />

### <a name="dynamic-top-shelf-content"></a>Верхняя полка, динамического содержимого

Вместо отображения статическое изображение Полка верхней, Полка Top может содержать динамические строки [может иметь фокус элементы](~/ios/tvos/app-fundamentals/navigation-focus.md#Focus-and-Selection) или динамический набор прокрутки ленты. Оба эти динамические стиля позволяют выделить содержимое, предоставляемый приложением или переход в наиболее часто используемыми функциями.

<a name="Sectioned-Content-Row" />

#### <a name="sectioned-content-row"></a>Разделенных содержимое строки

Этот тип динамического содержимого Полка верхней представляется одной строке прокрутки, может иметь фокус элементов при необходимости разбить на разделы. Он обычно используется для выделения новых, избранных или недавно просмотренных содержимого приложения.

Содержимое представлено в виде единого, горизонтальной прокрутки списка содержимого с подписью, отображающихся в разделе частью содержимое, выбранное (который в настоящий момент фокус). Если пользователь выбирает конкретной части содержимого, приложение будет запущено и их нужно учитывать непосредственно этого содержимого.

Потребуются следующие размеры содержимого:

||Плакат (2:3)|Квадрат (1:1)|ВЫСОКОЙ ЧЕТКОСТИ (16:9)|
|---|---|---|---|
|Фактический размер|404x608px|608x608px|908x512px|
|Размер зоны безопасности|380x570px|570x570px|852x479px|
|Размер без фокуса ввода|333x500px|500x500px|782x440px|
|Размер фокусом ввода|380x570px|570x570px|852x479px|

Компания Apple предоставляет следующие рекомендации для разделенных содержимого строки:

- **Заполнить строку** — должен предоставить достаточно содержимого выводятся на всю ширину экрана.
- **Масштабирование изображений смешанного** — разделенных содержимого строка может содержать сочетание размеров изображения (из списка, приведенные выше). Если размеры изображения следует смешивать тем не менее, следует помнить, что дополнительные масштабирование будет применяться для нормализации отображение содержимого.

<a name="Scrolling-Inset-Banners" />

#### <a name="scrolling-inset-banners"></a>Прокрутка рисуется внутренняя ленты

При необходимости при Полка верхней как автоматически прокрутки и циклов коллекцию объявления, которые почти весь экран Xamarin.tvOS приложения может вызвать его содержимого. Этот стиль обычно используется для демонстрации богатую содержимого, такого как новый ТВ-передачи.

Помимо автоматическая прокрутка, пользователь может получить контроль над заголовков и прокрутки в любом направлении, с помощью удаленного Siri. Внесение небольших, циклические жестов на удаленном Siri, если заголовок находится в фокусе можно активировать эффект фокусировки для этого заголовка.

**Изображение баннера (лишние широкий)**

|   |   |
|---|---|
|Фактический размер|1940x624px|
|Размер зоны безопасности|1740x620px|
|Размер без фокуса ввода|1740x560px|
|Размер фокусом ввода|1740x620px|

Прокрутка рисуется внутренняя ленты можно либо указать статический `.png` или многоуровневая `.lsr` файла.

Apple предоставляет следующие рекомендации для ленты рисуется внутренняя прокрутки.

- **Сумма содержимого** -прокрутка до естественным необходимо обеспечить как минимум три (3) ленты. Должно содержать не более 8 (восьми) ленты или берет на себя навигации жестких для конечного пользователя.
- **Текст содержимого** — Если требуется плаката текста в должны быть включены в изображение баннера. Если используется многоуровневая изображения, текст следует верхнего уровня.

См. в разделе Apple [TVServices Framework ссылки](https://developer.apple.com/library/prerelease/tvos/documentation/TVServices/Reference/TVServices_Ref/index.html#//apple_ref/doc/uid/TP40016412) Дополнительные сведения о добавлении расширение Полка Top в приложение для обеспечения динамического содержимого Полка Top.

<a name="Game-Center-Images" />

## <a name="game-center-images"></a>Образы Game Center

Если вы включили поддержку Game Center Xamarin.tvOS приложения — это игра, потребуются некоторые дополнительные ресурсы изображений:

- **Значки достижение** -непрозрачное изображение является обязательным для каждого успехов, будут автоматически обрезаны в кружке. Достижениях являются элементами, не может иметь фокус.
- **Панель мониторинга иллюстрации** -Необязательное изображение может быть предоставленный, которые появятся в верхней части панели мониторинга вашего приложения в Game Center. Эти образы являются не может иметь фокус.
- **Таблица лидеров иллюстрации** -необходимо указать между один (1) до трех (3) изображений соотношение сторон 16:9 для каждой Таблица лидеров, поддерживаемого приложением. Это может быть либо статическими `.png` или многоуровневая `.lsr` файлов. Таблица лидеров иллюстрации может получать фокус.

||Достижение значков|Иллюстрации панели мониторинга|Таблица лидеров иллюстрации|
|---|---|---|---|
|Отображается размер|200x200px|923x150px|Н/Д|
|Фактический размер|320x320px|Н/Д|659x371px|
|Размер зоны безопасности|Н/Д|Н/Д|618x348px|
|Размер без фокуса ввода|Н/Д|Н/Д|548x309px|
|Размер фокусом ввода|Н/Д|Н/Д|618x348px|

Дополнительные сведения о работе с Game Center см. в разделе Apple [руководство по программированию Game Center](https://developer.apple.com/library/prerelease/tvos/documentation/NetworkingInternet/Conceptual/GameKit_Guide/Introduction/Introduction.html).

<a name="Working-with-Images" />

## <a name="working-with-images"></a>Работа с образами

Поскольку tvOS 9 — это подмножество iOS 9, же методы, используемые для включения и отображения изображений в приложении Xamarin.iOS, также работают для Xamarin.tvOS приложения. См. в нашем [отображения изображения](~/ios/app-fundamentals/images-icons/displaying-an-image.md) Дополнительные сведения см.

<a name="Setting-Xamarin.tvOS-Project-Images" />

## <a name="setting-xamarintvos-project-images"></a>Установка изображений Xamarin.tvOS проекта

Как уже говорилось выше, все приложения tvOS требуют [запуска изображения](#Launch-Image), и [значка приложения](#App-Icons). В этом разделе рассматриваются Выбор запуска изображения и значка приложения для проекта приложения Xamarin.tvOS после указания в каталоге активов.

Выполните следующие действия:

1. В **обозревателе решений**, дважды щелкните `Info.plist` чтобы открыть его для редактирования: 

    [![](icons-images-images/info01.png "Файл Info.plist")](icons-images-images/info01.png#lightbox)
2. В **редактор Info.Plist**, выберите каталог, активы (настроенных выше в [Настройка значков приложения](#Setting-the-App-Icons) раздел) для **значки приложений**: 

    [![](icons-images-images/info02.png "Редактор Info.Plist")](icons-images-images/info02.png#lightbox)
3. Затем выберите каталог средств (настроенных выше в [изображение запуска](#Setting-the-Launch-Image) раздел) для **запуска изображения**.
4. Сохраните изменения.

<a name="Summary" />

## <a name="summary"></a>Сводка

В этой статье был проиллюстрирован все типы изображений и размеры использовался в приложении Xamarin.tvOS. Во-первых охваченных запуска изображения, многоуровневая изображения, значки приложений, образы Полка верхней и образы Game Center. Затем он рассматривается работа с образами в приложении Xamarin.tvOS.

## <a name="related-links"></a>Связанные ссылки

- [Примеры tvOS](https://developer.xamarin.com/samples/tvos/all/)
- [tvOS](https://developer.apple.com/tvos/)
- [tvOS человека направляющие интерфейса](https://developer.apple.com/tvos/human-interface-guidelines/)
- [Приложение руководство по программированию для tvOS](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/)
