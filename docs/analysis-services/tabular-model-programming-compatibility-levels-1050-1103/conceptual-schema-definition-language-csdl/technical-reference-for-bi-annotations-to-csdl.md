---
title: "Технический справочник по заметки бизнес-Аналитики для языка CSDL | Документы Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 63b3e069-6ba5-474e-b769-47b7cc87b7dd
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0cf821eb8c5db3410901f3d72826e0c2c8b8a274
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="technical-reference-for-bi-annotations-to-csdl"></a>Технический справочник по аннотациям бизнес-аналитики для языка CSDL
  В этом разделе приведен список элементов, атрибутов и свойств, используемых в CSDL, которые представляют табличные модели [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Некоторые элементы новые; другие помечены или расширены для поддержки построения моделей бизнес-аналитики.  
  
 Обзор табличной модели и как сущности, связи и формулы представлены на языке CSDL см. в разделе [заметки языка CSDL для бизнес-аналитики &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md).  
  
## <a name="extended-csdl-elements-complex-types"></a>Расширенные элементы языка CSDL: Сложные типы  
 Следующие элементы языка CSDL добавлены или расширены для поддержки моделей данных бизнес-аналитики, как табличных, так и многомерных.  
  
-   [Элемент AssociationSet &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)  
  
-   [Элемент BaseProperty &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)  
  
-   [Элемент DefaultDetails &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/defaultdetails-element-csdlbi.md)  
  
-   [Элемент DisplayKey &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/displaykey-element-csdlbi.md)  
  
-   [Элемент EntityContainer &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitycontainer-element-csdlbi.md)  
  
-   [Элемент EntitySet &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)  
  
-   [Элемент EntityType &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)  
  
-   [Элемент Hierarchy &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md)  
  
-   [Элемент KPI &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)  
  
-   [Элемент KpiGoal &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpigoal-element-csdlbi.md)  
  
-   [Элемент KpiStatus &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpistatus-element-csdlbi.md)  
  
-   [Элемент Level &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/level-element-csdlbi.md)  
  
-   [Элемент measure &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/measure-element-csdlbi.md)  
  
-   [Элемент member &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/member-element-csdlbi.md)  
  
-   [Элемент MemberRef &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md)  
  
-   [Элемент NavigationProperty &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/navigationproperty-element-csdlbi.md)  
  
-   [Элемент Property &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)  
  
-   [Элемент PropertyRef &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)  
  
## <a name="simple-type-and-subtypes"></a>Простой тип и подтипы  
 В следующей таблице приведены некоторые простые типы и некоторые малые сложные типы, входящие в определения сложных типов, перечисленных выше. Документация для каждого простого типа или подтипа, названного в левом столбце, содержится в родительских элементах, названных в правом столбце.  
  
|Простой тип|Есть в разделе|  
|-----------------|--------------------|  
|Выравнивание|[Элемент BaseProperty &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)|  
|CompareOptions|[Элемент EntityContainer &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitycontainer-element-csdlbi.md)|  
|Содержание|[Элемент EntityType &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)|  
|ContextualNameRule|[Элемент member &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/member-element-csdlbi.md)|  
|DefaultAggregationFunction|[Элемент Property &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)|  
|DirectQueryMode|[Элемент EntityContainer &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitycontainer-element-csdlbi.md)|  
|GroupingBehavior|[Элемент Property &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)|  
|MemberRefs|[Элемент MemberRef &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md)|  
|PropertyRefs|[Элемент PropertyRef &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)|  
|SortDirection|[Элемент BaseProperty &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)|  
|Состояние|[Элемент AssociationSet &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)|  
|Стабильность|[Элемент Property &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)|  
|SortDirection|[Элемент BaseProperty &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)|  
  
## <a name="see-also"></a>См. также:  
 [Основные понятия CSDLBI](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)  
  
  