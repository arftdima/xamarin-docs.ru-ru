---
title: Подключение к компьютеру Mac
description: Расширение Xamarin.iOS для Visual Studio позволяет разработчикам создавать, отлаживать приложения iOS и выполнять их сборку на компьютере Windows с помощью интегрированной среды разработки Visual Studio. Это руководство описывает функции, предоставляемые Xamarin.iOS для Visual Studio, а также подключение к узлу сборки Mac.
ms.prod: xamarin
ms.assetid: 39DD7B3F-3E69-4E2A-B743-4C26AF613025
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/19/2017
ms.openlocfilehash: 5a76c443521276a66e820fa0b1877ae2a4cce8f0
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="connecting-to-the-mac"></a>Подключение к компьютеру Mac

_Расширение Xamarin.iOS для Visual Studio позволяет разработчикам создавать, отлаживать приложения iOS и выполнять их сборку на компьютере Windows с помощью интегрированной среды разработки Visual Studio. В этом руководстве перечислены функции, предоставляемые Xamarin.iOS для Visual Studio, а также описано, как подключиться к узлу сборки Mac._

Visual Studio подключается к Mac через SSH, что дает несколько преимуществ, включая следующие:

- Visual Studio может напрямую запускать и контролировать агент сборки. Больше нет видимого пользователю приложения, которое требуется запускать и останавливать вручную.

- Новый диспетчер подключений в Visual Studio позволяет обнаруживать, запоминать узел сборки Mac и проверять его подлинность.

- Так как весь обмен данными безопасно туннелируется через SSH, требуется подключение всего к одному порту с номером 22.

- Visual Studio уведомляет об изменениях по мере их возникновения. Например, при подключении устройства iOS панель инструментов сразу же обновляется.

- Можно подключить несколько экземпляров Visual Studio одновременно.

- Соединение не будет вмешиваться в процесс разработки. Соединение с Mac запрашивается только при выполнении операции, для которой Mac необходим, например при отладке или использовании конструктора iOS.

Подключение к компьютеру Mac состоит из нескольких процессов, отвечающих за разные функциональные возможности, например агент конструктора iOS и агент сборки, которыми управляет брокер. Visual Studio контролирует и обновляет этот брокер и автоматически перезапускает любые независимые процессы в случае их аварийного завершения.

На схеме ниже представлен рабочий процесс разработки с помощью Xamarin.iOS в общей форме:

[![Рабочий процесс разработки iOS](images/xma2.png)](images/xma2.png#lightbox)

> [!IMPORTANT]
> Для сборки проектов Visual Studio запускает отдельный процесс MSBuild. Этот процесс создает новое подключение к компьютеру Mac, то есть во время выполнения сборки в среде Visual Studio между компьютерами Windows и Mac имеются два подключения SSH. При сборке из [командной строки](#commandline) создается только один процесс MSBuild. Для простоты все подключения на схеме представлены одной стрелкой.

## <a name="requirements"></a>Требования

Расширение Xamarin.iOS для Visual Studio дает удивительную возможность: оно позволяет разработчикам создавать, выполнять сборку и отладку приложений iOS на компьютере Windows с помощью интегрированной среды разработки Visual Studio. Однако оно не может использоваться отдельно — приложения iOS невозможно создавать без компилятора Apple и развертывать без сертификатов и средств подписывания кода Apple. Это означает, что для выполнения этих задач расширению Xamarin.iOS для Visual Studio требуется соединение с подключенным к сети компьютером с Mac OS X (который называется *узлом* или *узлом сборки*). После настройки работа со средствами Xamarin максимально удобна.

### <a name="system-requirements"></a>Требования к системе

Дополнительные сведения о системных требованиях см. в руководстве по [установке Xamarin.iOS в Windows](~/ios/get-started/installation/windows/index.md#system-requirements).


#### <a name="compatibility"></a>Совместимость

> [!IMPORTANT]
> На компьютере Windows должна использоваться та же версия Xamarin.iOS, что и на компьютере Mac, к которому он подключается. Для этого должно выполняться указанное ниже требование:                                                    
>                                                                                                                 
> - **Visual Studio 2015 и более ранние версии**: необходимо использовать тот же [канал обновлений](https://developer.xamarin.com/recipes/cross-platform/ide/change_updates_channel/), что и для Visual Studio для Mac.
>                                                                                                                 
> - **Visual Studio 2017, версия выпуска**: необходимо использовать канал **Стабильный** Visual Studio для Mac.
>                                                                                                                 
> - **Visual Studio 2017, предварительная версия**: необходимо использовать канал **Альфа** Visual Studio для Mac. Visual Studio не будет проверять наличие пакета SDK Xamarin.iOS и Xcode и совместимость их версий.
>   Это проверяет агент сборки, что приводит к ошибкам сборки, а также агент конструктора iOS, что приводит к ошибкам конструктора.

### <a name="connecting-to-the-mac"></a>Подключение к компьютеру Mac

#### <a name="mac-setup"></a>Настройка Mac

Чтобы настроить узел Mac, нужно обеспечить взаимодействие между расширением Xamarin для Visual Studio и компьютером Mac. Для этого разрешите **удаленный вход** на компьютере Mac, выполнив следующие действия:

1. Откройте *Spotlight* (**⌘+ПРОБЕЛ**), выполните поиск по запросу *удаленный вход* и выберите результат *Sharing* (Общий доступ). Откроется панель *Sharing* (Общий доступ) в программе *System Preferences* (Системные настройки):

   [![Поиск удаленного входа в Spotlight](images/spotlight.png)](images/spotlight.png#lightbox)

2. В списке *Service* (Служба) в левой части окна установите флажок *Remote Login* (Удаленный вход), чтобы разрешить Xamarin для Visual Studio подключаться к компьютеру Mac:

   [![Установка флажка "Remote Login" (Удаленный вход) в списке "Service" (Служба)](images/sharing.png)](images/sharing.png#lightbox)

3. Для параметра *Remote Login* (Удаленный вход) нужно разрешить доступ всем пользователям (*All*) либо включить свое имя пользователя Mac или группу в список разрешенных пользователей справа.

Кроме того, если в брандмауэре OS X настроено блокирование подписанных приложений по умолчанию, может потребоваться разрешить программе `mono-sgen` принимать входящие подключения. В этом случае появляется диалоговое окно с соответствующим предупреждением.

При наличии открытого сеанса компьютер Mac теперь должен обнаруживаться средой Visual Studio, если они находятся в одной сети.

Visual Studio будет запускать и останавливать агент на компьютере Mac, поэтому вам, как пользователю, больше ничего запускать не нужно.

### <a name="windows-setup"></a>Программа установки Windows

Обязательно [установите](~/ios/get-started/installation/windows/index.md) инструменты Xamarin на компьютере Windows.

### <a name="connecting-to-the-mac-build-host"></a>Подключение к узлу сборки Mac

Подключиться к узлу сборки Mac можно двумя способами:

Через панель инструментов iOS:

[![Панель инструментов iOS](images/image1.png)](images/image1.png#lightbox)

Кроме того, можно выбрать **Сервис > Параметры** в Visual Studio, затем выбрать **Xamarin > Параметры iOS** и нажать кнопку **Найти Xamarin Mac Agent**:

[![Поиск агента Xamarin для Mac](images/image2.png)](images/image2.png#lightbox)

В любом случае вы попадете в диалоговое окно **агента для Mac**, как показано ниже:

[![Диалоговое окно агента для Mac](images/image3.png)](images/image3.png#lightbox)

Оно содержит список всех компьютеров, которые либо были подключены ранее и сохранены в качестве известных, либо доступны для *удаленного входа*.

Подключитесь к компьютеру Mac, дважды щелкнув его. При первом подключении к компьютеру Mac вам будет предложено ввести свои учетные данные пользователя Mac, чтобы разрешить удаленное подключение:

[![Ввод учетных данных пользователя Mac](images/image4.png)](images/image4.png#lightbox)

Агент будет использовать эти учетные данные для создания подключения SSH к компьютеру Mac. В случае успеха создается ключ SSH, который [регистрируется](#commandline) в файле `authorized_keys` на этом компьютере Mac. При последующих подключениях агент будет использовать имя пользователя и файл ключа для подключения к последнему известному узлу сборки.

> [!NOTE]
> При вводе учетных данных нужно использовать _имя пользователя_, а не _полное имя_.  Чтобы узнать его, можно выполнить команду `whoami` в Terminal.  Например, на приведенном ниже снимке экрана имя учетной записи будет **amyb**, а не **Amy Burns**:
>
> ![Поиск имени пользователя в приложении Terminal](images/image5.png)

Когда подключение успешно установлено, оно отображается в диалоговом окне "Выбор узла" со значком **подключено**, как показано ниже:

[![Диалоговое окно "Выбор узла" со значком подключения](images/image6.png)](images/image6.png#lightbox)

Одновременно может быть подключен только один Mac.

Для любого компьютера в списке — как подключенного, так и нет — доступно контекстное меню, открываемое щелчком правой кнопкой мыши, где можно выбрать **Подключить**, **Отключить** или **Не сохранять данные этого Mac**:

[![Параметры "Подключить", "Отключить" или "Не сохранять данные этого Mac" в контекстном меню](images/image7.png)](images/image7.png#lightbox)

Если вы решили **Не сохранять данные этого Mac**, для повторного подключения к нему потребуется снова ввести учетные данные.

<a name="manual-add"/>

### <a name="manually-adding-a-mac"></a>Добавление Mac вручную

В некоторых случаях может потребоваться вручную добавить компьютер Mac, если его mDNS-имя не отображается в диалоговом окне "Выбора узла". Выполните указанные ниже действия:

1. Определите IP-адрес компьютера Mac, перейдя в раздел **System Preferences > Sharing > Remote Login** (Системные настройки > Общий доступ > Удаленный вход) на Mac:

   [![IP-адрес Mac в разделе "System Preferences" (Системные настройки)](images/image8.png)](images/image8.png#lightbox)

   Или, если вы предпочитаете использовать командную строку, можно узнать свой IP-адрес, введя `ipconfig getifaddr en0` в Terminal (обратите внимание, что, в зависимости от типа соединения, переменная может быть `en1`, `en2` и т. д.):

   [![IP-адрес в принижении Terminal](images/image9.png)](images/image9.png#lightbox)

2. Вернитесь в Visual Studio и в диалоговом окне "Выбор узла" выберите **Добавить компьютер Mac...**:

   [![Диалоговое окно "Выбор узла"](images/image10.png)](images/image10.png#lightbox)

3. Введите IP-адрес компьютера Mac в диалоговом окне "Добавить компьютер Mac" и нажмите кнопку **Добавить**:

   [![Ввод IP-адреса компьютера Mac в диалоговом окне "Добавить компьютер Mac"](images/image11.png)](images/image11.png#lightbox)

4. Наконец, введите имя пользователя (а не полное имя) своей учетной записи администратора Mac и соответствующий пароль:

   [![Ввод имени пользователя и пароля](images/image12.png)](images/image12.png#lightbox)

После нажатия кнопки **Вход** Visual Studio входит на компьютер Mac с помощью SSH и добавляет его в список известных компьютеров.

<a name="commandline"/>

### <a name="command-line-support"></a>Поддержка командной строки

Агент также позволяет создавать конфигурацию Xamarin.iOS из командной строки.  Чтобы использовать эту функцию, нужно передавать следующие обязательные параметры в MSBuild:

- `ServerAddress` — IP-адрес сервера Mac.

- `ServerUser` — имя пользователя (а не полное имя), используемое для входа на сервер Mac.

- `ServerPassword` — пароль, используемый для входа на узел Mac (необязательно).

Параметр `ServerPassword` не является обязательным.

Вместо этого при первой передаче пароля (с помощью Visual Studio или командной строки) для этой конкретной конфигурации Windows, Mac и пользователя создается пара ключей, которая сохраняется на компьютере Windows для дальнейшего использования. Она хранится в **%localappdata%\Xamarin\MonoTouch\id_rsa**.  Если вы не передаете параметр `ServerPassword`, для проверки подлинности будет использоваться файл ключа `id_rsa`.

Ниже показан пример команды для подключения к Mac 10.211.55.2 с использованием учетной записи **xamUser** с паролем **mypassword**:

```bash
C:\samples\App1>msbuild App1.sln /p:ServerAddress=10.211.55.2 /p:ServerUser=xamUser /p:Platform=iPhoneSimulator /p:ServerPassword=mypassword
```

### <a name="summary"></a>Сводка

В этой статье рассмотрено взаимодействие между Visual Studio и инструментами сборки и конструктора iOS на Mac, которые позволяют создавать приложения Xamarin.iOS с помощью Visual Studio.

### <a name="related-links"></a>Связанные ссылки

- [Установка](~/ios/get-started/installation/windows/index.md)
- [Устранение неполадок при подключении](~/ios/get-started/installation/windows/connecting-to-mac/troubleshooting.md)
- [Подключение компьютера Mac к среде Visual Studio с помощью XMA (видео)](https://university.xamarin.com/lightninglectures/xamarin-mac-agent)
