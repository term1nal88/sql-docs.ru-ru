---
title: "Свойства - пользовательские иерархии уровня | Документы Microsoft"
ms.custom: 
ms.date: 03/04/2017
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
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7fa44b453e1c91d8a43dde01ec582b59f22d3824
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="user-hierarchies---level-properties"></a>Пользовательские иерархии - свойства уровня
  В следующей таблице приведен список и описание свойств уровня в пользовательской иерархии.  
  
|Свойство|Description|  
|--------------|-----------------|  
|Description|Содержит описание уровня.|  
|HideMemberIf|Указывает, необходимо ли и когда необходимо скрывать элемент уровня от клиентских приложений. Это свойство может иметь следующие значения:<br /><br /> Никогда<br /> Элементы никогда не скрываются. Это значение по умолчанию.<br /><br /> OnlyChildWithNoName<br /> Элемент скрывается, когда он является единственным дочерним элементом своего родительского элемента и его имя пусто.<br /><br /> OnlyChildWithParentName<br /> Элемент скрывается, когда он является единственным дочерним элементом своего родительского элемента и его имя идентично имени родительского элемента.<br /><br /> NoName<br /> Элемент скрывается, когда его имя пусто.<br /><br /> ParentName<br /> Элемент скрывается, когда его имя идентично имени родительского элемента.|  
|Идентификатор|Содержит уникальный идентификатор уровня.|  
|Название|Содержит понятное имя уровня. По умолчанию имя уровня совпадает с именем исходного атрибута.|  
|SourceAttribute|Содержит имя исходного атрибута, на котором основан уровень.|  
  
## <a name="see-also"></a>См. также:  
 [Свойства пользовательской иерархии](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  