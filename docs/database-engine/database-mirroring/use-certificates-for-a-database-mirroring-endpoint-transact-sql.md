---
title: "Использование сертификатов для конечной точки зеркального отображения базы данных (Transact-SQL) | Документы Майкрософт"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: f7c23cc2-48dc-4b78-b441-89ca29a0bd9e
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5ece75ebe6293747d9ac677a4913bc7323615c8f
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="use-certificates-for-a-database-mirroring-endpoint-transact-sql"></a>Использование сертификатов для конечной точки зеркального отображения базы данных (Transact-SQL)
  Для обеспечения возможности выполнения проверки подлинности при помощи сертификата при зеркальном отображении базы данных на данном экземпляре сервера, системный администратор должен настроить каждый экземпляр сервера для использования сертификатов, как для входящих, так и для исходящих соединений. Вначале должны быть настроены исходящие соединения.  
  
> [!NOTE]  
>  Все соединения зеркального отображения экземпляра сервера используют одну и ту же конечную точку зеркального отображения базы данных, и при ее создании необходимо задать метод проверки подлинности экземпляра сервера. Таким образом, экземпляр сервера может использовать только одну форму проверки подлинности при зеркальном отображении базы данных.  
  
## <a name="configuring-outbound-connections"></a>Настройка исходящих соединений  
 На каждом экземпляре сервера, настраиваемом для зеркального отображения базы данных, должны быть выполнены следующие шаги:  
  
1.  В базе данных **master** создайте главный ключ базы данных.  
  
2.  В базе данных **master** создайте зашифрованный сертификат для экземпляра сервера.  
  
3.  Создайте конечную точку для экземпляра сервера при использовании его сертификата.  
  
4.  Создайте резервную копию сертификата в файле и защищенным образом скопируйте этот файл на другие системы.  
  
 Все эти этапы необходимо выполнить для каждого из участников, а также для следящего сервера, если он есть.  
  
 Дополнительные сведения см. в разделе [Включение использования сертификатов для исходящих соединений в конечной точке зеркального отображения базы данных (Transact-SQL)](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md).  
  
## <a name="configuring-inbound-connections"></a>Настройка входящих соединений  
 Для каждого из участников, настраиваемых для зеркального отображения базы данных, выполните следующие шаги. В базе данных **master** :  
  
1.  Создайте имя входа для другой системы.  
  
2.  Создайте пользователя для этого имени входа.  
  
3.  Получите сертификат для конечной точки зеркального отображения другого экземпляра сервера.  
  
4.  Свяжите сертификат с пользователем, созданным на шаге 2.  
  
5.  Предоставьте этому имени входа разрешение CONNECT на эту конечную точку зеркального отображения.  
  
 Если имеется следящий сервер, для него также необходимо настроить входящие соединения. Для этого нужно настроить имена входа, пользователей и сертификаты для следящего сервера на обоих участниках, и наоборот.  
  
 Дополнительные сведения см. в разделе [Включение использования сертификатов для входящих соединений в конечной точке зеркального отображения базы данных (Transact-SQL)](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md).  
  
## <a name="security"></a>Безопасность  
 За исключением случаев, когда сеть гарантированно защищена, рекомендуется для соединений зеркального отображения базы данных применять шифрование. Дополнительные сведения см. в разделе [Конечная точка зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
 При копировании сертификата на другую систему используйте безопасный метод копирования. Отнеситесь с особым вниманием к хранению сертификатов в безопасном месте.  
  
## <a name="see-also"></a>См. также:  
 [Создание главного ключа базы данных](../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [CREATE MASTER KEY (Transact-SQL)](../../t-sql/statements/create-master-key-transact-sql.md)   
 [Безопасность транспорта для зеркального отображения баз данных и групп доступности AlwaysOn (SQL Server)](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Центр обеспечения безопасности для Базы данных Azure SQL и ядра СУБД SQL Server](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [Конечная точка зеркального отображения базы данных (SQL Server)](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
