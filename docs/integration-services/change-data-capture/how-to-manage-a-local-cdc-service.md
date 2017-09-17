---
title: "Как управлять локальной службой CDC | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f9be649-cd93-40c1-bc48-0480106f207c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40678ff92e4513354db09cca42d48ed0302369ac
ms.contentlocale: ru-ru
ms.lasthandoff: 08/03/2017

---
# <a name="how-to-manage-a-local-cdc-service"></a>Как управлять локальной службой CDC
  В этой процедуре описывается использование консоли настройки службы CDC для управления конкретными службами CDC.  
  
### <a name="to-manage-a-specific-cdc-service"></a>Управление конкретной службой CDC  
  
1.  В меню **Пуск** выберите пункт **Конфигурация служб CDC для Oracle**.  
  
2.  На левой панели консоли настройки службы CDC разверните список **Локальные службы CDC**.  
  
3.  Выберите службу CDC, с которой требуется выполнить действия.  
  
     Также можно щелкнуть правой кнопкой мыши службу CDC, с которой требуется начать работу, и выбрать нужное действие.  
  
     **или**  
  
     На левой панели консоли настройки службы CDC выберите пункт **Локальные службы CDC** и в средней части консоли настройки службы CDC выберите службу, с которой необходимо начать работу.  
  
     Также можно щелкнуть правой кнопкой мыши службу CDC, с которой требуется начать работу, и выбрать нужное действие.  
  
4.  При работе со службой CDC можно выполнять следующие задачи.  
  
    -   **Удаление службы**  
  
         На панели **Действия** в правой стороне консоли настройки службы CDC щелкните **Удалить** , чтобы удалить службу.  
  
         Можно также щелкнуть правой кнопкой мыши службу CDC, которую необходимо удалить, и выбрать команду **Удалить**.  
  
         **Примечание**. Если на момент удаления службы она запущена, перед удалением выполняется ее остановка.  
  
         Чтобы удалить определение службы Windows для Oracle CDC, программе нужен доступ в режиме UPDATE к базе данных MSXDBCDC в соответствующем экземпляре [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . После нажатия кнопки **ОК** для удаления службы программа попытается выполнить удаление регистрации службы Oracle CDC в базе данных MSXDBCDC. При ошибке, возникающей из-за отсутствия необходимых разрешений, отображается диалоговое окно ввода имени входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с правами доступа к базе данных MSXDBCDC.  
  
         Дополнительные сведения о вводе данных в диалоговом окне «Подключение к SQL Server» см. в разделах [Manage an Oracle CDC Service](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md) и [Connection to SQL Server for Delete](../../integration-services/change-data-capture/connection-to-sql-server-for-delete.md).  
  
    -   **Изменение свойств службы CDC**  
  
         На панели **Действия** в правой стороне консоли настройки службы CDC щелкните пункт **Свойства**.  
  
         Также можно щелкнуть правой кнопкой мыши службу CDC, свойства которой требуется изменить, и выбрать команду **Свойства**.  
  
## <a name="see-also"></a>См. также раздел  
 [Управление службой CDC Oracle](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  