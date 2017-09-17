---
title: "Функция Lookup (построитель отчетов и службы SSRS) | Документы Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4426bffe23295c623d0bba5592c1488cb0ede770
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---lookup-function"></a>Функции построителя отчетов - функции поиска
  Возвращает первое совпадающее значение для заданного имени из набора данных, содержащего пары «имя-значение».  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Синтаксис  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Параметры  
 *source_expression*  
 (**Variant**) Выражение, вычисляемое в текущей области и указывающее имя или ключ для поиска. Например, `=Fields!ProdID.Value`.  
  
 *destination_expression*  
 (**Variant**) Выражение, вычисляемое для каждой строки в наборе данных и указывающее имя или ключ для сопоставления. Например, `=Fields!ProductID.Value`.  
  
 *result_expression*  
 (**Variant**) Выражение, которое вычисляется для строки в наборе данных, где *source_expression* = *destination_expression*, и указывает возвращаемое значение. Например, `=Fields!ProductName.Value`.  
  
 *набор данных*  
 Константа, задающая имя набора данных в отчете. Например, «Продукты».  
  
## <a name="return"></a>Возвращает  
 Возвращает значение **Variant**или **Nothing** , если совпадения нет.  
  
## <a name="remarks"></a>Замечания  
 Функция **Lookup** позволяет извлечь значение из указанного набора данных, состоящего из пар "имя-значение" с отношением "один к одному". Например, для поля ID в таблице функция **Lookup** может быть использована для поиска соответствующего поля Name в наборе данных, не привязанном к области данных.  
  
 Функция**Lookup** выполняет следующие действия.  
  
-   Вычисляет исходное выражение в текущей области.  
  
-   Вычисляет целевое выражение для каждой строки указанного набора данных после применения фильтров с учетом заданных для него параметров сортировки.  
  
-   При первом совпадении исходного и целевого выражений вычисляет результирующее выражение для этой строки в наборе данных.  
  
-   Возвращает результирующее значение выражения.  
  
 Для получения множества значений по одному имени или ключевому полю, если существует отношение связь "один ко многим", пользуйтесь [функцией LookupSet (построитель отчетов и службы SSRS)](../../reporting-services/report-design/report-builder-functions-lookupset-function.md). Для вызова **уточняющего запроса** набор значений, используйте [функция Multilookup &#40; Построитель отчетов и службы SSRS &#41; ](../../reporting-services/report-design/report-builder-functions-multilookup-function.md).  
  
 Существуют следующие ограничения.  
  
-   Функция**Lookup** вычисляется после применения всех выражений фильтров.  
  
-   Поддерживается только один уровень уточняющего запроса. Исходное, целевое и результирующее выражения не могут включать в себя ссылки на функцию уточняющего запроса.  
  
-   Исходное и результирующее выражения должны возвращать один и тот же тип данных. Возвращаемый тип совпадает с типом данных вычисленного результирующего выражения.  
  
-   Исходное, целевое и результирующее выражения не могут включать в себя ссылки на переменные отчета или группы.  
  
-   Функцию**Lookup** нельзя использовать в качестве выражения для следующих элементов отчета:  
  
    -   динамические строки соединения для источника данных;  
  
    -   вычисляемые поля в наборе данных;  
  
    -   параметры запроса в наборе данных;  
  
    -   фильтры в наборе данных;  
  
    -   параметры отчета;  
  
    -   Свойство Report.Language.  
  
 Дополнительные сведения см. в разделах [Справочник по агрегатным функциям (построитель отчетов и службы SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) и [Область выражения для суммирования, агрегатных функций и встроенных коллекций (построитель отчетов и службы SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Пример  
 В следующем примере предположим, что таблица привязана к набору данных, включающему в себя поле для идентификатора продукта ProductID. Отдельный набор данных с именем Product содержит соответствующий идентификатор продукта ID и его название Name.  
  
 В следующем выражении функция **Lookup** сравнивает значение ProductID со значением ID для каждой из строк набора данных Product и, при совпадении, возвращает значение поля Name для этой строки.  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>См. также  
 [Использование выражений в отчетах &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Примеры выражений &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Типы данных в выражениях &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Область выражения для итогов, статистические выражения и встроенных коллекций &#40; Построитель отчетов и службы SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  