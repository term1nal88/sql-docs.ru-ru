---
title: "Разрешения функциональной области (службы Master Data Services) | Документы Майкрософт"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functional area permissions [Master Data Services], about functional area permissions
- functional area permissions [Master Data Services]
- permissions [Master Data Services], functional areas
ms.assetid: a80b87b3-b904-4cda-8582-0761c2617c57
caps.latest.revision: 10
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 34aa40c2c999709c871fe7b1e283c5d6e30ab1b4
ms.contentlocale: ru-ru
ms.lasthandoff: 09/07/2017

---
# <a name="functional-area-permissions-master-data-services"></a>Разрешения функциональной области (службы Master Data Services)
  Разрешения можно назначать функциональным областям пользовательского интерфейса [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Ниже приведен список функциональных областей.  
  
-   **Обозреватель**  
  
-   **Управление версиями**  
  
-   **Управление интеграцией**  
  
-   **Администрирование системы**  
  
-   **Разрешения пользователей и групп**  
  
-   **Суперпользователь**  
  
 Если предоставляется разрешение на работу в функциональной области, эта область пользовательского интерфейса становится видимой для пользователя или группы.  
  
 Внутри функциональной области **Обозреватель** дополнительные разрешения на объекты модели и члены иерархии определяют, какие данные доступны пользователю. В остальных функциональных областях пользователь должен быть администратором модели, чтобы просматривать или использовать модель. Дополнительные сведения см. в статье [Администраторы (службы Master Data Services)](../master-data-services/administrators-master-data-services.md).  
  
> [!IMPORTANT]  
>  Пользователь с разрешениями суперпользователя получает права администратора для всех моделей, а также все остальные функциональные разрешения.  
  
 Чтобы иметь доступ к **, пользователь или группа должны иметь разрешение хотя бы для одной функциональной области и одной модели на вкладке** Модели [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="see-also"></a>См. также:  
 [Назначение разрешений для функциональной области (службы Master Data Services)](../master-data-services/assign-functional-area-permissions-master-data-services.md)   
 [Разрешения объекта модели (службы Master Data Services)](../master-data-services/model-object-permissions-master-data-services.md)   
 [Разрешения на элементы иерархии (службы Master Data Services)](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Способ определения разрешений (службы Master Data Services)](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  