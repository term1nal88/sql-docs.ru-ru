---
title: sp_help_fulltext_columns (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns
- sp_help_fulltext_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns
ms.assetid: 92c8656b-f7fd-4904-9796-acc9ffed4106
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 622a0eafad0c4b029c0fd9512c25defa63229fc0
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169364"
---
# <a name="sphelpfulltextcolumns-transact-sql"></a>sp_help_fulltext_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Возвращает столбцы, предназначенные для полнотекстового индексирования.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Используйте [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) вместо этого представление каталога.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Аргументы  
 [  **@table_name=**] **"**_таблицы\_имя_**"**  
 Одно- или двухкомпонентное имя таблицы, для которой запрашиваются сведения о полнотекстовом индексе. *TABLE_NAME* — **nvarchar(517)**, со значением по умолчанию NULL. Если *table_name* опущен, сведения о столбце полнотекстового индекса извлекаются для каждой таблицы с индексом полнотекстового поиска.  
  
 [  **@column_name=**] **"**_столбец\_имя_**"**  
 Имя столбца, для которого запрашиваются метаданные полнотекстового индекса. *column_name* — **sysname**, со значением по умолчанию NULL. Если *column_name* опущен или имеет значение NULL, возвращаются сведения о столбце полнотекстового поиска для каждого полнотекстового индексированного столбца для *table_name*. Если *table_name* также опущен или имеет значение NULL, возвращаются сведения о столбце полнотекстового индекса для каждого полнотекстового индексированного столбца для всех таблиц в базе данных.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="result-sets"></a>Результирующие наборы  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Владелец таблицы. Это имя пользователя базы данных, создавшего таблицу.|  
|**TABLE_ID**|**int**|Идентификатор таблицы.|  
|**ИМЯ_ТАБЛИЦЫ**|**sysname**|Имя таблицы.|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|Столбец таблицы с полнотекстовым индексом, предназначенной для индексирования.|  
|**FULLTEXT_COLID**|**int**|Идентификатор столбца с полнотекстовым индексом.|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|Столбец в таблице с полнотекстовым индексом, указывающий тип документа столбца с полнотекстовым индексом. Это значение применимо только в случае, когда полнотекстовый индексированный столбец является **varbinary(max)** или **изображение** столбца.|  
|**FULLTEXT_BLOBTP_COLID**|**int**|Идентификатор столбца типа документа. Это значение применимо только в случае, когда полнотекстовый индексированный столбец является **varbinary(max)** или **изображение** столбца.|  
|**FULLTEXT_LANGUAGE**|**sysname**|Язык, используемый для полнотекстового поиска в столбце.|  
  
## <a name="permissions"></a>Разрешения  
 По умолчанию разрешения на выполнение предоставлены членам роли **public** .  
  
## <a name="examples"></a>Примеры  
 В нижеследующем примере возвращаются сведения о столбцах, которые были предназначены для полнотекстового индексирования в таблице `Document`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_columns 'Production.Document';  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [Системные хранимые процедуры (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
