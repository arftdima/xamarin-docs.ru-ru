---
title: Навигация
description: Xamarin.Forms предоставляет ряд возможностей навигации другую страницу, в зависимости от используемого типа страницы.
ms.prod: xamarin
ms.assetid: BC5D0C6C-D5A9-4B12-A492-ED1F570CEC87
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 12/01/2017
ms.openlocfilehash: 1a184e1ebfd9d87ba82642ebdfc30a8d3f92cce1
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/04/2018
---
# <a name="navigation"></a>Навигация

_Xamarin.Forms предоставляет ряд возможностей навигации другую страницу, в зависимости от используемого типа страницы._

![](images/page-types.png "Типы страниц Xamarin.Forms")

## <a name="hierarchical-navigationhierarchicalmd"></a>[Иерархическая навигация](hierarchical.md)

Класс [`NavigationPage`](https://developer.xamarin.com/api/type/Xamarin.Forms.NavigationPage/) обеспечивает иерархическую навигацию, при которой пользователь может переходить по страницам вперед и назад по своему желанию. Этот класс реализует навигацию на основе стека объектов [`Page`](https://developer.xamarin.com/api/type/Xamarin.Forms.Page/) по методу LIFO (последним поступил — первым обслужен).

## <a name="tabbedpagetabbed-pagemd"></a>[TabbedPage](tabbed-page.md)

Xamarin.Forms [ `TabbedPage` ](https://developer.xamarin.com/api/type/Xamarin.Forms.TabbedPage/) состоит из списка вкладок и увеличить область сведений, с каждой из вкладок загрузки содержимого в область данных.

## <a name="carouselpagecarousel-pagemd"></a>[CarouselPage](carousel-page.md)

Xamarin.Forms [ `CarouselPage` ](https://developer.xamarin.com/api/type/Xamarin.Forms.CarouselPage/) — это страница, пользователи могут проведите стороны перемещаться по страницам содержимого, такие как коллекции.

## <a name="masterdetailpagemaster-detail-pagemd"></a>[MasterDetailPage](master-detail-page.md)

Xamarin.Forms [ `MasterDetailPage` ](https://developer.xamarin.com/api/type/Xamarin.Forms.MasterDetailPage/) — страница, которая управляет двумя страницами связанных данных, — Главная страница, которая представляет элементы и страницу сведений, которая представляет сведения об элементах на главной странице.

## <a name="modal-pagesmodalmd"></a>[Модальные страницы](modal.md)

Xamarin.Forms также предоставляет поддержку для модального страниц. На модальной странице пользователь должен выполнить отдельную задачу, причем он не может уйти с этой страницы, пока задача не будет выполнена или отменена.

## <a name="displaying-pop-upspop-upsmd"></a>[Отображение всплывающих элементов](pop-ups.md)

Xamarin.Forms предоставляет два pop повышение подобные элементы интерфейса: предупреждение и листом действия. Эти элементы интерфейса можно использовать простые вопросы пользователей и проводят пользователя через задачи.

