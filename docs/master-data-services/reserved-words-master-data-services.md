---
title: "Зарезервированные слова (службы Master Data Services) | Документы Майкрософт"
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
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
caps.latest.revision: 11
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: af5326c054f80b376e43db0d18dfeb2b9ef85997
ms.contentlocale: ru-ru
ms.lasthandoff: 09/07/2017

---
# <a name="reserved-words-master-data-services"></a>Зарезервированные слова (службы Master Data Services)
  В [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]при создании элементов и объектов модели нельзя использовать некоторые слова. В противном случае могут возникнуть ошибки.  
  
> [!NOTE]  
>  Кроме того, следует ограничить использование специальных знаков (особых символов, знаков переноса и т. п.).  
  
-   [Модели](../master-data-services/reserved-words-master-data-services.md#models)  
  
-   [Сущности](../master-data-services/reserved-words-master-data-services.md#entities)  
  
-   [Явные иерархии](../master-data-services/reserved-words-master-data-services.md#exhierarchies)  
  
-   [Атрибуты](../master-data-services/reserved-words-master-data-services.md#attributes)  
  
-   [Члены](../master-data-services/reserved-words-master-data-services.md#members)  
  
##  <a name="models"></a> Модели  
 Если модель создается с именем **Name** или **Code**, не выбирайте **Создать сущность с именем модели** , поскольку **Name** или **Code** нельзя использовать в качестве имени сущности.  
  
##  <a name="entities"></a> Сущности  
 В качестве имен сущностей нельзя указывать **Name** и **Code**.  
  
##  <a name="exhierarchies"></a> Явные иерархии  
 В качестве имен явных иерархий нельзя указывать **Name** и **Code**.  
  
##  <a name="attributes"></a> Атрибуты  
  
-   **Идентификатор**  
  
-   **Code**  
  
-   **EnterUserName**  
  
-   **LastChgUserName**  
  
-   **Name**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> Члены  
 Для элементов нельзя использовать **MDMMemberStatus**, **MDMUnused**или **ROOT** в качестве значения атрибута **Code** .  
  
## <a name="see-also"></a>См. также:  
 [Общие сведения о службах Master Data Services (MDS)](../master-data-services/master-data-services-overview-mds.md)  
  
  