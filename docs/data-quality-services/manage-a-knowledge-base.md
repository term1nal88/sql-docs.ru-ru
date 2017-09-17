---
title: "Управление базой знаний | Microsoft Docs"
ms.custom: ""
ms.date: "06/04/2013"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Управление базой знаний
  В этом разделе описано, как выполнять функции управления в базе знаний служб [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Вы можете удалить базу знаний, разблокировать ее, отменить работу в ней, переименовать ее и отобразить ее свойства.  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Чтобы управлять базой знаний, база знаний уже должна быть создана и либо опубликована (если ее создал другой пользователь), либо закрыта (если ее создали вы).  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Для открытия базы знаний необходима роль dqs_kb_editor или dqs_administrator в базе данных DQS_MAIN.  
  
##  <a name="Manage"></a> Управление базой знаний  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запустите клиентское приложение DQS](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главной странице [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] нажмите кнопку **Открыть базу знаний**.  
  
3.  Щелкните правой кнопкой мыши базу знаний в таблице баз знаний.  
  
4.  В контекстном меню вы можете выбрать следующее:  
  
    1.  **Откройте**: щелкните, чтобы открыть базу знаний в действии, выбранном в **Выбор действия** области.  
  
    2.  **Разблокировать**: можно разблокировать базу знаний, если вы являетесь пользователем работал над базой знаний на одном из шагов управления доменами, обнаружения знаний или операции политики сопоставления, и закрыли ее. Если вы выгрузите базу знаний, другой пользователь сможет открыть ее и работать с ней. Эта команда недоступна, если база знаний не находится в состоянии деятельности. Дополнительные сведения см. в разделе [Открытие базы знаний](../data-quality-services/open-a-knowledge-base.md).  
  
    3.  **Отменить работу**: щелкните, когда база знаний находится в состоянии с ней, как показано на запись в поле состояния в таблице. Эта команда недоступна, если база знаний не находится в состоянии активности; она также недоступна, если база знаний заблокирована. Дополнительные сведения см. в разделе [Открытие базы знаний](../data-quality-services/open-a-knowledge-base.md).  
  
    4.  **Переименование**: щелкните, чтобы разрешить изменение поля Knowledge Base таблицы в базе знаний, правой кнопкой мыши. Измените имя, затем щелкните эту базу знаний и другую в этом поле, чтобы изменение имени было принято.  
  
    5.  **Удалить**: щелкните, чтобы удалить базу знаний из базы данных DQS_MAIN на [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
    6.  **Свойства**: нажмите эту кнопку для отображения свойств базы данных в только для чтения.  
  
        1.  **Исходная база знаний**: в базе знаний, построен на основе этой базы данных. Водить описание не обязательно.  
  
        2.  **Состояние**: Указывает, является ли база знаний **в работе** и если он находится в конкретном действии управления знаниями, как определено при последнего закрытия. Состояние может быть **в работе**, при базы знаний была открыта в сеансе управления наборами знаний, но не в определенное действие или **в работе** плюс действие управления наборами знаний, в которой база знаний была открыта в сеансе управления наборами знаний и конкретное действие.  
  
        3.  **Блокировки**: **True** Если база знаний заблокирована, **False** неправильное расположение  
  
        4.  **Содержит неопубликованное содержание**: True, если в базе знаний имеется содержание, которое не сохранено путем публикации, значение False, не  
  
        5.  **Кем заблокирована**: имя пользователя, который закрыл базу знаний, заблокировав ее  
  
        6.  **Дата блокировки**: дата, когда заблокирована  
  
        7.  **Кем создано**: имя пользователя, создавшего базы знаний с сетью, он или она принадлежит  
  
        8.  **Дата создания**: Дата создания  
  
##  <a name="FollowUp"></a> Дальнейшие действия: после управления базой знаний  
 После проведения управления базой знаний следующий шаг зависит от того, какое действие вы выполнили с базой знаний:  
  
-   Если вы открыли базу знаний, вы будете продолжать выбранное действие.  
  
-   Если вы разблокировали ее, она будет доступна в указанном состоянии другому пользователю для открытия и работы.  
  
-   Если вы отменили работу с ней, база знаний будет доступна в своем последнем опубликованном состоянии.  
  
-   Если вы переименовали ее, вам придется открыть переименованную базу знаний для работы с ней.  
  
-   Если вы удалили ее, вам придется выбрать другую базу знаний для работы или создать новую базу знаний.  
  
  