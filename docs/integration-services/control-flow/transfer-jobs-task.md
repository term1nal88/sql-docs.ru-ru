---
title: "Задача «Передача заданий» | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferjobstask.f1
- sql13.dts.designer.transferjobstask.general.f1
- sql13.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: a4264d737901fbb7c023e216d3d8faf5309469f9
ms.contentlocale: ru-ru
ms.lasthandoff: 08/11/2017

---
# <a name="transfer-jobs-task"></a>Задача «Передача заданий»
  Задача «Передача заданий» служит для передачи одного или нескольких заданий агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] между экземплярами [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Задачу «Передача заданий» можно настроить на передачу всех или только определенных заданий. Можно также указать, будут ли переданные задания доступны в месте назначения.  
  
 Задания, подлежащие передаче, могут уже существовать в месте назначения. Задачу «Передача заданий» можно настроить на обработку существующих задач одним из следующих способов:  
  
-   Перезаписать существующие задания.  
  
-   Аварийно завершить задачу при наличии дубликатов заданий.  
  
-   Пропустить дубликаты заданий.  
  
 Во время выполнения задача «Передача заданий» подключается к исходному и целевому серверу, используя один или два диспетчера соединений SMO. Диспетчер соединений SMO настраивается независимо от задачи «Передача заданий», но задача будет на него ссылаться. Диспетчер соединений SMO определяет сервер и режим проверки подлинности, используемый для доступа к серверу. Дополнительные сведения см. в статье [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>Передача заданий между экземплярами SQL Server  
 Задача «Передача заданий» поддерживает исходные серверы и серверы назначения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ограничений в отношении использования определенных версий источника или целевого объекта не существует.  
  
## <a name="events"></a>События  
 Задача «Передача заданий» инициирует уведомляющее событие, сообщающее число переданных заданий, а также событие-предупреждение в случае, когда задание перезаписывается. Задача не сообщает о ходе передачи задания; она сообщает лишь о выполнении 0% и 100%.  
  
## <a name="execution-value"></a>Значение выполнения  
 Значение выполнения, определяемое свойством **ExecutionValue** задачи, возвращает число переданных заданий. Назначив пользовательскую переменную значению свойства **ExecValueVariable** задачи "Передача заданий", можно сделать сведения о передаче заданий доступными для других объектов пакета. Дополнительные сведения см. в разделах [Переменные в службах Integration Services (SSIS)](../../integration-services/integration-services-ssis-variables.md) и [Использование переменных в пакетах](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  
  
## <a name="log-entries"></a>Записи журнала  
 Задача «Передача заданий» позволяет настраивать запись в журнал следующих событий:  
  
-   TransferJobsTaskStarTransferringObjects   Эта запись журнала сообщает о начале передачи. В записях журнала указывается время запуска.  
  
-   TransferJobsTaskStarTransferringObjects   Эта запись журнала сообщает об окончании передачи. В записях журнала указывается время завершения.  
  
 Кроме того, запись журнала о событии **OnInformation** сообщает число переданных заданий, а запись журнала о событии **OnWarning** производится при перезаписи каждого задания, находящегося на сервере назначения.  
  
## <a name="security-and-permissions"></a>Безопасность и разрешения  
 Чтобы передавать задания, пользователь должен быть членом предопределенной роли сервера sysadmin или членом одной из предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] для базы данных msdb как в экземпляре-источнике, так и в экземпляре назначения [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>Настройка задачи «Передача заданий»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о свойствах, которые можно задать в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] , см. в следующих разделах:  
  
-   [Страница "Выражения"](../../integration-services/expressions/expressions-page.md)  
  
 Дополнительные сведения об установке этих свойств программным путем см. в следующих разделах:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Связанные задачи  
 Дополнительные сведения об установке этих свойств в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] см. в следующем разделе:  
  
-   [Задание свойств задач или контейнеров](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-jobs-task-editor-general-page"></a>Редактор задачи «Передача заданий» (страница «Общие»)
  Используйте страницу **Общие** в диалоговом окне **Редактор задачи «Передача заданий»** , чтобы назвать и описать задачу передачи заданий.  
  
> [!NOTE]  
>  Только члены предопределенной роли сервера **sysadmin** или одной из предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на целевом сервере могут создавать задания. Чтобы получить доступ к задачам на исходном сервере, пользователи должны быть элементами, по меньшей мере, предопределенной роли базы данных **SQLAgentUserRole** . Дополнительные сведения о предопределенных ролях базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и их разрешениях см. в разделе [Предопределенные роли базы данных агента SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
### <a name="options"></a>Параметры  
 **Название**  
 Введите уникальное имя для задачи «Передача заданий». Это имя используется в качестве метки для значка задачи.  
  
> [!NOTE]  
>  Имена задач в пределах пакета должны быть уникальными.  
  
 **Description**  
 Введите описание задачи «Передача заданий».  
  
## <a name="transfer-jobs-task-editor-jobs-page"></a>Редактор задачи «Передача заданий» (страница «Задания»)
  Используйте страницу **Задания** диалогового окна **Редактор задачи «Передача заданий»** для определения свойств копирования одного или более заданий агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] из одного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в другой.  
  
> [!NOTE]  
>  Для доступа к задачам на исходном сервере пользователи должны быть членами хотя бы одной предопределенной роли базы данных **SQLAgentUserRole** на этом сервере. Для успешного создания задания на целевом сервере пользователь должен быть членом предопределенной роли сервера **sysadmin** или одной из предопределенных ролей базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Дополнительные сведения о предопределенных ролях базы данных агента [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] и их разрешениях см. в разделе [Предопределенные роли базы данных агента SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
### <a name="options"></a>Параметры  
 **SourceConnection**  
 Выберите из списка диспетчер соединений SMO или нажмите кнопку  **\<создать соединение... >** для создания нового соединения с исходным сервером.  
  
 **DestinationConnection**  
 Выберите из списка диспетчер соединений SMO или нажмите кнопку  **\<создать соединение... >** для создания нового соединения на сервере назначения.  
  
 **TransferAllJobs**  
 Укажите, должна задача копировать с исходного сервера на целевой все задания или только те, которые указаны агентом [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Параметры этого свойства приведены в следующей таблице.  
  
|Значение|Description|  
|-----------|-----------------|  
|**True**|Копировать все задания.|  
|**False**|Копировать только выбранные задания.|  
  
 **JobsList**  
 Нажмите кнопку обзора **(…)** , чтобы выбрать задания для копирования. Необходимо выбрать хотя бы одно задание.  
  
> [!NOTE]  
>  Прежде чем выбирать задания для копирования, укажите свойство **SourceConnection** .  
  
 Параметр **JobsList** недоступен, если параметр **TransferAllJobs** равен **True**.  
  
 **IfObjectExists**  
 Определите, как задача должна обрабатывать задания с именем, которое уже есть на целевом сервере.  
  
 Параметры этого свойства приведены в следующей таблице.  
  
|Значение|Description|  
|-----------|-----------------|  
|**FailTask**|Задача завершается сбоем, если задание с таким именем уже есть на целевом сервере.|  
|**Overwrite**|Задача перезаписывает задание с таким же именем на целевом сервере.|  
|**Skip**|Задача пропускает задание, если задание с таким именем уже есть на целевом сервере.|  
  
 **EnableJobsAtDestination**  
 Определите, будут ли активированы задания, скопированные на целевой сервер.  
  
 Параметры этого свойства приведены в следующей таблице.  
  
|Значение|Description|  
|-----------|-----------------|  
|**True**|Включить задания на целевом сервере.|  
|**False**|Отключить задания на целевом сервере.|  
  
## <a name="see-also"></a>См. также:  
 [Задачи служб Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Поток управления](../../integration-services/control-flow/control-flow.md)  
  
  