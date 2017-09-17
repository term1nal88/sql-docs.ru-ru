---
title: "Функции повышения производительности потока данных | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Integration Services packages, performance
- performance [Integration Services]
- data flow [Integration Services], troubleshooting
- SQL Server Integration Services packages, performance
- loading data
- control flow [Integration Services], troubleshooting
- SSIS packages, performance
- packages [Integration Services], performance
- queries [Integration Services], troubleshooting
- sorting data [Integration Services]
- aggregations [Integration Services]
ms.assetid: c4bbefa6-172b-4547-99a1-a0b38e3e2b05
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c812dc44b0348d6f77e7f7e8efe23acab85a0d48
ms.contentlocale: ru-ru
ms.lasthandoff: 08/03/2017

---
# <a name="data-flow-performance-features"></a>Data Flow Performance Features
  В этом разделе приведены советы по проектированию пакетов служб [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , помогающие избежать общих проблем с производительностью. Кроме того, в этом разделе содержатся сведения по функциям и средствам, позволяющим устранить неполадки с производительностью пакетов.  
  
## <a name="configuring-the-data-flow"></a>Настройка потока данных  
 Повысить производительность задачи потока данных можно путем настройки свойств этой задачи, изменения размера буфера и настройки пакета для параллельного выполнения.  
  
### <a name="configure-the-properties-of-the-data-flow-task"></a>Настройка свойств задачи потока данных  
  
> [!NOTE]  
>  Свойства, рассматриваемые в этом разделе, должны устанавливаться отдельно для каждой задачи потока данных в пакете.  
  
 Можно настроить следующие свойства задачи потока данных, влияющие на производительность.  
  
-   Указать местоположение временного хранилища буферных данных (свойство BufferTempStoragePath) и столбцов, содержащих данные объектов типа BLOB (свойство BLOBTempStoragePath). По умолчанию эти свойства содержат значения переменных среды TEMP и TMP. Для хранения временных файлов можно указать другие папки на другом или более быстром жестком диске либо распределить их по нескольким дискам. Можно указать несколько каталогов, разделяя имена каталогов точками с запятой.  
  
-   Определить размер буфера по умолчанию для задачи, установив свойство DefaultBufferSize, и задать максимальное количество строк для каждого буфера, установив свойство DefaultBufferMaxRows. Задайте свойство AutoAdjustBufferSize, указывающее, рассчитывается ли размер буфера по умолчанию на основе значения свойства DefaultBufferMaxRows. Размер буфера по умолчанию равен 10 МБ, а максимальный размер буфера равен 2^31-1 байт. Максимальное количество строк равно 10 000.  
  
-   Установить число потоков, которые может использовать задача в процессе выполнения, установив свойство EngineThreads. Это свойство рекомендует подсистеме обработки потока данных использовать определенное количество потоков. По умолчанию оно равно 10, минимальное количество потоков равно 3. Однако подсистема обработки потока данных не использует потоков больше, чем требуется, независимо от значения этого свойства. Подсистема обработки потока данных может также использовать больше потоков, чем задано этим свойством, если нужно избежать проблем параллелизма.  
  
-   Указать, следует ли выполнять задачу потока данных в режиме оптимизации (свойство RunInOptimizedMode). Режим оптимизации повышает производительность, удаляя из потока данных неиспользуемые столбцы, выходы и компоненты.  
  
    > [!NOTE]  
    >  Свойство с тем же именем, RunInOptimizedMode, можно задать в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] на уровне проекта, чтобы указать, что задача потока данных должна запускаться в режиме оптимизации во время отладки. Это свойство переопределяет свойство RunInOptimizedMode задач потока данных во время проектирования.  
  
### <a name="adjust-the-sizing-of-buffers"></a>Настройка размера буфера  
 Подсистема обработки потока данных начинает задачу определения размера буфера, вычисляя предполагаемый размер одной строки данных. Затем она умножает предполагаемый размер строки на значение DefaultBufferMaxRows, чтобы получить предварительное рабочее значение размера буфера.  
  
-   Если для параметра AutoAdjustBufferSize указано значение true, подсистема обработки потока данных использует вычисленное значение как размер буфера, а значение параметра DefaultBufferSize игнорируется.  
  
-   Если для параметра AutoAdjustBufferSize указано значение false, подсистема обработки потока данных использует следующие правила для определения размера буфера.  
  
    -   Если результат больше значения DefaultBufferSize, подсистема обработки потока данных уменьшает количество строк.  
  
    -   Если результат меньше внутренне вычисляемого минимального размера буфера, подсистема обработки потока данных увеличивает количество строк.  
  
    -   Если результат находится между минимальным размером буфера и значением DefaultBufferSize, подсистема обработки потока данных устанавливает размер буфера как можно ближе к предполагаемому размеру строки, умноженному на значение DefaultBufferMaxRows.  
  
 В начале тестирования задач потока данных используйте значения по умолчанию для свойств DefaultBufferSize и DefaultBufferMaxRows. Включите ведение журналов в задаче потока данных и выберите событие BufferSizeTuning для определения количества строк, содержащихся в каждом буфере.  
  
 Перед началом настройки размера буфера самым важным улучшением является уменьшение размера каждой строки данных путем удаления ненужных столбцов и соответствующая конфигурация типов данных.  
  
 Для определения оптимального числа буферов и их размеров поэкспериментируйте со значениями свойств DefaultBufferSize и DefaultBufferMaxRows, наблюдая за уровнем производительности и сведениями, получаемыми событием BufferSizeTuning.  
  
 Не увеличивайте размер буфер до такого размера, при котором он начнет записываться на диск. При записи буфера на диск производительность ниже, чем при неоптимизированном буфере. Чтобы определить, происходит ли запись на диск, наблюдайте за счетчиком производительности "Выгружено буферов" в оснастке "Производительность" консоли управления [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MMC).  
  
### <a name="configure-the-package-for-parallel-execution"></a>Настройка пакета для параллельного выполнения  
 Параллельное выполнение повышает производительность на компьютерах с несколькими физическими или логическими процессорами. Для поддержки параллельного выполнения различных задач в пакете в службах [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] используются два свойства **MaxConcurrentExecutables** и **EngineThreads**.  
  
#### <a name="the-maxconcurrentexcecutables-property"></a>Свойство MaxConcurrentExcecutables  
 Свойство **MaxConcurrentExecutables** является свойством самого пакета. Оно определяет число одновременно работающих задач. По умолчанию оно имеет значение –1, что означает число физических или логических процессоров +2.  
  
 Чтобы понять работу этого свойства, рассмотрим образец пакета, в котором есть три задачи потока данных. Если задать для свойства **MaxConcurrentExecutables** значение 3, то все три задачи потока данных смогут выполняться одновременно. Однако предположим, что каждая задача потока данных имеет 10 деревьев выполнения «источник-назначение». Если свойство **MaxConcurrentExecutables** имеет значение 3, то нельзя гарантировать, что деревья выполнения внутри каждой задачи потока данных будут работать параллельно.  
  
#### <a name="the-enginethreads-property"></a>Свойство EngineThreads  
 Свойство **EngineThreads** является свойство задачи потока данных. Это свойство определяет число потоков, которое подсистема обработки потока данных может создать и выполнять параллельно. Свойство **EngineThreads** применяется одинаково как к потокам источника, которые подсистема обработки потока данных создает для источников, так и к потокам исполнителя, которые подсистема создает для преобразований и назначений. Таким образом, если свойство **EngineThreads** имеет значение 10, подсистема может создавать до десяти потоков источника и до десяти потоков исполнителя.  
  
 Чтобы понять работу этого свойства, рассмотрим образец пакета с тремя задачами потока данных. Каждая задача потока данных содержит десять деревьев выполнения «источник-назначение». Если свойство EngineThreads для каждой задачи потока данных имеет значение 10, все 30 деревьев выполнения потенциально могут выполняться одновременно.  
  
> [!NOTE]  
>  Обсуждение работы с потоками выходит за пределы данного раздела. Однако общее правило — не запускать параллельно больше потоков, чем доступно процессоров. Запуск большего количества потоков, чем доступно процессоров, может снизить производительность из-за частого переключения контекста между потоками.  
  
## <a name="configuring-individual-data-flow-components"></a>Настройка отдельных компонентов потока данных  
 В этом разделе приведены общие рекомендации по настройке отдельных компонентов потоков данных для достижения лучшей производительности. Кроме того, существуют конкретные рекомендации по каждому из типов компонентов потока данных: источнику, преобразованию и назначению.  
  
### <a name="general-guidelines"></a>Общие рекомендации  
 Для всех компонентов потока данных есть две общие рекомендации, которым необходимо следовать для повышения производительности: оптимизация запросов и отказ от использования необязательных строк.  
  
#### <a name="optimize-queries"></a>Оптимизация запросов  
 Многие компоненты потока данных используют запросы как для извлечения данных из источников, так и для операций поиска, чтобы создать ссылочные таблицы. По умолчанию запрос использует инструкцию SELECT * FROM \<tableName > синтаксис. Этот тип запроса возвращает все столбцы исходной таблицы. Так как все столбцы доступны во время разработки, можно выбрать любой столбец в качестве столбца поиска, сквозного или исходного столбца. Однако после выбора используемых столбцов следует изменить запрос таким образом, чтобы в него были включены только выбранные столбцы. Удаление неиспользуемых столбцов делает поток данных пакета более эффективным, так как чем меньше столбцов, тем меньше создаваемая строка. А чем короче строка, тем больше строк может быть загружено в один буфер и тем меньше усилий потребует обработка всех строк набора данных.  
  
 Запрос можно создать путем ввода или с помощью построителя запросов.  
  
> [!NOTE]  
>  При запуске пакета в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]на вкладке «Ход выполнения» конструктора служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] отображаются предупреждения. Они включают обнаружение любых столбцов данных, которые источник делает доступными для потока данных, но которые впоследствии не используются нисходящими компонентами потока данных. Для автоматического удаления таких столбцов можно использовать свойство **RunInOptimizedMode** .  
  
#### <a name="avoid-unnecessary-sorting"></a>Исключение ненужной сортировки  
 Сортировка является потенциально медленной операцией, поэтому исключение ненужной сортировки может повысить производительность потока данных пакета.  
  
 Иногда источник данных уже упорядочен до использования нисходящим компонентом. Такая предварительная сортировка может происходить при использовании запроса SELECT с предложением ORDER BY, а также при вставке данных в источник в порядке сортировки. Для подобных, предварительно отсортированных исходных данных можно предоставить указание о том, что эти данные уже отсортированы, чтобы избежать использования преобразования «Сортировка» в соответствии с требованиями определенных нисходящих преобразований. Например, для преобразования «Слияние» и «Соединение слиянием» требуются отсортированные входные данные. Чтобы предоставить указание о том, что данные отсортированы, необходимо выполнить следующие задачи.  
  
-   Присвойте значение **IsSorted** свойству **True**на выходе из вышестоящего компонента потока данных.  
  
-   Укажите ключевые столбцы, по которым отсортированы данные.  
  
 Дополнительные сведения см. в разделе [Сортировка данных для преобразований "Слияние" и "Соединение слиянием"](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Если данные должны быть отсортированы в потоке данных, производительность потока данных может быть повышена за счет использования минимального количества операций сортировки. Например, в потоке данных для копирования набора данных используется преобразование «Многоадресная доставка». Выполните сортировку набора данных один раз перед запуском преобразования «Многоадресная доставка» вместо сортировки выходных данных после преобразования.  
  
 Дополнительные сведения см. в разделах [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md), [Merge Transformation](../../integration-services/data-flow/transformations/merge-transformation.md), [Merge Join Transformation](../../integration-services/data-flow/transformations/merge-join-transformation.md)и [Multicast Transformation](../../integration-services/data-flow/transformations/multicast-transformation.md).  
  
### <a name="sources"></a>Источники  
  
#### <a name="ole-db-source"></a>Источник OLE DB  
 При получении данных из представления с помощью источника OLE DB выберите режим доступа к данным «Команда SQL» и введите инструкцию SELECT. Обращение к данным с помощью инструкции SELECT дает более высокую производительность, чем при выборе режима доступа к данным «Таблица или представление».  
  
### <a name="transformations"></a>Преобразования  
 Советы в этом разделе служат для повышения производительности при преобразованиях «Статистическая обработка», «Нечеткий уточняющий запрос», «Нечеткое группирование», «Уточняющий запрос», «Cоединение слиянием» и «Медленно изменяющееся измерение».  
  
#### <a name="aggregate-transformation"></a>Преобразование «Статистическая обработка»  
 Преобразование «Статистическая обработка» содержит свойства **Keys**, **KeysScale**, **CountDistinctKeys**и **CountDistinctScale** . Эти свойства улучшают производительность, позволяя преобразованию предварительно выделять память в размере, необходимом для кэширования данных. Если известно точное или приблизительное число групп, которые будут являться результатом операции **Группировать по** , задайте свойства **Keys** и **KeysScale** соответственно. Если известно точное или приблизительное число различающихся значений, которые будут являться результатом операции **Подсчет различных объектов** , задайте свойства **CountDistinctKeys** и **CountDistinctScale** соответственно.  
  
 Если в потоке данных необходимо создать несколько статистических выражений, попробуйте использовать одно преобразование «Статистическая обработка» вместо создания нескольких преобразований. Такой подход, в частности, повысит производительность, если статистическая обработка является подмножеством другой статистической обработки, поскольку преобразование сможет оптимизировать внутреннее хранилище и просматривать входящие данные только один раз. Например, если статистическое выражение использует предложение GROUP BY и статистическое выражение AVG, объединение их в одно преобразование может повысить производительность. Однако выполнение нескольких статистических выражений в пределах одного преобразования «Агрегатная обработка» сериализует операции статистической обработки, и таким образом производительность может не повышаться при независимом вычислении нескольких статистических выражений.  
  
#### <a name="fuzzy-lookup-and-fuzzy-grouping-transformations"></a>Преобразования «Нечеткий уточняющий запрос» и «Нечеткое группирование»  
 Сведения по оптимизации производительности преобразований «Нечеткий уточняющий запрос» и «Нечеткое группирование» см. в технической документации [Преобразования «Нечеткий уточняющий запрос» и «Нечеткое группирование» в службах SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604).  
  
#### <a name="lookup-transformation"></a>Преобразование «Уточняющий запрос»  
 Сделайте минимальным объем ссылочных данных в памяти. Для этого введите инструкцию SELECT, которая запрашивает только нужные столбцы. В этом случае производительность будет выше, чем при выборе целой таблицы или представления, поскольку в последнем случае возвращается большой объем ненужных данных.  
  
#### <a name="merge-join-transformation"></a>Merge Join Transformation  
 Настраивать значение свойства **MaxBuffersPerInput** больше не нужно, поскольку корпорация Майкрософт внесла изменения, которые уменьшили риск потребления чрезмерных ресурсов памяти при выполнении операции «Соединение слиянием». Эта проблема иногда возникает, если несколько входов операции «Соединение слиянием» производят данные с различной скоростью.  
  
#### <a name="slowly-changing-dimension-transformation"></a>Преобразование "Медленно изменяющееся измерение"  
 Мастер медленно изменяющихся измерений и преобразование «Медленно изменяющееся измерение» являются средствами общего назначения, удовлетворяющими запросам большинства пользователей. Однако поток данных, формируемый мастером, не оптимизирован по производительности.  
  
 Как правило, самые медленные компоненты преобразования «Медленно изменяющееся измерение» — преобразования «Команда OLE DB», выполняющие инструкции UPDATE одновременно только для одной строки. Таким образом, самым эффективным способом повысить производительность преобразования «Медленно изменяющееся измерение» — замена преобразований «Команда OLE DB». Эти преобразования можно заменить целевыми компонентами, сохраняющими все строки для обновления в промежуточной таблице. Затем можно добавить задачу «Выполнение SQL», которая выполняет одну инструкцию Transact-SQL UPDATE одновременно для всех строк.  
  
 Опытные пользователи могут сконструировать пользовательский поток данных для обработки медленно изменяющегося измерения, оптимизированного для больших измерений. Обсуждение и примеры по решению этой задачи см. в разделе "Сценарий уникального измерения" в техническом документе [Проект REAL: методики извлечения, преобразования и загрузки бизнес-аналитики](http://go.microsoft.com/fwlink/?LinkId=96602).  
  
### <a name="destinations"></a>Назначения  
 Чтобы добиться максимальной производительности при работе с назначениями, рассмотрите возможность использовать назначения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и проверьте их производительность.  
  
#### <a name="sql-server-destination"></a>Назначение SQL Server  
 Когда пакет загружает данные в экземпляр [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на этом же компьютере, используйте назначение [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Это назначение оптимизировано для высокоскоростной массовой загрузки.  
  
#### <a name="testing-the-performance-of-destinations"></a>Тестирование производительности назначений  
 Сохранение данных может занять больше времени, чем ожидается. Чтобы определить, вызвана ли низкая скорость недостаточным быстродействием назначения в обработке данных, можно временно заменить назначение преобразованием «Счетчик строк». Если пропускная способность заметно возрастает, вероятнее всего, замедление скорости вызвано назначением, загружающим данные.  
  
### <a name="review-the-information-on-the-progress-tab"></a>Просмотр сведений на вкладке «Выполнение»  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)]Предоставляет сведения о потока управления и потока данных при запуске пакета [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. На вкладке **Выполнение** приводится список задач и контейнеров в порядке выполнения, в том числе время запуска и окончания работы, предупреждения и сообщения об ошибках каждой задачи или контейнера, включая сам пакет. На ней также представлены список компонентов потока данных в порядке выполнения и сведения о ходе выполнения в виде процентов завершения и количества обработанных строк.  
  
 Чтобы включить или отключить отображение сообщений на вкладке **Выполнение** , установите или снимите флажок **Отчет о ходе отладки** в меню **Службы SSIS** . Отключение отчетов о состоянии способствует повышению производительности выполнения сложных пакетов в среде [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
## <a name="related-tasks"></a>Связанные задачи  
  
-   [Сортировка данных для слияния и преобразования соединения слиянием](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>См. также  
 **Статьи и сообщения в блогах**  
  
-   Техническая статья [Службы SQL Server 2005 Integration Services: стратегия повышения производительности](http://go.microsoft.com/fwlink/?LinkId=98899)на сайте technet.microsoft.com  
  
-   Техническая статья [Службы Integration Services: методы настройки производительности](http://go.microsoft.com/fwlink/?LinkId=98900)на сайте technet.microsoft.com  
  
-   Техническая статья [Increasing Throughput of Pipelines by Splitting Synchronous Transformations into Multiple Tasks (на английском языке)](http://sqlcat.com/technicalnotes/archive/2010/08/18/increasing-throughput-of-pipelines-by-splitting-synchronous-transformations-into-multiple-tasks.aspx)на сайте sqlcat.com  
  
-   Техническая статья [Руководство по производительности загрузки данных](http://go.microsoft.com/fwlink/?LinkId=220816)на сайте msdn.microsoft.com.  
  
-   Техническая статья [We Loaded 1TB in 30 Minutes with SSIS, and So Can You (на английском языке)](http://go.microsoft.com/fwlink/?LinkId=220817)на сайте msdn.microsoft.com.  
  
-   Техническая статья [Top 10 SQL Server Integration Services Best Practices (на английском языке)](http://go.microsoft.com/fwlink/?LinkId=220818)на сайте sqlcat.com.  
  
-   Техническая статья и образец кода [The «Balanced Data Distributor» for SSIS](http://go.microsoft.com/fwlink/?LinkId=220822)на сайте sqlcat.com.  
  
-   Сообщение в блоге [Troubleshooting SSIS Package Performance Issues (на английском языке)](http://go.microsoft.com/fwlink/?LinkId=238156)на сайте blogs.msdn.com  
  
 **Видеоролики**  
  
-   Серия видеоматериалов [Designing and Tuning for Performance your SSIS packages in the Enterprise (SQL Video Series)](http://go.microsoft.com/fwlink/?LinkId=400878)(Проектирование и настройка для повышения производительности пакетов служб SSIS на предприятии (видеоматериалы по SQL Server))  
  
-   Видеоматериал [Tuning Your SSIS Package Data Flow in the Enterprise (SQL Server Video)](http://technet.microsoft.com/sqlserver/ff686901.aspx)(Настройка потока данных пакетов служб SSIS в выпуске Enterprise (видеоматериал по SQL Server)) на сайте technet.microsoft.com  
  
-   Видеоматериал [Understanding SSIS Data Flow Buffers (SQL Server Video)](http://technet.microsoft.com/sqlserver/ff686905.aspx)(Основные сведения о буферах потока данных служб SSIS (видеоматериал по SQL Server)) на сайте technet.microsoft.com  
  
-   Видеоматериал [Microsoft SQL Server Integration Services Performance Design Patterns](http://go.microsoft.com/fwlink/?LinkID=233698&clcid=0x409)на сайте channel9.msdn.com.  
  
-   Презентация [How Microsoft IT Leverages SQL Server 2008 SSIS Dataflow Engine Enhancements (на английском языке)](http://go.microsoft.com/fwlink/?LinkId=217660)на сайте sqlcat.com.  
  
-   Видеоматериал [Balanced Data Distributor](http://go.microsoft.com/fwlink/?LinkID=226278&clcid=0x409)на сайте technet.microsoft.com.  
  
## <a name="see-also"></a>См. также  
 [Инструменты устранения неполадок при разработке пакета](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)   
 [Средства устранения неполадок при выполнении пакета](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  