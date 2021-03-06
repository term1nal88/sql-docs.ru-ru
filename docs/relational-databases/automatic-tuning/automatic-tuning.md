---
title: Автоматическая настройка | Документация Майкрософт
description: Дополнительные сведения об автоматической настройке в SQL Server и базы данных SQL Azure
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 639b2f5fd09ad017f94881358f8b2731cbd39c51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849332"
---
# <a name="automatic-tuning"></a>Автоматическая настройка
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Функция автоматической настройки базы данных предоставляет сведения о возможных проблемах с обработкой запросов и рекомендуемые решения. Она также может автоматически исправлять выявленные проблемы.

Автоматическая настройка в [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] уведомляет об обнаружении потенциальных проблем производительности и позволяет применять корректирующие действия или позволяет [!INCLUDE[ssde_md](../../includes/ssde_md.md)] автоматически устранять проблемы с производительностью.
Автоматическая настройка в [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] позволяет выявлять и устранять проблемы с производительностью из-за **регрессией в выборе плана SQL**. Автоматическая настройка в [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] создает необходимые индексы и удаляет неиспользуемые индексы.

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] отслеживает запросы, которые выполняются в базе данных и автоматически повышает производительность рабочей нагрузки. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] имеет встроенный аналитический механизм, который может автоматически настраивать и повышать производительность запросов путем динамической адаптации базы данных к рабочей нагрузке. Существует два функций автонастройки, которые доступны.

 -  **Автоматическое исправление плана** (в [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] и [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]), определяющий планов выполнения проблемных запросов и проблемы производительности плана исправления SQL.
 -  **Автоматическое управление индексами** (доступно только в [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]), определяющий, индексы, которые должны быть добавлены в базу данных или, которые должны быть удалены.

## <a name="why-automatic-tuning"></a>Почему Автоматическая настройка?

Три из главных задач при администрировании классической базы данных мониторинга рабочей нагрузки, определение важных [!INCLUDE[tsql_md](../../includes/tsql-md.md)] запросы, индексы, которые должны быть добавлены для повышения производительности и идентифицирующий редко используется. [!INCLUDE[ssde_md](../../includes/ssde_md.md)] обеспечивает точное представление о запросах и индексах, которые необходимо отслеживать. Тем не менее постоянно отслеживает базу данных — это сложная и трудоемкая задача, особенно при работе с несколькими базами данных. Управление огромным числом баз данных может быть невозможно эффективно. Вместо того чтобы выполнять мониторинг и настройку базы данных вручную, вы рекомендуем делегировать некоторые мониторинг и действия по настройке [!INCLUDE[ssde_md](../../includes/ssde_md.md)] с помощью функции автоматической настройки.

### <a name="how-does-automatic-tuning-work"></a>Как работает автоматическая настройка?

Автоматическая настройка — это непрерывный мониторинг и анализ процесс, который постоянно отслеживают характеристики рабочей нагрузки и выявить потенциальные проблемы и усовершенствования.

![Процесс автоматической настройки](./media/tuning-process.png)

Этот процесс позволяет базе данных динамически адаптироваться к рабочей нагрузке поиска индексы и планы могут способствовать повышению производительности рабочих нагрузок и какие индексы, влияющие на рабочую нагрузку. На основании этих данных, автоматическая настройка применяет действия по настройке, которые повышают производительность рабочей нагрузки. Кроме того база данных постоянно отслеживает производительность после любого изменения, сделанные автоматической настройкой, чтобы убедиться, что они повышают производительность рабочей нагрузки. Любое действие, которое не повысило производительность, автоматически отменяется. Процесс проверки является ключевой возможностью, которая гарантирует, что любые изменения, сделанные автоматической настройкой падать производительность рабочей нагрузки.

## <a name="automatic-plan-correction"></a>Автоматическое исправление плана

Автоматическое исправление плана — автоматической функции настройки, определяющий **Выбор регрессии планов SQL** и автоматически устранить проблему, можно применить последний известный удачный план.

### <a name="what-is-sql-plan-choice-regression"></a>Что такое Регрессия Выбор плана SQL?

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] может использовать разные планы SQL для выполнения [!INCLUDE[tsql_md](../../includes/tsql-md.md)] запросов. Планы запросов зависят от статистики, индексы и других факторов. Оптимальный план, который должен использоваться для выполнения некоторых [!INCLUDE[tsql_md](../../includes/tsql-md.md)] запрос может изменяться с течением времени. В некоторых случаях новый план не может быть лучше, чем предыдущий, и новый план может вызвать снижение производительности.

 ![Регрессия Выбор плана SQL](media/plan-choice-regression.png "регрессии Выбор плана SQL") 

Каждый раз, когда вы заметили планом, вы должны найти хорошие предыдущих планирования и заставить его вместо текущего один с использованием `sp_query_store_force_plan` процедуры.
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] в [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] предоставляет сведения о бюллетене планы и рекомендуемые действия по исправлению.
Кроме того [!INCLUDE[ssde_md](../../includes/ssde_md.md)] позволяет полностью автоматизировать этот процесс и позволить [!INCLUDE[ssde_md](../../includes/ssde_md.md)] устранить проблему, найти связанные с изменением плана.

### <a name="automatic-plan-choice-correction"></a>Автоматическое исправление выбранного плана

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] может автоматически переключиться на последний известный удачный план при обнаружении планом.

![Исправление выбранного плана SQL](media/force-last-good-plan.png "исправление выбранного плана SQL") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] автоматически обнаруживает любые потенциальные регрессии выбором плана, включая план, который должен использоваться вместо неправильный план.
Когда [!INCLUDE[ssde_md](../../includes/ssde_md.md)] применяет последний известный эффективный план, автоматически отслеживается также производительность принудительного плана. Если план не лучше плана с ухудшением, новый план будет ухудшением и [!INCLUDE[ssde_md](../../includes/ssde_md.md)] будет компилироваться новый план. Если [!INCLUDE[ssde_md](../../includes/ssde_md.md)] проверяет, что лучше, чем регрессионных принудительного плана, план будет сохранен до перекомпиляции (например, при следующей смене статистические данные или схему), если лучше плана с ухудшением.

Примечание: Все планы, автоматически принудительно сделать не persit при перезапуске экземпляра SQL Server.

### <a name="enabling-automatic-plan-choice-correction"></a>Включение автоматического исправления выбранного плана

Вы можете отдельно для каждой базы данных включить автоматическую настройку и указать, что при ухудшении производительности после изменения плана следует принудительно использовать последний известный эффективный план. Автоматическая настройка включается с помощью следующей команды.

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
После включения этого параметра [!INCLUDE[ssde_md](../../includes/ssde_md.md)] автоматически принудительно где предполагаемое Процессора замедлится более чем на 10 секунд, или количество ошибок в новом плане больше, чем количество ошибок в рекомендуемом и убедитесь, что Принудительный план лучше текущего.

### <a name="alternative---manual-plan-choice-correction"></a>Альтернатива — исправление выбранного плана вручную

Без автоматической настройки пользователи должны периодически проверять состояние системы и искать запросы, в которых были потери производительности. Если производительность была снижена любого плана, пользователь должен найти хорошие предыдущих планирования и заставить его вместо текущего один с использованием `sp_query_store_force_plan` процедуры. Рекомендуемым способом будет принудительно использовать последний известный удачный план, поскольку старые планы могут быть недоступными из-за изменения статистики или индекса. Пользователь, который заставляет последний известный удачный план необходимо отслеживать производительность запроса, который выполняется с помощью принудительного плана и убедиться, этой форсированном плане работает должным образом. В зависимости от результатов, мониторинга и анализа плана следует принудительно использовать, или пользователь должен найти другим способом для оптимизации запроса.
Вручную принудительными планами должен не используют неограниченно долго, так как [!INCLUDE[ssde_md](../../includes/ssde_md.md)] должны иметь возможность применить оптимальные планы. Пользователь или администратор базы данных должен в конечном итоге отменить принудительное использование плана с помощью `sp_query_store_unforce_plan` процедуры и позволяют [!INCLUDE[ssde_md](../../includes/ssde_md.md)] найти оптимальный план.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] предоставляет все необходимые представления и процедуры, необходимые для наблюдения за производительностью и устранения проблем в Store запроса.

В [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], можно найти с помощью системных представлений запросов Store регрессией в выборе плана. В [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], [!INCLUDE[ssde_md](../../includes/ssde_md.md)] и показывает потенциальных регрессией в выборе плана и рекомендуемые действия, которые должны быть применены в [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md) представления. В представлении отображаются сведения о проблеме, важность проблемы и сведения, такие как выявленных запросов, идентификатор плана с ухудшением, идентификатор плана, который был использован в качестве базовых показателей для сравнения и [!INCLUDE[tsql_md](../../includes/tsql-md.md)] инструкцию, которая может выполняться для исправления проблема.

| Тип | description | DATETIME | score | подробности | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | Изменено с 4 мс до 14 мс времени ЦП | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | Изменено с 37 мс до 84 мс времени ЦП | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

В следующем списке описываются некоторые столбцы из данного представления:
 - Тип Рекомендуемое действие - `FORCE_LAST_GOOD_PLAN`.
 - Описание, которое содержит сведения, почему [!INCLUDE[ssde_md](../../includes/ssde_md.md)] считает, что это изменение плана потенциальных снижения производительности.
 - Дата и время, при обнаружении потенциальных регрессии.
 - Оценка этой рекомендации. 
 - Сведения о неполадках, таких как идентификатор обнаруженных плана, идентификатор плана с ухудшением, идентификатор плана, которое должно обязательно устраните ее причину, [!INCLUDE[tsql_md](../../includes/tsql-md.md)] скрипт, который может применяться для устранения проблемы и т. д. Сведения хранятся в [формат JSON](../../relational-databases/json/index.md).

Используйте следующий запрос, чтобы получить сценарий, который устраняет проблемы и Дополнительные сведения о предполагаемым получить:

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount+recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage-recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount>recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
  CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            [current plan_id] int '$.regressedPlanId',
            [recommended plan_id] int '$.recommendedPlanId',

            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,

            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float

          ) as planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | скрипт | запрос\_идентификатор | текущий план\_идентификатор | Рекомендуется использовать план\_идентификатор | предполагаемый\_получить | Ошибка\_ошибкам
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Изменено с 3 мс на 46 мс времени ЦП | 36 | EXEC sp\_запроса\_хранения\_принудительно\_плана 12, 17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` Представляет предполагаемое количество секунд, которые будут сохранены, если Рекомендуемый план будет выполняться вместо текущего плана. Рекомендуемый план должен принудительно вместо текущего плана, если выигрыш больше 10 секунд. Если дополнительные ошибки (например, значения времени ожидания или прерванных выполнений) в текущем плане, чем в Рекомендуемый план, столбец `error_prone` может быть присвоено значение `YES`. Ошибка ошибкам план — еще одна причина, почему рекомендуется плана следует принудительно использовать вместо текущей.

Несмотря на то что [!INCLUDE[ssde_md](../../includes/ssde_md.md)] предоставляет все данные, необходимые для идентификации регрессией в выборе плана; непрерывный мониторинг и устранение проблем с производительностью может быть утомительным процессом. Автоматическая настройка упрощает этот процесс.

Примечание: Данные в это динамическое административное Представление не сохраняются после перезапуска данного экземпляра SQL Server.

## <a name="automatic-index-management"></a>Автоматическое управление индексами

В [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)], Управление индексами легко поскольку [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] узнает о рабочей нагрузке и гарантирует, что ваши данные всегда оптимально индексируется. Правильное Проектирование индекса имеет решающее значение для достижения оптимальной производительности рабочей нагрузки и автоматическое управление индексами может помочь оптимизировать индексы. Автоматическое управление индексами можно устранять проблемы с производительностью в неправильно индексированных базах данных, или поддерживать и оптимизировать индексы в существующую схему базы данных. Автоматическая настройка в [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] выполняет следующие действия:

 - Определяет индексы, которые могут повысить производительность запросов T-SQL, которые считывают данные из таблиц.
 - Определяет избыточные индексы или индексы, которые не использовались в более длительного периода времени, который может быть удален. Удаление ненужных индексов улучшает производительность запросов, которые обновляют данные в таблицах.

### <a name="why-do-you-need-index-management"></a>Зачем нужно Управление индексами?

Индексы ускоряют некоторые запросы на чтение данных из таблиц; Тем не менее они могут снизить производительность запросов для обновления данных. Необходимо тщательно проанализировать необходимость создания индекса и столбцы, которые необходимо включить в индекс. Некоторые индексы могут оказаться ненужными через некоторое время. Таким образом необходимо периодически определить и удалить индексы, которые не приносят никаких преимуществ. Если вы игнорировать неиспользуемые индексы, производительность запросов, которые обновляют данные может уменьшиться без каких-либо преимуществ для запросов, которые считывают данные. Неиспользуемые индексы также влияют на общую производительность системы, так как дополнительные обновления требуют ненужного ведения журнала.

Поиск оптимального набора индексов, которые повышают производительность запросов, чтение данных из таблиц и оказывают минимальное влияние на обновления может потребовать непрерывного и сложного анализа.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] использует встроенную аналитику и расширенные фильтры, которые анализируют запросы, определяют индексы, которые оптимально подходили бы для все существующие рабочие нагрузки и индексы могут быть удалены. База данных SQL Azure гарантирует, что имеется минимально необходимый набор индексов, оптимизирующих запросы, которые считывают данные, с минимальным воздействием на другие запросы.

### <a name="automatic-index-management"></a>Автоматическое управление индексами

Помимо обнаружения [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] можно автоматически применять выявленных рекомендации. Если обнаружится, что встроенные правила повышают производительность базы данных, можно разрешить [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] автоматически управлять индексами.

Чтобы включить автоматическую настройку в базе данных SQL Azure и позволить функция автоматической настройки полностью управлять рабочей нагрузкой, см. в разделе [включить автоматическую настройку в базе данных SQL Azure с помощью портала Azure](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable).

Когда [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] применяет рекомендацию CREATE INDEX или DROP INDEX, он автоматически отслеживает производительность запросов, которые были затронуты индекс. Создание индекса будут храниться только в том случае, если улучшить производительность соответствующих запросов. Удаленный индекс будет автоматически создан повторно, если существуют некоторые запросы, которые работать медленнее из-за отсутствия индекса.

### <a name="automatic-index-management-considerations"></a>Рекомендации по управлению автоматической индексации

Действия, необходимые для создания необходимых индексов в [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] может потреблять ресурсы и временно повлиять на производительность рабочей нагрузки. Чтобы свести к минимуму влияние процесса создания индекса на производительность рабочей нагрузки, базы данных SQL Azure находит соответствующее временное окно для любой операции управления индексом. Действия по настройке отложены, если в базе данных необходимы ресурсы для выполнения рабочей нагрузки и запускается, когда база данных имеет достаточно неиспользуемых ресурсов, которые можно использовать для задач обслуживания. Одна из важных функций автоматического управления индексами — это проверка действий. Когда базы данных SQL Azure создает или удаляет индекс, процесс мониторинга анализирует производительность рабочей нагрузки, чтобы убедиться, что действие повышена производительность. Если значительным улучшениям, действие немедленно отменяется. Таким образом, база данных SQL Azure гарантирует, что автоматические действия не оказывают негативного влияния на производительность рабочей нагрузки. Индексы, созданные автоматической настройкой, прозрачны для операции обслуживания в базовой схеме. Изменения схемы, например удаление или переименование столбцов не блокируются при наличии автоматически созданных индексов. Индексы, которые автоматически создаются в базе данных SQL Azure, немедленно удаляются при связанных удалении таблицы или столбцы.

### <a name="alternative---manual-index-management"></a>Альтернатива — Управление индексами вручную

Без автоматического управления индексами, пользователю необходимо будет вручную запросить [sys.dm_db_missing_index_details &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md) представление, чтобы найти индексы, которые могут повысить производительность, создавать индексы, используя указанные данные в состав этого представления и вручную монитор производительности запроса. Чтобы найти индексы, которые должны быть удалены, пользователям необходимо отслеживать статистику операционного использования индексов для поиска редко используемые индексы.

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] упрощает этот процесс. [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] анализирует рабочую нагрузку, определяет запросы, которые могут выполняться быстрее с новым индексом и перечислены неиспользуемые или повторяющиеся индексы. Дополнительные сведения об идентификации индексов, которые должны быть изменены в [найти рекомендации по индексам на портале Azure](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal).

## <a name="see-also"></a>См. также  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [Функции JSON](../../relational-databases/json/index.md)
