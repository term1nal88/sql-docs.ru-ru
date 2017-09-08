---
title: "PredictAssociation (расширения интеллектуального анализа данных) | Документы Microsoft"
ms.custom: 
ms.date: 09/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PredictAssociation
dev_langs:
- DMX
helpviewer_keywords:
- PredictAssociation function
ms.assetid: 33eb66b5-84c6-449f-aaae-316345bc4ad5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1fcebadb217b3ecbf2de828cc9566f4af5ffeddd
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="predictassociation-dmx"></a>PredictAssociation (расширения интеллектуального анализа данных)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Прогнозирует ассоциированное членство.  
  
Например функция PredictAssociation можно использовать для получения набора рекомендаций, учитывая его текущее состояние корзины покупок для клиента. 
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
PredictAssociation(<table column reference>, option1, option2, n ...)  
```  
  
## <a name="applies-to"></a>Объект применения  
 Содержащие прогнозируемые вложенные таблицы, включая связи и некоторые алгоритмы классификации. Алгоритмы классификации, которые поддерживают вложенные таблицы: [!INCLUDE[msCoName](../includes/msconame-md.md)] дерева принятия решений, [!INCLUDE[msCoName](../includes/msconame-md.md)] упрощенного алгоритма Байеса и [!INCLUDE[msCoName](../includes/msconame-md.md)] алгоритмы нейронной сети.  
  
## <a name="return-type"></a>Тип возвращаемых данных  
 \<Таблица выражения >  
  
## <a name="remarks"></a>Замечания  
 Параметры для **PredictAssociation** функции включают EXCLUDE_NULL, INCLUDE_NULL, INCLUSIVE, EXCLUSIVE (по умолчанию), INPUT_ONLY, INCLUDE_STATISTICS и INCLUDE_NODE_ID.  
  
> [!NOTE]  
>  Параметры INCLUSIVE, EXCLUSIVE, INPUT_ONLY и INCLUDE_STATISTICS применяются только к ссылкам на столбцы таблицы, а EXCLUDE_NULL и INCLUDE_NULL — только к ссылкам на скалярные столбцы.  
  
 Возвращает только INCLUDE_STATISTICS **$Probability** и **$AdjustedProbability**.  
  
 Если задан числовой параметр  *n*  указано, **PredictAssociation** функция возвращает top n наиболее подходящих значений, на основе вероятности:  
  
```  
PredictAssociation(colref, [$AdjustedProbability], n)  
```  
  
 При включении **$AdjustedProbability**, инструкция возвращает верхние  *n*  значения в зависимости от **$AdjustedProbability**.  
  
## <a name="examples"></a>Примеры  
 В следующем примере используется **PredictAssociation** функция, возвращающая четыре продуктов в Adventure Works базы данных, которые, скорее всего, будут проданы совместно.  
  
```  
SELECT  
  PredictAssociation([Association].[v Assoc Seq Line Items],4)  
From  
  [Association]  
```  
В следующем примере показано, как можно использовать вложенную таблицу в качестве входного для прогнозирующую функцию, с помощью предложения SHAPE. Запроса SHAPE создает набор строк с customerId как один столбец и вложенной таблицы в качестве второй столбец, который содержит список продуктов, которые у него клиент уже открыт. 

~~~~
SELECT T.[CustomerId], PredictAssociation(MyNestedTable, 5) // returns top 5 associated items
FROM My Model
PREDICTION JOIN
SHAPE {
    OPENQUERY([Adventure Works DW],'SELECT CustomerID, OrderNumber
    FROM vAssocSeqOrders ORDER BY OrderNumber')
} APPEND (
    {OPENQUERY([Adventure Works DW],'SELECT OrderNumber, model FROM 
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}
  RELATE OrderNumber to OrderNumber) AS T
~~~~  

  
## <a name="see-also"></a>См. также:  
 [Расширения интеллектуального анализа данных &#40; расширений интеллектуального анализа данных &#41; Справочник по функциям](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Функции &#40; расширений интеллектуального анализа данных &#41;](../dmx/functions-dmx.md)   
 [Общие функции прогнозирования &#40; расширений интеллектуального анализа данных &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
