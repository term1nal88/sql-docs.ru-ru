---
title: "Настройки сведений об устройстве PPTX | Документы Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 09/11/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- render
- powerpoint
- pptx
- export
ms.assetid: 4dc2045f-8025-41a3-8f9d-5635fb24cf4a
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3aa67165e961e76569daadff1fc610c4d16a1e63
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="pptx-device-information-settings"></a>Настройки сведений об устройстве PPTX
  В следующей таблице перечислены настройки сведений об устройстве, предназначенные для подготовки отчетов [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] к просмотру в формате PPTX.  
  
|Настройка|Значение|  
|-------------|-----------|  
|**Столбцы**|Задаваемое число столбцов в отчете. Это значение переопределяет исходные параметры отчета.|  
|**ColumnSpacing**|Интервал между столбцами, который должен быть задан для отчета. Это значение переопределяет исходные параметры отчета.|  
|**DpiX**|Горизонтальное разрешение изображения вывода. Значение по умолчанию — **96**. Применяется к форматам вывода **BMP**, **GIF**, **PNG**и **TIFF** .|  
|**DpiY**|Вертикальное разрешение изображения вывода. Значение по умолчанию — **96**. Применяется к форматам вывода **BMP**, **GIF**, **PNG**и **TIFF** .|  
|**EndPage**|Последняя подготавливаемая к просмотру страница отчета. Значением по умолчанию является значение для **StartPage**.|  
|**MarginBottom**|Задаваемая ширина нижнего поля отчета, в дюймах. Необходимо включить целочисленное или десятичное значение, за которым следует строка "in" (например, **1in**). Это значение переопределяет исходные параметры отчета.|  
|**MarginLeft**|Задаваемая ширина левого поля отчета, в дюймах. Необходимо включить целочисленное или десятичное значение, за которым следует строка "in" (например, **1in**). Это значение переопределяет исходные параметры отчета.|  
|**MarginRight**|Задаваемая ширина правого поля отчета, в дюймах. Необходимо включить целочисленное или десятичное значение, за которым следует строка "in" (например, **1in**). Это значение переопределяет исходные параметры отчета.|  
|**MarginTop**|Задаваемая ширина верхнего поля отчета, в дюймах. Необходимо включить целочисленное или десятичное значение, за которым следует строка "in" (например, **1in**). Это значение переопределяет исходные параметры отчета.|  
|**PageHeight**|Задаваемая высота страницы отчета, в дюймах. Необходимо включить целочисленное или десятичное значение, за которым следует строка "in" (например, **11in**). Это значение переопределяет исходные параметры отчета.|  
|**PageWidth**|Задаваемая ширина страницы отчета, в дюймах. Необходимо включить целочисленное или десятичное значение, за которым следует строка "in" (например, **8,5in**). Это значение переопределяет исходные параметры отчета.|  
|**StartPage**|Первая подготавливаемая к просмотру страница отчета. Значение **0** указывает, что к просмотру подготовлены все страницы. Значение по умолчанию — **1**.|  
|**UseReportPageSize**|Если UseReportPageSize =**false** , то размер слайда по умолчанию соответствует стандартному значению PowerPoint — 13,333 x 7,5 дюйма (пропорции 16:9). Если UseReportPageSize = true, то размер слайда по умолчанию соответствует заданному размеру страницы отчета.<br /><br /> Значение по умолчанию равно **false**.<br /><br /> Обратите внимание, что параметры PageWidth и PageHeight переопределяют стандартную ширину и высоту.|  
  
## <a name="see-also"></a>См. также  
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>   
 [Передача настроек сведений об устройстве для модулей подготовки отчетов](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [Настройка параметров модуля подготовки отчетов в RSReportServer.Config](../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Технический справочник по &#40; Службы SSRS &#41;](../reporting-services/technical-reference-ssrs.md)  
  
  
