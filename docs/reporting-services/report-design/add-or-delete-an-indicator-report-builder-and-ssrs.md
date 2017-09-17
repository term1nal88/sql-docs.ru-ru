---
title: "Добавление или удаление индикатора (построитель отчетов и службы SSRS) | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a8b1aac1-53ef-47a4-afc0-8fa866c6c480
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1356d575f58eb36d00f52bcbac1483ce902b1954
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="add-or-delete-an-indicator-report-builder-and-ssrs"></a>Добавление или удаление индикатора (построитель отчетов и службы SSRS)
  В отчетах [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] с разбиением на страницы индикаторы — это минимальные датчики, обеспечивающие возможность быстрого определения состояния одиночного значения данных. Дополнительные сведения см. в разделе [Индикаторы (построитель отчетов и службы SSRS)](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md).  
  
 Индикаторы обычно размещаются в ячейках таблицы или матрицы, но можно использовать сами индикаторы, параллельно с датчиками или внедренные в датчиках.  
  
 При первом добавлении индикатора он по умолчанию настраивается для использования процентных единиц измерения. Процентные диапазоны равномерно распределяются между элементами набора индикаторов, а область значений, отображаемых индикатором, является для индикатора родительским элементом, таким как таблица или матрица.  
  
 Можно обновить значения и состояния индикаторов. Дополнительные сведения см. в следующих разделах:  
  
-   [Изменение значков индикаторов и наборов индикаторов &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md)  
  
-   [Выбор и настройка единиц измерения &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/set-and-configure-measurement-units-report-builder-and-ssrs.md)  
  
-   [Задание области действия синхронизации &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/set-synchronization-scope-report-builder-and-ssrs.md)  
  
 Поскольку индикатор располагается внутри панели датчиков, необходимо выбрать вместо панели индикатор при необходимости настройки индикатора с помощью диалогового окна **Свойства индикатора** или панели **Свойства** . На следующем рисунке отображается выбранный индикатор на панели датчиков.  
  
 ![rs_GaugePanelWithIndicator](../../reporting-services/report-design/media/rs-gaugepanelwithindicator.gif "rs_GaugePanelWithIndicator")  
  
> [!NOTE]  
>  В зависимости от ширины столбца и длины значений данных, текст в ячейках таблицы или матрицы может переноситься по словам на несколько строк. В этом случае значок индикатора может растянуться и изменить форму. В результате значок индикатора воспринимается хуже. Во избежание растяжений значка разместите индикатор внутри прямоугольника.  
  
## <a name="to-add-an-indicator-to-a-table-or-matrix"></a>Добавление индикатора в таблицу или матрицу  
  
1.  Откройте существующий отчет или создайте новый отчет, содержащий таблицу и матрицу с данными, которые необходимо отобразить. Дополнительные сведения см. в разделе [Tables &#40; Построитель отчетов и службы SSRS &#41; ](../../reporting-services/report-design/tables-report-builder-and-ssrs.md) или [матрицы](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md).  
  
2.  Вставьте столбец в таблицу или матрицу. Дополнительные сведения см. в разделе [Вставка или удаление столбца (построитель отчетов и службы SSRS)](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  При необходимости на вкладке **Вставка** нажмите кнопку **Прямоугольник**, а затем щелкните ячейку в новом столбце.  
  
4.  На вкладке **Вставка** нажмите кнопку **Индикатор**, а затем щелкните ячейку в новом столбце.  
  
     Если в ячейку был добавлен прямоугольник, щелкните эту ячейку.  
  
5.  В диалоговом окне **Выбор стиля индикатора** в левой панели выберите тип нужного индикатора, а затем выберите набор индикаторов.  
  
6.  Нажмите кнопку **ОК**.  
  
7.  Щелкните индикатор. Откроется панель **Данные датчика** .  
  
8.  В области **Значения** в раскрывающемся списке **(Не указано)** выберите поле, значения которого необходимо отобразить в качестве индикатора.  
  
     Индикатор настроен для использования значений по умолчанию. По умолчанию индикаторы настроены для использования в качестве единиц измерения процентных соотношений, диапазоны процентного соотношения равномерно распределяются между элементами индикатора, а для значений, указываемых индикатором, используется область ближайшей группы.  
  
## <a name="to-delete-an-indicator-to-a-table-or-matrix"></a>Удаление индикатора из таблицы или матрицы  
  
1.  Щелкните индикатор правой кнопкой мыши и выберите **Удалить**.  
  
    > [!NOTE]  
    >  Индикатор должен быть расположен на панели датчиков, содержащей другие индикаторы или датчики. Если панель датчиков содержит несколько элементов, убедитесь, что для их удаления выбран индикатор, а не панель датчиков. Если нажать и удалить панель датчиков, то будут удалены панели датчиков и все элементы в них.  
  
2.  Щелкните **Удалить**.  
  
## <a name="see-also"></a>См. также  
 [Индикаторы &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  