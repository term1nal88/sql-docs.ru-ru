---
title: Синтаксис запроса XML для XML-данных отчета (службы SSRS) | Документы Майкрософт
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- namespaces [Reporting Services]
- data processing extensions [Reporting Services], data sources
- xmldp [Reporting Services]
- XML [Reporting Services], data retrieval
ms.assetid: d203886f-faa1-4a02-88f5-dd4c217181ef
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d0c2b65f24b76f875b8fa11896cc70f62bb0902b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668762"
---
# <a name="xml-query-syntax-for-xml-report-data-ssrs"></a>Синтаксис запроса XML для XML-данных отчета (SSRS)
  В службах [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]можно создавать наборы данных для источников XML-данных. После определения источника данных можно создать запрос для получения набора данных. В зависимости от типа XML-данных, на которые указывает источник данных, этот запрос создается путем включения либо элемента XML **Query** , либо пути к элементу. Элемент XML **Query** начинается с тега **\<Query>** и включает пространства имен и XML-элементы, зависящие от источника данных. Путь к элементу не зависит от пространства имен и указывает необходимые узлы и атрибуты узлов в базовых XML-данных при помощи XPath-подобного синтаксиса. Дополнительные сведения о путях к элементу см. в разделе [Синтаксис пути к элементу для XML-данных отчета (службы SSRS)](../../reporting-services/report-data/element-path-syntax-for-xml-report-data-ssrs.md).  
  
 Источник данных XML можно создать для следующих типов XML-данных:  
  
-   XML-документы, на которые указывает URL-адрес по протоколу HTTP;  
  
-   конечные точки веб-службы, возвращающей XML-данные;  
  
-   встроенные XML-данные.  
  
 Способ указания элемента XML **Query** или пути к элементу зависит от типа XML-данных.  
  
 Для XML-документа элемент XML **Query** необязателен. Если он включен, то может содержать необязательный элемент XML **ElementPath**. В значении элемента XML **ElementPath** используется синтаксис пути к элементу. Элементы XML **Query** и XML **ElementPath** включаются, чтобы обеспечить правильную обработку пространства имен, если это нужно для XML-данных источника данных.  
  
 Для конечной точки веб-службы, на которую указывает URL-адрес строки соединения, элемент XML **Query** определяет метод веб-службы, действие SOAP или и то, и другое. Поставщик XML-данных создает запрос веб-службы, который получает XML-данные для отчета.  
  
> [!NOTE]  
>  Если пространство имен веб-службы содержит символ косой черты (**/)** , включите как метод веб-службы, так и действие SOAP, чтобы модуль обработки XML-данных мог правильно определить пространство имен.  
  
 Для встроенных XML-документов элемент XML **Query** определяет встроенные XML-данные, включает дополнительные пространства имен и содержит необязательный элемент XML **ElementPath**.  
  
## <a name="specifying-query-parameters-for-xml-data"></a>Указание параметров запроса XML-данных  
 Для XML-документов можно указать параметры запроса.  
  
-   Параметры включаются в URL-адрес как стандартные URL-параметры.  
  
-   В случае запросов к веб-службе параметры запросов передаются методу веб-службы. Для определения параметра запроса используется страница **Параметры** диалогового окна **Свойства набора данных** . 
  
### <a name="example"></a>Пример  
 Примеры, представленные в следующей таблице, иллюстрируют получение данных от веб-службы сервера отчетов, из XML-документа, а также встроенных XML-данных.  
  
|Источник данных XML|Пример запроса|  
|---------------------|-------------------|  
|XML-данные веб-службы с помощью метода <xref:ReportService2010.ReportingService2010.ListChildren%2A> .|`<Query>`<br /><br /> `<Method Name="ListChildren" Namespace="http://schemas.microsoft.com/sqlserver/2005/06/30/reporting/reportingservices" />`<br /><br /> `</Query>`|  
|XML-данные веб-службы при помощи действия SoapAction.|`<Query xmlns=namespace>`<br /><br /> `<SoapAction>http://schemas/microsoft.com/sqlserver/2005/03/23/reporting/reportingservices/ListChildren</SoapAction>`<br /><br /> `</Query>`|  
|XML-документ или внедренные XML-данные, использующие пространства имен.<br /><br /> Элемент запроса, задающий пространства имен для пути к элементу.|`<Query xmlns:es="http://schemas.microsoft.com/StandardSchemas/ExtendedSales">`<br /><br /> `<ElementPath>/Customers/Customer/Orders/Order/es:LineItems/es:LineItem</ElementPath>`<br /><br /> `</Query>`|  
|Встроенный XML-документ.|`<Query>`<br /><br /> `<XmlData>`<br /><br /> `<Customers>`<br /><br /> `<Customer ID="1">Bobby</Customer>`<br /><br /> `</Customers>`<br /><br /> `</XmlData>`<br /><br /> `<ElementPath>Customer {@}</ElementPath>`<br /><br /> `</Query>`|  
|XML-документ, использующий значения по умолчанию.|*No query*.<br /><br /> Путь к элементу определяется на основе самого XML-документа и не зависит от пространства имен.|  
  
> [!NOTE]  
>  Первый пример веб-службы перечисляет содержимое сервера отчетов, применяющего метод <xref:ReportService2006.ReportingService2006.ListChildren%2A> . Для выполнения этого запроса необходимо создать новый источник данных и задать строку подключения: `http://localhost/reportserver/reportservice2006.asmx`. Метод <xref:ReportService2006.ReportingService2006.ListChildren%2A> имеет два параметра: **Item** и **Recursive**. Для **Item** установите значение по умолчанию **/** , а для параметра **Recursive** — значение **1**.  
  
## <a name="specifying-namespaces"></a>Указание пространств имен  
 Для указания пространств имен, используемых XML-данными из источника данных, используется элемент XML **Query** . Следующий XML-запрос использует пространство имен **sales**. Узлы XML **ElementPath** для элементов `sales:LineItems` и `sales:LineItem` используют пространство имен **sales**.  
  
```  
<Query xmlns:sales=  
"http://schemas.microsoft.com/StandardSchemas/ExtendedSales">  
   <SoapAction>  
      http://schemas.microsoft.com/SalesWebService/ListOrders   
   </SoapAction>  
   <ElementPath>  
      Customers/Customer/Orders/Order/sales:LineItems/sales:LineItem  
   </ElementPath>  
</Query>  
```  
  
 Чтобы указать пространство имен поставщика данных, оставив пространство имен по умолчанию пустым, используется **xmldp**. Это показано в следующем примере.  
  
### <a name="example"></a>Пример  
 В следующих примерах используется XML-документ DPNamespace.xml, который для наглядности приводится после таблицы. В таблице представлены два примера синтаксиса пути XML ElementPath, включающие префиксы пространства имен.  
  
|Элемент XML-запроса|Полученные в результате поля набора данных|  
|-----------------------|-------------------------------------|  
|\<Query/>|Значение A: `http://schemas.microsoft.com/...`<br /><br /> Значение B: `http://schemas.microsoft.com/...`<br /><br /> Значение C: `http://schemas.microsoft.com/...`|  
|`<xmldp:Query xmlns:xmldp="http://schemas.microsoft.com/sqlserver/2005/02/reporting/XmlDPQuery" xmlns:ns="http://schemas.microsoft.com/...">`<br /><br /> `<xmldp:ElementPath>Root {}/ns:Element2/Node</xmldp:ElementPath>`<br /><br /> `</xmldp:Query>`|Значение D<br /><br /> Значение E<br /><br /> Значение F|  
  
#### <a name="xml-document-dpnamespacexml"></a>XML-документ: DPNamespace.xml  
 Можно скопировать этот XML-документ и сохранить его по URL-адресу, который конструктор отчетов будет использовать в качестве источника XML-данных, например http://localhost/DPNamespace.xml.  
  
```  
<Root xmlns:ns="http://schemas.microsoft.com/...">  
   <ns:Element1>  
      <Node>Value A</Node>  
      <Node>Value B</Node>  
      <Node>Value C</Node>  
   </ns:Element1>  
   <ns:Element2>  
      <Node>Value D</Node>  
      <Node>Value E</Node>  
      <Node>Value F</Node>  
   </ns:Element2>  
</Root>  
```  
  
## <a name="see-also"></a>См. также:  
 [Тип соединения XML (службы SSRS)](../../reporting-services/report-data/xml-connection-type-ssrs.md)   
 [Учебники по службам Reporting Services (SSRS)](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  
