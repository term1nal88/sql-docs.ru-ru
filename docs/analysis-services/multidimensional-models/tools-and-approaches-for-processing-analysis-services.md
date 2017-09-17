---
title: "Средства и подходы для обработки (службы Analysis Services) | Документы Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- process [Analysis Services]
- processing [Analysis Services]
ms.assetid: 82347a16-4145-4655-8adf-2a300f1fdf99
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5eecf424cf155c53a2f636590ba002028f24db84
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="tools-and-approaches-for-processing-analysis-services"></a>Средства и способы обработки (службы Analysis Services)
  Обработка — это операция, при которой службы Analysis Services запрашивают реляционный источник данных и заполняют этими данными объекты служб Analysis Services.  
  
 Как администратор служб Analysis Services, вы можете выполнять и мониторить обработку объектов служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] с применением следующих подходов.  
  
-   Проведение анализа влияния для получения представления о зависимостях объектов и области операций.  
  
-   Обработка отдельных объектов в среде [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Обработка отдельных или нескольких объектов в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   Проведение анализа влияния для просмотра списка связанных объектов, обработка которых будет отменена в результате текущего действия.  
  
-   Создание и выполнение скрипта в окне запросов XMLA служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] в среде [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] для обработки отдельных или нескольких объектов.  
  
-   Использование командлетов PowerShell в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Использование потоков управления и задач в пакетах служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
-   Наблюдение за обработкой с помощью приложения SQL Server Profiler.  
  
-   Программирование пользовательского решения с помощью объектов AMO. Дополнительные сведения см. в статье [Programming AMO OLAP Basic Objects](../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md).  
  
 Обработка имеет широкие возможности настройки, управляемые набором параметров обработки, которые определяют тип обработки (полная или добавочная), выполняемой на уровне объектов. Дополнительные сведения об обработке параметров и объектов см. в разделах [Параметры обработки (службы Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md) и [Обработка объектов служб Analysis Services](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md).  
  
> [!NOTE]  
>  В этом разделе описываются средства и подходы для обработки многомерных моделей. Дополнительные сведения об обработке табличных моделей см. в разделах [Обработка базы данных, таблицы или секции (службы Analysis Services)](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md) и [Обработка данных (табличные службы Analysis Services)](../../analysis-services/tabular-models/process-data-ssas-tabular.md).  
  
### <a name="processing-objects-in-sql-server-management-studio"></a>Обработка объектов в среде SQL Server Management Studio  
  
1.  Запустите среду [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] и подключитесь к службам Analysis Services.  
  
2.  Щелкните правой кнопкой мыши объект служб Analysis Services, который необходимо обработать, и выберите команду **Обработать**. Данные можно обрабатывать на любом из следующих уровней:  
  
    -   Базы данных  
  
    -   Кубы  
  
    -   Группы мер или отдельные секции в группе мер  
  
    -   Измерения  
  
    -   Модели интеллектуального анализа данных  
  
    -   Структуры интеллектуального анализа данных  
  
     Объекты служб Analysis Services являются иерархическими. При выборе базы данных может произойти обработка всех содержащихся в базе данных объектов. Происходит ли обработка фактически, зависит от выбранных параметров обработки и состояния объектов. В частности, если объект не обработан, то при обработке его родительского объекта будет обработан и сам этот объект. Дополнительные сведения о зависимостях объектов см. в разделе [Processing Analysis Services Objects](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md).  
  
3.  В диалоговом окне **Обработка** в поле **Параметры обработки**оставьте заданное по умолчанию значение или выберите другой вариант из списка. Дополнительные сведения о каждом параметре см. в разделе [Настройка параметров обработки (службы Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
4.  Нажмите кнопку **Анализ влияния** , чтобы выделить и при необходимости обработать зависимые объекты, которые будут затронуты при обработке объектов, перечисленных в диалоговом окне «Обработка».  
  
5.  Также можно нажать кнопку **Изменить параметры** , чтобы изменить порядок обработки, операции обработки при определенных видах ошибок или другие параметры.  
  
6.  Нажмите кнопку **ОК**.  
  
     В диалоговом окне «Ход обработки» отображается текущее состояние выполнения каждой из команд. Если сообщение о состоянии усечено, нажмите кнопку **Просмотр подробностей** , чтобы просмотреть сообщение целиком.  
  
### <a name="processing-objects-in-sql-server-data-tools"></a>Обработка объектов в SQL Server Data Tools  
  
1.  Запустите среду [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] и откройте уже развернутый проект.  
  
2.  В обозревателе решений откройте папку **Измерения** , вложенную в развернутый проект.  
  
3.  Щелкните измерение правой кнопкой мыши и выберите команду **Обработать**. Вы можете щелкнуть правой кнопкой мыши несколько измерений, чтобы одновременно обработать несколько объектов. Дополнительные сведения см. в разделе [Пакетная обработка (службы Analysis Services)](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md).  
  
4.  Убедитесь в том, что в диалоговом окне **Обработка измерения** в разделе **Список объектов** для столбца **Параметры обработки**выбран параметр **Обработка. Полная**. Если этот параметр не выбран, выделите столбец **Параметры обработки**, а затем в раскрывающемся списке выберите пункт **Полная обработка** .  
  
5.  Нажмите кнопку **Запустить**.  
  
6.  После завершения обработки нажмите кнопку **Закрыть**.  
  
##  <a name="bkmk_impactanalysis"></a> Проведение анализа влияния для определения зависимостей объектов и области операций  
  
1.  Перед обработкой объекта служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] в среде [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] или [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]можно выполнить анализ влияния на связанные объекты, нажав кнопку **Анализ влияния** в одном из диалоговых окон **Обработка объектов** .  
  
2.  Щелкните правой кнопкой мыши измерение, куб, группу мер или секцию, чтобы открыть диалоговое окно **Обработка объектов** .  
  
3.  Нажмите кнопку **Анализ влияния**. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] просматривают модель и сообщают о требованиях повторной обработки для объектов, которые связаны с объектом, выбранным для обработки.  
  
### <a name="processing-objects-using-xmla"></a>Обработка объектов с помощью XMLA  
  
1.  Запустите среду [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] и подключитесь к службам Analysis Services.  
  
2.  Щелкните правой кнопкой мыши обрабатываемый объект и выберите команду **Обработать**.  
  
3.  В диалоговом окне **Обработка** выберите нужный параметр обработки. При необходимости измените другие параметры. Запустите анализ влияния, чтобы определить, какие изменения может потребоваться внести.  
  
4.  На экране **Обработать объекты** нажмите кнопку **Скрипт** .  
  
     Будет сформирован скрипт XMLA, а затем откроется окно «Службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] — запрос XML для аналитики».  
  
5.  Закройте диалоговое окно. Скрипт содержит команду обработки и параметры, указанные в диалоговом окне.  
  
6.  Также вы можете продолжить добавление инструкций в скрипт, если нужно обработать в этом пакете дополнительные объекты. Чтобы продолжить, повторите предыдущие действия, добавив инструкции в созданный скрипт, чтобы получить один скрипт для всех операций обработки. Пример см. в разделе [Schedule SSAS Administrative Tasks with SQL Server Agent](../../analysis-services/instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md).  
  
7.  Нажмите в строке меню кнопку **Запрос**и выберите пункт **Выполнить**.  
  
### <a name="processing-objects-using-powershell"></a>Обработка объектов с помощью PowerShell  
  
1.  Начиная с этого выпуска SQL Server, командлеты служб Analysis Services PowerShell можно использовать для обработки объектов. Следующие командлеты можно запускать интерактивно или из скрипта:  
  
    -   [Командлет Invoke-ProcessCube](../../analysis-services/powershell/invoke-processcube-cmdlet.md)  
  
    -   [Командлет Invoke-ProcessDimension](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)  
  
    -   [Командлет Invoke-PolicyEvaluation](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)  
  
    -   [Командлет Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md), который может использоваться для выполнения скриптов XMLA, MDX или DMX, содержащих команды обработки.  
  
### <a name="monitoring-object-processing-using-sql-server-profiler"></a>Наблюдение за обработкой объектов в приложении SQL Server Profiler  
  
1.  Подключитесь к экземпляру служб Analysis Services в приложении SQL Server Profiler.  
  
2.  В окне «Выбор событий» нажмите кнопку **Показать все события** , чтобы добавить все события в список.  
  
3.  Выберите следующие события.  
  
    -   **Начало команды** и **Завершение команды** , чтобы показать, когда обработка начинается и останавливается.  
  
    -   **Ошибка** , чтобы регистрировать ошибки.  
  
    -   **Начало отчета о состоянии**, **Текущий отчет о состоянии**и **Окончание отчета о состоянии** , чтобы сообщать о состоянии обработки и показывать SQL-запросы, используемые для получения данных.  
  
    -   **Начало выполнения скрипта многомерных выражений** и **Конец выполнения скрипта многомерных выражений** , чтобы показать вычисления кубов.  
  
    -   Также можно добавить события блокировки, если идет диагностика проблем с производительностью, относящихся к обработке.  
  
### <a name="process-analysis-services-objects-using-integration-services"></a>Обработка объектов служб Analysis Services с использованием служб Integration Services  
  
1.  В службах [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]создайте пакет, который используют задачу «Обработка средствами Analysis Services» для автоматического заполнения объектов новыми данными при регулярном обновлении исходной реляционной базы данных.  
  
2.  В окне **Область элементов служб SSIS**дважды щелкните элемент **Обработка средствами Analysis Services** , чтобы добавить его в пакет.  
  
3.  Измените задачу, указав соединение с базой данных, объекты для обработки и параметр обработки. Дополнительные сведения о реализации этой задачи см. в разделе [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md).  
  
## <a name="see-also"></a>См. также  
 [Обработка многомерной модели (службы Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  