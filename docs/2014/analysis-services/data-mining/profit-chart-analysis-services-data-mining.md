---
title: Диаграмма роста прибыли (службы Analysis Services — Интеллектуальный анализ данных) | Документация Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- accuracy, charting
- revenue, estimating
- benefits, estimating
- charts [Analysis Services]
- profit charts [Analysis Services]
ms.assetid: 760ee051-6fd8-48e3-8d2e-82db3ab45e45
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 898f0d6fe8dacfb2ec2a8148297d7bd5c0eeb949
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239934"
---
# <a name="profit-chart-analysis-services---data-mining"></a>Диаграмма роста прибыли (службы Analysis Services — интеллектуальный анализ данных)
  В диаграмме роста прибыли отображается теоретический прирост прибыли, связанный с использованием модели интеллектуального анализа данных. Предположим, что модель прогнозирует, с какими клиентами компании следует связаться в определенном бизнес-сценарии. В этом случае следует добавить в диаграмму роста прибыли данные о стоимости проведения кампании целевой рассылки. И тогда в готовой диаграмме вы увидите сравнение прибыли при правильном выборе целевых клиентов и при обращении к клиентам случайным образом.  
  
## <a name="build-a-profit-chart"></a>Создание диаграммы роста прибыли  
 Диаграмма роста прибыли аналогична диаграмме точности прогнозов. Начните с создания диаграммы точности прогнозов, а затем добавьте сведения об издержках и прибыли.  
  
 Чтобы построить диаграмму роста прибыли, у вас должна быть существующая модель.  
  
 В этом примере мы использовали модель дерева принятия решений по целевой рассылке. Модель выделяет тех клиентов, которые, скорее всего, купят велосипед. **Диаграмма роста прибыли** позволит определить, сколько нужно отобрать клиентов для обращений, чтобы получить максимальную прибыль.  
  
 Если у вас нет образца модели, можно создать его с помощью [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md).  
  
1.  Откройте средство построения диаграммы точности интеллектуального анализа.  
  
    -   В SQL Server Management Studio щелкните правой кнопкой мыши имя модели и выберите **Просмотр диаграммы точности прогнозов**.  
  
    -   В SQL Server Data Tools откройте проект, в котором создана эта модель, и щелкните вкладку **Диаграмма точности интеллектуального анализа** .  
  
2.  На вкладке **Выбор входа** выберите модель и прогнозируемое значение атрибута.  
  
     В данном конкретном случае вас интересует только рентабельность точного прогнозирования одного значения: [Bike Buyer] =1.  
  
     Но бывают ситуации, в которых не менее важно правильно прогнозировать ложные значения. Например, получение ложных положительных заключений при медицинской диагностике может повлечь существенные расходы. При прогнозной оценке прибыльности нужно учесть этот вариант, а также стоимость ложных отрицательных результатов. В таких сценариях следует оценивать все возможные исходы.  
  
3.  Выберите набор данных для проверки. В нашем примере выберите тестовый набор данных.  
  
4.  Затем щелкните вкладку **Диаграмма точности прогнозов** .  
  
     Диаграмма точности прогнозов создается автоматически.  
  
5.  Чтобы преобразовать ее в диаграмму роста прибыли, выберите пункт **Диаграмма роста прибыли** в списке **Тип диаграммы** .  
  
6.  Как только вы выберете диаграмму роста прибыли, автоматически откроется диалоговое окно **Настройка диаграммы роста прибыли** .  
  
     Это диалоговое окно помогает указать издержки и прибыль, связанные с кампанией целевой рассылки. Для диаграммы в этом примере были использованы следующие значения.  
  
    |Настройка|Значение|Комментарии|  
    |-------------|-----------|--------------|  
    |**Заполнение**|20 000|Установите значение для всей целевой популяции<br /><br /> База данных может содержать много заказчиков, но чтобы сэкономить на рассылке, выберите только 20 000 заказчиков, которых модель определяет как наиболее вероятных покупателей. Такой список можно получить, выполнив прогнозирующий запрос с сортировкой по значению вероятности из прогнозирующей модели.|  
    |**Фиксированные издержки**|500|Введите единовременные затраты по организации кампании целевой рассылки, рассчитанной на 20 000 человек. Сюда относятся расходы на печать или расходы на рассылку электронных писем.|  
    |**Индивидуальные издержки**|3|Введите удельные затраты для кампании целевой рассылки.<br /><br /> Эта сумма будет умножена на 20 000 или меньшее число, в зависимости от количества клиентов, которых модель оценит как возможных покупателей.|  
    |**Доход на единицу**|400|Введите значение, представляющее объем прибыли или дохода, который можно ожидать при удачном исходе. В нашем случае мы предположим, что рассылка каталога позволит продать велосипеды или аксессуары на среднюю сумму 400 долларов.<br /><br /> Эта сумма будет использоваться для проектирования общей прибыли, связанной с весьма вероятными вариантами.|  
  
7.  Когда будут готовы все нужные параметры, нажмите кнопку **ОК**.  
  
8.  Диаграмма обновится и покажет кривую прибыли.  
  
## <a name="understanding-the-profit-chart"></a>Основные сведения о диаграмме роста прибыли  
 На следующей диаграмме показана диаграмма, которая была основана на этих параметрах. Ось Y на диаграмме представляет прибыль, а ось X — количество клиентов, с которыми связалась компания, в процентах от общего количества.  
  
 Как видите, диаграмма роста прибыли может сравнивать разные модели, если они прогнозируют один и тот же дискретный атрибут.  
  
 ![Сравнение моделей три диаграммы роста прибыли](../media/dm14-profitchartupdated.gif "сравнение моделей три диаграммы роста прибыли")  
  
 Обратите внимание на серую вертикальную линию на диаграмме. Если щелкнуть и перетащить эту линию, появится всплывающая подсказка с указанием процента целевой аудитории, соответствующего этой точке кривой.  
  
 Когда вы перемещаете линию, окно **Обозначения интеллектуального анализа данных** также обновляется, отображая процентное отношение, оценку прибыли и вероятность прогноза, связанную с процентной долей целевой аудитории на серой вертикальной линии.  
  
 Например, если по этой модели вы определяете, кому отправлять свои рекламные материалы, на основании прогноза вероятности вы можете выбрать 25 % целевой аудитории. При этом площадь под кривой прибыли будет максимальной в диапазоне от 40 % до 70 %. Это означает, что вы можете увеличить прибыль, включив в рассылку большее количество людей, несмотря на снижение процента откликнувшихся.  
  
## <a name="saving-charts"></a>Сохранение диаграмм  
 При создании диаграммы точности прогнозов или диаграммы роста прибыли никакие объекты на сервере не создаются. Выполняются только запросы к существующей модели, результаты которых отображаются в средстве просмотра. Если требуется сохранить результаты, следует скопировать диаграмму или результаты в Excel или другой файл.  
  
## <a name="related-content"></a>См. также  
 Следующие разделы содержат дополнительные сведения о том, как создавать и использовать диаграммы точности.  
  
|Подраздел|Ссылки|  
|------------|-----------|  
|Объясняет, как создать диаграмму точности прогнозов для модели целевой рассылки.|[Учебник по основам интеллектуального анализа данных](../../tutorials/basic-data-mining-tutorial.md)<br /><br /> [Проверка точности при помощи диаграммы точности прогнозов &#40;учебник интеллектуального анализа данных&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)|  
|Объясняет типы соответствующих диаграмм.|[Диаграмма точности прогнозов &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [Матрица классификации &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](classification-matrix-analysis-services-data-mining.md)<br /><br /> [Точечная диаграмма &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](scatter-plot-analysis-services-data-mining.md)|  
|Описывает перекрестную проверку для моделей интеллектуального анализа данных и структур интеллектуального анализа данных.|[Перекрестная проверка &#40;службы Analysis Services — Интеллектуальный анализ данных&#41;](cross-validation-analysis-services-data-mining.md)|  
|Описывает шаги для создания диаграммы точности прогнозов и других диаграмм точности.|[Тестирование и проверка задачи и инструкции по &#40;интеллектуального анализа данных&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>См. также  
 [Тестирование и проверка &#40;интеллектуального анализа данных&#41;](testing-and-validation-data-mining.md)   
 [Проверка точности при помощи диаграммы точности прогнозов &#40;учебник интеллектуального анализа данных&#41;](../../tutorials/testing-accuracy-with-lift-charts-basic-data-mining-tutorial.md)  
  
  