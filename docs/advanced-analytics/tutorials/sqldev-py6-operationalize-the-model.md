---
title: Ввод в эксплуатацию модели Python, с помощью SQL Server | Документация Майкрософт
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d95edb081edc0f18a3734025a5902d13f8e9a295
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806814"
---
# <a name="operationalize-the-python-model-using-sql-server"></a>Ввод в эксплуатацию модели Python, с помощью SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Эта статья входит учебник по, [Python в базе данных аналитики для разработчиков SQL](sqldev-in-database-python-for-sql-developers.md). 

На этом шаге вы узнаете, как *ввод в эксплуатацию* моделей, обученных и сохраненные на предыдущем шаге.

В этом сценарии ввода в эксплуатацию означает, что развертывание модели в рабочей среде для оценки. Интеграция с SQL Server делает это довольно просто, так как код Python, его можно внедрить в хранимой процедуре. Чтобы получить прогнозы из модели, основанной на новых входных данных, вызовите хранимую процедуру из приложения и передачи новых данных.

На этом занятии рассматривается два метода для создания прогнозов на основе модели Python: пакетной оценки и оценки по строкам.

- **Пакетная оценка:** чтобы предоставить несколько строк входных данных, передать запрос SELECT в качестве аргумента хранимой процедуры. Результатом является таблица наблюдений, соответствующую входным вариантам.
- **Отдельные оценки:** передать набор отдельных значений параметров в качестве входных данных.  Хранимая процедура возвращает одну строку или значение.

Весь код Python, необходимые для оценки предоставляется как часть хранимой процедуры.

| Имя хранимой процедуры | Пакет или один | Источник модели|
|----|----|----|
|PredictTipRxPy|пакет (1)| revoscalepy модели|
|PredictTipSciKitPy|пакет (1) |scikit-Дополнительные сведения о модели|
|PredictTipSingleModeRxPy|одна строка| revoscalepy модели|
|PredictTipSingleModeSciKitPy|одна строка| scikit-Дополнительные сведения о модели|

## <a name="batch-scoring"></a>Пакетная оценка

Первые две хранимые процедуры иллюстрируют базовый синтаксис для заключения вызова прогноза Python в хранимой процедуре. Обе хранимые процедуры требуют таблицу данных в качестве входных данных.

- Имя точные модели для использования предоставляется как входной параметр хранимой процедуры. Хранимая процедура загружает сериализованную модель из таблицы базы данных `nyc_taxi_models`.table, с помощью инструкции SELECT в хранимой процедуре.
- Сериализованную модель хранится в переменной Python `mod` для дальнейшей обработки с помощью Python.
- Новые варианты, которые нужно оценить получаются из [!INCLUDE[tsql](../../includes/tsql-md.md)] запрос, указанный в `@input_data_1`. По мере считывания данных запроса строки сохраняются в кадре данных по умолчанию `InputDataSet`.
- Оба хранимой процедуры использовать функции из `sklearn` для вычисления метрики точности, а AUC (площадь под кривой). Метрики точности, такие как AUC могут создаваться, только если вы предоставите целевой метке ( _tipped_ столбца). Прогнозы не обязательно целевой метке (переменной `y`), в отличие от вычисления метрик точности.

    Таким образом, если у вас нет целевой метки для данных для оценки, можно изменить хранимую процедуру для удаления вычисления AUC и возвращать только вероятности совет функций от вредоносных программ (переменная `X` в хранимой процедуре).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

Хранимая процедура должна уже были созданы для вас. Если не удается найти его, выполните следующие инструкции T-SQL для создания хранимых процедур.

Эта хранимая процедура требует модель, основанная на scikit-Узнайте пакета, так как оно использует функции, относящиеся к этого пакета:

+ Передаваемые данные рамку, содержащую входные данные `predict_proba` функция модели логистической регрессии, `mod`. `predict_proba` Функция (`probArray = mod.predict_proba(X)`) возвращает **float** , представляет вероятность того, что получит чаевые (для любой суммы).

```SQL
CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
  EXEC sp_execute_external_script
    @language = N'Python',
    @script = N'
        import pickle;
        import numpy;
        from sklearn import metrics
        
        mod = pickle.loads(lmodel2)
        
        X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
        y = numpy.ravel(InputDataSet[["tipped"]])
        
        probArray = mod.predict_proba(X)
        probList = []
        for i in range(len(probArray)):
          probList.append((probArray[i])[1])
        
        probArray = numpy.asarray(probList)
        fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
        aucResult = metrics.auc(fpr, tpr)
        print ("AUC on testing data is: " + str(aucResult))
        
        OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
        ',  
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttiprxpy"></a>PredictTipRxPy

Эта хранимая процедура использует такие входные и создает тот же тип оценки как предыдущих хранимой процедуры, но использует функции из **revoscalepy** указан с помощью машинного обучения SQL Server пакет.

> [!NOTE] 
> Код для этой хранимой процедуры немного изменилась между ранние версии выпуска и RTM-версии, чтобы отразить изменения в пакете revoscalepy. См. в разделе [изменения](#changes) таблице за сведениями.

```SQL
CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);

  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict(mod, X)
      prob_list = prob_array["tipped_Pred"].values 
      
      probArray = numpy.asarray(probList)
      fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
      aucResult = metrics.auc(fpr, tpr)
      print ("AUC on testing data is: " + str(aucResult))
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',    
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="run-batch-scoring-using-a-select-query"></a>Запустить пакетную оценку, используя запрос SELECT

Хранимые процедуры **PredictTipSciKitPy** и **PredictTipRxPy** требуют два входных параметра: 

- Запрос, который извлекает данные для оценки
- Имя обученной модели

Передавая эти аргументы в хранимую процедуру, можно выбрать конкретной модели или изменить данные, используемые для оценки.

1. Чтобы использовать **scikit-Узнайте** модель для оценки, вызовите хранимую процедуру **PredictTipSciKitPy**, передав имя модели и строку запроса в качестве входных данных.

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    Хранимая процедура возвращает прогнозируемые значения вероятности для каждой поездки, который был передан в составе входного запроса. 
    
    Если вы используете SSMS (SQL Server Management Studio) для выполнения запросов, вероятности будет отображаться в виде таблицы **результаты** области. **Сообщений** области выводит метрики точности (AUC или площадь под кривой) со значением около 0.56.

2. Чтобы использовать **revoscalepy** модель для оценки, вызовите хранимую процедуру **PredictTipRxPy**, передав имя модели и строку запроса в качестве входных данных.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Оценка одной строки

В некоторых случаях вместо пакетной оценки, может потребоваться передать в одном корпусе, извлечение значений из приложения и возвращая один результат на основании этих значений. Например можно настроить Excel лист, веб-приложения или отчет для вызова хранимой процедуры, и передайте ему входные данные, типизированные или выбранные пользователями.

В этом разделе вы узнаете, как создавать отдельные прогнозы путем вызова двух хранимых процедур:

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) предназначен для одной строки оценки с использованием scikit-Дополнительные сведения о модели.
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy) предназначен для оценки одной строки с помощью revoscalepy модели.
+ Если вы еще не еще обучения модели, вернитесь к [шаг 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

Обе модели принимают ряд отдельных значений, таких как зависимости от количества пассажиров, расстояние поездки и т. д. Функции, возвращающие табличные значения, `fnEngineerFeatures`, используемый для преобразования широты и долготы значений из входных данных в новый компонент, расстояние по прямой. [Занятие 4](sqldev-py4-create-data-features-using-t-sql.md) содержит описание этой функции, возвращающие табличные значения.

Обе хранимые процедуры создать оценку на основе модели Python.

> [!NOTE]
> 
> Важно предоставить входные признаки, необходимые для модели Python при вызове хранимой процедуры из внешнего приложения. Чтобы избежать ошибок, может потребоваться приведение или преобразование входных данных с типом данных Python, а также проверка типа и длины данных.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Внимательно изучите код хранимой процедуры, которая выполняет оценку **scikit-Узнайте** модели.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
    @passenger_count,
    @trip_distance,
    @trip_time_in_secs,
    @pickup_latitude,
    @pickup_longitude,
    @dropoff_latitude,
    @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      probList = []
      probList.append((mod.predict_proba(X)[0])[1])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
    ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

Следующая хранимая процедура выполняет оценку **revoscalepy** модели.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures]( 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      from revoscalepy.functions.RxPredict import rx_predict;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict(mod, X)
      
      probList = []
      prob_list = prob_array["tipped_Pred"].values
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="generate-scores-from-models"></a>Формирование оценок из моделей

После создания хранимых процедур, несложно создать оценку, основанную на любой модели. Просто откройте новую **запроса** окна и введите или вставьте параметры для каждого из столбцов признаков. Семь необходимых значений для столбцов характеристик, в порядке:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Для создания прогноза с помощью **revoscalepy** модели, выполните следующую инструкцию:
  
    ```SQL
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Для создания оценки с помощью **scikit-Узнайте** модели, выполните следующую инструкцию:

    ```SQL
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

В результате обе процедуры — вероятность суммы чаевых за поездки такси с указанными параметрами или функции.

### <a name="changes"></a> Изменения

В этом разделе перечислены изменения в код, используемый в этом руководстве. Эти изменения были внесены в соответствии с последней **revoscalepy** версии. Справка по API, см. в разделе [Python функции Справочник по библиотеке](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference).

| Изменить сведения | Примечания|
| ----|----|
| Удалить `import pandas` в все образцы| Теперь загружаются по умолчанию pandas|
| функция `rx_predict_ex` изменено на `rx_predict`| RTM и предварительных версий требуется `rx_predict_ex`|
| функция `rx_logit_ex` изменено на `rx_logit`| RTM и предварительных версий требуется `rx_logit_ex`|
| ` probList.append(probArray._results["tipped_Pred"])` изменено на `prob_list = prob_array["tipped_Pred"].values`| обновления для API|

Если вы установили службы Python, с помощью предварительной версии SQL Server 2017, мы рекомендуем выполнить обновление. Также можно обновить только компоненты Python и R с помощью последней версии сервера машинного обучения. Дополнительные сведения см. в разделе [с помощью привязки, чтобы обновить экземпляр SQL Server,](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="conclusions"></a>Заключение

В этом руководстве вы узнали, как работать с кодом Python, внедренным в хранимые процедуры. Интеграция с [!INCLUDE[tsql](../../includes/tsql-md.md)] значительно упрощает развертывание моделей Python для прогнозирования и включения, повторного обучения моделей в рамках рабочего процесса данных предприятия.

## <a name="previous-step"></a>Предыдущий шаг

[Обучение и сохранение модели Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>См. также

[Расширение Python в SQL Server](../concepts/extension-python.md)
