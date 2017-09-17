---
title: "SQL и R данных типов и объектов данных (R в быстрый запуск SQL Server) | Документы Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
- SQL
ms.assetid: 1a17fc5b-b8c5-498f-b8b1-3b7b43a567e1
caps.latest.revision: 8
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e71e4a5d6fc6a88d0482ecd10d4238c12cd5ceaa
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="r-and-sql-data-types-and-data-objects-r-in-sql-quickstart"></a>SQL и R данных типов и объектов данных (R в быстрый запуск SQL Server)

На этом шаге вы узнаете о некоторых распространенных проблем, возникающих при перемещении данных между R и SQL Server:

+ Иногда типы данных не совпадают.
+ Неявные преобразования может иметь место
+ Иногда требуются операции приведения и преобразования.
+ R и SQL используют разные объекты данных.

## <a name="always-return-r-data-as-a-data-frame"></a>Возвращение данных R в виде кадра данных

Когда скрипт возвращает результаты из R в SQL Server, он должен возвращать данные в виде **data.frame**. Любой другой тип объекта, создаваемого в скрипте (список, коэффициент, вектор или двоичные данные) нужно преобразовать в кадр данных, если нужно вывести его как часть результатов хранимой процедуры. К счастью существует несколько функций R, поддерживающих изменение других объектов на кадр данных. Вы даже можете сериализовать двоичную модель и возвратить ее в блок данных, что вы сделаете далее в этом руководстве.

Во-первых давайте поэкспериментировать с некоторых основных объектов R R — векторов, матрицы и списки — и посмотрите, как преобразование в кадр данных изменяется выходные данные передаются в SQL Server.

Сравнить эти два сценария «Hello World» на R. Скрипты выглядят практически одинаково, но первый возвращает один столбец из трех значений, тогда как второй возвращает три столбца с одним значением каждого.

**Пример 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**Пример 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identifying-the-schema-and-data-types-of-r-data"></a>Определение схемы и типов данных R

Почему результаты настолько отличаются?

Обычно ответ можно найти, использовав команду R `str()`. Добавьте функцию `str(object_name)` в скрипте R для получения сведений о схеме данных возвращаемого объекта R в виде информационного сообщения. Сообщения можно просмотреть на панели **Сообщения** Visual Studio Code или на вкладке **Сообщения** в среде SSMS.

Чтобы понять, почему результаты примера 1 и 2 так сильно отличаются, вставьте строку `str(OutputDataSet)` в конце определения переменной _@script_ в каждой инструкции следующим образом:

**Пример 1 в функции str добавлен**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**Пример 2 с помощью функции str добавлен**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet)' , 
  @input_data_1 = N'  ';
```

Теперь просмотрите текст на вкладке **Сообщения**, в котором можно определить причину такой разницы.

**Результаты примера 1**

```
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**Результаты примера 2**

```
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

Как видно, небольшие изменения в синтаксисе R сильно повлияли на схему результатов. Мы не будем останавливаться на причину, из-за различия в типах данных R объясняются более тщательно контролировать в этой статье по Hadley Wickham: [структуры данных R](http://adv-r.had.co.nz/Data-structures.html).

Сейчас помните, что необходимо проверить ожидаемые результаты при приведении объектов R в кадры данных.

> [!TIP]
> 
> Можно также использовать функции идентификации R, такие как `is.matrix`, `is.vector`и т. д.

## <a name="implicit-conversion-of-data-objects"></a>Неявное преобразование объектов данных

Каждый объект данных R имеет собственные правила обработки значений в сочетании с другими объектами данных, если объекты данных имеют одинаковое количество измерений или если любой объект данных содержит разнородные типы данных.

Например, предположим, что вы выполняете следующую инструкцию для умножения матриц с помощью R. Вы умножаете матрицу с одним столбцом и тремя значения на массив с четырьмя значениями и в результате ожидаете получить матрицу 4x3.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

Один столбец с тремя значениями преобразуется в матрицу с одним столбцом. Так как матрица представляет собой особый вид массива в R, массив `y` неявно приводится к матрице с одним столбцом, чтобы обеспечить соответствие двух аргументов.

**Результаты**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

Однако обратите внимание, что происходит при изменении размера массива `y`.

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

На этот раз код R вернет одно значение в качестве результата.

**Результаты**
    
|Col1|
|---|
|1542|

Почему? В этом случае из-за двух аргументов может обрабатываться как векторов одинаковую длину, как матрица R возвращает скалярное произведение.  Это ожидаемое поведение в соответствии с правилами линейной алгебры. Тем не менее могут возникнуть проблемы, если нисходящее приложение ожидает, что выходная схема вывода не должна изменяться.

> [!TIP]
> 
> Отображаются сообщения об ошибках? Для этих примеров требуются таблицы **RTestData**. Если вы еще не создали тестовую таблицу данных, вернитесь на этот раздел: [работа с входными и выходными данными](../tutorials/rtsql-working-with-inputs-and-outputs.md).
> 
> Если таблица создана, но по-прежнему возникает ошибка, убедитесь в том, что хранимая процедура выполняется в контексте базы данных, содержащую таблицу, а не в **master** или другой базе данных.
> 
> Кроме того мы рекомендуем не использовать временные таблицы в приведенных ниже примерах. Некоторые клиенты R нарушит соединений между пакетами, удаление временных таблиц.

## <a name="merge-or-multiply-columns-of-different-length"></a>Слияние или перемножение столбцов разной длины

R обеспечивает большую гибкость при работе с векторами различных размеров и для этих столбцов структуры, объединение кадров данных. Списки векторов могут выглядеть как таблица, но они не подчиняются всем правилам, управляющим таблицами базы данных.

Например, следующий скрипт определяет числовой массив, длина которого равна 6, и сохраняет его в переменной R `df1`. Числовой массив затем сочетается с целыми числами RTestData таблицы, которое содержит три (3) значения, чтобы сделать новый кадр данных `df2`.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

Чтобы заполнить кадр данных, R повторно использует элементы, полученные из RTestData, столько раз, сколько требуется в соответствии с числом элементов в массиве `df1`.

**Результаты**
    
|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

Помните, что кадр данных только выглядит как таблица и на самом деле является списком векторов.

## <a name="cast-or-convert-sql-server-data"></a>Приведение или преобразование данных SQL Server

R и SQL Server используют разные типы данных, поэтому при выполнении запроса в SQL Server для получения данных и их передаче в среду выполнения R обычно выполняется неявное преобразование. Кроме того, преобразования выполняются при возвращении данных из R в SQL Server.

- Передает данные из запроса к процессу R, управляется службой панели запуска SQL Server и преобразует его в внутреннего представления для повышения эффективности.
- Среда выполнения R загружает данные в переменную data.frame и выполняет собственные операции с данными.
- Ядро СУБД возвращает данные в SQL Server по защищенному внутреннему соединению и представляет данные в контексте типов данных SQL Server.
- Вы можете получить данные путем подключения к SQL Server с помощью клиентской или сетевой библиотеки, которая может выполнять запросы SQL и обрабатывать табличные наборы данных. Это клиентское приложение может и по-другому влиять на данные.

Чтобы увидеть, как это работает, выполните запрос наподобие этого в хранилище данных AdventureWorksDW. Это представление возвращает данные продаж, используемые для создания прогнозов.

```sql
SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
> 
> Можно использовать любую версию базы данных AdventureWorks или создавать другой запрос, используя базу данных свой собственный. Важно для обработки некоторых данных, который содержит текст, даты и времени и числовых значений.

Попробуйте вставить этот запрос в качестве входного для хранимой процедуры.

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW2014].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

Если появляется сообщение об ошибке, возможно, необходимо внести некоторые изменения в текст запроса. Например, строковый предикат в предложении WHERE нужно заключать в два набора одинарных кавычек.

После того, как запрос начнет действовать, просмотрите результаты выполнения функции `str`, чтобы увидеть, как R обрабатывает входные данные.

**Результаты**

```
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

+ Столбец datetime был обработан с использованием типа данных R **POSIXct**.
+ Текстовый столбец «ProductSeries» было определено как **коэффициент**, то есть категориальной переменной. Строковые значения обрабатываются как коэффициенты по умолчанию. Если передать строку в R, она преобразуется в целое число для внутреннего использования и сопоставляется со строками на выходе.

### <a name="summary"></a>Сводка

Даже эти короткие примерах появится необходимость проверки эффекты преобразования данных при передаче SQL запросов в качестве входного. Так как некоторые типы данных SQL Server не поддерживаются с помощью R, рассмотрим эти решения для исправления ошибки.

+ Проверка данных, заранее и проверьте столбцов или значения в схеме, возможно, возникла проблема при передаче в код R.
+ Указывайте столбцы из источника входных данных по отдельности. Не используйте `SELECT *`. Определите способ обработки каждого столбца.
+ Во избежание непредвиденных ситуаций во время подготовки входных данных при необходимости выполняйте явные приведения.
+ Избегайте столбцов передачи данных (например, идентификаторы GUID или идентификаторами rowguids) привести к ошибкам, неприменимых для моделирования.

Дополнительные сведения о типах данных, поддерживаемых и неподдерживаемых см. в разделе [R библиотек и типы данных](../r/r-libraries-and-data-types.md).

Дополнительные сведения о влияние на производительность во время выполнения преобразования строк в числовые факторов, в разделе [оптимизации производительности SQL Server R Services](../r/sql-server-r-services-performance-tuning.md).

## <a name="next-lesson"></a>Следующее занятие

На следующем шаге вы узнаете о том, как применять функции R к данным SQL Server.

[С помощью функций R с данными SQL Server](../../advanced-analytics/tutorials/rtsql-using-r-functions-with-sql-server-data.md)
