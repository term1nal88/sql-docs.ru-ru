---
title: "Входные XML-образец файла с пользовательской конфигурацией (DTA) | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: b29c9716-e5c3-4003-9efb-3ade2197b630
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b11febc0d8f432453516237b93a753a588014691
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="xml-input-file-sample-with-user-specified-configuration-dta"></a>Образец входного XML-файла с пользовательской конфигурацией (DTA)
  Скопируйте и вставьте этот образец входного XML-файла, определяющего пользовательскую конфигурацию с помощью элемента **Конфигурация** , в свой привычный XML-редактор или редактор текста. Это позволит выполнить анализ гипотетических вариантов. Анализ гипотетических вариантов предполагает использование элемента **Конфигурация** , чтобы определить набор гипотетических структур физического проектирования для настраиваемой базы данных. Затем можно применить помощник по настройке ядра СУБД для анализа эффекта от запуска рабочей нагрузки с учетом этой гипотетической конфигурации с целью выяснить, насколько повышается производительность выполнения запросов. Этот тип анализа позволяет проводить оценку новой конфигурации без затрат, связанных с ее фактическим внедрением. Если гипотетическая конфигурация не дает желаемого увеличения производительности, ее можно легко изменить и снова проанализировать до получения конфигурации, позволяющей достигнуть желаемых результатов.  
  
 После копирования образца в редактор замените значения элементов **Server**, **Database**, **Schema**, **Table**, **Workload**, **TuningOptions**и **Configuration** значениями, соответствующими конкретным особенностям данного сеанса настройки. Дополнительные сведения обо всех атрибутах и дочерних элементах, которые могут использоваться с этими элементами, см. в разделе [Справочник по входным XML-файлам (помощник по настройке ядра СУБД)](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md). В следующем образце используется только подмножество доступных атрибутов и параметров дочерних элементов.  
  
## <a name="code"></a>код  
  
```  
<?xml version="1.0" encoding="utf-16" ?>  
<DTAXML xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/sqlserver/2004/07/dta">  
  <DTAInput>  
    <Server>  
      <Name>MyServerName</Name>  
<!-- To tune multiple databases, list them and their associated tables in the following section. -->  
      <Database>  
        <Name>MyDatabaseName</Name>  
        <Schema>  
          <Name>MyDatabaseSchemaName</Name>  
<!-- You can list as many tables as necessary in the following section. -->  
          <Table>  
            <Name>MyTableName1</Name>  
          </Table>  
          <Table>  
            <Name>MyTableName2</Name>  
          </Table>  
        </Schema>  
      </Database>  
    </Server>  
    <Workload>  
<!-- The following element specifies a workload file, which can be a trace file or a Transact-SQL script file. -->  
      <File>c:\PathToYourWorkloadFile</File>  
    </Workload>  
    <TuningOptions>  
      <TuningTimeInMin>180</TuningTimeInMin>  
      <StorageBoundInMB>10000</StorageBoundInMB>  
      <FeatureSet>IDX_IV</FeatureSet>  
      <Partitioning>NONE</Partitioning>  
      <KeepExisting>NONE</KeepExisting>  
      <OnlineIndexOperation>OFF</OnlineIndexOperation>  
    </TuningOptions>  
    <Configuration SpecificationMode="Absolute">  
      <Server>  
        <Name>MyServerName</Name>  
          <Database>  
            <Name>MyDatabaseName</Name>  
            <Schema>  
              <Name>MyDatabaseSchemaName</Name>  
                <Table>  
                  <Name>MyTableName1</Name>  
                  <Recommendation>  
                    <Create>  
                      <Index Clustered="true" Unique="false" Online="false" IndexSizeInMB="873.75">  
                        <Name>MyIndexName</Name>  
                        <Column Type="KeyColumn" SortOrder="Ascending">  
                          <Name>MyColumnName1</Name>  
                        </Column>  
                        <Filegroup>MyFileGroupName1</FileGroup>  
                      </Index>  
                    </Create>  
                  </Recommendation>  
                </Table>  
            </Schema>  
          </Database>  
      </Server>  
    </Configuration>  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="comments"></a>Комментарии  
  
-   Удаление структур физического проектирования при указании режима **Absolute** элемента **Configuration** (`Configuration SpecificationMode="Absolute"`) не поддерживается.  
  
-   Нельзя создавать и удалять одинаковые структуры физического проектирования в режимах**Relative** и **Absolute**элемента **Configuration** .  
  
## <a name="see-also"></a>См. также:  
 [Запуск и использование помощника по настройке ядра СУБД](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Просмотр и работа с выходными данными помощника по настройке ядра СУБД](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Справочник по входным XML-файлам (помощник по настройке ядра СУБД)](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  