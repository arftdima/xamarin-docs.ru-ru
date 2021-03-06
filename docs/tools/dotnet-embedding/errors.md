---
title: Внедрение ошибок .NET
ms.prod: xamarin
ms.assetid: 932C3F0C-D968-42D1-BB14-D97C73361983
ms.technology: xamarin-cross-platform
author: topgenorth
ms.author: toopge
ms.date: 11/14/2017
ms.openlocfilehash: 64caaf6610d9f9193a686d91b4731cd4d4953fa6
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="em0xxx-binding-error-messages"></a>EM0xxx: сообщения об ошибках привязки

Например, параметры, среды

<!-- 0xxx: the generator itself, e.g. parameters, environment -->
<h3><a name="EM0000"/>EM0000: Непредвиденная ошибка - заполните отчет об ошибках в https://github.com/mono/Embeddinator-4000/issues</h3>

Произошла непредвиденная ошибка. Проверьте [файл проблему](https://github.com/mono/Embeddinator-4000/issues) как можно больше информации, включая:

* Полные журналы, построений с максимальная степень подробности
* Минимальный тестовый случай, воспроизведите ошибку
* Все версии сведения

Чтобы получить сведения о точной версии проще всего использовать **Xamarin Studio** меню, **о Xamarin Studio** элемента, **Показать подробности** кнопку и скопируйте его версия сведения (можно использовать **сведения о копировании** кнопка).

<h3><a name="EM0001"/>EM0001: Не удалось создать выходной каталог `X`</h3>

Имя каталога, указанное в `-o=DIR` не существует и не может быть создан. Может быть недопустимое имя для файловой системы.

<h3><a name="EM0002"/>EM0002: Параметр `X` не поддерживается</h3>

Средство не поддерживает параметр `X`. Это возможно, что другая версия средства поддерживает его или что он не применяется в этой среде.

<h3><a name="EM0003"/>EM0003: Платформа `X` является недопустимым.</h3>

Средство не поддерживает платформу `X`. Это возможно, что другая версия средства поддерживает его или что он не применяется в этой среде.

<h3><a name="EM0004"/>EM0004: Целевой `X` является недопустимым.</h3>

Средство не поддерживает целевой объект `X`. Это возможно, что другая версия средства поддерживает его или что он не применяется в этой среде.

<h3><a name="EM0005"/>EM0005: Целевого объекта компиляции `X` является недопустимым.</h3>

Средство не поддерживает целевого объекта компиляции `X`. Это возможно, что другая версия средства поддерживает его или что он не применяется в этой среде.

<h3><a name="EM0006"/>EM0006: Не удалось найти расположение Xcode.</h3>

Средство не удалось найти выбранного расположения Xcode с помощью `xcode-select -p` команды. Убедитесь, что эта команда завершается успешно и возвращает правильное расположение Xcode.

<h3><a name="EM0007"/>EM0007: Не удалось получить версию пакета sdk для {sdk}.</h3>

Средство не удалось получить версию пакета SDK с помощью `xcrun --show-sdk-version --sdk {sdk}` команды. Убедитесь, что эта команда завершается успешно и возвращает версию пакета SDK.

<h3><a name="EM0008"/>EM0008: Архитектура {arch} является недопустимым для {платформы}. Допустимые архитектуры для {платформы}: {архитектур}.</h3>

Архитектура в сообщении об ошибке не поддерживается для целевой платформы. Убедитесь, что параметр--abi передается является допустимой архитектурой.

<h3><a name="EM0009"/>EM0009: Компонент `X` в настоящее время не реализуется генератор</h3>

Это известная проблема, которую мы собираемся исправить в будущем выпуске генератора. Комментарии приветствуются.

<h3><a name="EM0010"/>EM0010: Не удается выполнить слияние платформы {simulatorFramework} и {deviceFramework}, так как существует как файл «{}».</h3>

Средство не удалось объединить платформы, упомянутые в сообщении об ошибке, так как между ними общих файлов.

Это может указывать на ошибку в Embeddinator 4000; Отправьте отчет об ошибках в [ https://github.com/mono/Embeddinator-4000/issues ](https://github.com/mono/Embeddinator-4000/issues) с тестовым случаем.

<h3><a name="EM0011"/>EM0011: Сборка `X` не существует.</h3>

Средство не удалось найти сборку `X` указаны в аргументах.

<h3><a name="EM0012"/>EM0012: Имя сборки `X` не является уникальным</h3>

Указано более одной сборки имеют одинаковую, внутренняя имя и не возможно различать их во время выполнения.

Наиболее вероятной причиной является указано сборки несколько раз на аргументы командной строки. Однако по-прежнему сохраняет переименованный сборки, исходное имя и несколько копий нельзя сосуществует.

<h3><a name="EM0013"/>EM0013: Не удалось найти сборку «X», ссылается на «Y».</h3>

Средство не удалось найти сборку «X», ссылается сборка «Y». Убедитесь, что все сборки, на которую указывает ссылка, в том же каталоге, что сборка может быть привязано.

<h3><a name="EM0014"/>EM0014: Не удалось найти {продукта} ({продукта} {min_version} является обязательным).</h3>

Зависимость, упомянутые в сообщении об ошибке не найден в системе.

<h3><a name="EM0015"/>EM0015: Не удалось найти допустимую версию {продукта} ({version} найден, но по крайней мере {min_version} является обязательным).</h3>

Зависимость упомянутые в сообщении об ошибке, сообщение найдено в системе, но она устарела. Выполните обновление до более новой версии.

<h3><a name="EM0016">EM0016: Не удается создать символьную ссылку «{файл}» -> «{target}»: ошибка {число}</h3>

Не удается создать символьную ссылку, упомянутые в сообщении об ошибке.

<h3><a name="EM0026"/>Не удалось EM0026 проанализировать аргумент командной строки «A»: *</h3>

Синтаксис, заданный для параметра командной строки `A` не удалось проанализировать с помощью средства. Вполне вероятно, неверные, обратитесь к документации или справки правильный синтаксис.

<h3><a name="EM0099"/>EM0099: Внутренняя ошибка *. Отправьте отчет об ошибках с тестовым случаем (https://github.com/mono/Embeddinator-4000/issues).</h3>

Это сообщение об ошибке появляется в том случае, когда проверка внутренней согласованности в Embeddinator-4000 завершается неудачно.

Это указывает на ошибку в Embeddinator 4000; Отправьте отчет об ошибках в [ https://github.com/mono/Embeddinator-4000/issues ](https://github.com/mono/Embeddinator-4000/issues) с тестовым случаем.


<!-- 1xxx: code processing -->

# <a name="em1xxx-code-processing"></a>EM1xxx: Обработка кода

<h3><a name="EM1010"/>Тип `T` не создается, поскольку `X` не поддерживаются.</h3>

Это **предупреждение** , тип `T` игнорируются (т. е. ничего не будет создаваться) так как оно использует `X`, функцию, которая не поддерживается.

Примечание: Поддерживаемые функции также будет изменяться новые версии средства.


<h3><a name="EM1011"/>Тип `T` не возникает, поскольку он не имеет собственного аналога.</h3>

Это **предупреждение** , тип `T` игнорируются (т. е. ничего не будет создаваться), так как он использует предоставляют что-нибудь из .NET framework, которая не имеет эквивалента в собственной платформы.


<h3><a name="EM1011"/>Тип `T` не создается, так как он не имеет код маршалинга с собственного аналога.</h3>

Это **предупреждение** , тип `T` игнорируются (т. е. ничего не будет создаваться) так как оно использует предоставляют что-нибудь из .NET framework, которая требует дополнительного маршалинг.

Примечание: Это то, что может получить поддерживается с некоторыми ограничениями в будущей версии средства.


<h3><a name="EM1020"/>Конструктор `C` не создается из-за типа параметра `T` не поддерживается.</h3>

Это **предупреждение** , конструктор `C` игнорируются (т. е. ничего не будет создаваться) так как тип параметра `T` не поддерживается.

Должен быть типа предыдущих предупреждение, предоставляя дополнительные сведения о том, почему `T` не поддерживается.

Примечание: Поддерживаемые функции также будет изменяться новые версии средства.


<h3><a name="EM1021"/>Конструктор `C` имеет значения по умолчанию, для которых создается без оболочки.</h3>

Это **предупреждение** , параметры по умолчанию конструктора `C` любой дополнительный код не создается. Наиболее распространенной причиной является, что существующий метод уже имеет ту же сигнатуру. Например, в .net могут быть:

```
public class MyType {
    public MyType () { ... }
    public MyType (int i = 0) { ... }
}
```

В таких случаях только два созданных `init` селекторы будет создана, оба вызова моно, но никакой оболочки для более поздней версии будут существовать.


<h3><a name="EM1030"/>Метод `M` не создается, поскольку тип возвращаемого значения `T` не поддерживается.</h3>

Это **предупреждение** , метод `M` игнорируются (т. е. ничего не будет создан), так как он имеет тип возвращаемого значения `T` не поддерживается.

Должен быть типа предыдущих предупреждение, предоставляя дополнительные сведения о том, почему `T` не поддерживается.

Примечание: Поддерживаемые функции также будет изменяться новые версии средства.


<h3><a name="EM1031"/>Метод `M` не создается из-за типа параметра `T` не поддерживается.</h3>

Это **предупреждение** , метод `M` игнорируются (т. е. ничего не будет создаваться) так как тип параметра `T` не поддерживается.

Должен быть типа предыдущих предупреждение, предоставляя дополнительные сведения о том, почему `T` не поддерживается.

Примечание: Поддерживаемые функции также будет изменяться новые версии средства.


<h3><a name="EM1032"/>Метод `M` имеет значения по умолчанию, для которых создается без оболочки.</h3>

Это **предупреждение** , по умолчанию параметры метода `M` любой дополнительный код не создается. Наиболее распространенной причиной является, что существующий метод уже имеет ту же сигнатуру. Например, в .net могут быть:

```
public class MyType {
    public int Increment () { ... }
    public int Increment (int i = 0) { ... }
}
```

В таких случаях только два созданных `increment` селекторы будет создана, оба вызова моно, но никакой оболочки для более поздней версии будут существовать.


<h3><a name="EM1033"/>Метод `M` не создается, поскольку другой метод предоставляет оператор с понятным именем.</h3>

Это **предупреждение** , метод `M` не создается, поскольку другой метод предоставляет оператор с понятным именем. (https://msdn.microsoft.com/en-us/library/ms229032(v=vs.110).aspx)


<h3><a name="EM1034"/>Метод расширения `M` не создается внутри категории, так как они не могут создаваться на тип-примитив `T`. Создан обычный, статический метод.</h3>

Это **предупреждение** , метод расширения primivite типа (например `System.Int32`) был найден. В ObjC не можно создать категории на тип-примитив. Вместо этого генератор будет создавать нормальный, статический метод.



<h3><a name="EM1040"/>Свойство `P` не создается из-за типа параметра `T` не поддерживается.</h3>

Это **предупреждение** , свойство `P` игнорируются (т. е. ничего не будет создаваться) из-за выведенного типа `T` не поддерживается.

Должен быть типа предыдущих предупреждение, предоставляя дополнительные сведения о том, почему `T` не поддерживается.

Примечание: Поддерживаемые функции также будет изменяться новые версии средства.

<h3><a name="EM1041"/>Индексированные свойства на `T` не создается, поскольку несколько индексированные свойства не поддерживаются.</h3>

Это **предупреждение** , индексированные свойства на `T` будут игнорироваться (т. е. ничего не будет создаваться) из-за нескольких индексированные свойства не поддерживаются.


<h3><a name="EM1050"/>Поле `F` не создается из-за типа поля `T` не поддерживается.</h3>

Это **предупреждение** , поле `F` игнорируются (т. е. ничего не будет создаваться) из-за выведенного типа `T` не поддерживается.

Должен быть типа предыдущих предупреждение, предоставляя дополнительные сведения о том, почему `T` не поддерживается.

Примечание: Поддерживаемые функции также будет изменяться новые версии средства.

<h3><a name="EM1051"/>Элемент `E` вместо этого формируется как `F` , так как его имя конфликтует с селектора важные цели c.</h3>

Это **предупреждение** , элемент `E` вместо этого будет создан как `F` , так как его имя конфликтует с селектора важные цели c.

Селекторы на [NSObjectProtocol](https://developer.apple.com/reference/objectivec/1418956-nsobject?language=objc) имеют важные значения в objective-c, который должен быть переопределен внимательно.

Примечание: Список зарезервированных селекторы будет меняться вместе с новыми версиями средства.


<!-- 2xxx: code generation -->

# <a name="em2xxx-code-generation"></a>EM2xxx: Создание кода


<!-- 3xxx: reserved -->
<!-- 4xxx: reserved -->
<!-- 5xxx: reserved -->
<!-- 6xxx: reserved -->
<!-- 7xxx: reserved -->
<!-- 8xxx: reserved -->
<!-- 9xxx: reserved -->
