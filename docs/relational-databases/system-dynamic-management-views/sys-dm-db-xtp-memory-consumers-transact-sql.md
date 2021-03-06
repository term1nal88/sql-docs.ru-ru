---
title: sys.dm_db_xtp_memory_consumers (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers
- dm_db_xtp_memory_consumers_TSQL
- sys.dm_db_xtp_memory_consumers_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_memory_consumers dynamic management view
ms.assetid: f7ab2eaf-e627-464d-91fe-0e170b3f37bc
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3f1a3a5403c4549205c226f25d6c925ef81d4b10
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47856522"
---
# <a name="sysdmdbxtpmemoryconsumers-transact-sql"></a>sys.dm_db_xtp_memory_consumers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Сообщает о потребителях памяти уровня базы данных в компоненте Database Engine [!INCLUDE[hek_2](../../includes/hek-2-md.md)]. Представление возвращает по строке для каждого потребителя памяти, используемого компонентом Database Engine. Используйте это динамическое административное Представление, чтобы увидеть, как память распределяется между различных внутренних объектов.  
  
 Дополнительные сведения см. в разделе [In-Memory OLTP (оптимизация в памяти)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|memory_consumer_id|**bigint**|Идентификатор (внутренний) потребителя памяти.|  
|memory_consumer_type|**int**|Тип потребителя памяти:<br /><br /> 0 = агрегатная функция. (Суммирует использование памяти для двух или более потребителей. Не должен отображаться.)<br /><br /> 2 = VARHEAP (Отслеживает потребление памяти для кучи переменной длины.)<br /><br /> 3 = HASH (Отслеживает потребление памяти для индекса.)<br /><br /> 5 = пул страниц БД (Отслеживает потребление памяти для пула страниц базы данных, используемого для операций времени выполнения. Например, переменных таблиц и некоторых сериализуемых сканирований. Для одной базы данных существует только один потребитель памяти этого типа.)|  
|memory_consumer_type_desc|**Nvarchar(64)**|Тип потребителя памяти: VARHEAP, HASH или PGPOOL.<br /><br /> 0 — (Он не должен отображаться.)<br /><br /> 2 — VARHEAP<br /><br /> 3 — HASH<br /><br /> 5 — PGPOOL|  
|memory_consumer_desc|**Nvarchar(64)**|Описание экземпляра потребителя памяти.<br /><br /> VARHEAP: <br />Куча базы данных. Используется для выделения данных пользователя для базы данных (строк).<br />Куча системы базы данных. Используется для выделения данных базы данных, которые будут включены в дампы памяти и не содержат пользовательских данных.<br />Куча индекса диапазона. Частная куча, используемая индексом диапазона для выделения страниц BW.<br /><br /> ХЭШ: Описание отсутствует, поскольку object_id указывает таблицу, а index_id сам хэш-индекс.<br /><br /> PGPOOL: Для базы данных имеется только одна страница пула пул страниц Database 64K.|  
|object_id|**bigint**|Идентификатор объекта, к которому относится выделенная память. Для системных объектов значение отрицательное.|  
|xtp_object_id|**bigint**|Идентификатор объекта для таблицы, оптимизированной для памяти.|  
|index_id|**int**|Идентификатор индекса потребителя (если применимо). Значение NULL для базовых таблиц.|  
|allocated_bytes|**bigint**|Число байтов, зарезервированных для этого потребителя памяти.|  
|used_bytes|**bigint**|Число байтов, используемых этим потребителем. Относится только к varheap.|  
|allocation_count|**int**|Количество выделений.|  
|partition_count|**int**|Только для внутреннего применения.|  
|sizeclass_count|**int**|Только для внутреннего применения.|  
|min_sizeclass|**int**|Только для внутреннего применения.|  
|max_sizeclass|**int**|Только для внутреннего применения.|  
|memory_consumer_address|**varbinary**|Внутренний адрес потребителя памяти. Только для внутреннего применения.|  
|xtp_object_id|**bigint**|Идентификатор объекта в памяти OLTP, соответствует таблице, оптимизированной для памяти.|  
  
## <a name="remarks"></a>Примечания  
 На выходе выделения пространства на уровнях базы данных представляют собой пользовательские таблицы, индексы и системные таблицы. VARHEAP с object_id = NULL относится к памяти, выделенной для таблицы со столбцами переменной длины.  
  
## <a name="permissions"></a>Разрешения  
 Если имеется разрешение VIEW DATABASE STATE в текущей базе данных, возвращаются все строки. В противном случае возвращается пустой набор строк.  
  
 Если разрешения VIEW DATABASE нет, возвращаются все столбцы для строк в таблицах, для которых включено разрешение SELECT.  
  
 Системные таблицы возвращаются только для пользователей с разрешением VIEW DATABASE STATE.  
  
## <a name="general-remarks"></a>Общие замечания  
 Когда оптимизированных для памяти таблица имеет индекс columnstore, система использует некоторые из внутренних таблиц, которые используют определенный объем памяти, для отслеживания данных для индекса columnstore. Дополнительные сведения об этих внутренних таблицах и примеры запросов, отображающий их показатель потребления памяти см. [sys.memory_optimized_tables_internal_attributes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-memory-optimized-tables-internal-attributes-transact-sql.md).
 
  
## <a name="examples"></a>Примеры  
  
```  
-- memory consumers (database level)  
SELECT OBJECT_NAME(object_id), *   
FROM sys.dm_db_xtp_memory_consumers;  
```  
  
## <a name="user-scenario"></a>Пользовательский сценарий  
  
```  
-- memory consumers (database level)  
  
select  convert(char(10), object_name(object_id)) as Name,   
convert(char(10),memory_consumer_type_desc ) as memory_consumer_type_desc, object_id,index_id, allocated_bytes,  used_bytes   
from sys.dm_db_xtp_memory_consumers  
```  
  
 Ниже приводятся выходные данные с подмножеством столбцов. Механизмы распределения памяти на уровнях базы данных — это пользовательские таблицы, индексы и системные таблицы. VARHEAP с object_id = NULL (последняя строка) — это память, выделенная строкам данных в таблицах (в примере ниже это t1). Число выбранных байт, преобразованное в МБ, составляет 1340 МБ.  
  
```  
Name       memory_consumer_type_desc object_id   index_id    allocated_bytes      used_bytes  
---------- ------------------------- ----------- ----------- -------------------- --------------------  
t3         HASH                      629577281   2           8388608              8388608  
t2         HASH                      597577167   2           8388608              8388608  
t1         HASH                      565577053   2           1048576              1048576  
NULL       HASH                      -6          1           2048                 2048  
NULL       VARHEAP                   -6          NULL        0                    0  
NULL       HASH                      -5          3           8192                 8192  
NULL       HASH                      -5          2           8192                 8192  
NULL       HASH                      -5          1           8192                 8192  
NULL       HASH                      -4          1           2048                 2048  
NULL       VARHEAP                   -4          NULL        0                    0  
NULL       HASH                      -3          1           2048                 2048  
NULL       HASH                      -2          2           8192                 8192  
NULL       HASH                      -2          1           8192                 8192  
NULL       VARHEAP                   -2          NULL        196608               26496  
NULL       HASH                      0           1           2048                 2048  
NULL       PGPOOL                    0           NULL        0                    0  
NULL       VARHEAP                   NULL        NULL        1405943808           1231220560  
  
(17 row(s) affected)  
```  
  
 Общий объем памяти выделенного и используемого из этого динамического административного Представления совпадает с уровнем объекта в [sys.dm_db_xtp_table_memory_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql.md).  
  
```  
select  sum(allocated_bytes)/(1024*1024) as total_allocated_MB,   
        sum(used_bytes)/(1024*1024) as total_used_MB  
from sys.dm_db_xtp_memory_consumers  
  
total_allocated_MB   total_used_MB  
-------------------- --------------------  
1358                 1191  
```  
  
## <a name="see-also"></a>См. также  
 [Оптимизированные для памяти динамические административные представления таблиц &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
