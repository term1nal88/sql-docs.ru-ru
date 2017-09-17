---
title: "Элемент ColumnID (EventColumn) (ASSL) | Документы Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ColumnID Element (EventColumn)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ColumnID
helpviewer_keywords:
- ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 38cac2f8ddbe9fd79e14308ff9587099c1991426
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="columnid-element-eventcolumn-assl"></a>Элемент ColumnID (EventColumn) (ASSL)
  Содержит идентификатор (ID) столбца с данными, которые будут захвачены для события как часть [трассировки](../../../analysis-services/scripting/objects/trace-element-assl.md) элемента.  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="element-characteristics"></a>Характеристики элемента  
  
|Характеристика|Описание|  
|--------------------|-----------------|  
|Тип данных и длина|Строковые значения|  
|Значение по умолчанию|None|  
|Количество элементов|1-1: обязательный элемент, который может появляться только один раз.|  
  
## <a name="element-relationships"></a>Связи элемента  
  
|Связь|Элемент|  
|------------------|-------------|  
|Родительский элемент|[EventColumn](../../../analysis-services/scripting/data-type/eventcolumn-data-type-assl.md)|  
|Дочерние элементы|Нет.|  
  
## <a name="remarks"></a>Замечания  
 Элемент, соответствующий родителю параметра **ColumnID** в модели объектов Analysis Management объекты AMO — <xref:Microsoft.AnalysisServices.TraceColumn>.  
  
## <a name="see-also"></a>См. также:  
 [Элемент Columns &#40; ASSL &#41;](../../../analysis-services/scripting/collections/columns-element-assl.md)   
 [Элемент Event &#40; ASSL &#41;](../../../analysis-services/scripting/objects/event-element-assl.md)   
 [Элемент Events &#40; ASSL &#41;](../../../analysis-services/scripting/collections/events-element-assl.md)   
 [Свойства &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  