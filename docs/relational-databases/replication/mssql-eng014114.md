---
title: "MSSQL_ENG014114 | Документация Майкрософт"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014114 error
ms.assetid: f5f04590-e1c6-40d8-ab2b-98c791a0fc44
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0e2f6a83763be1e01adfb8ed08147cc1fb4905d2
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng014114"></a>MSSQL_ENG014114
    
## <a name="message-details"></a>Сведения о сообщении  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|14114|  
|Источник события|MSSQLSERVER|  
|Компонент|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Символическое имя||  
|Текст сообщения|'%s' не настроен в качестве распространителя.|  
  
## <a name="explanation"></a>Объяснение  
 Если в сообщении об ошибке указан конкретный экземпляр, отличный от NULL, это означает, что указанный экземпляр не был настроен должным образом для распознавания распространителем.  
  
 Если в сообщении на месте распространителя указано значение NULL, это означает, что в **главной** базе данных нет записи для локального сервера или что эта запись неверна (например, если компьютер был переименован). Репликация предполагает, что все серверы в топологии должны быть зарегистрированы с использованием имени компьютера и необязательного имени экземпляра (в случае кластеризованного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] имени виртуального сервера и необязательного имени экземпляра). Для правильного функционирования репликации необходимо, чтобы значение, возвращаемое `SELECT @@SERVERNAME` для каждого сервера в топологии, соответствовало имени компьютера или имени виртуального сервера с необязательным именем экземпляра.  
  
 Репликация не поддерживается, если какой-либо из экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] зарегистрирован при помощи IP-адреса или полностью определенного имени домена (FQDN). Эта ошибка может возникать, если при настройке репликации любой из экземпляров [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] был зарегистрирован по IP-адресу или по FQDN в [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
## <a name="user-action"></a>Действие пользователя  
 Если в ошибке указан конкретный экземпляр, необходимо настроить сервер в качестве распространителя. Дополнительные сведения см. в статье [Настройка распространения](../../relational-databases/replication/configure-distribution.md).  
  
 Если в сообщении не указан конкретный экземпляр (NULL), убедитесь, что экземпляр распространителя правильно зарегистрирован. Если сетевое имя компьютера отличается от имени экземпляра SQL Server.  
  
-   Добавьте уникальное имя данного экземпляра SQL Server в качестве допустимого сетевого имени. Один из методов установки альтернативного сетевого имени — это добавление имени в локальный файл hosts. Файл локальных узлов по умолчанию расположен в каталоге WINDOWS\system32\drivers\etc или WINNT\system32\drivers\etc. Дополнительные сведения см. в документации по Windows.  
  
     Например, если имя компьютера — comp1, IP-адрес компьютера — 10.193.17.129, имя экземпляра — inst1/instname, то следует добавить в файл hosts следующую запись:  
  
     10.193.17.129 inst1  
  
-   Отключите распространение, зарегистрируйте экземпляр и восстановите распространение. Если значение @@SERVERNAME недопустимо для некластеризованного экземпляра, выполните следующие действия:  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     После выполнения хранимой процедуры [sp_addserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) необходимо перезапустить службу [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], чтобы изменения параметра @@SERVERNAME вступили в силу.  
  
     Если значение @@SERVERNAME недопустимо для кластеризованного экземпляра, необходимо изменить имя с помощью администратора кластера. Дополнительные сведения см. в статье [Экземпляры отказоустойчивого кластера AlwaysOn (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
## <a name="see-also"></a>См. также:  
 [Справочник по ошибкам и событиям (репликация)](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
