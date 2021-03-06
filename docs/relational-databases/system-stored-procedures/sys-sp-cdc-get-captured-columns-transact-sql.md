---
title: процедуру sys.sp_cdc_get_captured_columns (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns
- sys.sp_cdc_get_captured_columns_TSQL
- sp_cdc_get_captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_get_captured_columns
- sp_cdc_get_captured_columns
- change data capture [SQL Server], querying metadata
ms.assetid: d9e680be-ab9b-4e0c-b63a-90658f241df8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2cffffa064bbfc5d5d1b106a06fb5429d6ca2c72
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781752"
---
# <a name="sysspcdcgetcapturedcolumns-transact-sql"></a>sys.sp_cdc_get_captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Возвращает сведения о метаданных системы отслеживания измененных данных для исходных столбцов, отслеживаемых указанным экземпляром отслеживания. Система отслеживания измененных данных доступна не во всех выпусках [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Сведения о функциях, поддерживаемых различными выпусками [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], см. в статье [Возможности, поддерживаемые выпусками SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
sys.sp_cdc_get_captured_columns   
    [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>Аргументы  
 [ @capture_instance =] '*capture_instance*"  
 Имя экземпляра отслеживания, связанного с исходной таблицей. *capture_instance* — **sysname** и не может иметь значение NULL.  
  
 Чтобы создать отчет на экземпляры отслеживания для таблицы, выполните [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) хранимой процедуры.  
  
## <a name="return-code-values"></a>Значения кода возврата  
 0 (успешное завершение) или 1 (неуспешное завершение)  
  
## <a name="result-sets"></a>Результирующие наборы  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|Имя схемы исходной таблицы.|  
|source_table|**sysname**|Имя исходной таблицы.|  
|capture_instance|**sysname**|Имя экземпляра отслеживания.|  
|column_name|**sysname**|Имя отслеживаемого исходного столбца данных.|  
|column_id|**int**|Идентификатор столбца в исходной таблице.|  
|column_ordinal|**int**|Положение столбца в исходной таблице.|  
|Тип данных|**sysname**|Тип данных столбца.|  
|character_maximum_length|**int**|Максимальная длина символьного столбца; в противном случае — NULL.|  
|numeric_precision|**tinyint**|Точность чисел для числового столбца; в противном случае — NULL.|  
|numeric_precision_radix|**smallint**|Основание определения точности числовых столбцов; в противном случае — NULL.|  
|numeric_scale|**int**|Масштаб числового столбца; в противном случае — NULL.|  
|datetime_precision|**smallint**|Точность для столбца типа datetime; в противном случае — NULL.|  
  
## <a name="remarks"></a>Примечания  
 Чтобы получить сведения об отслеживаемых столбцах, возвращаемых функций запроса системы отслеживания измененных экземпляра, используйте процедуру sys.sp_cdc_get_captured_columns [cdc.fn_cdc_get_all_changes_ < экземпляр_отслеживания >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) или [cdc.fn_cdc_get_net_changes_ < экземпляр_отслеживания >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md). Имена, идентификаторы и положение столбцов не изменяются в течение всего времени существования экземпляра отслеживания. Изменяется только тип данных столбца, если изменяется тип данных базового исходного столбца отслеживаемой таблицы. Столбцы, добавлении или удалении из исходной таблицы не оказывают влияния на существующие экземпляры отслеживания отслеживаемых столбцов.  
  
 Используйте [sys.sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) для получения сведений об определении данных инструкции языка DDL, применяется к исходной таблице. Результирующий набор содержит сведения обо всех изменениях DDL, изменивших структуру отслеживаемого исходного столбца.  
  
## <a name="permissions"></a>Разрешения  
 Необходимо членство в предопределенной роли базы данных db_owner. Всем остальным пользователям необходимо разрешение SELECT для всех отслеживаемых столбцов в исходной таблице. Кроме того, если для экземпляра отслеживания была определена шлюзовая роль, требуется членство в этой роли базы данных. Если вызывающий объект не имеет разрешения на просмотр исходных данных, то функция возвращает ошибку 22981 (Объект не существует или доступ запрещен).  
  
## <a name="examples"></a>Примеры  
 В следующем примере извлекается информация о столбцах, обрабатываемых экземпляром отслеживания `HumanResources_Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_get_captured_columns   
    @capture_instance = N'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>См. также  
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
