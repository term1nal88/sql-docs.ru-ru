---
title: "UPPER (выражение служб SSIS) | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1764b39b0242ce7e23d56c9c74f7b953f45009b2
ms.contentlocale: ru-ru
ms.lasthandoff: 08/03/2017

---
# <a name="upper-ssis-expression"></a>UPPER (выражение служб SSIS)
  Возвращает символьное выражение после преобразования символов в нижнем регистре в символы верхнего регистра.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
UPPER(character_expression)  
```  
  
## <a name="arguments"></a>Аргументы  
 *character_expression*  
 Символьное выражение для преобразования в верхний регистр.  
  
## <a name="result-types"></a>Типы результата  
 DT_WSTR  
  
## <a name="remarks"></a>Замечания  
 Функция UPPER работает только с типом данных DT_WSTR. Аргумент *character_expression* , являющийся строковым литералом или столбцом данных с типом данных DT_STR, неявно приведен к типу данных DT_WSTR до выполнения функции UPPER. Прочие типы данных должны быть явно приведены к типу данных DT_WSTR. Дополнительные сведения см. в разделах [Типы данных служб Integration Services](../../integration-services/data-flow/integration-services-data-types.md) и [Приведение (выражение служб SSIS)](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Функция UPPER возвращает значение NULL, если аргумент имеет значение NULL.  
  
## <a name="expression-examples"></a>Примеры выражений  
 Этот пример преобразует строковый литерал в верхний регистр. Возвращаемый результат — «HELLO».  
  
```  
UPPER("hello")  
```  
  
 Этот пример преобразует первый символ столбца **FirstName** в символ верхнего регистра. Если значение **FirstName** — «anna», возвращается результат «A». Дополнительные сведения см. в разделе [SUBSTRING (выражение служб SSIS)](../../integration-services/expressions/substring-ssis-expression.md).  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 Этот пример преобразует значение переменной **PostalCode** в верхний регистр. Если значение **PostalCode** — «k4b1s2», возвращается результат «K4B1S2».  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>См. также  
 [НИЖНЕГО &#40; Выражение служб SSIS &#41;](../../integration-services/expressions/lower-ssis-expression.md)   
 [Функции &#40; Выражение служб SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  