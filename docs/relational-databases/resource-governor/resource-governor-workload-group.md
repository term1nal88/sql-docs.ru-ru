---
title: "Группа рабочей нагрузки регулятора ресурсов | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, workload group
- workload groups [SQL Server]
- workload groups [SQL Server], overview
ms.assetid: a84c3c3f-55b6-4a30-9c42-13f082d9281e
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f67e0fd5de601ceb4d808f42fa710c02fa23d3d1
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="resource-governor-workload-group"></a>Группа рабочей нагрузки регулятора ресурсов
  В регуляторе ресурсов [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] группа рабочей нагрузки выступает в качестве контейнера для запросов сеансов, имеющих подобные критерии классификации. Рабочая нагрузка обеспечивает статистический мониторинг сеансов и определяет политики для сеансов. Каждая группа рабочей нагрузки находится в пуле ресурсов, который представляет подмножество физических ресурсов экземпляра компонента [!INCLUDE[ssDE](../../includes/ssde-md.md)]. После запуска сеанса классификатор регулятора ресурсов назначает этот сеанс конкретной группе рабочей нагрузки, и этот сеанс должен функционировать с использованием политик, назначенных этой группе рабочей нагрузки, и ресурсов, определенных для пула ресурсов.  
  
## <a name="workload-group-concepts"></a>Основные понятия группы рабочей нагрузки  
 Группа рабочей нагрузки выступает в качестве контейнера для запросов сеансов, которые являются подобными в соответствии с критериями классификации, применяемыми к каждому из запросов. Группа рабочей нагрузки позволяет вести статистический контроль потребления ресурсов и приложения в рамках единообразной политики для всех запросов в группе. Группа определяет политики для ее членов.  
  
> [!NOTE]  
>  Определяемые пользователем группы рабочей нагрузки можно перемещать из одного пула ресурсов в другой.  
  
 В регуляторе ресурсов есть две стандартные группы рабочей нагрузки: внутренняя группа и группа по умолчанию. Пользователь не может изменить ничего из того, что классифицировано как внутренняя группа, но может вести за ней наблюдение. Запросы классифицируются в группу по умолчанию при выполнении следующих условий.  
  
-   Отсутствуют критерии классификации запроса.  
  
-   Предпринимается попытка классифицировать запрос в несуществующую группу.  
  
-   Происходит общий сбой классификации.  
  
 В регуляторе ресурсов предусмотрены инструкции DDL для создания, изменения и удаления групп рабочей нагрузки.  
  
## <a name="workload-group-tasks"></a>Задачи группы рабочей нагрузки  
  
|Описание задачи|Раздел|  
|----------------------|-----------|  
|Описывает, как создать группу рабочей нагрузки.|[Создание группы рабочей нагрузки](../../relational-databases/resource-governor/create-a-workload-group.md)|  
|Описывает, как изменить параметры группы рабочей нагрузки.|[Изменение параметров группы рабочей нагрузки](../../relational-databases/resource-governor/change-workload-group-settings.md)|  
|Описывает, как удалить группу рабочей нагрузки.|[Удаление группы рабочей нагрузки](../../relational-databases/resource-governor/delete-a-workload-group.md)|  
  
## <a name="see-also"></a>См. также:  
 [Регулятор ресурсов](../../relational-databases/resource-governor/resource-governor.md)   
 [Активация регулятора ресурсов](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Пул ресурсов регулятора ресурсов](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Функция-классификатор регулятора ресурсов](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [Настройка регулятора ресурсов с помощью шаблона](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Просмотр свойств регулятора ресурсов](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  