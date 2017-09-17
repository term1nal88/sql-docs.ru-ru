---
title: "Создание управляемой данными подписки (учебник по службам SSRS) | Документы Microsoft"
ms.custom: 
ms.date: 05/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
caps.latest.revision: 50
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7ca542c75d289b79284c5affeea5095ac032e1e0
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>Создание управляемой данными подписки (учебник по службам SSRS)
В этом учебнике по [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] рассматриваются концепции управляемых данными подписок на основе простого примера, в котором создается управляемая данными подписка для создания и сохранения отфильтрованных выходных данных отчета в общую папку. 
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Управляемые данными подписки позволяют настраивать и автоматизировать распространение отчета на основе динамических данных подписчиков. Управляемые данными подписки предназначены для следующих типов сценариев:  
  
-   Распространение отчетов среди большого числа получателей, чье членство может меняться от одного цикла распространения к следующему. Например, рассылка ежемесячного отчета всем текущим заказчикам по электронной почте.  
  
-   Распространение отчета среди определенной группы получателей на основании предопределенного критерия. Например, отправка отчета об эффективности продаж всем менеджерам в организации.
+ Автоматизация создания отчетов в различных форматах, например XLSX и PDF.  
  
## <a name="what-you-will-learn"></a>Обзор учебника  
 Учебник разделен на три занятия.  
 Занятие | Комментарии
 ------- | --------------
 [Занятие 1. Создание образца базы данных подписчика](../reporting-services/lesson-1-creating-a-sample-subscriber-database.md) | На этом занятии создается локальная табличная база данных [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , в которой содержатся сведения о подписчике. Сведения о номерах заказов, используемые для фильтрации и вывода форматов файлов.
[Занятие 2. Настройка свойств источника данных отчета](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md) |На этом занятии настраивается источник данных отчета для обеспечения автоматического выполнения отчета по расписанию. Для обеспечения автоматического выполнения необходимы сохраненные учетные данные. Вы также измените набор данных отчета, включив в него параметр, значение которого берется из данных подписчика. Этот параметр используется для фильтрации данных отчета на основе номера заказа.
 [Занятие 3. Определение управляемой данными подписки](../reporting-services/lesson-3-defining-a-data-driven-subscription.md) | На этом занятии создается управляемая данными подписка. На этом занятии будет подробно разобрана каждая страница в мастере управляемой данными подписки.

 На приведенной ниже схеме иллюстрируется базовый рабочей процесс, описываемый в учебнике.

Шаг  |Description 
---------|---------
(1)     |  В конфигурации подписки указываются исходный отчет, расписание и сопоставление полей с базой данных подписчиков.        
(2)     | Таблица OrderInfo содержит 4 номера заказа для фильтрации (по одному на файл). Таблица также содержит форматы файлов для создаваемых отчетов.
(3)     | Сведения из базы данных Adventureworks фильтруются и возвращаются в отчете. 
(4)     | Отчеты создаются в форматах файлов, указанных в таблице Orderinfo.

 
 
   ![ssrs_tutorial_datadriven_flow](../reporting-services/media/ssrs-tutorial-datadriven-flow.png) 
  
## <a name="requirements"></a>Требования  
Управляемые данными подписки обычно создаются и поддерживаются администраторами сервера отчетов. Для создания управляемых данными подписок требуется опыт в построении запросов, знание источников данных, которые содержат данные подписчиков, а также повышенные разрешения на доступ к серверу отчетов.  
  
В этом учебнике используется отчет *Заказ на продажу* , созданный при работе с учебником [Создание простого табличного отчета (учебник по службам SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) , и данные из образца базы данных **AdventureWorks2014**.  
  
Чтобы использовать этот учебник, в операционной системе компьютера должны присутствовать следующие компоненты:  
  
-   Выпуск [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , поддерживающий управляемые данными подписки. Дополнительные сведения см. в статье [Выпуски и компоненты SQL Server 2016](../sql-server/editions-and-components-of-sql-server-2016.md).  
  
-   Сервер отчетов должен работать в собственном режиме. Пользовательский интерфейс, описанный в этом учебнике, основан на сервере отчетов, работающем в собственном режиме. Подписки поддерживаются сервером отчетов, работающим в режиме интеграции с SharePoint, но в этом случае пользовательский интерфейс будет отличаться от описанного в этом учебнике.  
  
-   Должна быть запущена служба агента SQL Server.  
  
-   Отчет, который включает параметры. В этом учебнике используется образец отчета `Sales Orders` , созданный при работе с учебником [Создание простого табличного отчета (учебник по службам SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  
  
-   Образец базы данных **AdventureWorks2014** , который предоставляет данные для образца отчета.  
  
-   Назначение ролей [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] , которое включает задачу "Управление всеми подписками" для образца отчета. Эта задача обязательна для определения управляемой данными подписки. Если пользователь является администратором компьютера, назначение ролей по умолчанию для локальных администраторов предоставляет разрешения, необходимые для создания управляемых данными подписок. Дополнительные сведения см. в статье [Granting Permissions on a Native Mode Report Server](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).  
  
-   Общая папка, на которую имеется разрешение на запись. Общая папка должна быть доступна через сетевое подключение.  
  
**Предполагаемое время для выполнения заданий учебника:** 30 минут. И еще 30 минут, если вы еще не прошли учебник по созданию простого отчета.  
  
## <a name="see-also"></a>См. также:  
[Data-Driven Subscriptions](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[Создание простого табличного отчета (учебник по службам SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)
 

