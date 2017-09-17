---
title: "Пользовательские свойства источника CDC | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 744e9357-94a9-4202-abe8-1d3d202697e9
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 106f7ecb0798682b26c806ea9c2d943524dd87d4
ms.contentlocale: ru-ru
ms.lasthandoff: 08/03/2017

---
# <a name="cdc-source-custom-properties"></a>Пользовательские свойства источника «CDC»
  В следующей таблице описаны пользовательские свойства источника «CDC». Все свойства доступны для чтения и записи.  
  
|Имя свойства|Тип данных|Description|  
|-------------------|---------------|-----------------|  
|Соединение|Соединение ADO.Net|Соединение ADO.NET с базой данных CDC [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] для доступа к таблицам изменений.|  
|StateVariable|Строковые значения|Строковая переменная пакета служб SSIS, которая поддерживает состояние CDC текущего прогона CDC.|  
|CdcProcessingMode|Integer (перечисление)|Этот режим определяет, как осуществляется обработка. Возможными параметрами являются **Все**, **Все со старыми значениями**, **Суммарные**, **Суммарные с маской обновления**и **Суммарные со слиянием**.<br /><br /> Режимы, названия которых начинаются со слова «Все», возвращают все изменения, а режимы со словом «Суммарные» возвращают только суммарные изменения.<br /><br /> Таблицы без первичного ключа могут принимать только значения ALL.<br /><br /> **Суммарные с маской обновления** добавляет столбцы логических значений с шаблоном имени **__ $\<имя столбца >\__Changed** , указывающие на измененные столбцы в текущей строке изменения.<br /><br /> Дополнительные сведения о значениях этого свойства см. в разделе [Редактор источника "CDC" (страница "Диспетчер соединений")](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md).|  
|CaptureInstance|Строковые значения|Имя экземпляра отслеживания CDC с таблицей CDC, подлежащей считыванию. Отслеживаемая исходная таблица может иметь один или два отслеживаемых экземпляра для обеспечения возможности беспрепятственных переходов определения таблицы во время изменений схемы. Если для исходной таблицы отслеживания определено больше одного экземпляра отслеживания, выберите экземпляр отслеживания, который должен здесь использоваться. По умолчанию имени экземпляра системы отслеживания для таблицы [схема]. [таблица] имеет \<схема > _\<таблицы >, но что имена экземпляров самого захвата используется может отличаться. Действительную таблицу, которая считывается из таблицы CDC, является **cdc.\< экземпляр отслеживания > _CT**.|  
|ReprocessingIndicator|Логическое значение|Значение, которое указывает, добавляется ли столбец **__$reprocessing** . Этот специальный выходной столбец позволяет разработчикам служб SSIS трактовать ошибки согласованности по-другому при работе с начальным диапазоном обработки.<br /><br /> Если задано значение **true**, добавляется столбец  **__$reprocessing** .<br /><br /> Значением этого столбца является **true** , если диапазон обработки CDC перекрывается с начальным диапазоном обработки (диапазоном номеров LSN, соответствующим периоду начальной загрузки) или если диапазон обработки CDC обрабатывается повторно вслед за ошибкой в предыдущем прогоне. Этот столбец индикатора позволяет разработчику служб SSIS трактовать ошибки иначе при повторной обработке изменений (например, пропускать действия наподобие удаления несуществующей строки или вставки, которая окончилась неудачей из-за дублирующегося ключа).<br /><br /> Значение по умолчанию — **false**.|  
|CommandTimeOut|Целочисленный|Это значение указывает время ожидания (в секундах), которое используется при взаимодействии с базой данных [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Это значение используется в тех случаях, если время ответа из базы данных весьма продолжительно и значение по умолчанию (30 секунд) является недостаточным.|  
  
 Дополнительные сведения об источнике CDC см. в разделе [CDC Source](../../integration-services/data-flow/cdc-source.md).  
  
  