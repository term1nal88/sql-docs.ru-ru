---
title: "MSSQLSERVER_3961 | Документация Майкрософт"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4bee6f2a3420267cca465ef81adb25436f105166
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3961"></a>MSSQLSERVER_3961
  
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|3961|  
|Источник события|MSSQLSERVER|  
|Компонент|SQLEngine|  
|Символическое имя|XACT_METADATA_INVALID|  
|Текст сообщения|Ошибка транзакции в режиме изоляции моментального снимка в базе данных «%.*ls»: объект, к которому производится обращение в данной инструкции, был изменен инструкцией DDL другой, параллельной транзакции после начала данной транзакции.  Это запрещено, поскольку управление версиями метаданных не поддерживается. Одновременное обновление метаданных может привести к несогласованности при совместном использовании с режимом изоляции моментального снимка.|  
  
## <a name="explanation"></a>Объяснение  
Эта ошибка может произойти при запросе метаданных в режиме изоляции моментального снимка при одновременном обновлении этих метаданных параллельной инструкцией DDL. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] не поддерживает управление версиями метаданных. Поэтому не все операции DDL могут выполняться в явной транзакции, работающей с уровнем изоляции моментального снимка. Неявная транзакция, по определению, — это единственная инструкция, для которой возможно выполнение семантики изоляции моментального снимка, даже для инструкций DDL. Следующие инструкции DDL нельзя использовать после инструкции BEGIN TRANSACTION в условиях изоляции моментального снимка: ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME, а также любые инструкции DDL среды CLR. Эти инструкции разрешены к использованию в неявных транзакциях, работающих при уровне изоляции моментального снимка. Неявная транзакция, по определению, — это единственная инструкция, для которой возможно выполнение семантики изоляции моментального снимка, даже для инструкций DDL.  
  
## <a name="user-action"></a>Действие пользователя  
Перед запросом метаданных измените уровень изоляции моментального снимка на другой уровень изоляции, например на уровень изоляции зафиксированной операции чтения.  
  
