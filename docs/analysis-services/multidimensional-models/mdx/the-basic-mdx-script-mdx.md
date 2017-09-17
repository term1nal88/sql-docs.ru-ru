---
title: "Базовый скрипт многомерных Выражений (MDX) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default MDX scripts
- statements [MDX]
- expressions [MDX], scripts
- scripts [MDX], about scripts
ms.assetid: 83d9afda-7d34-42b5-8f28-20172a905f23
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f3f42d92332116ff94f0175619cc42face9a8b36
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="the-basic-mdx-script-mdx"></a>Базовый скрипт многомерных выражений (многомерные выражения)
  Скрипт многомерных выражений определяет процесс вычисления куба в службах [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Существует два типа скриптов многомерных выражений.  
  
 **Скрипт многомерных выражений по умолчанию**  
 При создании куба службы [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] создают стандартный скрипт многомерных выражений для этого куба. В этом скрипте определяется этап вычисления для всего куба.  
  
 **Пользовательский скрипт многомерных выражений**  
 После создания куба можно добавить пользовательские скрипты многомерных выражений, расширяющие характеристики вычисления куба.  
  
## <a name="the-default-mdx-script"></a>Скрипт многомерных выражений по умолчанию  
 Скрипт многомерных выражений по умолчанию, создаваемый службами [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] при определении куба, содержит одну инструкцию CALCULATE. Эта инструкция CALCULATE находится в начале скрипта многомерных выражений по умолчанию и говорит о том, что весь куб должен быть рассчитан во время первого этапа вычислений.  
  
 Скрипт многомерных выражений по умолчанию также включает в себя команды, создающие именованные наборы, назначения и вычисляемые элементы, созданные в конструкторе кубов.  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] добавляют команды непосредственно в скрипт многомерных выражений по умолчанию.  
  
-   Для каждого именованного набора в кубе в скрипт многомерных выражений по умолчанию добавляется соответствующая инструкция CREATE SET.  
  
-   Для каждого вычисляемого элемента в кубе в скрипт многомерных выражений по умолчанию добавляется соответствующая инструкция CREATE MEMBER.  
  
 Порядком команд, именованных наборов и вычисляемых элементов в скрипте многомерных выражений по умолчанию можно управлять на вкладке **Вычисления** конструктора кубов. Дополнительные сведения об определении вычислений, записываемых в скрипт многомерных выражений по умолчанию, см. в разделе [Вычисления в многомерных моделях](../../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md).  
  
 Если с кубом не связан ни один скрипт многомерных выражений, куб вычисляется по скрипту многомерных выражений по умолчанию. Куб должен быть связан хотя бы с одним скриптом многомерных выражений, поскольку только в скрипте определяется порядок вычисления куба. Другими словами, куб, не связанный со скриптом многомерных выражений или связанный с пустым скриптом многомерных выражений, не может и не будет вычислять значения ячеек. Если кубы создаются программно при помощи команд языка скриптов служб Analysis Services (ASSL) или объектов AMO, рекомендуется создать для куба скрипт многомерных выражений по умолчанию с одной инструкцией CALCULATE.  
  
## <a name="mdx-script-content"></a>Содержимое скрипта многомерных выражений  
 Скрипт многомерных выражений может содержать следующие инструкции и выражения.  
  
 Все инструкции сценариев многомерных выражений  
 Инструкции скриптов многомерных выражений управляют контекстом и областью вычислений, а также поведением других инструкций в скрипте многомерных выражений. В эту категорию входят следующие инструкции:  
  
-   [CALCULATE](../../../mdx/mdx-scripting-calculate.md)  
  
-   [FREEZE](../../../mdx/mdx-scripting-freeze.md)  
  
-   [SCOPE](../../../mdx/mdx-scripting-scope.md)  
  
 Дополнительные сведения об инструкциях сценариев многомерных выражений см. в разделе [Инструкции сценариев многомерных выражений (многомерные выражения)](../../../mdx/mdx-scripting-statements-mdx.md).  
  
 [CREATE MEMBER](../../../mdx/mdx-data-definition-create-member.md)  
 Инструкция CREATE MEMBER служит для создания вычисляемых элементов. Дополнительные сведения о создании вычисляемых элементов см. в разделе [Создание вычисляемых элементов в многомерных выражениях (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
 [CREATE SET](../../../mdx/mdx-data-definition-create-set.md)  
 Инструкция CREATE SET служит для создания именованных наборов. Дополнительные сведения о создании именованных наборов см. в разделе [Построение именованных наборов в многомерных выражениях (многомерные выражения)](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md).  
  
 Условные инструкции  
 Условные инструкции позволяют создавать ветвления в скриптах многомерных выражений. В эту категорию входят инструкции [CASE](../../../mdx/case-statement-mdx.md) и [IF](../../../mdx/mdx-scripting-if.md) .  
  
 Выражения присваивания  
 Выражения присваивания присваивают ограниченному вложенному кубу некое выражение, например просто значение. Выражение ограниченного вложенного куба — это коллекция ограниченных выражений наборов, определяющих «грани» вложенного куба в скрипте многомерных выражений. Ниже продемонстрирован синтаксис выражения ограниченного вложенного куба:  
  
```  
<Constrained subcube> ::= (   
    ( <Constrained set> [<Crossjoin operator> <Constrained set>...] |  
    <ROOT function> |  
    <TREE function> |  
    LEAVES() |  
    * ) [, <Constrained subcube>...]  
<Constrained set> ::=   
    <Natural hierarchy>.MEMBERS |   
    <Natural hierarchy>.LEVEL(<numeric expression>).MEMBERS |   
    { <Natural hierarchy member> } |   
    DESCENDANTS( <Natural hierarchy member>, <Level expression>, ( SELF | AFTER | SELF_AND_AFTER ) ) |   
    DESCENDANTS( <Natural hierarchy member>, , LEAVES )  
<Natural hierarchy> ::= <Hierarchy identifier>  
<Natural hierarchy member> ::= <Natural hierarchy>.<identifier>[.<identifier>...]  
```  
  
## <a name="see-also"></a>См. также  
 [Справочник по языку многомерных выражений (многомерные выражения)](../../../mdx/mdx-language-reference-mdx.md)   
 [Основные принципы создания скриптов многомерных выражений (службы Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  