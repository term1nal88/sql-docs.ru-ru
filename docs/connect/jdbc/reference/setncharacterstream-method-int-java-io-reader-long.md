---
title: Метод setNCharacterStream для объекта java.io.Reader - long | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36396dc9-f109-4da0-bd64-726704046bbf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3d32bdf91cfe9ddbbdc8e3bb85e101943aebcf4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736273"
---
# <a name="setncharacterstream-method-int-javaioreader-long"></a>Метод setNCharacterStream (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Задает указанному параметру заданный объект Reader.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                  java.io.Reader value,  
                                                                long length)  
```  
  
#### <a name="parameters"></a>Параметры  
 *parameterIndex*  
  
 Значение типа **int**, указывающее индекс параметра.  
  
 *value*  
  
 Объект Reader, содержащий значение параметра.  
  
 *length*  
  
 Значение **long**, которое указывает количество символов в потоке.  
  
## <a name="exceptions"></a>Исключения  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Этот метод setNCharacterStream указывается с помощью метода setNCharacterStream в интерфейсе java.sql.PreparedStatement.  
  
 Этот метод следует использовать для **NCHAR**, **NVARCHAR**, **NTEXT**, и **XML** типов данных.  
  
 Если длина потока отличается от указанной в параметре *length*, драйвер JDBC выдаст исключение при обновлении или вставке строки.  
  
 Если длина потока неизвестна, параметр *length* может иметь значение "–1", показывающее, что драйвер должен принимать поток любой длины. Если приложению нужно обновлять столбец из потока, длина которого неизвестна, рекомендуется для sqljdbc4.jar пользоваться методом JDBC 4.0 [Метод setNCharacterStream (int, java.io.Reader)](../../../connect/jdbc/reference/setncharacterstream-method-int-java-io-reader.md).  
  
## <a name="see-also"></a>См. также:  
 [Метод setNCharacterStream (SQLServerPreparedStatement)](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [Элементы SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
