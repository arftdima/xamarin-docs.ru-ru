---
title: Пользовательская конфигурация компоновщика
ms.prod: xamarin
ms.assetid: F8A99E3F-2197-4399-AC81-F1DBAB5729C9
ms.technology: xamarin-cross-platform
author: asb3993
ms.author: amburns
ms.date: 03/22/2017
ms.openlocfilehash: 8b74d537d88c5a484c858e33d294352cdfd1d116
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="custom-linker-configuration"></a>Пользовательская конфигурация компоновщика

Если набора параметров по умолчанию недостаточно, вы можете выполнить связывание с помощью XML-файла, который описывает требования к компоновщику.

Вы можете предоставить компоновщику дополнительные определения, чтобы он не исключал из приложения определенные типы, методы и (или) поля. В собственном коде лучше всего применить пользовательский атрибут `[Preserve]`, который описан в руководствах [Компоновка в iOS](~/ios/deploy-test/linker.md) и [Компоновка в Android](~/android/deploy-test/linker.md).
Но если вам нужны несколько определений из сборки пакета SDK или продукта, то лучшим решением будет создать XML-файл (вместо того, чтобы добавлять отдельный код только для того, чтобы компоновщик не удалял нужные элементы).

Этот XML-файл нужно определить с элементом верхнего уровня <linker>, который будет содержать узлы *assembly* (сборка), в которых будут расположены узлы *type* (тип), содержащие в свою очередь узлы *method* (метод) и *field* (поле).

Создав такой файл с описанием для компоновщика, добавьте его в проект и выполните следующее:

-  **Для Android**: для параметра **Действие сборки** укажите **LinkDescription**;
-  **Для iOS**: для параметра **Действие сборки** укажите **LinkDescription**.


В следующем примере показано, как выглядит такой XML-файл.

```xml
<linker>
        <assembly fullname="mscorlib">
                <type fullname="System.Environment">
                        <field name="mono_corlib_version" />
                        <method name="get_StackTrace" />
                </type>
        </assembly>
        <assembly fullname="My.Own.Assembly">
                <type fullname="Foo" preserve="fields">
                        <method name=".ctor" />
                </type>
                <type fullname="Bar">
                        <method signature="System.Void .ctor(System.String)" />
                        <field signature="System.String _blah" />
                </type>
                <namespace fullname="My.Own.Namespace" />
                <type fullname="My.Other*" />
        </assembly>
</linker>
```

Получив указанный выше файл, компоновщик считает и применит инструкции для сборок `mscorlib.dll` (поставляется с Mono для Android) и `My.Own.Assembly` (пользовательский код).

Первый раздел для `mscorlib.dll` указывает, что тип `System.Environment` сохранит поле с именем `mono_corlib_version` и его метод `get_StackTrace`.
Обратите внимание, что здесь нужно указать имена методов считывания и задания, поскольку компоновщик работает с промежуточным языком и не поддерживает свойства C#.

Второй раздел для `My.Own.Assembly.dll` обеспечит сохранение в типе `Foo` всех полей (т. е. атрибута `preserve="fields"`) и всех конструкторов (т. е. всех методов с именем `.ctor` на промежуточном языке). Тип `Bar` сохранит отдельные сигнатуры (не имена) для одного конструктора (который принимает один строковый параметр) и для конкретного строкового поля `_blah`.
Пространство имен `My.Own.Namespace` сохранит все типы, которые оно содержит.
И наконец, будут сохранены все поля и методы для любого типа, полное имя которого (включая пространство имен) соответствует подстановочному шаблону "My.Other\*". Подстановочный символ `*` может встречаться в шаблоне "полное имя типа" несколько раз.



## <a name="related-links"></a>Связанные ссылки

- [Компоновка в iOS](~/ios/deploy-test/linker.md)
- [Компоновка в Android](~/android/deploy-test/linker.md)
