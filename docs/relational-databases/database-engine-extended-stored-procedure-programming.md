---
title: Программирование расширенных хранимых процедур ядра СУБД | Документация Майкрософт
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], programming
- stored procedures [SQL Server], extended
- Database Engine [SQL Server], stored procedures
- macros [SQL Server]
- Extended Stored Procedure API [SQL Server]
ms.assetid: 158a6765-0542-4e84-b5ab-f173d946ef5e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a8e404c4673ccaa55dae0ffb66b381599f7b9d4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845562"
---
# <a name="database-engine-extended-stored-procedure-programming"></a>Программирование расширенных хранимых процедур ядра СУБД
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../includes/ssnotedepfuturedontuse-md.md)] Пользуйтесь вместо этого интеграцией со средой CLR. Дополнительные сведения см. в статье [Основные понятия о программировании интеграции со средой CLR](../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md).  
  
 API расширенных хранимых процедур [!INCLUDE[msCoName](../includes/msconame-md.md)] предоставляет серверный интерфейс API для расширения функциональных возможностей [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. API-интерфейс состоит из функций на языках C и C++ и макросов, предназначенных для построения приложений следующих категорий: расширенные хранимые процедуры и шлюзовые приложения.  
  
 Расширенные хранимые процедуры позволяют создавать собственные внешние подпрограммы на языках программирования, подобных C. Расширенные хранимые процедуры представляются пользователям как обычные хранимые процедуры и выполняются тем же способом. Расширенным хранимым процедурам могут передаваться аргументы, и эти процедуры могут возвращать результаты и статус.  
  
## <a name="in-this-section"></a>в этом разделе  
 [Программирование расширенных хранимых процедур](../relational-databases/extended-stored-procedures-programming/database-engine-extended-stored-procedures-programming.md)  
 Содержит описание способов создания, управления и использования расширенных хранимых процедур.  
  
 [Справочник по программированию расширенных хранимых процедур](../relational-databases/extended-stored-procedures-reference/database-engine-extended-stored-procedures-reference.md)  
 Содержит разделы справки по API расширенных хранимых процедур.  
  
  
