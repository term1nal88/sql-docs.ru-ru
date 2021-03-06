---
title: xml_schema_namespace (Transact-SQL) | Документы Майкрософт
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 02139927b133d65816881b4ea9f2f2c018511cb3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47763192"
---
# <a name="xmlschemanamespace"></a>xml_schema_namespace
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Перестраивает все схемы или определенную схему в указанной коллекции XML-схем. Эта функция возвращает экземпляр типа данных **xml** .  
  
![Значок ссылки на раздел](../../database-engine/configure-windows/media/topic-link.gif "Значок ссылки на раздел") [Синтаксические обозначения в Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
## <a name="arguments"></a>Аргументы  
 *Relational_schema*  
 Имя реляционной схемы. *Relational_schema* — **sysname**.  
  
 *XML_schema_collection_name*  
 Имя коллекции XML-схем, которую необходимо перестроить. *XML_schema_collection_name* — **sysname**.  
  
 *Пространство имен*  
 URI пространства имен XML-схемы, которую требуется перестроить. Максимальная длина — 1000 символов. Если URI пространства имен не предоставлен, перестраивается вся коллекция XML-схем. *Namespace* — **nvarchar(4000)**.  
  
## <a name="return-types"></a>Типы возвращаемых данных  
 **xml**  
  
## <a name="remarks"></a>Remarks  
 При импорте компонентов XML-схемы в базу данных с помощью инструкций [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) или [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) сохраняются характеристики схемы, используемые для проверки правильности. Поэтому перестроенная схема лексически может отличаться от исходного документа схемы. В частности, теряются комментарии, пробельные символы и заметки, а также данные неявных типов преобразуются в явные. Например, \<xs:element name="e1" /> преобразуется в \<xs:element name="e1" type="xs:anyType"/>. Кроме этого, префиксы пространства имен не сохраняются.  
  
 Если указан параметр пространства имен, в результирующем документе схемы будут содержаться определения для всех компонентов схемы в этом пространстве имен, даже если они были добавлены в других документах схемы или во время выполнения этапов языка DDL (или если имели место оба случая).  
  
 Эту функцию нельзя использовать для создания документов XML-схемы из коллекции XML-схем **sys.sys**.  
  
## <a name="examples"></a>Примеры  
 В следующем примере коллекция XML-схем `ProductDescriptionSchemaCollection` запрашивается из производственной реляционной схемы в базе данных `AdventureWorks`.  
  
```  
USE AdventureWorks;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>См. также:  
 [Просмотр хранимой коллекции схем XML](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [Коллекции XML-схем (SQL Server)](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
