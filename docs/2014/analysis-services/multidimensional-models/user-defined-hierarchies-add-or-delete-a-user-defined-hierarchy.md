---
title: Добавление или удаление пользовательской иерархии | Документация Майкрософт
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], adding
- removing hierarchies
- adding hierarchies
- deleting hierarchies
- hierarchies [Analysis Services], removing
ms.assetid: 953818b4-9543-4c01-bb20-1d45ec6dfb91
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79c6f928f8f3931960dcfa7ee72b8b3f237cf1e8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183984"
---
# <a name="add-or-delete-a-user-defined-hierarchy"></a>Добавление или удаление пользовательскую иерархию
  Добавление пользовательской иерархии в измерение и ее удаление производится на вкладке **Структура измерения** конструктора измерений в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 При добавлении пользовательской иерархии она будет недоступна для пользователей до тех пор, пока ее экземпляр не будет создан в экземпляре служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] и пока не выполнена обработка измерения. Дополнительные сведения см. в разделе [базы данных многомерных моделей &#40;SSAS&#41; ](multidimensional-model-databases-ssas.md) и [обработку объекта многомерных моделей](processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-add-a-user-defined-hierarchy-to-a-dimension"></a>Добавление пользовательской иерархии к измерению  
  
1.  В среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]откройте соответствующий проект служб [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , а затем откройте нужное измерение.  
  
     Измерение открывается в конструкторе измерений на вкладке **Структура измерения** .  
  
2.  Перетащите атрибут, который хотите использовать в пользовательской иерархии, из панели **Атрибуты** на панель **Иерархии** .  
  
3.  Перетащите дополнительные атрибуты, чтобы сформировать уровни в пользовательской иерархии.  
  
     Порядок, в котором атрибуты перечислены в иерархии, имеет значение. Например, в иерархии времени годы должны находиться выше дней.  
  
4.  При необходимости можно переупорядочить уровни в пользовательской иерархии, перетащив их на соответствующие позиции.  
  
5.  При необходимости измените свойства пользовательской иерархии или ее уровней.  
  
     Например, можно указать имя для пользовательской иерархии, переименовать один или несколько ее уровней и определить пользовательское имя для уровня «Все». Дополнительные сведения см. в разделе [свойства пользовательской иерархии](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md), и [свойства уровня &#91;Paved над&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md).  
  
    > [!NOTE]  
    >  По умолчанию пользовательская иерархия — это просто путь детализации данных для пользователей. Но если между уровнями имеются связи, производительность запросов может быть увеличена путем настройки связей атрибутов между уровнями. Дополнительные сведения см. в разделах [Связи атрибутов](../multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md) и [Определение связей атрибутов](attribute-relationships-define.md).  
  
### <a name="to-remove-a-user-defined-hierarchy-from-a-dimension"></a>Удаление пользовательской иерархии из измерения  
  
-   На панели **Иерархии** вкладки **Структура измерения** выберите пользовательскую иерархию, которую хотите удалить. На панели инструментов щелкните **Удалить**.  
  
     — или —  
  
-   На панели **Иерархия** щелкните правой кнопкой мыши пользовательскую иерархию, которую необходимо удалить, и выберите **Удалить**.  
  
     — или —  
  
-   Удалите иерархию из области конструктора с помощью мыши.  
  
## <a name="see-also"></a>См. также  
 [Пользовательские иерархии](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Создание определяемых пользователем иерархий](user-defined-hierarchies-create.md)  
  
  
