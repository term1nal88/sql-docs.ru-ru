---
title: "sys.dm_io_cluster_valid_path_names (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_io_cluster_valid_path_names
- dm_io_cluster_valid_path_names_TSQL
- sys.dm_io_cluster_valid_path_names_TSQL
- dm_io_cluster_valid_path_names
dev_langs: TSQL
helpviewer_keywords:
- dm_io_cluster_valid_path_names
- sys.dm_io_cluster_valid_path_names
- cluster valid path names
- csv name
- cluster shared volume names
ms.assetid: 5bc8a0e5-6c72-425b-8c58-f276eb9add2c
caps.latest.revision: "6"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ceaf5223a8f86f5ede0bff6bbc20844a7ede26b7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmioclustervalidpathnames-transact-sql"></a>sys.dm_io_cluster_valid_path_names (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Возвращает сведения обо всех допустимых общих дисках, включая кластеризованные общие тома, для экземпляра отказоустойчивого кластера SQL Server. Если экземпляр не кластеризован, то возвращается пустой набор строк.  
  
|Имя столбца|Тип данных|Description|  
|-----------------|---------------|-----------------|  
|**путь**|**Nvarchar(512)**|Точка подключения тома или путь к диску, который может использоваться как корневой каталог для файлов баз данных и журналов. Не допускает значение NULL.|  
|**cluster_owner_node**|**Nvarchar(64)**|Текущий владелец диска. Для кластеризованных общих томов (CSV) ― это владелец узла, на котором размещен сервер метаданных. Не допускает значение NULL.|  
|**is_cluster_shared_volume**|**Бит**|Возвращает значение 1, если диск, на котором находится этот путь, является общим томом кластера. В противном случае возвращается значение 0.|  
  
## <a name="remarks"></a>Замечания  
 Для хранения файлов баз данных и журналов экземпляр отказоустойчивого кластера SQL Server (FCI) должен использовать хранилище, которое является общим для всех узлов отказоустойчивого кластера. В данном представлении приведен список дисков из группы кластерных ресурсов, связанной с этим экземпляром. Только эти диски можно использовать для хранения файлов данных и журналов.  
  
> [!NOTE]  
>  Данное представление заменит [sys.dm_io_cluster_shared_drives &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md) в будущем выпуске.  
  
## <a name="permissions"></a>Permissions  
 Пользователь должен иметь на экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] разрешение VIEW SERVER STATE.  
  
## <a name="examples"></a>Примеры  
 В следующем примере показано применение функции sys.dm_io_cluster_valid_path_names для определения общих дисков на экземпляре кластеризованного сервера:  
  
```  
SELECT * FROM sys.dm_io_cluster_valid_path_names;  
```  
  
## <a name="see-also"></a>См. также:  
 [sys.dm_os_cluster_nodes &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-cluster-nodes-transact-sql.md)   
 [sys.dm_io_cluster_shared_drives &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [Динамические административные представления и функции (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
