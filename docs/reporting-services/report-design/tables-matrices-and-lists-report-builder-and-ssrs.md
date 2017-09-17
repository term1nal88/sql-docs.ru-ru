---
title: "Таблицы, матрицы и списки (построитель отчетов и службы SSRS) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.tablixgroup.f1
- "10045"
- sql13.rtp.rptdesigner.tablix.visibility.f1
- "10039"
- sql13.rtp.rptdesigner.groupproperties.visibility.f1
- "10104"
- "10047"
- sql13.rtp.rptdesigner.groupproperties.advanced.f1
- "10044"
- sql13.rtp.rptdesigner.groupproperties.filters.f1
- sql13.rtp.rptdesigner.tablix.sort.f1
- sql13.rtp.rptdesigner.tablix.general.f1
- sql13.rtp.rptdesigner.groupproperties.general.f1
- sql13.rtp.rptdesigner.groupproperties.variables.f1
- "10046"
- "10101"
- sql13.rtp.rptdesigner.tablix.filter.f1
- sql13.rtp.rptdesigner.groupproperties.sort.f1
- "10042"
- "10041"
- "10102"
- "10103"
- "10043"
- sql13.rtp.rptdesigner.groupproperties.pagebreaks.f1
ms.assetid: 9dcf3fc8-bf9c-4a14-a03d-e78254aa4098
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: aa7d5ba489e0f23c6802a1d6596a22f2263decd8
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="tables-matrices-and-lists-report-builder-and-ssrs"></a>Таблицы, матрицы и списки (построитель отчетов и службы SSRS)
 В [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]таблицы, матрицы и списки — это *области данных* , где данные отчета с разбиением на страницы отображаются в ячейках, распределенных по строкам и столбцам. Ячейки, как правило, содержат текстовые данные, например текст, даты и числа, но могут также содержать датчики, диаграммы или элементы отчетов, такие как изображения. К таблицам, матрицам и спискам часто применяется общее название — области данных *табликса* .  
  
 В основе шаблонов таблиц, матриц и списков лежит область данных табликса, которая представляет собой гибкую сетку, позволяющую отображать данные в ячейках. В шаблонах таблиц и матриц ячейки выстроены в виде строк и столбцов. Шаблоны — это разные варианты базовой универсальной данных табликса, можно отобразить данные в сочетании с форматами шаблонов и изменения таблицы, матрицы или списка путем включения характеристик другой области данных по мере разработки конкретного отчета. Например, если после добавления таблицы обнаруживается, что она не соответствует конкретным требованиям, то можно добавить группы столбцов, чтобы преобразовать таблицу в матрицу.  
  
 Области данных таблицы и матричные области данных позволяют отображать сложные связи между данными путем включения вложенных таблиц, матриц, списков, диаграмм и датчиков. Таблицы и матрицы имеют табличный макет, и их данные берутся из единственного набора данных на базе единственного источника данных. Ключевое различие между таблицами и матрицами состоит в том, что таблицы могут включать в себя только группы строк, тогда как матрицы содержат группы строк и группы столбцов.  
  
 Списки имеют небольшое отличие. Они поддерживают макеты произвольной формы и могут включать в себя несколько одноранговых таблиц или матриц, в каждой из которых используются данные из другого набора данных. Списки могут также использоваться для таких форм, как счета.  
  
 На приведенных ниже рисунках показаны простые отчеты с таблицей, матрицей или списком.  
  
 ![RS_TableMatrixList](../../reporting-services/report-design/media/rs-tablematrixlist.gif "RS_TableMatrixList")  
  
 Чтобы быстро приступить к работе с таблицами, матрицами и списками, см. разделы [Создание простого табличного отчета (построитель отчетов)](../../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md), [Учебник. Создание матричного отчета (построитель отчетов)](../../reporting-services/tutorial-creating-a-matrix-report-report-builder.md) и [Учебник. Создание отчета в свободной форме (построитель отчетов)](../../reporting-services/tutorial-creating-a-free-form-report-report-builder.md).  
  
> [!NOTE]  
>  Таблицы, матрицы и списки можно публиковать отдельно от отчета как элементы отчета. Узнайте больше об [элементах отчета](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
##  <a name="Table"></a> Таблица  
 Таблица используется для отображения подробных данных, организации данных в группы строк либо для того и другого одновременно. Шаблон таблицы содержит три столбца со строкой заголовка таблицы и строкой подробных сведений для данных. На приведенном ниже рисунке показан исходный шаблон таблицы, выбранный в области конструктора.  
  
 ![Шаблон таблицы в область конструктора выбранный](../../reporting-services/report-design/media/rs-tabletemplatenewselected.gif "шаблон таблицы в область конструктора выбранного")  
  
 Данные можно сгруппировать по одному полю, по нескольким полям или написать свое собственное выражение. Предусмотрена возможность создавать вложенные группы или независимые, смежные группы и отображать статистические значения для сгруппированных данных, а также добавлять итоги к группам. Например, если в таблице есть группа строк с именем [Категория], то можно добавить подытог для каждой группы, а также общий итог для отчета. Чтобы улучшить внешний вид таблицы и выделить данные, которые необходимо сделать более заметными, можно выполнить слияние ячеек и применить форматирование к заголовкам таблицы и данным.  
  
 Можно первоначально скрыть подробные или сгруппированные данные и включить в отчет переключатели углубленной детализации, позволяющие пользователям в интерактивном режиме выбирать, какие данные нужно показать.  
  
 Дополнительные сведения см. в разделе [Таблицы (построитель отчетов и службы SSRS)](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
##  <a name="Matrix"></a> Матрица  
 Матрица используется для отображения статистических сводок по данным, сгруппированным в строки и столбцы, аналогично сводным или перекрестным таблицам. Число строк и столбцов для групп определяется числом уникальных значений для каждой группы строк и столбцов. На приведенном ниже рисунке показан исходный шаблон матрицы, выбранный в области конструктора.  
  
 ![Новая матрица добавлен с панели элементов, выбранных](../../reporting-services/report-design/media/rs-matrixtemplatenewselected.gif "новой матрицы добавлен с панели элементов, выбранных")  
  
 Данные можно группировать по нескольким полям либо выражениям в группах строк и столбцов. Во время выполнения, когда происходит объединение данных отчета и областей данных, матрица расширяется на странице по горизонтали и вертикали по мере добавления столбцов к группам столбцов и строк к группам строк. Значения в ячейках матрицы отображают статистические значения, областью действия которых являются пересечения групп строк и столбцов, к которым принадлежит ячейка. Например, если в матрице есть группа строк («Категория») и две группы столбцов («Территория» и «Год»), где отображается сумма продаж, то в отчете будут две ячейки с суммами продаж для каждого значения в группе «Категория». Областью действия ячеек являются два пересечения: «Категория» и «Территория», а также «Категория» и «Год». В матрице могут быть вложенные и смежные группы. Вложенные группы имеют связь «родители-потомки», а смежные группы — одноранговую связь. Предусмотрена возможность добавлять подытоги для всех уровней вложенных групп строк и столбцов в пределах матрицы.  
  
 Чтобы сделать матричные данные более удобными для чтения и выделить данные, к которым необходимо привлечь внимание, можно выполнить слияние ячеек или провести разбиение по горизонтали и вертикали и применить форматирование к данным и заголовкам групп.  
  
 Можно также включить переключатели детализации, которые по умолчанию скрывают подробные данные, чтобы пользователи могли по желанию отобразить подробные сведения.  
  
 Дополнительные сведения см. в разделе [Создание матрицы](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md).  
  
##  <a name="List"></a> Список  
 Список используется для создания макета свободной формы. Возможности не ограничены созданием макета сетки, поля можно располагать в списке произвольно. С помощью списка можно создавать формы для отображения большого количества полей набора данных или нескольких областей данных рядом для сгруппированных данных. Например, можно определить для списка группу, добавить таблицу, диаграмму и изображение, затем отобразить каждое из значений в табличной или графической форме, как для записи о сотруднике или пациенте.  
  
 ![Добавлен новый список из элементов, выбранных](../../reporting-services/report-design/media/rs-listtemplatenewselected.gif "добавлен новый список из элементов, выбранных")  
  
 Дополнительные сведения см. в разделе [Создание счета-фактуры и формы со списками].  
  
##  <a name="PreparingData"></a> Подготовка данных  
 Такие области данных, как таблица, матрица и список, отображают данные из набора данных. Можно подготовить данные в запросе, который получает данные для набора данных, либо указать свойства в таблице, матрице или списке.  
  
 Языки запросов, например [!INCLUDE[tsql](../../includes/tsql-md.md)], которые используются при получении данных для наборов данных отчета, позволяют подготавливать данные с помощью фильтров для включения только подмножества данных, с заменой значения NULL или пробелов константами, что делает отчет более удобным для чтения, а также обеспечивает сортировку и группирование данных.  
  
 Если решено подготавливать данные в области данных отчета (в таблице, матрице или списке), то свойства задаются применительно к области данных или к ячейкам в области данных. Если требуется фильтровать или сортировать данные, задавайте свойства применительно к области данных. Например, чтобы отсортировать данные, укажите столбцы, по которым выполняется сортировка, и направление сортировки. Если требуется предоставить альтернативное значение для поля, задайте значения текста ячейки, в которой отображается поле. Например, для отображения текста «Пусто» в пустом поле или поле со значением NULL можно использовать выражение, задающее такое значение.  
  
 Дополнительные сведения см. в разделе [Подготовка данных для отображения в области данных табликса (построитель отчетов и службы SSRS)](../../reporting-services/report-design/preparing-data-for-display-in-a-tablix-data-region-report-builder-and-ssrs.md).  
  
##  <a name="BuildingConfiguringTableMatrixList"></a> Построение и настройка таблицы, матрицы или списка  
 При добавлении к отчету таблиц или матриц можно воспользоваться мастером таблиц и матриц или создать их вручную на основе шаблонов построителя отчетов и конструктора отчетов. Списки формируются вручную с помощью шаблона списка.  
  
 Мастер помогает быстро построить и настроить таблицу или матрицу. После завершения работы мастера или создания области данных табликса с нуля можно продолжить настройку и доработку этих объектов. Диалоговые окна, которые можно вызывать из контекстных меню в областях данных, упрощают ввод наиболее часто задаваемых свойств разрывов страницы, повторяемости и видимости верхних и нижних колонтитулов, параметров отображения, фильтров и сортировки. Однако множество дополнительных свойств, предусмотренных для области данных табликса, можно задавать только на панели «Свойства» построителя отчетов. Например, если набор данных для таблицы, матрицы или списка пуст, то для отображения соответствующего сообщения текст сообщения необходимо задать в свойстве табликса NoRowsMessage на панели "Свойства".  
  
##  <a name="ChangingBetweenTablixTemplates"></a> Смена шаблонов табликсов  
 Выбор не ограничивается исходным шаблоном табликса. По мере добавления групп, итогов и меток может возникнуть необходимость изменить формат табликса. Например, можно начать с таблицы, затем удалить строку подробных сведений и добавить группы столбцов. Дополнительные сведения см. в разделе [Изучение возможностей области данных табликса (построитель отчетов и службы SSRS)](../../reporting-services/report-design/exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md).  
  
 Далее можно создать таблицу, матрицу или список путем добавления любого элемента табликса. Среди возможностей табликса есть такие функции, как отображение подробных данных или статистики для сгруппированных данных в строках или столбцах. Можно создавать вложенные группы, независимые смежные или рекурсивные группы. Можно фильтровать и сортировать сгруппированные данные или без затруднений объединять группы путем включения нескольких выражений групп в определение группы  
  
 Кроме того, можно добавлять итоги по группам или общие итоги для области данных. Можно скрывать строки или столбцы, чтобы упростить внешний вид отчета и позволить пользователю включать и отключать отображение скрытых данных, как в отчете с углубленной детализацией. Дополнительные сведения см. в разделе [Управление отображением области данных табликса на странице отчетов (построитель отчетов и службы SSRS)](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md).  
  
##  <a name="HowTo"></a> Инструкции  
 В этом разделе перечислены процедуры, которые показывают шаг за шагом, как работать с таблицами, матрицами и списками в конкретных отчетах, как отображать данные в строках и столбцах, добавлять и удалять столбцы, подвергать слиянию ячейки и включать подытоги для групп строк и столбцов.  
  
-   [Добавление группы подробных сведений (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md)  
  
-   [Добавление итога в группу или область данных табликса (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
-   [Изменение элемента в ячейке (построитель отчетов и службы SSRS)](../../reporting-services/report-design/change-an-item-within-a-cell-report-builder-and-ssrs.md)  
  
-   [Изменение высоты строки или ширины столбца (построитель отчетов и службы SSRS)](../../reporting-services/report-design/change-row-height-or-column-width-report-builder-and-ssrs.md)  
  
-   [Вставка или удаление столбца (построитель отчетов и службы SSRS)](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md)  
  
-   [Вставка или удаление строки (построитель отчетов и службы SSRS)](../../reporting-services/report-design/insert-or-delete-a-row-report-builder-and-ssrs.md)  
  
-   [Объединение ячеек в области данных (построитель отчетов и службы SSRS)](../../reporting-services/report-design/merge-cells-in-a-data-region-report-builder-and-ssrs.md)  
  
-   [Создание группы рекурсивной иерархии (построитель отчетов и службы SSRS)](../../reporting-services/report-design/create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
-   [Добавление или удаление группы в области данных (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
-   [Отображение верхних и нижних колонтитулов в группе (построитель отчетов и службы SSRS)](../../reporting-services/report-design/display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
-   [Создание пошагового отчета (построитель отчетов и службы SSRS)](../../reporting-services/report-design/create-a-stepped-report-report-builder-and-ssrs.md)  
  
-   [Добавление, перемещение или удаление таблицы, матрицы или списка (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs.md)  
  
##  <a name="InThisSection"></a> В этом разделе  
 В следующих разделах приведены сведения о работе с областью данных табликса.  
  
 [Область данных табликса (построитель отчетов и службы SSRS)](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)  
 Объясняет основные понятия, связанные с областью данных табликса, например области табликса, подробные данные и сгруппированные данные, группы столбцов и строк, а также статические и динамические строки и столбцы.  
  
 [Добавление данных в область данных табликса (построитель отчетов и службы SSRS)](../../reporting-services/report-design/adding-data-to-a-tablix-data-region-report-builder-and-ssrs.md)  
 Содержит подробные сведения о добавлении подробных данных и сгруппированных данных, подытогах и итогах, а также метках для области данных табликса.  
  
 [Управление отображением области данных табликса на странице отчетов (построитель отчетов и службы SSRS)](../../reporting-services/report-design/controlling-the-tablix-data-region-display-on-a-report-page.md)  
 Описывает свойства области данных табликса, с помощью которых можно менять режим отображения области данных табликса во время просмотра этой области в отчете.  
  
 [Управление заголовками строк и столбцов (построитель отчетов и службы SSRS)](../../reporting-services/report-design/controlling-row-and-column-headings-report-builder-and-ssrs.md)  
 Описывает управление заголовками строк и столбцов, когда область данных таблицы, матрицы или списка может охватывать несколько страниц по горизонтали или по вертикали.  
  
 [Создание групп рекурсивной иерархии (построитель отчетов и службы SSRS)](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
 Описывает, как отображать рекурсивные данные, в которых связь между родительским и дочерним объектами представлена полями в наборе данных.  
  
 [Основные сведения о группах (построитель отчетов и службы SSRS)](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)  
 Объясняет, что представляют собой группы и когда они используются, а также описывает группы, доступные для других областей данных табликса.  
  
## <a name="see-also"></a>См. также  
 [Добавление фильтров набора данных, фильтров области данных и групповых фильтров (построитель отчетов и службы SSRS)](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Вложенные области данных &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [Связывание нескольких областей данных к тому же набору данных &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [Выражения &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Фильтр, группы и сортировка данных &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Параметры отчета &#40; Построитель отчетов и конструктор отчетов &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Диаграммы &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Датчики &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  