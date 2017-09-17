---
title: "MSSQLSERVER_1505 | Документация Майкрософт"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1505 (Database Engine error)
ms.assetid: ef4df75d-0f36-4c8b-b36c-e427f65f91ca
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8383fd472e054f26db78ab8ec28b4a67e81e7f02
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1505"></a>MSSQLSERVER_1505
  
## <a name="details"></a>Сведения  
  
|||  
|-|-|  
|Название продукта|SQL Server|  
|Идентификатор события|1505|  
|Источник события|MSSQLSERVER|  
|Компонент|SQLEngine|  
|Символическое имя|DUP_KEY|  
|Текст сообщения|Выполнение инструкции CREATE UNIQUE INDEX прервано, поскольку обнаружен повторяющийся ключ, относящийся к имени объекта '%.*ls' и имени индекса '%.\*ls'.  Повторяющимся значением ключа является %ls.|  
  
## <a name="explanation"></a>Объяснение  
Эта ошибка происходит при попытке создать уникальный индекс, а указанное повторяющееся значение содержится больше чем в одной строке в таблице. Уникальный индекс создается при создании индекса и указании ключевого слова UNIQUE либо при создании ограничения UNIQUE. Таблица не может содержать какие-либо строки, которые имеют повторяющиеся значения в столбцах, определенных в индексе или ограничении.  
  
Давайте рассмотрим данные в таблице **Employee**:  
  
|LastName|FirstName|Название должности|HireDate|  
|------------|-------------|------------|------------|  
|Уолтерс|Роб|Старший конструктор средств|2004-11-19|  
|Коричневый|Кевин|Специалист по маркетингу|NULL|  
|Коричневый|Джо|Инженер-проектировщик|NULL|  
|Уолтерс|Роб|Конструктор средств|2001-08-09|  
  
Из-за того, что в строках есть повторяющиеся значения, мы не можем создать уникальный индекс по столбцу **LastName** или сочетанию столбцов **LastName**, **FirstName**.  
  
Менее очевидно, что в столбце **HireDate** также может нарушаться уникальность. В целях индексирования значения NULL рассматриваются как равные. Следовательно, нельзя создать уникальный индекс или ограничение, если значения ключа NULL присутствуют больше чем в одной строке. С учетом вышесказанного мы не можем создать уникальный индекс по столбцу **HireDate** или сочетанию столбцов **LastName**, **HireDate**.  
  
В сообщении об ошибке 1505 возвращается первая строка, нарушающая ограничение уникальности. В таблице могут быть другие повторяющиеся строки. Чтобы найти все повторяющиеся строки, выполните запрос к указанной таблице и используйте предложения GROUP BY и HAVING, чтобы получить информацию о повторяющихся строках. Например, следующий запрос возвращает строки таблицы **Employee**, в которых есть повторяющиеся значения имени и фамилии:  
  
SELECT LastName, FirstName, count(*) FROM dbo.Employee GROUP BY LastName, FirstName HAVING count(\*) > 1;  
  
## <a name="user-action"></a>Действие пользователя  
Рассмотрим следующие решения.  
  
-   Добавить или удалить столбцы в определении индекса или ограничения, чтобы создать уникальное сочетание. В предыдущем примере мы можем решить проблему повторения значений, добавив в определение индекса или ограничения столбец **MiddleName**.  
  
-   Выбирайте столбцы, определенные как NOT NULL, при определении столбцов для уникального индекса или ограничения уникальности. При этом исключается возможность возникновения нарушения уникальности, когда больше чем в одной строке содержится значение NULL в значениях ключа.  
  
-   Если дублирование значений является результатом ошибок ввода данных, исправьте данные вручную и затем создайте индекс или ограничение. Дополнительные сведения об удалении повторяющихся строк из таблицы вы найдете в статье базы знаний 139444: [Удаление повторяющихся строк из таблицы в SQL Server](http://support.microsoft.com/kb/139444).  
  
## <a name="see-also"></a>См. также:  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[Создание уникальных индексов](~/relational-databases/indexes/create-unique-indexes.md)  
[Создание ограничений уникальности](~/relational-databases/tables/create-unique-constraints.md)  
  
