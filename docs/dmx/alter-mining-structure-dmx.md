---
title: ALTER MINING STRUCTURE (РАСШИРЕНИЯ ИНТЕЛЛЕКТУАЛЬНОГО АНАЛИЗА ДАННЫХ) | Документация Майкрософт
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f26ffdf21519a1b5aa2ce26060a2c6d36a53d6ff
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145929"
---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE (расширения интеллектуального анализа данных)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Создает новую модель интеллектуального анализа данных, основанную на уже существующей структуре интеллектуального анализа данных.  При использовании **ALTER MINING STRUCTURE** инструкцию, чтобы создать новую модель интеллектуального анализа данных, структура уже должен существовать. Напротив, при использовании инструкции [CREATE MINING MODEL &#40;расширений интеллектуального анализа данных&#41;](../dmx/create-mining-model-dmx.md), создать модель и автоматически создавать его базовой структуры интеллектуального анализа данных, в то же время.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
ALTER MINING STRUCTURE <structure>  
ADD MINING MODEL <model>  
(  
    <column definition list>  
  [(<nested column definition list>) [WITH FILTER (<nested filter criteria>)]]  
)  
USING <algorithm> [(<parameter list>)]   
[WITH DRILLTHROUGH]  
[,FILTER(<filter criteria>)]  
```  
  
## <a name="arguments"></a>Аргументы  
 *Структура*  
 Имя структуры интеллектуального анализа данных, к которой будет добавлена модель.  
  
 *model*  
 Уникальное имя модели интеллектуального анализа данных.  
  
 *Список определений столбца*  
 Список определений столбцов с разделителями-запятыми.  
  
 *списком определений вложенных столбцов*  
 Список с разделителями-запятыми столбцов вложенной таблицы, если применимо.  
  
 *вложенные условия фильтра*  
 Критерий фильтра, применяющийся к столбцам вложенной таблицы.  
  
 *алгоритм*  
 Имя алгоритма интеллектуального анализа данных, определенное поставщиком.  
  
> [!NOTE]  
>  Список алгоритмов, поддерживаемых текущим поставщиком могут быть получены с помощью [набор строк DMSCHEMA_MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset). Чтобы просмотреть алгоритмы, поддерживаемые в текущий экземпляр [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], см. в разделе [Data Mining Properties](../analysis-services/server-properties/data-mining-properties.md).  
  
 *список параметров*  
 Необязательный параметр. Список параметров, определенных поставщиком для алгоритма и разделенный запятыми.  
  
 *условия фильтра*  
 Критерий фильтра, применяющийся к столбцам таблицы вариантов.  
  
## <a name="remarks"></a>Примечания  
 Если структура интеллектуального анализа данных содержит составные ключи, то модель интеллектуального анализа данных должна включать в себя все ключевые столбцы, определенные в структуре.  
  
 Если модель не требуется прогнозируемый столбец, например, модели, построенные с помощью [!INCLUDE[msCoName](../includes/msconame-md.md)] кластеризации и [!INCLUDE[msCoName](../includes/msconame-md.md)] алгоритмы кластеризации последовательностей, не нужно включать определение столбца в инструкции. Все атрибуты в создаваемой модели будут рассматриваться как входы.  
  
 В **WITH** предложение, которое применяется к таблице вариантов, можно указать параметры фильтрации и детализации:  
  
-   Добавить **ФИЛЬТРА** ключевое слово и условия фильтра. Фильтр применяется к вариантам модели интеллектуального анализа данных.  
  
-   Добавить **ДЕТАЛИЗАЦИИ** ключевое слово разрешить пользователям проводить детализацию углублением от результатов модели к данным вариантов из модели интеллектуального анализа данных. Для расширений интеллектуального анализа данных активировать детализацию можно только при создании модели.  
  
 Для использования вариантов фильтрации и детализации, объединить ключевые слова в одном **WITH** предложения, используя синтаксис, показанный в следующем примере:  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>Список определений столбца  
 Структура модели задается списком определений столбцов, который содержит следующие данные для каждого столбца:  
  
-   имя (обязательно);  
  
-   псевдоним (необязательно);  
  
-   флаги моделирования;  
  
-   Указывает запрос на прогнозирование, указывающий алгоритму данный столбец содержит прогнозируемую величину, **PREDICT** или **PREDICT_ONLY** предложение  
  
 Чтобы определить один столбец, используйте следующий синтаксис для списка определений столбца.  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>Имя и псевдоним столбца  
 В списке определений столбцов должно использоваться то же имя столбца, что и в структуре интеллектуального анализа данных. Однако по желанию можно задать псевдоним, который будет представлять столбец из структуры интеллектуального анализа данных в модели интеллектуального анализа данных. Кроме того, для одного и того же столбца структуры можно создать несколько определений столбца, а затем присвоить этим копиям разные псевдонимы и разные способы использования в прогнозировании. По умолчанию, если псевдоним не задан, будет использоваться имя столбца структуры. Дополнительные сведения см. в разделе [создать псевдоним для столбца модели](../analysis-services/data-mining/create-an-alias-for-a-model-column.md).  
  
 Для столбцов вложенной таблицы, укажите имя вложенной таблицы, укажите тип данных в качестве **таблицы**, а затем укажите список вложенных столбцов для включения в модель, заключен в круглые скобки.  
  
 Критерий фильтра, применяемый к вложенной таблице, можно задать, добавив выражение условия фильтра после определения столбцов вложенной таблицы.  
  
### <a name="modeling-flags"></a>Флаги моделирования  
 Службы [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] поддерживают следующие флаги моделирования для столбцов моделей интеллектуального анализа данных.  
  
> [!NOTE]  
>  Флаг моделирования NOT_NULL применяется к столбцу структуры интеллектуального анализа данных. Дополнительные сведения см. в статье [CREATE MINING STRUCTURE (DMX)](../dmx/create-mining-structure-dmx.md).  
  
|||  
|-|-|  
|Термин|Определение|  
|**REGRESSOR**|Указывает, что алгоритм может использовать заданный столбец в формуле регрессии алгоритмов регрессии.|  
|**MODEL_EXISTENCE_ONLY**|Указывает, что само присутствие атрибута важнее, чем значения столбца атрибута.|  
  
 Для любого столбца можно задать несколько флагов моделирования. Дополнительные сведения об использовании флагов модели см. в разделе [флаги моделирования &#40;расширений интеллектуального анализа данных&#41;](../dmx/modeling-flags-dmx.md).  
  
### <a name="prediction-clause"></a>Прогнозирующее предложение  
 Прогнозирующее предложение описывает, как будет использоваться прогнозируемый столбец. В следующей таблице перечислены возможные предложения.  
  
|||  
|-|-|  
|**PREDICT**|Данный столбец может быть спрогнозирован с помощью модели, и его значения можно использовать во входных вариантах для вычисления значений других прогнозируемых столбцов.|  
|**PREDICT_ONLY**|Данный столбец может быть спрогнозирован с помощью модели, однако его нельзя использовать во входных вариантах для вычисления значений других прогнозируемых столбцов.|  
  
## <a name="filter-criteria-expressions"></a>Выражения условия фильтра  
 Можно задать фильтр, который будет ограничивать число вариантов, используемых в модели интеллектуального анализа данных. Фильтр можно применить к столбцам таблицы вариантов, к строкам вложенной таблицы либо к тому и другому одновременно.  
  
 Выражения условия фильтра представляют собой упрощенные предикаты расширений интеллектуального анализа данных, подобные предложению WHERE. Выражения условий фильтра представляют собой формулы, в которых допускаются только основные математические операторы, скалярные величины и имена столбцов. Исключение представляет собой оператор EXISTS, который возвращает значение true, если вложенный запрос вернул хотя бы одну строку. Предикаты можно сочетать с помощью распространенных логических операторов: И, OR и NOT.  
  
 Дополнительные сведения об использовании фильтров в модели интеллектуального анализа данных см. в разделе [фильтры для моделей интеллектуального анализа данных &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Столбцы фильтра должны быть столбцами структуры интеллектуального анализа данных. Нельзя создавать фильтры для столбцов модели или псевдонимов столбцов.  
  
 Дополнительные сведения об операторах расширений интеллектуального анализа данных и синтаксисе см. в разделе [столбцы модели интеллектуального анализа данных](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="parameter-definition-list"></a>Список определений параметров  
 Добавив параметры алгоритма к списку параметров, можно настраивать производительность и функции модели. Возможность использования параметров зависит от алгоритма, заданного в предложении USING. Список параметров, которые связаны с каждым алгоритмом, см. в разделе [алгоритмы интеллектуального анализа данных &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 Синтаксис списка параметров следующий:  
  
```  
[<parameter> = <value>, <parameter> = <value>,…]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>Пример 1: Добавление модели к структуре  
 В следующем примере добавляется модель интеллектуального анализа данных упрощенного алгоритма Байеса для **New Mailing** структуры интеллектуального анализа данных и ограничения, максимальное количество состояний атрибута значение 50.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes (MAXIMUM_STATES = 50)  
```  
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>Пример 2: Добавление в структуру модели с фильтром  
 В следующем примере добавляется модель интеллектуального анализа данных `Naive Bayes Women`, **New Mailing** структуры интеллектуального анализа данных. У новой модели та же базовая структура, что и у модели интеллектуального анализа данных, добавленной в примере 1; однако эта модель ограничивается только теми вариантами из структуры интеллектуального анализа данных, в которых клиентами являются женщины старше 50 лет.  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes Women]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes  
WITH FILTER([Gender] = 'F' AND [Age] >50)  
```  
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>Пример 3: Добавление отфильтрованной модели в структуру с вложенной таблицей  
 В следующем примере модель интеллектуального анализа данных добавляется к измененной версии структуры интеллектуального анализа данных Market Basket. Структуры интеллектуального анализа данных, используемых в этом примере был изменен для добавления **регион** столбец, который содержит атрибуты для региона клиента, и **Income Group** , подразделяющий доход клиента с помощью значения **высокой**, **умеренной**, или **низкой**.  
  
 Структура интеллектуального анализа данных также включает в себя вложенную таблицу с перечислением приобретенных данным клиентом товаров.  
  
 Поскольку структура интеллектуального анализа данных содержит вложенную таблицу, можно применить фильтр к таблице вариантов, вложенной таблице или к обеим таблицам. В данном примере фильтр вариантов и фильтр вложенных строк сочетаются, чтобы рассматривать только варианты для европейских покупателей с высоким доходом, купивших одну из моделей дорожной шины.  
  
```  
ALTER MINING STRUCTURE [Market Basket with Region and Income]  
ADD MINING MODEL [Decision Trees]  
(  
    CustomerKey,   
    Region,  
    [Income Group],  
    [Product] PREDICT (Model)   
WITH FILTER (EXISTS (SELECT * FROM [v Assoc Seq Line Items] WHERE   
 [Model] = 'HL Road Tire' OR  
 [Model] = 'LL Road Tire' OR  
 [Model] = 'ML Road Tire' )  
)  
) WITH FILTER ([Income Group] = 'High' AND [Region] = 'Europe')  
USING Microsoft_Decision Trees  
```  
  
## <a name="see-also"></a>См. также  
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; инструкции определения данных](../dmx/dmx-statements-data-definition.md)   
 [Расширения интеллектуального анализа данных &#40;расширений интеллектуального анализа данных&#41; инструкций по обработке данных](../dmx/dmx-statements-data-manipulation.md)   
 [Справочник по расширениям интеллектуального анализа данных (расширения интеллектуального анализа данных)](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
