---
title: "Требования к системе для драйвера JDBC | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 447792bb-f39b-49b4-9fd0-1ef4154c74ab
caps.latest.revision: 73
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eed93fab6f0ceec655b7b9f6b392abc390b5f0ff
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-for-the-jdbc-driver"></a>Требования к системе для драйвера JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Для доступа к данным из [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] или [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] с помощью [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], необходимо установить на компьютере следующие компоненты:  
  
-   [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]  
  
     Драйвер Microsoft JDBC можно загрузить из центра загрузки Майкрософт по ссылкам ниже: 
     * [6.2 драйвер Microsoft JDBC для SQL Server](http://go.microsoft.com/fwlink/?linkid=852460)
     * [Microsoft JDBC Driver 6.0 для SQL Server](http://go.microsoft.com/fwlink/?linkid=841535)
     * [Microsoft JDBC Driver 4.2 для SQL Server](http://go.microsoft.com/fwlink/?linkid=841534) 
     * [Microsoft JDBC Driver 4.1 для SQL Server](http://go.microsoft.com/fwlink/?linkid=841533) 
     * [Драйвер Microsoft JDBC 4.0 для SQL Server](http://go.microsoft.com/fwlink/?linkid=841532)
  
-   Среда выполнения Java  
  
## <a name="java-runtime-environment-requirements"></a>Требования к среде выполнения Java  
 Начиная с версии Microsoft JDBC Driver 4.2 для SQL Server, поддерживается пакет SDK для Sun Java SE (JDK) 8.0 и среда выполнения Java (JRE) 8.0. Поддержка спецификации API JDBC была расширена за счет включения API JDBC 4.1 и 4.2.  
  
 Начиная с версии Microsoft JDBC Driver 4.1 для SQL Server, поддерживается пакет SDK для Sun Java SE (JDK) 7.0 и среда выполнения Java (JRE) 7.0.  
  
 Начиная с [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)], драйвер JDBC поддержка Java Database Connectivity (JDBC) Spec API была расширена для включения JDBC 4.0 API. Версия API JDBC 4.0 впервые появилась в составе комплекта разработчика Sun Java SE (JDK) 6.0 и среды выполнения Java (JRE) 6.0. JDBC 4.0 является супермножеством API JDBC 3.0.  
  
 При развертывании [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] в операционных системах Windows и UNIX необходимо использовать пакеты установки, *sqljdbc_\<версия > _enu.exe* и *sqljdbc_\<версии > _ enu.tar.gz*соответственно. Дополнительные сведения о развертывании драйвера JDBC см. в разделе [развертывание драйвера JDBC](../../connect/jdbc/deploying-the-jdbc-driver.md) раздела.  
  
**Драйвер Microsoft JDBC 6.2 для SQL Server:**  
  
  6.2 драйвера JDBC содержит две библиотеки классов JAR в каждом пакете установки: **mssql jdbc-6.2.1.jre7.jar**, и **mssql jdbc-6.2.1.jre8.jar**. 
  
 6.2 драйвер JDBC предназначен для работы с и должны поддерживаться всеми основными Sun эквивалентные Java виртуальных машин, однако протестирован только в Sun JRE 5.0, 6.0, 7.0 и 8.0. 
  
 Ниже приведены сведения о поддержке, предоставляемые две JAR-файлы, входящие в состав Microsoft JDBC Driver 6.0 и 4.2 для SQL Server:  
  
|JAR|Соответствие версии JDBC|Рекомендуемая версия Java|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|MSSQL jdbc-6.2.1.jre7.jar|4.1|7|Требуется среда выполнения Java (JRE) версии 7.0. В случае использования JRE 6.0 или более ранней возникает исключение.<br /><br /> Новые возможности в 6.2 включают: проверка подлинности Azure AD для Linux, метод субъект и пароль проверки подлинности Kerberos, автоматическое обнаружение СФЕРУ имени участника-службы для проверки подлинности между доменами, ограниченное делегирование Kerberos, время ожидания запроса, время ожидания для сокета и подготовленных Дескриптор инструкции, повторного использования. |  
|MSSQL jdbc-6.2.1.jre8.jar|4.2|8|Требуется среда выполнения Java (JRE) версии 8.0. В случае использования JRE 7.0 или более ранней возникает исключение.<br /><br /> Новые возможности в 6.2 включают: проверка подлинности Azure AD для Linux, метод субъект и пароль проверки подлинности Kerberos, автоматическое обнаружение СФЕРУ имени участника-службы для проверки подлинности между доменами, ограниченное делегирование Kerberos, время ожидания запроса, время ожидания для сокета и подготовленных Дескриптор инструкции повторного использования|    

  6.2 драйвер JDBC также доступна на центральный репозиторий Maven и может добавлять в проект Maven, добавив следующий код в POM. XML 
  
 ```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```    

 **Microsoft JDBC Driver 6.0 и 4.2 для SQL Server:**  
  
  Драйверы JDBC Driver 6.0 и 4.2 включают две библиотеки классов JAR в каждом пакете установки: **sqljdbc41.jar**, и **sqljdbc42.jar**. 
  
 Драйверы JDBC Driver 6.0 и 4.2 предназначены для работы с и должны поддерживаться всеми основными Sun эквивалентные Java виртуальных машин, но протестирован только в Sun JRE 5.0, 6.0, 7.0 и 8.0. 
  
 Ниже приведены сведения о поддержке, предоставляемые две JAR-файлы, входящие в состав Microsoft JDBC Driver 6.0 и 4.2 для SQL Server:  
  
|JAR|Соответствие версии JDBC|Рекомендуемая версия Java|Description|  
|---------|-----------------------------|----------------------|-----------------|   
|sqljdbc41.jar|4.1|7|Требуется среда выполнения Java (JRE) версии 7.0. В случае использования JRE 6.0 или более ранней возникает исключение.<br /><br /> В число новых возможностей в пакетах 6.0 и 4.2 входит массовое копирование и соответствие JDBC 4.1.<br /><br /> Кроме того, новые возможности в пакете 6.0 включают: подготовки прозрачный подключений для группы доступности AlwaysOn, улучшения в параметр извлечения метаданных для постоянного шифрования табличное значение параметры Azure проверки подлинности Active Directory, запросы и международного доменного имени (IDN)|  
|sqljdbc42.jar|4.2|8|Требуется среда выполнения Java (JRE) версии 8.0. В случае использования JRE 7.0 или более ранней возникает исключение.<br /><br /> В число новых возможностей в пакетах 6.0 и 4.2 входит массовое копирование, соответствие JDBC 4.1 и соответствие JDBC 4.2.<br /><br /> Кроме того, новые возможности в пакете 6.0 включают: подготовки прозрачный подключений для группы доступности AlwaysOn, улучшения в параметр извлечения метаданных для постоянного шифрования табличное значение параметры Azure проверки подлинности Active Directory, запросы и международного доменного имени (IDN)|  
  
 **Microsoft JDBC Driver 4.1 для SQL Server:**  
  
 Драйвер JDBC Driver 4.1 включает в себя один библиотеки классов JAR в каждом пакете установки: **sqljdbc41.jar**.  
    
|JAR|Description|  
|---------|-----------------|  
|sqljdbc41.jar|**sqljdbc41.JAR** библиотека классов обеспечивает поддержку JDBC 4.0 API. Он включает все функции драйвера JDBC 4.0, а также методы JDBC 4.0 API. JDBC 4.1 не поддерживается (будет выдано исключение SQLFeatureNotSupportedException).<br /><br /> **sqljdbc41.JAR** библиотеке классов требуется среда выполнения Java (JRE) 7.0. С помощью **sqljdbc41.jar** в JRE 6.0 и 5.0 возникает исключение.<br /><br /> 
  
 Обратите внимание, что драйвер JDBC разработан и поддерживается при использовании со всеми основными аналогами виртуальных машин Java от Sun, но его проверка выполнялась в Sun JRE 5.0, 6.0 и 7.0.  
  
 Ниже приведены сведения о поддержке, предоставляемые JAR-файл, входящие в состав Microsoft JDBC Driver 4.1 для SQL Server.  
  
|JAR|Версия JDBC|JRE (можно выполнять)|JDK (можно компилировать)|  
|---------|------------------|---------------------|-------------------------|   
|sqljdbc41.jar|4|7|7 6 5|  
  
 **Драйвер Microsoft JDBC 4.0 для SQL Server:**  
  
 Для поддержки обратной совместимости и возможных сценариев обновления, драйвер JDBC содержит две библиотеки классов JAR в каждом пакете установки: **sqljdbc.jar** и **sqljdbc4.jar**.  
  
|JAR|Description|  
|---------|-----------------|  
|sqljdbc.jar|**sqljdbc.JAR** библиотека классов обеспечивает поддержку JDBC 3.0.<br /><br /> **sqljdbc.JAR** библиотеке классов требуется среда выполнения Java (JRE) версии 5.0. С помощью **sqljdbc.jar** в JRE 6.0 или JRE 7.0 вызовет исключение при подключении к базе данных.<br /><br /> **Примечание:** драйвер JDBC не поддерживает JRE 1.4. При использовании драйвера JDBC необходимо обновить JRE 1.4 до версии 5.0, 6.0 или 7.0. В некоторых случаях может потребоваться перекомпиляция приложения, если оно несовместимо с API JDK 5.0 или API JDK 6.0. Дополнительные сведения см. в документации на веб-сайте Sun Microsystems.<br /><br /> [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]не поддерживает JDK 7.|  
|sqljdbc4.jar|**sqljdbc4.JAR** библиотека классов обеспечивает поддержку JDBC 4.0 API. Она включает все возможности **sqljdbc.jar** а также новые методы JDBC 4.0 API.<br /><br /> **sqljdbc4.JAR** библиотеке классов требуется среда выполнения Java (JRE) версии 6.0 или 7.0. С помощью **sqljdbc4.jar** в JRE 5.0 возникает исключение.<br /><br /> **Примечание:** использовать **sqljdbc4.jar** при приложения необходимо выполнить в JRE 6.0 или 7.0, даже если приложение не использует возможности JDBC 4.0 API.|  
  
 Обратите внимание, что драйвер JDBC разработан и поддерживается при использовании со всеми основными аналогами виртуальных машин Java от Sun, но его проверка выполнялась в Sun JRE 5.0, 6.0 и 7.0.  
  
## <a name="sql-server-requirements"></a>Требования к SQL Server  
 Драйвер JDBC поддерживает подключения к базе данных Azure SQL и SQL Server. Для драйвера Microsoft JDBC 4.2 и 4.1 для SQL Server поддержка начинается с SQL Server 2008. Для Microsoft JDBC Driver 4.0 для SQL Server поддержка начинается с SQL Server 2005.  
  
## <a name="operating-system-requirements"></a>Требования к операционной системе  
 Драйвер JDBC разработан для использования с любой операционной системой, поддерживающей использование виртуальной машины Java (JVM). Однако официально протестированы только системы Sun Solaris, SUSE Linux и Windows.  
  
## <a name="supported-languages"></a>Поддерживаемые языки  
 Драйвер JDBC поддерживает все [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] параметры сортировки столбцов. Дополнительные сведения о параметрах сортировки, поддерживаемых драйвером JDBC см. в разделе [международные функции драйвера JDBC](../../connect/jdbc/international-features-of-the-jdbc-driver.md).  
  
 Дополнительные сведения о параметрах сортировки см. в разделе «Работа с параметрами сортировки» в [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] электронной документации.  
  
## <a name="see-also"></a>См. также:  
 [Общие сведения о драйвере JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
