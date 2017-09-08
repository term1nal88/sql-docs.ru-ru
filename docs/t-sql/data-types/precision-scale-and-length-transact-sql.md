---
title: "Точность, масштаб и длина (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], length
- data types [SQL Server], scale
- precision [SQL Server], data types
- lengths [SQL Server], data types
- number of digits
- scale [SQL Server]
- scale [SQL Server], data types
- data types [SQL Server], precision
ms.assetid: fbc9ad2c-0d3b-4e98-8fdd-4d912328e40a
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 557d7a5c45e9cc5a0839dfb4a1fdb0d08c2bf83f
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="precision-scale-and-length-transact-sql"></a>Точность, масштаб и длина (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Точность представляет собой количество цифр в числе. Масштаб представляет собой количество цифр справа от десятичной запятой в числе. Например, у числа 123,45 точность равна 5, а масштаб равен 2.
  
В [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], по умолчанию максимальная точность **числовое** и **десятичное** типы данных составляет 38 разрядов. В более ранних версиях [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] максимум по умолчанию составляет 28.
  
Длиной для числовых типов данных является количество байт, используемых для хранения числа. Длина символьной строки или данных в Юникоде равняется количеству символов. Длина **двоичных**, **varbinary**, и **изображение** типов данных — количество байтов. Например **int** тип данных может содержать 10 разрядов, храниться в 4 байтах и не должен содержать десятичный разделитель. **Int** тип данных имеет точность 10, длину 4 и масштаб 0.
  
Если два **char**, **varchar**, **двоичных**, или **varbinary** выражения объединяются, а длина результирующего выражения Сумма длин двух исходных выражений или 8 000 символов, какое значение меньше.
  
Если два **nchar** или **nvarchar** выражения объединяются, длина результирующего выражения является суммой длин двух исходных выражений или 4 000 символов, какое значение меньше.
  
Если два выражения одного и того же типа данных, но разной длины, сравниваются с помощью предложения UNION, EXCEPT или INTERSECT, длина результата будет равняться длине максимального из двух выражений.
  
Точность и масштаб числовых типов данных помимо **десятичное** являются фиксированными. Если арифметический оператор объединяет два выражения одного и того же типа, результат будет иметь тот же тип данных с точностью и масштабом, определенными для этого типа. Если оператор объединяет два выражения с различными числовыми типами данных, тип данных результата будет определяться правилами старшинства типов данных. Результат имеет точность и масштаб, определенные для этого типа данных.
  
Следующая таблица определяет, как вычисляется точность и масштаб результата, если результат операции имеет тип **десятичное**. В результате **десятичное** когда верно одно из следующих:
-   Оба выражения имеют **десятичное**.  
-   Одно из выражений является **десятичное** , а другой — тип данных с более низким приоритетом, чем **десятичное**.  
  
Операнды выражений обозначены как выражение e1 с точностью p1 и масштабом s2 и выражение e2 с точностью p2 и масштабом s2. Точность и масштаб для любого выражения, не **десятичное** имеет точность и масштаб, определенные для типа данных выражения.
  
|Операция|Точность результата|Масштаб результата *|  
|---|---|---|
|e1 + e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 - e2|max(s1, s2) + max(p1-s1, p2-s2) + 1|max(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + max(6, s1 + p2 + 1)|max(6, s1 + p2 + 1)|  
|E1 {UNION &#124; За исключением &#124; E2 INTERSECT}|max(s1, s2) + max(p1-s1, p2-s2)|max(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|max(s1, s2)|  
  
\*Точность и масштаб результата имеют абсолютный максимум, равный 38. Когда точности превышает 38, он сокращается до 38 и соответствующий масштаб уменьшается, чтобы предотвратить усечение интегральной части результата. В некоторых случаях, таких как умножение или деление коэффициент масштабирования не уменьшается для сохранения согласованности десятичную точность, несмотря на то, что может возникнуть ошибка переполнения.

В операции сложения и вычитания нам нужно `max(p1 – s1, p2 – s2)` места для хранения неотъемлемой частью десятичное число. Если имеется достаточно места для хранения их, т. е. `max(p1 – s1, p2 – s2) < min(38, precision) – scale`, масштаб уменьшается до предоставляет достаточно места для целой части. Полученный масштаб равен `MIN(precision, 38) - max(p1 – s1, p2 – s2)`, поэтому дробная часть может округляться до помещаются в результирующей шкалы.

В операции умножения и деления должны `precision - scale` места для хранения неотъемлемой частью результат. Масштаб может снизиться, используя следующие правила:
1.  Полученный масштаб уменьшается до `min(scale, 38 – (precision-scale))` ли составной частью меньше 32, так как он не может быть больше, чем `38 – (precision-scale)`. В этом случае может округляться результат.
1. Масштаб не будут изменены, если оно меньше 6, а составной частью больше, чем 32. В этом случае ошибка переполнения может быть вызвано, если он не может поместиться в десятичных (38, масштаб) 
1. Если больше 6 и составной частью больше, чем 32 6 установит шкалы. В этом случае будут снижены составной частью и масштаб, и результирующим типом является decimal(38,6). Результат может округляться до 6 знаков после запятой, или выдается ошибка переполнения при составной частью не помещаются в 32 цифры.

## <a name="examples"></a>Примеры
Следующее выражение возвращает результат `0.00000090000000000` без округления, так как результат помещается в `decimal(38,17)`:
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
В этом случае точностью 61, и масштаб равен 40.
Составной частью (точность шкалы = 21), меньше 32, поэтому это случай (1) в правилах умножения и масштаб рассчитывается как `min(scale, 38 – (precision-scale)) = min(40, 38 – (61-40)) = 17`. Тип результата — `decimal(38,17)`.

Следующее выражение возвращает результат `0.000001` и не помещаются в `decimal(38,6)`:
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
В этом случае точностью 61, и масштаб равен 20.
Масштаб больше 6 и целочисленные части (`precision-scale = 41`) больше, чем 32. Это случай (3) в правилах умножения и типом результата является `decimal(38,6)`.

## <a name="see-also"></a>См. также:
[Выражения (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)  
[Типы данных (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)
  
  
