---
title: "Распределения столбцов (интеллектуальный анализ данных) | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 96b2502e351f371163d5b748b432d381d237a8a9
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="column-distributions-data-mining"></a>Распределения столбцов (интеллектуальный анализ данных)
  В службах [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]можно определить распределения столбцов в структуре интеллектуального анализа данных, чтобы влиять на то, как алгоритмы обрабатывают данные в этих столбцах при создании моделей интеллектуального анализа данных. В некоторых алгоритмах лучше задавать распределение для всех столбцов, содержащих непрерывные данные, до начала обработки модели в случае, если указанные столбцы содержат общие распределения значений. Если распределения не заданы, создаваемые модели интеллектуального анализа данных могут работать менее точно, чем модели с заданными распределениями, так как на вход алгоритмов будет подаваться меньшее количество данных для анализа.  
  
 Алгоритмы, доступные в службах [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , поддерживают следующие типы распределения.  
  
 **Нормальный**  
 Значения для непрерывного столбца формируют гистограмму с нормальным распределением.  
  
 ![Гистограмма с нормальным распределением](../../analysis-services/data-mining/media/normal-distribution.gif "гистограмма с нормальным распределением")  
  
 **Логарифмическое нормальное**  
 Значения для непрерывного столбца формируют гистограмму, вытянутую в верхнем конце и скошенную в нижнем конце.  
  
 ![Гистограмма с логарифмически нормальным распределением](../../analysis-services/data-mining/media/log-normal-distribution.gif "гистограмма с логарифмически нормальным распределением")  
  
 **Равномерное**  
 На основе значений столбца непрерывных данных может быть сформирована плоская кривая, на которой все значения являются равновероятными.  
  
 ![Гистограмма с равномерным распределением](../../analysis-services/data-mining/media/uniform-distribution.gif "гистограмма с равномерным распределением")  
  
 Дополнительные сведения об алгоритмах в [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] см. в разделе [Алгоритмы интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>См. также:  
 [Типы содержимого (интеллектуальный анализ данных)](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Структуры интеллектуального анализа данных (службы Analysis Services — интеллектуальный анализ данных)](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Методы дискретизации &#40; интеллектуального анализа данных &#41;](../../analysis-services/data-mining/discretization-methods-data-mining.md)   
 [Распределения &#40; расширений интеллектуального анализа данных &#41;](../../dmx/distributions-dmx.md)   
 [Столбцы структуры интеллектуального анализа данных](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  