---
title: "(Вкладка «порядок») свойства клиентских протоколов | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e92bac20c6f709964dabf08710c2b18b5db0c1e4
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# Свойства клиентских протоколов (вкладка «Порядок»)
  Используйте страницу **Порядок**диалогового окна **Свойства клиентских протоколов** для просмотра и включения клиентских протоколов.  
  
 Щелкните протокол, а затем выберите команду **Включить** или **Выключить** для перемещения выбранного протокола в список **Отключенные протоколы** или **Включенные протоколы** .  
  
 Попытки использования протоколов происходят в перечисленной в списке последовательности: сначала осуществляется попытка соединения при помощи самого верхнего протокола, затем при помощи протокола, второго в списке, и так далее. Передвигать протоколы вверх и вниз по списку **Включенные протоколы** можно, нажимая кнопки со стрелкой вверх и со стрелкой вниз. При подключении к [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с клиента на том же компьютере в первую очередь происходит попытка подключения через протокол **Общая память** , если он включен.  
  
> [!NOTE]  
>  Эти настройки не используются клиентом [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient. В порядке протоколов для клиента .NET SqlClient первым идет протокол TCP, а затем именованные каналы. Этот порядок нельзя изменить.  
  
## Параметры  
 **Отключенные протоколы**  
 Содержит список установленных, но не используемых в данный момент протоколов.  
  
 **Включенные протоколы**  
 Содержит список протоколов, доступных для клиентов [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] на этом компьютере.  
  
 **>**  
 Включает выделенный протокол в окне **Отключенные протоколы** и переносит его в окно **Включенные протоколы** .  
  
 **\<**  
 Отключает выделенный протокол в окне **Включенные протоколы** и переносит его в окно **Отключенные протоколы** .  
  
 Стрелка вверх  
 Перемещает выделенный протокол вверх по списку. Это позволяет повысить приоритет использования сетевой библиотекой выбранного протокола для соединений.  
  
 Стрелка вниз  
 Перемещает выделенный протокол вниз по списку. Это позволяет понизить приоритет использования сетевой библиотекой выбранного протокола для соединений.  
  
 **Включить протокол общей памяти**  
 Включает протокол общей памяти, который всегда используется первым (в том случае, если он включен) при подключении к [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] с клиента на том же компьютере.  
  
> [!NOTE]  
>  Если протокол определен через префикс или как часть строки соединения, то попытка подключения будет происходить только через определенный протокол.  
  
## См. также  
 [Выбор сетевого протокола](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  