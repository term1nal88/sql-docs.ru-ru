---
title: "Средство запуска управляющей программы полнотекстовой фильтрации SQL (диспетчер конфигурации SQL Server) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3b4768f274310400e99a355676b2c0cd7a27666e
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Средство запуска управляющей программы полнотекстовой фильтрации SQL (диспетчер конфигурации SQL Server)
  Начиная с версии [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], в полнотекстовом поиске [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] используется средство запуска управляющей программы полнотекстовой фильтрации SQL (средство запуска FDHOST) для запуска хост-процесса управляющей программы полнотекстовой фильтрации, которая выполняет фильтрацию полнотекстового поиска и разбиение по словам. Для использования полнотекстового поиска эта служба должна быть запущена. Средство запуска FDHOST представляет собой привязанную к экземпляру службу, которая связана с конкретным экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Эта служба передает сведения об учетной записи службы в каждый запущенный хост-процесс управляющей программы фильтрации. Сведения о хост-процессах управляющей программы фильтрации см. в разделе "Архитектура компонента Full-Text Search" электронной документации по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  