---
title: "Публикация базы данных (среда SQL Server Management Studio) | Документация Майкрософт"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98b2914e-7147-40af-ba7d-87253bbe8bf9
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b86537401dc8866f271472e7fa6c1b4eb33d8827
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="publish-a-database-sql-server-management-studio"></a>Публикация базы данных (среда SQL Server Management Studio)
  **Мастер формирования и публикации скриптов** служит для публикации всей базы данных или отдельных ее объектов на поставщике услуг размещения.  
  
> [!NOTE]  
>  Функциональные возможности, использование которых описано в этом разделе, раньше обеспечивал мастер публикации базы данных. В мастер формирования и публикации скриптов также было добавлено средство публикации, а мастер публикации базы данных больше не поддерживается.  
  
## <a name="generate-and-publish-scripts-wizard"></a>Мастер формирования и публикации скриптов  
 Мастер формирования и публикации скриптов можно использовать для публикации базы данных или отдельных ее объектов на поставщике услуг размещения. Поставщик услуг размещения SQL Server представляет собой интерфейс обмена данными для веб-службы. Веб-служба создается с помощью проекта Database Publishing Service в пакете SQL Server Hosting Toolkit на CodePlex. Веб-служба облегчает клиентам поставщика услуг размещения публикацию баз данных с помощью мастера формирования и публикации скриптов. Дополнительные сведения о загрузке пакета SQL Server Hosting Toolkit см. на странице [SQL Server Database Publishing Services](http://go.microsoft.com/fwlink/?LinkId=142025).  
  
 Мастер формирования и публикации скриптов также может использоваться для создания скриптов переноса базы данных.  
  
#### <a name="to-publish-a-database-to-a-web-service"></a>Публикация базы данных на веб-службе  
  
1.  В обозревателе объектов разверните узел **Базы данных**, щелкните правой кнопкой мыши базу данных, выберите пункт **Задачи**, а затем **Формирование и публикация скриптов**. Следуя шагам мастера, создайте скрипт для публикации объектов базы данных.  
  
2.  На странице **Выбор объектов** выберите объекты для публикации в веб-службе размещения.  
  
3.  На странице **Задание параметров скрипта** выберите пункт **Опубликовать в веб-службе**.  
  
    1.  В поле **Поставщик** задайте поставщика для веб-службы. Если настроенный поставщик услуг размещения отсутствует, нажмите кнопку **Управление поставщиками** и в диалоговом окне **Управление поставщиками** настройте поставщика для веб-службы.  
  
    2.  Чтобы задать дополнительные параметры публикации, нажмите кнопку **Дополнительно** в разделе **Опубликовать в веб-службе** .  
  
4.  На странице **Сводка** просмотрите выбранные параметры. Чтобы изменить выбранные параметры, нажмите кнопку **Назад** . Для публикации выделенных объектов нажмите кнопку **Далее** .  
  
5.  На странице **Сохранение или публикация скриптов** можно наблюдать ход выполнения публикации.  
  
## <a name="see-also"></a>См. также:  
 [Формирование скриптов (среда SQL Server Management Studio)](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)   
 [Копирование баз данных на другие серверы](../../relational-databases/databases/copy-databases-to-other-servers.md)  
  
  