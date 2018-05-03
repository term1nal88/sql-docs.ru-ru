---
title: Что такое блокировки? | Документы Майкрософт
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c28c8b420b6ed8662d503c55594a85ef8d2c98ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="what-is-a-lock"></a>Что такое блокировки?
Блокировка — это процесс, с помощью которого СУБД ограничивает доступ к строке в многопользовательской среде. При режиме монопольной блокировки строки или столбца, другим пользователям не разрешается доступ к заблокированным данным, пока блокировка снимается. Это гарантирует, что два пользователя не может одновременно обновить же столбец в строке.  
  
 Блокировки могут быть очень затратным с точки зрения ресурсов и должны использоваться только при необходимости для сохранения целостности данных. В базе данных, где сотен или тысяч пользователей может быть попытка доступа к записи каждую секунду — например базы данных, подключенной к Интернету — ненужные блокировки быстро может привести к снижению производительности приложения.  
  
 Можно управлять как источник данных и библиотеку курсоров ADO управлять параллелизмом, выбрав соответствующий параметр блокировки.  
  
 Задать **LockType** свойство перед открытием **записей** для указания, какой поставщик блокировки следует использовать при его открытии. Прочесть свойство для возврата типа блокировки используется открытый **записей** объекта.  
  
 Поставщики могут не поддерживать все типы блокировок. Если поставщик не поддерживает запрошенный **LockType** задание, он заменит другой тип блокировки. Чтобы определить фактический блокировки функциональные возможности, доступные в **записей** , используйте [поддерживает](../../../ado/reference/ado-api/supports-method.md) метод с **adUpdate** и **adUpdateBatch**.  
  
 **AdLockPessimistic** параметр не поддерживается, если [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) свойству **adUseClient.** Если задано недопустимое значение, ошибка не приведет к; ближайшее поддерживается **LockType** вместо него будет использоваться.  
  
 **LockType** свойство доступно для чтения/записи при **записей** — закрытые и только для чтения при открытом.  
  
 Этот раздел содержит следующие подразделы.  
  
-   [Типы блокировок](../../../ado/guide/data/types-of-locks.md)