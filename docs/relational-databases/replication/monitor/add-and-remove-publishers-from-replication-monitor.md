---
title: "Добавление и удаление издателей в мониторе репликации | Документация Майкрософт"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Replication Monitor, adding and removing Publishers
ms.assetid: fa36c4b4-bfa5-494e-92e3-07a02d7332c3
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ea5906fa0b1afa7a5276dcce4fbef605794af190
ms.contentlocale: ru-ru
ms.lasthandoff: 06/22/2017

---
# <a name="add-and-remove-publishers-from-replication-monitor"></a>Добавление и удаление издателей в мониторе репликации
  Сервер, с которого запускается монитор репликации, автоматически добавляется в монитор, если это издатель. Дополнительные издатели могут быть добавлены в диалоговом окне **Добавление издателя** . После добавления издателя он отображается в группе на левой панели монитора. Группа **Мои издатели** включена в состав по умолчанию, но можно создать новые группы для управления одной или несколькими топологиями репликации. Сведения о запуске монитора репликации см. в [этой статье](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-add-a-sql-server-publisher"></a>Добавление издателя SQL Server  
  
1.  Щелкните правой кнопкой мыши узел **Монитор репликации** или узел группы издателей на левой панели, затем выберите **Добавить издатель**.  
  
2.  В диалоговом окне **Добавление издателя** щелкните **Добавить**, а затем — **Добавить издатель SQL Server**.  
  
3.  В диалоговом окне **Соединение с сервером** введите имя издателя, а затем выберите тип проверки подлинности. Если выбран параметр **Проверка подлинности SQL Server**, введите имя и пароль. Указанные учетные данные сохраняются монитором репликации для последующего использования при соединении с этим сервером. Учетная запись Windows или указанное имя входа в SQL Server должны быть членами предопределенной роли сервера **sysadmin** или предопределенной роли **replmonitor** базы данных в базе данных распространителя.  
  
4.  Нажмите кнопку **Соединить**. Если издатель использует удаленный распространитель, выводится запрос на соединение с распространителем в диалоговом окне **Соединение с сервером** . Указанные учетные данные сохраняются монитором репликации для последующего использования при соединении с этим сервером. Учетная запись Windows или указанное имя входа в SQL Server должны быть членами предопределенной роли сервера **sysadmin** или предопределенной роли **replmonitor** базы данных в базе данных распространителя.  
  
5.  Имена издателя и распространителя отображаются в сетке **Начать наблюдение за следующими издателями** .  
  
6.  Чтобы задать параметры обновления и соединения для издателя, выберите издатель в сетке и измените параметры требуемым образом. Дополнительные сведения об обновлении параметров см. в разделе [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Выберите группу, в которой должен отображаться издатель в мониторе репликации. Чтобы создать группу, щелкните **Создать группу**и введите ее имя группы. Затем выберите группу в списке **Отображать эти издатели в следующей группе** .  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-an-oracle-publisher"></a>Добавление издателя Oracle  
  
1.  Щелкните правой кнопкой мыши узел **Монитор репликации** или узел группы издателей на левой панели, затем выберите **Добавить издатель**.  
  
2.  В диалоговом окне **Добавление издателя** щелкните **Добавить**, а затем — **Добавить издатель Oracle**.  
  
3.  В диалоге **Соединение с сервером** введите имя распространителя [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , связанного с издателем Oracle, а затем выберите тип проверки подлинности. Если выбран параметр **Проверка подлинности SQL Server**, введите имя и пароль. Указанные учетные данные сохраняются монитором репликации для последующего использования при соединении с этим сервером. Учетная запись Windows или указанное имя входа в SQL Server должны быть членами предопределенной роли сервера **sysadmin** или предопределенной роли **replmonitor** базы данных в базе данных распространителя.  
  
4.  Нажмите кнопку **Соединить**.  
  
5.  Имена издателя и распространителя отображаются в сетке **Начать наблюдение за следующими издателями** .  
  
6.  Чтобы задать параметры обновления и соединения для издателя, выберите издатель в сетке и измените параметры требуемым образом. Дополнительные сведения об обновлении параметров см. в разделе [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Выберите группу, в которой должен отображаться издатель в мониторе репликации. Чтобы создать группу, щелкните **Создать группу**и введите ее имя группы. Затем выберите группу в списке **Отображать эти издатели в следующей группе** .  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-one-or-more-publishers-that-use-the-same-distributor"></a>Добавление одного или нескольких издателей, использующих один и тот же распределитель  
  
1.  Щелкните правой кнопкой мыши узел **Монитор репликации** или узел группы издателей на левой панели, затем выберите **Добавить издатель**.  
  
2.  В диалоговом окне **Добавление издателя** щелкните **Добавить**, а затем — **Укажите распространитель и добавьте его издателей**.  
  
3.  В диалоговом окне **Соединение с сервером** введите имя распространителя, а затем выберите тип проверки подлинности. Если выбран параметр **Проверка подлинности SQL Server**, введите имя и пароль. Указанные учетные данные сохраняются монитором репликации для последующего использования при соединении с этим сервером. Учетная запись Windows или указанное имя входа в SQL Server должны быть членами предопределенной роли сервера **sysadmin** или предопределенной роли **replmonitor** базы данных в базе данных распространителя.  
  
4.  Нажмите кнопку **Соединить**.  
  
5.  Имена распространителя и каждого издателя отображаются в сетке **Начать наблюдение за следующими издателями** . Если издатель уже был добавлен в монитор репликации, он не появится в сетке.  
  
6.  Чтобы задать параметры обновления и соединения для издателя, выберите издатель в сетке и измените параметры требуемым образом. Дополнительные сведения об обновлении параметров см. в разделе [Caching, Refresh, and Replication Monitor Performance](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
7.  Выберите группу, в которой должны отображаться издатели в мониторе репликации. Чтобы создать группу, щелкните **Создать группу**и введите ее имя группы. Затем выберите группу в списке **Отображать эти издатели в следующей группе** .  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-modify-settings-for-the-publisher-and-publisher-groups"></a>Изменение настроек для издателя и групп издателей  
  
1.  Щелкните правой кнопкой мыши издателя на левой панели, затем щелкните **Настройки издателя**.  
  
2.  Внесите любые необходимые изменения в диалоговом окне **Настройки издателя** .  
  
    -   Чтобы изменить учетные данные, используемые монитором репликации для подключения к серверу, щелкните **Соединение с издателем** или **Соединение с распространителем**, а затем укажите учетные данные в диалоговом окне **Соединение с сервером** .  
  
    -   Чтобы переместить издателя из группы в группу, выберите издателя в сетке **Начать наблюдение за следующими издателями** , затем выберите новую группу в списке **Отображать эти издатели в следующей группе** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-publisher-from-replication-monitor"></a>Удаление издателя из монитора репликации  
  
1.  Щелкните правой кнопкой издателя на левой панели.  
  
2.  Щелкните **Удалить**.  
  
### <a name="to-add-a-publisher-group-to-replication-monitor"></a>Добавление группы издателей в монитор репликации  
  
1.  Группы издателей можно создавать только при добавлении издателя или изменении настроек издателя. Дополнительные сведения см. в разделах «Как...», в которых описываются процедуры добавления издателя.  
  
### <a name="to-remove-a-publisher-group-from-replication-monitor"></a>Удаление группы издателей из монитора репликации  
  
1.  Переместите всех издателей в другую группу или удалите их из монитора репликации. Дополнительные сведения см. в описании предыдущих процедур в данном разделе.  
  
2.  Щелкните правой кнопкой мыши группу издателей, затем щелкните **Удалить**.  
  
## <a name="see-also"></a>См. также:  
 [Настройка распространения](../../../relational-databases/replication/configure-distribution.md)   
 [Наблюдение за репликацией](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  