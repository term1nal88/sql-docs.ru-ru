---
title: "НАЛИЧИЕ (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HAVING
- HAVING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restricting conditions for result set
- search conditions [SQL Server], HAVING clause
- HAVING clause
- HAVING clause, about HAVING clause
ms.assetid: 55650709-001e-42f4-902f-ead09a3c34af
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9bff75a84689090f6e416db052a2561e57fa98a6
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="select---having-transact-sql"></a>SELECT — НАЛИЧИЕ (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Определяет условие поиска для группы или статистического выражения. Предложение HAVING можно использовать только в инструкции SELECT. Предложение HAVING обычно используется в предложении GROUP BY. Когда GROUP BY не используется, предложение HAVING работает так же, как и предложение WHERE.  
  
 ![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Синтаксис  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>Аргументы  
\<search_condition > указывает условие поиска, должна соответствовать группа или статистическое выражение.  
  
 **Текст**, **изображения**, и **ntext** типы данных не может использоваться в предложении HAVING.  
  
## <a name="examples"></a>Примеры  
 В следующем примере, который использует простое предложение `HAVING`, из таблицы `SalesOrderID` извлекается сумма всех полей `SalesOrderDetail`, значение которых превышает `$100000.00`.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID  
HAVING SUM(LineTotal) > 100000.00  
ORDER BY SalesOrderID ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Примеры: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] и[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 В следующем примере используется `HAVING` предложений, чтобы получить итог для каждого `SalesAmount` из `FactInternetSales` таблицу при `OrderDateKey` год 2004 г. или более поздней версии.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>См. также:  
 [Предложение GROUP BY &#40; Transact-SQL &#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [ГДЕ &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

