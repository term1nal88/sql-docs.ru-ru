---
title: Резервные копии только для копирования (SQL Server) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
caps.latest.revision: 46
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8d5ef086b610402e2c696196b2baae7705c5f920
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248884"
---
# <a name="copy-only-backups-sql-server"></a>Резервные копии только для копирования (SQL Server)
  *Резервная копия только для копирования* — это резервная копия [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], которая не зависит от обычной последовательности создания традиционных резервных копий [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Обычно создание резервного копирования приводит к изменению базы данных и влияет на то, как будут восстанавливаться последующие резервные копии. Однако иногда приходится выполнять резервное копирование базы данных для особых нужд, когда это не сказывается на общем процессе резервного копирования и восстановления. Этой цели служат резервные копии только для копирования.  
  
 Резервные копии только для копирования имеют следующие типы.  
  
-   Полные резервные копии только для копирования (все модели восстановления).  
  
     Резервная копия только для копирования не может служить в качестве базовой копии для разностного копирования или разностного резервного копирования и не влияет на базовую копию для разностного копирования.  
  
     Операция восстановления полной резервной копии только для копирования аналогична операции восстановления любой полной резервной копии.  
  
-   Резервные копии журналов только для копирования (модель полного восстановления и модель восстановления с неполным протоколированием).  
  
     Резервная копия журналов только для копирования сохраняет текущую точку архивирования журнала и, следовательно, не влияет на последовательность обычных резервных копий журналов. Никакой необходимости в резервных копиях журналов только для копирования обычно нет. Вместо этого можно создать новую обычную резервную копию журналов (с параметром WITH NORECOVERY), затем использовать ее совместно со всеми остальными ранее созданными резервными копиями журналов, которые необходимы для последовательности восстановления. Однако резервная копия журналов только для копирования иногда может быть полезна для выполнения восстановления в сети. Пример см. в разделе [Пример. Оперативное восстановление файла, доступного для чтения и записи (модель полного восстановления)](example-online-restore-of-a-read-write-file-full-recovery-model.md).  
  
     Журнал транзакций никогда не усекается после создания резервной копии только для копирования.  
  
 Резервные копии только для копирования записываются в столбец **is_copy_only** таблицы [backupset](/sql/relational-databases/system-tables/backupset-transact-sql) .  
  
## <a name="to-create-a-copy-only-backup"></a>Создание резервной копии только для копирования  
 Резервную копию только для копирования можно создать с помощью среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]или PowerShell.  
  
###  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
1.  На странице **Общие** диалогового окна **Создание резервной копии базы данных** выберите **Резервная копия только для копирования** .  
  
###  <a name="TsqlProcedure"></a> Использование Transact-SQL  
 Требуемый синтаксис [!INCLUDE[tsql](../../../includes/tsql-md.md)] выглядит следующим образом:  
  
-   Для полных резервных копий только для копирования:  
  
     BACKUP DATABASE *имя_базы_данных* TO \<устройство_резервного_копирования*>* ... WITH COPY_ONLY…  
  
    > [!NOTE]  
    >  Если параметр COPY_ONLY указан одновременно с параметром DIFFERENTIAL, он не имеет эффекта.  
  
-   Для резервных копий журнала только для копирования:  
  
     BACKUP LOG *имя_базы_данных* TO *\<* устройство_резервного_копирования*>* … WITH COPY_ONLY…  
  
###  <a name="PowerShellProcedure"></a> Использование PowerShell  
  
1.  Используйте `Backup-SqlDatabase` командлет с `-CopyOnly` параметра.  
  
##  <a name="RelatedTasks"></a> Связанные задачи  
 **Создание полной резервной копии или резервной копии журнала**  
  
-   [Создание полной резервной копии базы данных (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [Создание резервной копии журнала транзакций (SQL Server)](back-up-a-transaction-log-sql-server.md)  
  
 **Просмотр резервных копий только для копирования**  
  
-   [backupset (Transact-SQL)](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
 **Настройка и использование поставщика SQL Server PowerShell**  
  
-   [Поставщик SQL Server PowerShell](../../powershell/sql-server-powershell-provider.md)  
  

  
## <a name="see-also"></a>См. также  
 [Общие сведения о резервном копировании (SQL Server)](backup-overview-sql-server.md)   
 [Модели восстановления (SQL Server)](recovery-models-sql-server.md)   
 [Копирование баз данных путем создания и восстановления резервных копий](../databases/copy-databases-with-backup-and-restore.md)   
 [Обзор процессов восстановления (SQL Server)](restore-and-recovery-overview-sql-server.md)  
  
  