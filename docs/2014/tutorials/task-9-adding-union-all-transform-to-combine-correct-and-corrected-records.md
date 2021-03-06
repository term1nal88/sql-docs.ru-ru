---
title: 'Задача 9: Добавление объединить все преобразования для объединения верных и исправленных записей | Документация Майкрософт'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 24ba466d-a7d3-49e7-9111-b348399c9e58
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8900b595bcb90eb7ca0712d2b6e7e3010c4a7b24
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48180914"
---
# <a name="task-9-adding-union-all-transform-to-combine-correct-and-corrected-records"></a>Задача 9. Добавление преобразования «Объединить все» для объединения верных и исправленных записей
  В этой задаче в поток данных добавляется преобразование «Объединить все». Преобразование «Объединить все» объединяет несколько входов в один выход. В вашем сценарии это преобразование позволяет объединить верные и исправленные записи в одном потоке.  
  
1.  Перетащите **объединить все** преобразования из **распространенных** раздел **область элементов служб SSIS** для **потока данных** вкладку и поместите его под **Выбор верных и исправленных записей**.  
  
2.  Щелкните правой кнопкой мыши **объединить все** преобразования в **потока данных** , а щелкните **Переименовать**. Тип **объединение верных и исправленных записей**и нажмите клавишу **ввод**.  
  
     ![Объединение правильных и исправленных записей исправленных записей](../../2014/tutorials/media/et-addinguattocombinecacrecords-01.jpg "объединить правильный и исправленных записей")  
  
3.  Подключение **Выбор верных и исправленных записей** для **объединение верных и исправленных записей** в **потока данных** вкладки, используя голубой соединитель. Вы должны увидеть **Выбор входов и выходов** диалоговое окно.  
  
4.  В **ввода вывода** выберите **исправьте** для **вывода** и нажмите кнопку **ОК**.  
  
     ![Входных данных диалоговое окно выбора выходных данных](../../2014/tutorials/media/et-addinguattocombinecacrecords-02.jpg "входных данных диалоговое окно выбора выходных данных")  
  
5.  Переместите соединитель **исправьте** влево, перетащив точку в конце соединителя.  
  
     ![Соединение с правильными для объединения правильных и исправленных](../../2014/tutorials/media/et-addinguattocombinecacrecords-03.jpg "соединение с правильными для объединения правильных и исправленных записей")  
  
6.  При выборе **Выбор верных и исправленных записей** преобразования, вы должны увидеть еще один голубой соединитель. Перетащите этот голубой соединитель на **объединение верных и исправленных записей**.  
  
     ![Соединение с исправленными для объединения правильных и исправленных](../../2014/tutorials/media/et-addinguattocombinecacrecords-04.jpg "соединение с исправленными для объединения правильных и исправленных записей")  
  
7.  Это **соединитель** должен называться **исправлено**. Так как у вас есть только два условия **исправьте** и **исправлено**, и одно условие уже использовалось, **Выбор входов и выходов** диалоговое окно не отображается это время. Если соединители пересекаются, переместите один влево, а другой вправо с помощью перетаскивания.  
  
## <a name="next-step"></a>Следующий шаг  
 [Задача 10. Добавление преобразования "Нечеткое группирование" для обнаружения повторений](../../2014/tutorials/task-10-adding-fuzzy-group-transform-to-identify-duplicates.md)  
  
  
