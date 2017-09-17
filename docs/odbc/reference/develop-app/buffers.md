---
title: "Буферы | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input buffers [ODBC]
- length/indicator buffers [ODBC]
- output buffers [ODBC]
- buffers [ODBC], about buffers
- application buffers [ODBC]
- buffers [ODBC]
ms.assetid: 42c5226c-cb40-4d1e-809f-2ea50ce6bd55
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5953f3409a3886abbf76963d0207a89be1e83aec
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="buffers"></a>Буферы
Буфер является любая память приложения, используемый для передачи данных между приложением и драйвер. Например, буферы приложения может быть связан с, или *связаны с* результирующего набора столбцов с **SQLBindCol**. Каждая строка выбирается, данные возвращаются для каждого столбца в буфер. *Входные буферы* используются для передачи данных из приложения для драйвера. *Выходные буферы* используются для возврата данных с помощью драйвера в приложение.  
  
> [!NOTE]  
>  Если функция ODBC возвращает значение SQL_ERROR, содержимое любой из выходных аргументов для этой функции не определено.  
  
 Это не относится себя в основном с буферами неопределенного типа. Адреса эти буферы отображаются как аргументы типа указатель SQLPOINTER, такие как *TargetValuePtr* аргумент в **SQLBindCol**. Тем не менее, некоторые элементы, описанные здесь, такие как аргументы, используемые с буферами, применимы и к аргументам, используемым для передачи строк в драйвере, таких как *TableName* аргумент в **SQLTables**.  
  
 Эти буферы обычно представлены парами. *Буферы данных* , используется для передачи данных, а *буфер длины/индикатора* используются для передачи длину данных в буфере данных или специальное значение, например SQL_NULL_DATA, который указывает, что данные имеют значение NULL. Длина данных в буфере данных отличается от длины буфера данных, сам. На следующем рисунке показана связь между буфер данных и буфер длины/индикатора.  
  
 ![Буфер данных и длина &#47; буфера индикатора](../../../odbc/reference/develop-app/media/pr09.gif "pr09")  
  
 Буфер длины/индикатора требуется всякий раз, когда буфер данных содержит данные переменной длины, например символьных или двоичных данных. Если буфер данных содержит данные фиксированной длины, например структуру целое число или дату буфер длины/индикатора требуется только для передачи значения индикатора, так как длина данных уже известна. Если приложение использует буфер длины/индикатора с фиксированной длиной данных, драйвер пропускает любой длины, переданный в него.  
  
 Длина буфера данных и данных, содержащихся в нем измеряется в байтах, а не символы. Это различие не имеет значения для программ, использующих строки ANSI, так как длина в байтах и символы одинаковы.  
  
 Если буфер данных представляет поле дескриптора, определяемым драйвером, диагностические поля или атрибута, приложение должно указывать диспетчера драйверов характер аргумент функции, который указывает значение для поля или атрибута. Приложение устанавливается не длина аргумента в вызове любой функции, который задает поле или атрибут к одному из следующих значений. (То же самое верно для функций, получающих значения поля или атрибута, за исключением того, аргумент указывает значения, для параметра функции в качестве аргумента, сам).  
  
-   Если аргумент функции, который указывает значение для поля или атрибута является указателем на строку знаков *длина* аргумент — это длина строки или SQL_NTS.  
  
-   Если аргумент функции, который указывает значение для поля или атрибута является указателем на буфер, двоичный, приложение помещает результат SQL_LEN_BINARY_ATTR (*длина*) макрос в *длина* аргумент. В этом случае отрицательное значение в *длина* аргумент.  
  
-   Если аргумент функции, который указывает значение для поля или атрибута является указателем на значение, отличное от строки символов или двоичная строка *длина* аргумент должен иметь значение SQL_IS_POINTER.  
  
-   Если аргумент функции, который указывает значение для поля или атрибута содержит значение фиксированной длины, *длина* аргумент является SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT или SQL_ISI_USMALLINT, соответствующим образом.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Отложенное буферов](../../../odbc/reference/develop-app/deferred-buffers.md)  
  
-   [Выделение и освобождение буферов](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
-   [Использование буферов данных](../../../odbc/reference/develop-app/using-data-buffers.md)