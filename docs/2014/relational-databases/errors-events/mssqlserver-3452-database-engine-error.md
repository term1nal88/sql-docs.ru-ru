---
title: MSSQLSERVER_3452 | Документация Майкрософт
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0e811d36160cf0a4477452acec336c61bf52e793
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141152"
---
# <a name="mssqlserver3452"></a>MSSQLSERVER_3452
    
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|3452|  
|Источник события|MSSQLSERVER|  
|Компонент|SQLEngine|  
|Символическое имя|REC_CHECKIDENTITY|  
|Текст сообщения|Процедура восстановления базы данных «%.*ls» (%d) обнаружила возможное несовпадение тождественных значений в таблице со значением идентификатора %d. Запустите процедуру DBCC CHECKIDENT ("%.\*ls").|  
  
## <a name="explanation"></a>Объяснение  
 Во время обновления сервера до [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] процесс восстановления значений идентификаторов в базе данных обнаружил несогласованность в метаданных.  
  
## <a name="user-action"></a>Действие пользователя  
 Выполнить команду DBCC CHECKIDENT.  
  
  
