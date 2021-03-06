---
title: ListView и жизненный цикл действия
ms.prod: xamarin
ms.assetid: 40840D03-6074-30A2-74DA-3664703E3367
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 02/06/2018
ms.openlocfilehash: 6e15fb8796ae6a616c5eae44059caae3d9478aef
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="listview-and-the-activity-lifecycle"></a>ListView и жизненный цикл действия

Действия проходят определенных состояний как выполнения приложения, такие как запуск, запуска, приостановки и остановки. Дополнительные сведения и инструкции по обработке переходов между состояниями см. в разделе [учебник по жизненному циклу действия](~/android/app-fundamentals/activity-lifecycle/index.md).
Важно понять жизненный цикл действия и месте вашего `ListView` код в правильное расположение.

Все примеры в этом документе выполнения «Настройка задачи» в действии `OnCreate` метод и (при необходимости) выполняют «разборки» в `OnDestroy`. В примерах обычно используется небольших наборов данных, которые не изменяются, поэтому чаще повторной загрузки данных не нужен.

Однако, если данные часто изменяющиеся или использует много памяти возможно можно использовать методы различных жизненного цикла для заполнения и обновления вашей `ListView`. Например, если базовые данные постоянно изменяется (или могут быть затронуты обновлений для других действий), а затем Создание адаптера в `OnStart` или `OnResume` обеспечит последних данных отображается каждый раз, показано действие.

Если адаптер использует ресурсы, такие как память или управляемого курсора, не забудьте освобождать эти ресурсы в дополнительный метод, где они были созданы (например) объекты, созданные в `OnStart` могут быть уничтожены в `OnStop`).


## <a name="configuration-changes"></a>Изменения конфигурации

Важно помнить изменения конфигурации &ndash; особенно экране клавиатуры и поворота видимость &ndash; может привести к текущей активности быть удалении и повторном создании (если не указано иное использование `ConfigurationChanges` атрибут). Это означает, что в нормальных условиях, смена устройства будет привести `ListView` и `Adapter` повторного создания и (Если вы написали код `OnPause` и `OnResume`) Прокрутка выделения положение и строки состояния, будут потеряны.

Следующий атрибут могли бы помешать действия уничтожены и созданы повторно в результате изменения конфигурации:

```csharp
[Activity(ConfigurationChanges="keyboardHidden|orientation")]
```

Действие должно затем Переопределите `OnConfigurationChanged` реагировать на эти изменения. Дополнительные сведения о том, как обрабатывать изменения конфигурации см. в документации.

