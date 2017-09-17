---
title: "Основные функции уровня API (драйвер ODBC для Oracle) | Документы Microsoft"
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
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d3bc36063659da3cf0cd6b2b837be0c4fce46c6f
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Функции API-Интерфейс уровня ядра (драйвер ODBC для Oracle)
> [!IMPORTANT]  
>  Этот компонент будет удален в будущих версиях Windows. Избегайте использования этого компонента в новых разработках и запланируйте изменение существующих приложений, в которых он применяется. Вместо этого используйте драйвер ODBC, предоставляемого корпорацией Oracle.  
  
 Функции на этом уровне включают минимальный уровень совместимости интерфейс для драйверов ODBC.  
  
|API-функции|Примечания|  
|------------------|-----------|  
|**SQLAllocConnect**|Выделяет память для дескриптора соединения *hdbc*, в среде определяется *henv*. Диспетчер драйверов обрабатывает этот вызов и вызывает драйвер **SQLAllocConnect** каждый раз, когда функция **SQLConnect**, **SQLBrowseConnect**, или ** SQLDriverConnect** вызывается.|  
|**SQLAllocEnv**|Отображает диалоговое окно, указав требование для клиентского программного обеспечения Oracle, а затем возвращает значение SQL_NULL_HANDLE. Если клиентское по Oracle не установлена, эта функция выделяет память для дескриптора среды, *henv*и инициализирует интерфейс уровня вызова ODBC для использования в приложении.|  
|**SQLAllocStmt**|Выделяет память для дескриптора инструкции и связывает с указанное соединение hdbc дескриптора инструкции. Диспетчер драйверов передает этот вызов на драйвер, который выделяет память для структуры hstmt.|  
|**SQLBindCol**|Назначает дисковое пространство для столбца результирующего и указывает тип результата.|  
|**SQLCancel**|Отменяет обработку на дескриптор инструкции hstmt. В некоторых случаях Oracle не допускает отмены выполнения инструкции. Это означает, что выполнение инструкции будет продолжаться до Oracle завершает процесс, после чего результаты инструкции отменяются драйвером ODBC для Oracle.|  
|**SQLColAttributes**|Возвращает сведения о дескрипторе для столбца в результирующем наборе. Сведения о дескрипторе возвращается как символьная строка, зависящие от дескриптора 32-разрядное значение или является целым числом.|  
|**SQLConnect**|Подключается к источнику данных. Чтобы использовать проверку подлинности Oracle операционной системы, укажите «/» как *szUID* параметр и «» как *szAuthStr* параметра.|  
|**SQLDescribeCol**|Возвращает имя, тип, точность, масштаб и допустимость значений NULL столбца данного результата. **Примечание:****SQLDescribeCol** отчеты в виде SQL_VARCHAR вычисляемых столбцов.  |  
|**SQLDisconnect**|Закрывает соединение. Если включен пул соединений для совместно используемой среде, и приложение вызывает **SQLDisconnect** для подключения в этой среде, соединение возвращается в пул подключений и по-прежнему доступен для других компонентов, с помощью одной общей среде.|  
|**SQLError**|Возвращает ошибки или состояния сведения о последней ошибке. Драйвер поддерживает стека или список ошибок, которые могут быть возвращены для *hstmt*, *hdbc*, и *henv* аргументы, в зависимости от того, как вызов **SQLError ** выполняется. Ошибка очереди очищается после каждой инструкции. Обычно получает сообщение об ошибке Oracle, а в противном случае значение будет пустым.|  
|**SQLExecDirect**|Выполняет инструкцию SQL новый, аннулируется. Драйвер использует текущие значения переменных маркера параметра, если все параметры существуют в инструкции. Если на таблицу, представление или имена полей содержат пробелы, заключите имена кавычка после метки. Например, если база данных содержит таблицу с именем *My Table* и поле *Мое поле*, заключите каждый элемент идентификатора следующим образом:<br /><br /> ВЫБЕРИТЕ \`таблицы\`. \`Мои Field1\`, \`Таблицы\`.\` Мои Field2\` FROM \`таблицу "|  
|**SQLExecute**|Выполняет подготовленную инструкцию SQL (инструкция, уже созданные **SQLPrepare**). Драйвер использует текущие значения переменных маркера параметра, если все параметры существуют в инструкции.|  
|**SQLFetch**|Возвращает одну строку из результирующего набора в расположениях, указанных в предыдущих вызовов **SQLBindCol**. Подготавливает драйвер для вызова **SQLGetData** для несвязанных столбцов.|  
|**SQLFreeConnect**|Освобождает дескриптор соединения и освобождает всей памяти, выделенной для дескриптора.|  
|**SQLFreeEnv**|Драйвер ODBC для Oracle закрывает и освобождает всю память, связанные с драйвером.|  
|**SQLFreeStmt**|Останавливает обработку, связанные с определенной hstmt, закрывает все открытые курсоры, связанные с hstmt, отменяет ожидающие результаты и при необходимости освобождает все ресурсы, связанные с дескриптором инструкции.|  
|**SQLGetCursorName**|Возвращает имя курсора, связанный с данной hstmt.|  
|**SQLNumResultCols**|Возвращает число столбцов в результирующий набор курсора.|  
|**SQLPrepare**|Подготавливает инструкцию SQL, планируя как оптимизировать и выполнить инструкцию. Инструкция SQL компилируется для исполнения **SQLExecDirect**.<br /><br /> Если на таблицу, представление или имена полей содержат пробелы, заключите имена кавычка после метки. Например, если база данных содержит таблицу с именем *My Table* и поле *Мое поле*, заключите каждый элемент идентификатора следующим образом:<br /><br /> ВЫБЕРИТЕ \`таблицы\`.\` Мое поле\` FROM \`таблицу "<br /><br /> Сведения об использовании результирующих наборов, содержащими массивы как формальные параметры в разделе [возвращения массива параметров из хранимых процедур](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle не предоставляет способ определить количество строк в результирующем наборе, пока после извлечения последней строки, поэтому он возвращает значение – 1.|  
|**SQLSetCursorName**|Связывает имя курсора с дескриптором активный оператор, *hstmt*.|  
|**SQLSetParam**|Заменить SQLBindParameter в ODBC 2. *x*.|  
|**SQLTransact**|Запрашивает операции фиксации или отката для всех активных операций на все дескрипторы инструкций (hstmts), связанный с подключением или для всех подключений, связанных с этим дескриптором среды *henv*. В случае фиксации в ручной режим транзакции остается активным; Вы можете выполнить откат транзакции или повторите операцию фиксации. Если операция фиксации не в режиме автоматической транзакции, транзакция откатывается автоматически. транзакция не может быть неактивным.|