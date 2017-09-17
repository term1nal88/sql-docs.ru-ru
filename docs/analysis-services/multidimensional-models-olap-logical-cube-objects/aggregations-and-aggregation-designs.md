---
title: "Агрегаты и статистические схемы | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- aggregations [Analysis Services], about aggregations
- storage [Analysis Services], aggregations
- Storage Design Wizard
- data summary [Analysis Services]
- data storage [Analysis Services]
- storing data [Analysis Services], aggregations
- aggregations [Analysis Services]
ms.assetid: 35bd8589-39fa-4e0b-b28f-5a07d70da0a2
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8554ed91ce593803fe1043823aa0e97aa890043b
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="aggregations-and-aggregation-designs"></a>Агрегаты и статистические схемы
  Объект <xref:Microsoft.AnalysisServices.AggregationDesign> задает ряд определений статистической обработки, которые могут совместно использоваться в нескольких секциях.  
  
 Объект <xref:Microsoft.AnalysisServices.Aggregation> представляет результат суммирования данных группы мер при определенной гранулярности измерений.  
  
 Простой объект <xref:Microsoft.AnalysisServices.Aggregation> состоит из базовых сведений и измерений. Основная информация включает в себя имя статистической обработки, идентификатор, аннотации и описание. Измерения — это коллекции объектов <xref:Microsoft.AnalysisServices.AggregationDimension>, которые содержат список атрибутов гранулярности для измерения.  
  
 Агрегаты — это предварительно вычисляемые сводные данные конечных ячеек. Агрегаты содержат ответы на еще не заданные вопросы, что позволяет значительно сократить время ответа на запрос. Например, когда данные в таблице фактов хранилища данных содержат сотни тысяч строк, обработка запроса суммарных значений недельных продаж для конкретной линии продуктов может занять значительное время — ведь чтобы получить ответ, при его выполнении необходимо просмотреть и сложить все строки в таблице фактов. Однако ответ может быть практически немедленным, если были предварительно вычислены сводные данные для ответа на этот запрос. Это предварительное вычисление сводных данных происходит во время обработки и является основой быстрого отклика технологии OLAP.  
  
 Кубы в технологии OLAP являются способом организации сводных данных в многомерные структуры. Измерения и их иерархии атрибутов отражают запросы, которые могут быть применены к кубу. Агрегаты хранятся в многомерной структуре в ячейках с координатами, заданными измерениями. Например, вопрос "Каков объем продаж продукта X в 1998 году в северо-западном регионе?" включает в себя три измерения ("Продукт", "Время" и "География") и одну меру ("Продажи"). Значение ячейки в кубе, расположенной в заданных координатах («Продукт X», «1998», «Северо-запад»), представляет собой ответ, одиночное числовое значение.  
  
 Другие вопросы могут возвращать несколько значений, например: «Каковы поквартальные объемы продаж оборудования по регионам в 1998 году?». Подобные запросы возвращают наборы ячеек из координат, удовлетворяющих заданным условиям. Количество ячеек, возвращаемых запросом, зависит от количества элементов на уровне «Оборудование» измерения «Продукт», четырех кварталов в 1998 году и числа регионов в измерении «География». Если все сводные данные были предварительно рассчитаны в агрегатах, то время отклика на запрос будет зависеть только от того, сколько времени понадобится для извлечения значений из указанных ячеек. Вычисление и чтение данных из таблицы фактов при этом не потребуются.  
  
 Хотя предварительные вычисления всех возможных агрегатов в кубе могут обеспечить самое малое время отклика для всех запросов, службы [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] достаточно легко вычисляют значения некоторых агрегатов на основе других предварительно вычисленных агрегатов. Кроме того, вычисление значений всех возможных агрегатов требует значительных затрат на вычисление и хранение. Следовательно, существует компромисс между требованиями к объему хранилища и количеством возможных агрегатов, для которых производятся предварительные вычисления (в процентах). Если значения агрегатов не вычисляются (0 %), то необходимое время обработки и место для хранения будут для куба минимальны, но запросы будут выполняться медленно, потому что необходимые для ответа данные должны будут извлекаться из конечных ячеек и затем статистически обрабатываться при обработке каждого запроса. Например, чтобы получить единственное число в ответ на упомянутый выше вопрос («Каков объем продаж продукта X в 1998 году в Северо-Западном регионе?») может потребовать считывания тысяч строк данных и извлечения для каждой из них значения столбца, в котором хранятся значения меры «Продажи». Кроме того, время, затраченное на получение данных, будет зависеть от выбранного режима хранения — MOLAP, HOLAP или ROLAP.  
  
## <a name="designing-aggregations"></a>Проектирование статистических схем  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] включает в себя сложный алгоритм выборки агрегатов для предварительных вычислений, позволяющий быстро вычислять агрегаты на основе предварительно вычисленных значений. Например, если существуют предварительно вычисленные агрегаты для уровня «Месяц» измерения «Время», то вычисление для уровня «Квартал» потребует всего лишь сложения трех чисел, которое быстро выполняется по мере необходимости. Такой подход позволяет сократить время обработки и снизить требования к объему хранилища, практически не сказываясь при этом на времени отклика.  
  
 Мастер статистических схем предоставляет возможность задать ограничения хранилища и процентных показателей для алгоритма, позволяя достичь компромисса между временем отклика запросов и требованиями к объему хранилища. Однако алгоритм мастера статистических схем предполагает, что все возможные запросы одинаково вероятны. Мастер оптимизации с учетом использования позволяет изменить статистическую схему для группы мер путем анализа запросов, которые выдавались клиентскими приложениями. Мастер для настройки статистической схемы куба позволяет уменьшить время отклика на часто выполняемые запросы за счет редко выполняемых, не оказывая при этом значительного влияния на необходимый для куба объем хранилища.  
  
 Агрегаты проектируются при помощи мастеров, но не вычисляются до момента обработки секции, для которой они были спроектированы. Если после создания агрегата структура куба изменилась либо в исходных таблицах куба были изменены или добавлены данные, то обычно требуется проверка агрегатов куба и его повторная обработка.  
  
## <a name="see-also"></a>См. также:  
 [Обработка и режимы хранения секции](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  