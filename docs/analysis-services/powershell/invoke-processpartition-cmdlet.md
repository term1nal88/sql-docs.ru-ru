---
title: "Командлет Invoke-Policyevaluation | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 516fab44-734e-425b-9bd0-b4aee1fd338f
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b29970facb251e859e1e845c00d4c12587ca33c4
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="invoke-processpartition-cmdlet"></a>Командлет Invoke-PolicyEvaluation

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Обрабатывает секцию с использованием переменной конкретного типа обработки.  

>[!NOTE] 
>В этой статье может содержать устаревшие сведения и примеры. С помощью командлета Get-Help для последней версии.
  
## <a name="syntax"></a>Синтаксис  
 `Invoke-ProcessPartition [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [-CubeName] <System.String> [-MeasureGroupName] <System.String> [<CommonParameters>]`  
  
 `Invoke-ProcessPartition –DatabasePartition <Microsoft.AnalysisServices.Partition> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Командлет Invoke-ProcessParition обрабатывает определенную секцию базы данных служб Analysis Services для заданного куба и группы мер. Значение ProcessType определяет область операции. При обработке секции необходимо указать тип обработки. Дополнительные сведения см. в разделе [Настройка параметров обработки (службы Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="parameters"></a>Параметры  
  
### <a name="-name-string"></a>-Имя \<строка >  
 Указывает обрабатываемую секцию.  
  
|||  
|-|-|  
|Обязательно?|true|  
|Позиция?|0|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="-database-string"></a>-Базы данных \<строка >  
 Указывает базу данных, к которой относится куб.  
  
|||  
|-|-|  
|Обязательно?|true|  
|Позиция?|1|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="-cubename-string"></a>-CubeName \<строка >  
 Указывает куб, к которому принадлежит группа мер.  
  
|||  
|-|-|  
|Обязательно?|true|  
|Позиция?|2|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="-measuregroupname-string"></a>-MeasureGroupName \<строка >  
 Указывает группу мер, к которой принадлежит секция.  
  
|||  
|-|-|  
|Обязательно?|true|  
|Позиция?|2|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="-databasepartition-microsoftanalysisservicespartition"></a>-DatabasePartition \<Microsoft.AnalysisServices.Partition >  
 Указывает обрабатываемую секцию.  
  
|||  
|-|-|  
|Обязательно?|true|  
|Позиция?|2|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>Тип процесса - \<Microsoft.AnalysisServices.ProcessType >  
 Задает тип обработки: ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ProcessRecalc.  
  
|||  
|-|-|  
|Обязательно?|true|  
|Позиция?|именованный|  
|Значение по умолчанию||  
|Принимать входные данные конвейера?|false|  
|Принимать символы-шаблоны?|false|  
  
### <a name="commonparameters"></a>\<Общие параметры >  
 Этот командлет поддерживает общие параметры: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer и -OutVariable. Дополнительные сведения см. в разделе [Об общих параметрах](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Входы и выходы  
 Входной тип — это тип объектов, которые можно направить в командлет. Тип возвращаемого значения — это тип объектов, возвращаемых командлетом.  
  
|||  
|-|-|  
|Входные данные|Нет|  
|Выходные данные|Нет|  
  
## <a name="example-1"></a>Пример 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\Sales Orders\Partitions\Total_Orders_2004 > Get-Item .| Invoke-ProcessPartition –ProcessType:ProcessDefault`  
  
 Эта команда передает в конвейер удостоверение обрабатываемой секции.  
  
## <a name="example-2"></a>Пример 2  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups> Invoke-ProcessPartition –Name “Total_Orders_2003” –MeasureGroupname “Sales Order” –CubeName “Adventure Works” –database “AWTEST” –ProcessType “ProcessFull”`  
  
 Эта команда обрабатывает секцию Total_Orders_2003 в группе мер Sales Orders базы данных AWTEST.  
  
  
  