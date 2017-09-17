---
title: "Переименование хранимой процедуры | Документация Майкрософт"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 47182ebd082dfae0963d761e54c4045be927d627
ms.openlocfilehash: 1d0ddb568fd162f4be42234607b5b8484cb89f60
ms.contentlocale: ru-ru
ms.lasthandoff: 07/31/2017

---
# <a name="rename-a-stored-procedure"></a>Изменение имени хранимой процедуры
  В этом разделе описывается, как переименовать хранимую процедуру [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] при помощи среды [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Ограничения](#Restrictions)  
  
     [Безопасность](#Security)  
  
-   **Для переименования хранимой процедуры используется:**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Имена процедур должны соответствовать правилам для [идентификаторов](../../relational-databases/databases/database-identifiers.md).  
  
-   Переименование хранимой процедуры сохраняет `object_id` и все разрешения, которые были специально назначены для этой процедуры. Удаление и повторное создание объекта создает новый `object_id` и удаляет все разрешения, которые были специально назначены для этой процедуры.

-   При переименовании хранимой процедуры не изменяется имя соответствующего объекта в столбце определения **sys.sql_modules** в представлении каталога. Чтобы изменить его, нужно удалить хранимую процедуру и создать ее повторно с новым именем.  

-   Изменение имени или определения процедуры может привести к тому, что все зависящие от нее объекты при выполнении будут возвращать ошибку, если они не будут обновлены в соответствии с внесенными в процедуру изменениями. Дополнительные сведения см. в разделе [Просмотр зависимостей хранимой процедуры](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 CREATE PROCEDURE  
 Требуется разрешение CREATE PROCEDURE на базу данных и разрешение ALTER на схему, в которой создается процедура, либо членство в предопределенной роли базы данных **db_ddladmin** .  
  
 ALTER PROCEDURE  
 Требуется разрешение ALTER на процедуру или членство в предопределенной роли базы данных **db_ddladmin** .  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
#### <a name="to-rename-a-stored-procedure"></a>Изменение имени хранимой процедуры  
  
1.  В обозревателе объектов подключитесь к экземпляру [!INCLUDE[ssDE](../../includes/ssde-md.md)] и разверните его.  
2.  Последовательно разверните узел **Базы данных**, базу данных, которой принадлежит процедура, и узел **Программирование**.  
3.  [Определите зависимости хранимой процедуры](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
4.  Разверните узел **Хранимые процедуры**, щелкните процедуру правой кнопкой мыши и выберите команду **Переименовать**.  
5.  Измените имя хранимой процедуры.  
6.  Измените имя процедуры во всех зависимых от нее объектах и скриптах.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-rename-a-stored-procedure"></a>Изменение имени хранимой процедуры  
  
1.  Установите соединение с компонентом [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
2.  На панели «Стандартная» нажмите **Создать запрос**.  
3.  Скопируйте следующий пример в окно запроса и нажмите кнопку **Выполнить**. В этом примере показано, как переименовать процедуру путем ее удаления и повторного создания с новым именем. В первом примере создается хранимая процедура `'HumanResources.uspGetAllEmployeesTest`. Во втором примере имя хранимой процедуры меняется на `HumanResources.uspEveryEmployeeTest`.  
  
```sql  
--Create the stored procedure.  
USE AdventureWorks2012;  
GO  

CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
EXEC sp_rename 'HumanResources.uspGetAllEmployeesTest', 'HumanResources.uspEveryEmployeeTest'; 
```  
  
## <a name="see-also"></a>См. также:  
 [ALTER PROCEDURE (Transact-SQL)](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md)   
 [Создание хранимой процедуры](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Изменение хранимой процедуры](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Удаление хранимой процедуры](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [Просмотр определения хранимой процедуры](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Просмотр зависимостей хранимой процедуры](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
  
