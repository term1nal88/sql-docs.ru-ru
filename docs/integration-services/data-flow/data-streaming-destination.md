---
title: "Назначения потоковой передачи данных | Документы Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: b2a918e3460d23f33f432ea0925d722f9aefde78
ms.contentlocale: ru-ru
ms.lasthandoff: 08/17/2017

---
# <a name="data-streaming-destination"></a>Назначение потоковой передачи данных
  **Назначение потоковой передачи данных** — это компонент назначения служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS), который позволяет **поставщику OLE DB для служб SSIS** использовать выходные данные пакета служб SSIS в качестве табличного результирующего набора. Можно создать связанный сервер, использующий поставщик OLE DB для служб SSIS, а затем выполнить SQL-запрос к связанному серверу, чтобы просмотреть данные, возвращаемые пакетом служб SSIS.  
  
 В приведенном ниже примере следующий запрос возвращает выходные данные из пакета Package.dtsx в проекте SSISPackagePublishing в папке Power BI каталога служб SSIS. Этот запрос использует связанный сервер с именем [Default Linked Server for Integration Services], который, в свою очередь, использует новый поставщик OLE DB для служб SSIS. Запрос содержит имя папки, имя проекта и имя пакета в каталоге служб SSIS. Поставщик OLE DB для служб SSIS запускает пакет, указанный в запросе, и возвращает табличный результирующий набор.  
  
```  
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>Компоненты публикации веб-канала данных  
 К компонентам публикации веб-каналов данных относятся поставщик OLE DB для служб SSIS, назначение потоковой передачи данных и мастер публикации пакетов служб SSIS. С помощью мастера можно опубликовать пакет служб SSIS в экземпляре базы данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в виде представления SQL. Мастер помогает создать связанный сервер, использующий поставщик OLE DB для служб SSIS, и представление SQL, представляющее запрос на связанном сервере. Представление для результатов запроса запускается из пакета служб SSIS в качестве табличного набора данных.  
  
 Чтобы убедиться, что поставщик SSISOLEDB установлен, в SQL Server Management Studio разверните узлы **Объекты сервера**, **Связанные серверы**, **Поставщики**и проверьте, отображается ли поставщик **SSISOLEDB** . Дважды щелкните **SSISOLEDB**, установите параметр **Допускать в ходе процесса** , если он не установлен, а затем нажмите кнопку **ОК**.  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>Публикация пакета служб SSIS в качестве представления SQL  
 Ниже описаны действия по публикации пакета служб SSIS в качестве представления SQL.  
  
1.  Создайте пакет служб SSIS с помощью компонента **назначения потоковой передачи данных** и разверните пакет в каталоге служб SSIS.  
  
2.  Откройте **мастер публикации пакетов служб SSIS** , запустив файл ISDataFeedPublishingWizard.exe из расположения C:\Program Files\Microsoft SQL Server\130\DTS\Binn или мастер публикации веб-каналов данных в меню "Пуск".  
  
     Мастер создает связанный сервер с помощью поставщика OLE DB для служб SSIS (SSISOLEDB), а затем — представление SQL, состоящее из запроса на связанном сервере. Этот запрос содержит имя папки, имя проекта и имя пакета в каталоге служб SSIS.  
  
3.  Выполните представление SQL в SQL Server Management Studio и просмотрите результаты из пакета служб SSIS. Представление отправляет запрос поставщику OLE DB для служб SSIS через созданный связанный сервер. Поставщик OLE DB для служб SSIS выполняет пакет, указанный в запросе, и возвращает табличный результирующий набор.  
  
> [!IMPORTANT]  
>  Подробные инструкции см. в статье [Пошаговое руководство. Публикация пакета служб SSIS в представлении SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md).  
  
## <a name="expose-output-data-from-an-ssis-package-as-an-odata-feed-by-using-the-power-bi-admin-center"></a>Предоставление выходных данных из пакета служб SSIS в качестве веб-каналов OData с помощью Центра администрирования Power BI  
 С помощью Центра администрирования Power BI ИТ-администраторы могут предоставить пользователям данные из локальных источников данных в виде веб-каналов OData. По умолчанию в Центре администрирования Power BI можно зарегистрировать только источники данных SQL Server. Однако на портале в качестве источников данных можно зарегистрировать пакеты служб SSIS, используя **назначение потоковой передачи данных** и **поставщик OLE DB (Майкрософт) для служб SQL Server Integration Services (SSISOLEDB)** , и предоставить результирующие данные пакета служб SSIS пользователю в виде веб-канала OData.  
  
 Центр администрирования позволяет публиковать представления в базе данных SQL Server. Таким образом, вы можете опубликовать пакет служб SSIS в качестве представления SQL, используя мастер публикации пакетов служб SSIS. Затем в Центре администрирования Power BI можно выбрать представление, которое следует включить в веб-канал OData. Администратор данных может обращаться к веб-каналу из пакета служб SSIS, используя надстройку Power Query для Excel.  
  
 Подробное пошаговое руководство см. в разделе [Публикация пакетов служб SSIS в качестве источников веб-каналов OData](http://go.microsoft.com/fwlink/?LinkID=317367).  
  
## <a name="in-this-section"></a>В этом разделе  
  
-   [Пошаговое руководство. Публикация пакета служб SSIS в представлении SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
## <a name="configure-data-streaming-destination"></a>Настройка назначения потоковой передачи данных
  Настроить назначение потоковой передачи данных можно с помощью диалогового окна **Advanced Editor for Data Streaming Destination** (Расширенный редактор для назначения потоковой передачи данных). Чтобы открыть это диалоговое окно, дважды щелкните компонент или щелкните правой кнопкой мыши компонент в конструкторе потоков данных и выберите пункт **Изменить**.  
  
 Это диалоговое окно содержит три вкладки: **Свойства компонента**, **Входные столбцы**и **Свойства входов и выходов**.  
  
## <a name="component-properties-tab"></a>Вкладка "Свойства компонента"  
 Эта вкладка содержит следующие изменяемые поля:  
  
|Поле|Description|  
|-----------|-----------------|  
|Название|Имя компонента назначения потоковой передачи данных в пакете.|  
|ValidateExternalMetadata|Указывает, проверяется ли компонент во время разработки с использованием внешних источников данных. Если задано значение False, проверка с использованием внешних источников данных откладывается до времени выполнения.|  
|IDColumnName|В представлении, созданном в мастере публикации веб-каналов данных, есть дополнительный столбец идентификатора. Столбец идентификатора выступает в качестве EntityKey для выходных данных из потока данных, если данные используются в качестве канала OData в других приложениях.<br /><br /> Имя по умолчанию для этого столбца — _ID. Однако можно указать и другое имя.|  
  
## <a name="input-columns-tab"></a>Вкладка "Входные столбцы"  
 В верхней области этой вкладки отображаются все доступные входные столбцы. Выберите столбцы, которые требуется включить в выходные данные этого компонента. Выбранные столбцы отображаются в списке в нижней области. Имя выходного столбца можно изменить, введя новое имя в поле **Выходной псевдоним** в списке.  
  
## <a name="input-output-properties-tab"></a>Вкладка "Свойства входов и выходов"  
 Как и на вкладке "Входные столбцы", на этой вкладке можно изменить имена выходных столбцов. В древовидном представлении слева разверните узел **Data Streaming Destination Input** (Входные данные назначения потоковой передачи данных), а затем — **Входные столбцы**. Щелкните имя входного столбца и измените имя выходного столбца в области справа.  
  
## <a name="see-also"></a>См. также:  
 [Публикация пакетов служб SSIS в качестве источников веб-каналов OData](http://go.microsoft.com/fwlink/?LinkID=317367)  
  
  