---
title: "Настройки распространителя | Документация Майкрософт"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.DistributorSettings.f1
helpviewer_keywords:
- Distributor Settings dialog box
ms.assetid: 8276a521-bdd1-4783-bdb6-7ab43499c0ca
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f86500a4461bc2da64c7f3a3d8906bb919b28628
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="distributor-settings"></a>Параметры распространителя
  В диалоговом окне **Настройки распространителя** можно изменить настройки распространителей, добавленных на левую панель монитора репликации.  
  
## <a name="options"></a>Параметры  
 **Соединяться автоматически, когда запускается монитор репликации**  
 Выберите, чтобы разрешить монитору репликации соединяться с распространителем и получать сведения о состоянии.  
  
 **Соединение**  
 Нажмите, чтобы открыть диалоговое окно **Соединение с сервером** . Это позволяет просмотреть и изменить свойства соединения и учетные данные, которые монитор репликации использует для соединения с удаленным распространителем.  
  
 **Автоматически обновлять состояние этого распространителя и его публикаций**  
 Выберите, чтобы разрешить монитору репликации автоматически обновлять сведения о состоянии распространителя. Если выбран этот параметр, то монитор репликации опрашивает сведения о состоянии распространителя с интервалом опроса, заданным параметром **Частота обновления** . Дополнительные сведения об обновлении в мониторе репликации см. в разделе [Caching, Refresh, and Replication Monitor Performance](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Частота обновления**  
 Введите значение (в секундах), указывающее, как часто монитор репликации должен опрашивать распространитель для получения сведений о состоянии. Чем меньше значение, тем чаще происходит опрос. Это может снизить производительность распространителя, если производится наблюдение за большим числом издателей. Рекомендуется протестировать систему для определения подходящего значения. Параметр **Частота обновления** используется также и при включении режима **Автоматическое обновление** в любом окне сведений монитора репликации.  
  
 **Показать все издатели этого распространителя в следующей группе**  
 Выберите группу издателей из списка. Издатель отображается в свой группе в левой панели. Группы являются средством упорядочения издателей и не оказывают влияния на работу репликации.  
  
 **Создать группу**  
 Нажмите эту кнопку для создания новой группы издателей. Группа издателей представляет собой удобный способ упорядочения издателей в мониторе репликации. Группы не оказывают влияние на данные или связи между серверами в топологии репликации.  
  
## <a name="see-also"></a>См. также:  
 [Запуск монитора репликации](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Наблюдение за репликацией](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  