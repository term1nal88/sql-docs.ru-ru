---
title: "Прокрутка относительных и абсолютных | Документы Microsoft"
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
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cf5155a44827adb972881da17ac2bc05d92a0cd4
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="relative-and-absolute-scrolling"></a>Относительных и абсолютных прокрутки
Большинство параметров прокрутки в **SQLFetchScroll** курсор относительно текущей позиции или абсолютной позиции. **SQLFetchScroll** поддерживает выборку следующего, предыдущего, первого и последнего набора строк, как хорошо, как относительной (набора строк, * n * строк от начала текущего набора строк) и абсолютной (fetch набор строк, начиная со строки * n *). Если * n * имеет отрицательное значение при абсолютной выборке, то строки отсчитываются с конца результирующего набора. Таким образом абсолютная выборка строки -1 означает, что для выборки строк, который начинается с последней строки в результирующем наборе.  
  
 Динамические курсоры обнаруживает строки вставляются в, а также удаляется из результирующего набора, поэтому нет простого способа для динамических курсоров для извлечения строки по определенной число, отличное от чтения с самого начала результирующий набор, который может выполняться медленно. Кроме того абсолютной не очень удобен в динамические курсоры так, как изменить номера строк, так как строки вставки и удаления; Таким образом последовательная выборка один и тот же номер строки, могут выдавать различные строки.  
  
 Приложения, использующие **SQLFetchScroll** только для своего блока возможности курсора, таких как отчеты, обычно просматривают результирующий набор только один раз, используя только параметр для получения следующего набора строк. На экране приложений, с другой стороны, можно воспользоваться преимуществами все возможности **SQLFetchScroll**. Если приложение задает размер набора строк на число строк, отображаемых на экране и привязывает буферы экранов к результирующему набору, оно может преобразовывать операции полосы прокрутки непосредственно в вызовы **SQLFetchScroll**.  
  
|Операция полосы прокрутки|Параметр прокрутки SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|На страницу вверх|SQL_FETCH_PRIOR|  
|На страницу вниз|SQL_FETCH_NEXT|  
|На строку вверх|SQL_FETCH_RELATIVE с *FetchOffset* равно – 1|  
|На строку вниз|SQL_FETCH_RELATIVE с *FetchOffset* равен 1|  
|Полосы прокрутки в верхней|SQL_FETCH_FIRST|  
|Полосы прокрутки внизу|SQL_FETCH_LAST|  
|Случайное положение ползунка|SQL_FETCH_ABSOLUTE|  
  
 Такие приложения должны положение ползунка после прокрутки операции требуется номер текущей строки и число строк. Для номера текущей строки, приложения можно либо хранить список номер текущей строки или вызов **SQLGetStmtAttr** атрибутом SQL_ATTR_ROW_NUMBER, чтобы получить его.  
  
 Число строк в курсоре, размер результирующего задано, то доступны в качестве поля SQL_DIAG_CURSOR_ROW_COUNT диагностики заголовка. Это значение в этом поле указывается только после **SQLExecute**, **SQLExecDirect**, или **SQLMoreResult** был вызван. Этот счетчик может иметь приблизительное число или точное число, в зависимости от возможностей драйвера. Поддержка драйверов можно определить путем вызова **SQLGetInfo** с типы информации атрибуты курсора и проверки, возвращаются ли бит SQL_CA2_CRC_APPROXIMATE или SQL_CA2_CRC_EXACT для типа курсора.  
  
 Подсчет точных строк никогда не поддерживается для динамических курсоров. Для других типов курсоров драйвер может поддерживать либо количество строк точное или приблизительное, но не оба. Если драйвер поддерживает точное ни приблизительное количество строк для определенного типа курсора, поле SQL_DIAG_CURSOR_ROW_COUNT содержит количество строк, пока будут выбраны. Независимо от того, какой драйвер поддерживает **SQLFetchScroll** с *операции* SQL_FETCH_LAST вызовет поле SQL_DIAG_CURSOR_ROW_COUNT будет содержать число точных строк.