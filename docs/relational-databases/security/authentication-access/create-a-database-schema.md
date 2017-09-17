---
title: "Создание схемы базы данных | Документация Майкрософт"
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.schemas.general.f1
helpviewer_keywords:
- creating schemas with Management Studio
- CREATE SCHEMA [Management Studio]
- database schemas
- schemas [SQL Server], creating
ms.assetid: ed2a5522-f4d2-4111-95a4-d3e1e5081739
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 3a224f5be40f6f7a68a28cb4c8f741c24527e8bd
ms.openlocfilehash: b164e70bf4b1e7586d8e70ab8edb7baa1dfcaade
ms.contentlocale: ru-ru
ms.lasthandoff: 07/31/2017

---
# <a name="create-a-database-schema"></a>Создание схемы базы данных
  В этом разделе описывается создание схемы в [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] с помощью среды [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] или [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **В этом разделе**  
  
-   **Перед началом работы выполните следующие действия.**  
  
     [Ограничения](#Restrictions)  
  
     [Безопасность](#Security)  
  
-   **Создание схемы с помощью следующих средств**  
  
     [Среда SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Restrictions"></a> Ограничения  
  
-   Новая схема принадлежит одному из следующих участников уровня базы данных: пользователю базы данных, роли базы данных или роли приложения. Объекты, создаваемые в схеме, принадлежат владельцу схемы и имеют значение NULL для **principal_id** в **sys.objects**. Владение объектами, содержащимися в схеме, можно передать любому участнику уровня базы данных, однако у владельца схемы всегда остается разрешение CONTROL на объекты в схеме.  
  
-   Если при создании объекта базы данных указать допустимый субъект домена (пользователя или группу) в качестве владельца объекта, то этот субъект добавляется в базу данных в качестве схемы. Новая схема принадлежит этому субъекту домена.  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
  
-   Требует разрешения CREATE SCHEMA в базе данных.  
  
-   Чтобы назначить другого пользователя владельцем создаваемой схемы, у участника должно быть разрешение IMPERSONATE на этого пользователя. Если роль базы данных указана в качестве владельца, то вызывающий объект должен входить в роль или иметь на нее разрешение ALTER.  
  
##  <a name="SSMSProcedure"></a> Использование среды SQL Server Management Studio  
  
##### <a name="to-create-a-schema"></a>Создание схемы  
  
1.  В обозревателе объектов раскройте папку **Базы данных** .  
  
2.  Разверните базу данных, в которой создается новая схема базы данных.  
  
3.  Щелкните правой кнопкой мыши папку **Безопасность** , укажите на пункт **Создать**и выберите **Схема**.  
  
4.  В диалоговом окне **Схема — создать** на странице **Общие** введите имя новой схемы в поле **Имя схемы** .  
  
5.  В поле **Владелец схемы** введите имя пользователя или роли базы данных, которые будут владельцем схемы. Также можно нажать кнопку **Поиск** , чтобы открыть диалоговое окно **Поиск ролей и пользователей** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Дополнительные параметры  
 Диалоговое окно **Схема — Создать** также содержит параметры на двух дополнительных страницах: **Разрешения** и **Расширенные свойства**.  
  
-   На странице **Разрешения** перечислены все возможные защищаемые объекты и разрешения на эти объекты, которые могут быть предоставлены для имени входа.  
  
-   Страница **Расширенные свойства** позволяет добавлять пользовательские свойства пользователям базы данных.  
  
##  <a name="TsqlProcedure"></a> Использование Transact-SQL  
  
#### <a name="to-create-a-schema"></a>Создание схемы  
  
1.  В **обозревателе объектов**подключитесь к экземпляру компонента [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  На стандартной панели выберите пункт **Создать запрос**.  
  
3.  В следующем примере создается схема `Chains`, а затем таблица `Sizes`.  
    ```sql  
    CREATE SCHEMA Chains;
    GO
    CREATE TABLE Chains.Sizes (ChainID int, width dec(10,2));
    ```

4.  Дополнительные операции могут быть выполнены в рамках одной инструкции. В следующем примере создается принадлежащая Annik схема `Sprockets`, которая содержит таблицу `NineProngs`. Инструкция предоставляет разрешение `SELECT` для Mandar и запрещает `SELECT` для Prasanna.  

    ```sql  
    CREATE SCHEMA Sprockets AUTHORIZATION Annik  
        CREATE TABLE NineProngs (source int, cost int, partnumber int)  
        GRANT SELECT ON SCHEMA::Sprockets TO Mandar  
        DENY SELECT ON SCHEMA::Sprockets TO Prasanna;  
    GO  
    ```  
5. Чтобы просмотреть схемы в этой базе данных, выполните следующую инструкцию.

   ```sql
   SELECT * FROM sys.schemas;
   ```

 Дополнительные сведения см. в разделе [CREATE SCHEMA (Transact-SQL)](../../../t-sql/statements/create-schema-transact-sql.md).  
  
  
