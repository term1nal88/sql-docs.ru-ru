---
title: sys.dm_tcp_listener_states (Transact-SQL) | Документация Майкрософт
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tcp_listener_states
- dm_tcp_listener_states
- sys.dm_tcp_listener_states_TSQL
- dm_tcp_listener_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.dm_tcp_listener_states dynamic management view
ms.assetid: 9997ffed-a4c1-428f-8bac-3b9e4b16d7cf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ee55ca66cdddcc6fcb2a130bfd3427d210297aff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806852"
---
# <a name="sysdmtcplistenerstates-transact-sql"></a>sys.dm_tcp_listener_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Возвращает строку, содержащую сведения о динамическом состоянии для каждого прослушивателя TCP.  
  
> [!NOTE]
> Прослушиватель группы доступности может работать на том же порту, что и прослушиватель экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. В этом случае прослушиватели указываются в списке по отдельности, как и прослушиватель компонента Service Broker.  
  
|Имя столбца|Тип данных|Описание|  
|-----------------|---------------|-----------------|  
|**listener_id**|**int**|Внутренний идентификатор прослушивателя. Не допускает значение NULL.<br /><br /> Первичный ключ.|  
|**IP-адрес**|**nvarchar48**|IP-адрес прослушивателя, который доступен в сети и по которому в настоящее время идет прослушивание. Допустимы адреса IPv4 и IPv6. Если прослушиватель имеет адреса обоих типов, то они указываются в списке раздельно. Шаблон IPv4 отображается как «0.0.0.0». Шаблон IPv6 отображается как «::».<br /><br /> Не допускает значение NULL.|  
|**is_ipv4**|**bit**|Тип IP-адреса<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
|**port**|**int**|Номер порта, на котором работает прослушиватель. Не допускает значение NULL.|  
|**type**|**tinyint**|Тип прослушивателя, может принимать одно из следующих значений:<br /><br /> 0 = [!INCLUDE[tsql](../../includes/tsql-md.md)]<br /><br /> 1 = компонент Service Broker<br /><br /> 2 = зеркальное отображение базы данных<br /><br /> Не допускает значение NULL.|  
|**type_desc**|**nvarchar(20)**|Описание **тип**, используя один из:<br /><br /> TSQL<br /><br /> SERVICE_BROKER<br /><br /> DATABASE_MIRRORING<br /><br /> Не допускает значение NULL.|  
|**state**|**tinyint**|Состояние прослушивателя группы доступности, одно из следующих значений:<br /><br /> 1 = в сети. Прослушиватель принимает и обрабатывает запросы.<br /><br /> 2 = ожидание перезапуска. Прослушиватель не в сети и ожидает перезапуска.<br /><br /> Если прослушиватель группы доступности работает на том же порту, что и экземпляр сервера, то состояние этих двух прослушивателей всегда совпадает.<br /><br /> Не допускает значение NULL.<br /><br /> Примечание: Значения в этом столбце берутся из объекта TSD_listener. Столбец не поддерживает автономное состояние, поскольку при TDS_listener находится в автономном режиме, ее нельзя запросить для состояния.|  
|**state_desc**|**nvarchar(16) в формате**|Описание **состояние**, используя один из:<br /><br /> ONLINE<br /><br /> PENDING_RESTART<br /><br /> Не допускает значение NULL.|  
|**start_time**|**datetime**|Отметка времени, указывающая, когда был запущен прослушиватель. Не допускает значение NULL.|  
  
## <a name="security"></a>безопасность  
  
### <a name="permissions"></a>Разрешения  
 необходимо разрешение VIEW SERVER STATE на сервере.  
  
## <a name="see-also"></a>См. также  
 [Запросив системный каталог SQL Server часто задаваемые вопросы](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Представления каталога групп доступности AlwaysOn (Transact-SQL)](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Динамические административные представления и функции для групп доступности Always On &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
