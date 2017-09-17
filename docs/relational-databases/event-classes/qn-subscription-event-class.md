---
title: "Класс событий QN:Subscription | Документация Майкрософт"
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
- event classes [SQL Server], QN:Subscription
ms.assetid: 4916167e-8541-43b4-900e-ec8e6adcbc34
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 974995d2e76e47234003981115e08d10428182dd
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="qnsubscription-event-class"></a>Класс событий QN:Subscription
  Событие QN:Subscription возвращает данные о подписках на уведомления.  
  
## <a name="qnsubscription-event-class-data-columns"></a>Столбцы данных класса событий QN:Subscription  
  
|Столбец данных|Тип|Описание|Номер столбца|Фильтруемый|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|Имя клиентского приложения, установившего соединение с экземпляром [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Этот столбец заполняется значениями, передаваемыми приложением, а не отображаемым именем программы.|10|Да|  
|ClientProcessID|**int**|Идентификатор, присвоенный компьютером сервера процессу, в котором работает клиентское приложение. Этот столбец данных заполняется в том случае, если клиент вводит идентификатор клиентского процесса.|9|Да|  
|DatabaseID|**int**|Идентификатор базы данных, указанной в инструкции USE *database* , или базы данных по умолчанию, если для данного экземпляра инструкция USE *database*не выполнялась. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] отображает имя базы данных, если столбец данных «Имя сервера» захвачен при трассировке и сервер доступен. Определите значение для базы данных, используя функцию DB_ID.|3|Да|  
|DatabaseName|**nvarchar**|Имя базы данных, в которой выполняется инструкция пользователя.|35|Да|  
|EventClass|**int**|Тип события = 199.|27|Нет|  
|EventSequence|**int**|Порядковый номер этого события.|51|Нет|  
|EventSubClass|**nvarchar**|Тип подкласса событий, предоставляющий дополнительные сведения о каждом классе события. Данный столбец может содержать следующие значения.<br /><br /> **Подписка зарегистрирована**. Указывает на то, что подписка на уведомления о запросах успешно зарегистрирована в базе данных.<br /><br /> **Повторная подписка**. Указывает на то, что компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] получает запрос на подписку, которая полностью совпадает с уже существующей подпиской. В таком случае компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] устанавливает значение тайм-аута для существующей подписки, совпадающее со значением тайм-аута, указанным в новом запросе на подписку.<br /><br /> **Подписка запущена**. Указывает на то, что подписка на уведомление создает сообщение уведомления.<br /><br /> **Не удалось произвести подписку из-за ошибки компонента Service Broker**. Указывает на то, что сообщение уведомления не доставлено из-за ошибки компонента [!INCLUDE[ssSB](../../includes/sssb-md.md)] .<br /><br /> **Не удалось произвести подписку, при этом ошибка компонента Service Broker отсутствует**. Указывает на то, что сообщение уведомления не доставлено, но не из-за ошибки компонента [!INCLUDE[ssSB](../../includes/sssb-md.md)] .<br /><br /> **Перехвачена ошибка компонента Service Broker**. Указывает на то, что компонент [!INCLUDE[ssSB](../../includes/sssb-md.md)] передал ошибку в диалоге, который использует уведомление о запросе.<br /><br /> **Попытка удаления подписки**. Указывает на то, что для высвобождения ресурсов компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] пытался удалить подписку с истекшим сроком.<br /><br /> **Не удалось удалить подписку**. Указывает на то, что не удалось удалить подписку с истекшим сроком. Для высвобождения ресурсов компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] автоматически повторно запланирует удаление этой подписки.<br /><br /> **Подписка уничтожена**. Указывает на то, что компонент [!INCLUDE[ssDE](../../includes/ssde-md.md)] удалил подписку с истекшим сроком.|21|Да|  
|GroupID|**int**|Идентификатор группы рабочей нагрузки, в которой запускается событие трассировки SQL.|66|Да|  
|HostName|**nvarchar**|Имя компьютера, на котором выполняется клиентская программа. Заполнение этого столбца данных производится в том случае, если клиент предоставляет имя узла. Чтобы определить имя узла, используйте функцию HOST_NAME.|8|Да|  
|IsSystem|**int**|Указывает, произошло событие в системном или в пользовательском процессе.<br /><br /> 0 = пользовательский процесс<br /><br /> 1 = системный процесс|60|Нет|  
|LoginName|**nvarchar**|Имя входа пользователя (имя входа системы безопасности [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] или учетные данные входа Windows в формате ДОМЕН\имя_пользователя).|11|Нет|  
|LoginSID|**image**|Идентификатор безопасности вошедшего в систему пользователя. Эти сведения можно найти в представлении каталога sys.server_principals. Значение идентификатора безопасности уникально для каждого имени входа на сервере.|41|Да|  
|NTDomainName|**nvarchar**|Домен Windows, к которому принадлежит пользователь.|7|Да|  
|NTUserName|**nvarchar**|Имя пользователя, которому принадлежит соединение, создавшее это событие.|6|Да|  
|RequestID|**int**|Идентификатор запроса, содержащего инструкцию.|49|Да|  
|ServerName|**nvarchar**|Имя экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , подвергаемого трассировке.|26|Нет|  
|SessionLoginName|**nvarchar**|Имя входа пользователя, создавшего сеанс. Например, если приложение соединяется с [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] под именем Имя_входа1, а выполняет инструкции под именем Имя_входа2, то SessionLoginName содержит значение «Имя_входа1», а LoginName содержит значение «Имя_входа2». В этом столбце отображаются как имена входа [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , так и имена входа Windows.|64|Да|  
|SPID|**int**|Идентификатор сеанса, в котором произошло событие.|12|Да|  
|StartTime|**datetime**|Время начала события, если оно известно.|14|Да|  
|TextData|**ntext**|Возвращает XML-документ, содержащий сведения, специфические для этого события. Этот документ соответствует XML-схеме, доступной на странице [Схема событий приложения SQL Server Query Notification Profiler](http://go.microsoft.com/fwlink/?LinkId=63331) .|1|Да|  
  
  