---
title: "Функция SQLRemoveDSNFromIni | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 83c51c7363cd031aefa60c71270e3fa5e9f779ed
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="sqlremovedsnfromini-function"></a>Функция SQLRemoveDSNFromIni
**Соответствия**  
 Версии появился: ODBC 1.0  
  
 **Сводка**  
 **SQLRemoveDSNFromIni** удаляет источник данных из сведений о системе.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>Аргументы  
 *lpszDSN*  
 [Вход] Имя источника данных для удаления.  
  
## <a name="returns"></a>Возвращает  
 Функция возвращает значение TRUE, если он удаляет источник данных или источник данных не в файле Odbc.ini. Возвращается значение FALSE, если не удается удалить источник данных.  
  
## <a name="diagnostics"></a>Диагностика  
 Когда **SQLRemoveDSNFromIni** возвращает значение FALSE, связанный с ним * \*pfErrorCode* значение можно получить путем вызова **SQLInstallerError**. В следующей таблице перечислены * \*pfErrorCode* значения, которые могут быть возвращены **SQLInstallerError** и описание каждого из них в контексте этой функции.  
  
|*\*pfErrorCode*|Ошибка|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Установщик Общие ошибки|Произошла ошибка для которого нет ошибок определенного установщика.|  
|ODBC_ERROR_INVALID_DSN|Недопустимое имя источника данных|*LpszDSN* недопустимый аргумент.|  
|ODBC_ERROR_REQUEST_FAILED|Не удалось выполнить запрос|Программе установки не удалось удалить сведения источника данных из реестра.|  
|ODBC_ERROR_OUT_OF_MEM|Недостаточно памяти|Программе установки не удалось выполнить функцию из-за нехватки памяти.|  
  
## <a name="comments"></a>Комментарии  
 **SQLRemoveDSNFromIni** удаляет имя источника данных из раздела [источники данных ODBC], информация о системе. Раздел спецификации источника данных удаляется из сведений о системе.  
  
 Эта функция должна вызываться только из библиотеки установки драйвера.  
  
## <a name="related-functions"></a>Связанные функции  
  
|Сведения о|См.|  
|---------------------------|---------|  
|Добавление, изменение или удаление источника данных|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Добавление, изменение или удаление источника данных|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Удаление источника данных по умолчанию|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Добавление имени источника данных для сведений о системе|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|