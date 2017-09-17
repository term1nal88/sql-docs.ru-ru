---
title: "Обновление учетных данных в источниках данных отчетов с сайта SharePoint | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85652be59a369ff3b571f8858a744962b5b3f619
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="update-credentials-in-report-data-sources-from-a-sharepoint-site"></a>Обновление учетных данных в источниках данных отчетов с сайта SharePoint
  В этом разделе описывается процесс обновления источников данных, встроенных в отчеты, и совместно используемых источников данных, сохраненных в библиотеке документов SharePoint.  
  
 Во многих отчетах могут быть включены источники данных или общие источники данных, настроенные на использование проверки подлинности Windows. В некоторых ситуациях, например при создании предупреждений об изменении данных для отчетов, сохраненных в библиотеку документов SharePoint, необходимо настроить учетные данные источника данных на использование сохраненных учетных данных или на работу без учетных данных.  
  
 Для использования сохраненных учетных данных в отчетах вам может понадобиться создать и использовать новое имя входа SQL Server. Дополнительные сведения см. в разделе [Создание имени входа](../../relational-databases/security/authentication-access/create-a-login.md).  
  
### <a name="to-update-an-embedded-data-source-to-use-stored-credentials"></a>Настройка внедренного источника данных на использование сохраненных учетных данных  
  
1.  Перейдите к библиотеке документов SharePoint, в которой сохранен отчет.  
  
2.  Щелкните значок, чтобы развернуть раскрывающееся меню для отчета, и выберите пункт **Управление источниками данных**.  
  
     Откроется страница «Управление источниками данных».  
  
3.  В столбце **Имя** щелкните источник данных.  
  
4.  Убедитесь, что в поле **Тип соединения** выбран вариант **Пользовательский источник данных** .  
  
     Этот параметр указывает, что источник данных внедрен в отчет.  
  
5.  Оставьте в полях **Тип источника данных** и **Строка подключения** исходные значения, если вам не нужно, чтобы отчет подключался к другому типу источника данных, другому серверу или хранилищу данных.  
  
6.  В поле **Учетные данные**, выберите вариант **Сохраненные учетные данные**. Этот вариант работает, только если источник данных не принимает учетные данные или если учетные данные передаются каким-то другим способом.  
  
     Вариант **Учетные данные не требуются** также можно использовать в определенных обстоятельствах.  
  
     Для некоторых типов источников данных необходимо настроить на сервере отчетов учетную запись автоматического выполнения. Дополнительные сведения см. в подразделе по соответствующему типу источника данных: [Добавление данных из внешних источников данных (службы SSRS)](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) и [Настройка учетной записи автоматического выполнения (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
7.  Введите имя пользователя и пароль.  
  
    -   Если учетная запись является учетной записью пользователя домена Windows, укажите его в следующем формате: \<домена >\\< учетная запись\>, а затем выберите **использовать учетные данные Windows при подключении к источнику данных**.  
  
    -   Если имя пользователя и пароль являются учетными данными базы данных, флажок **Использовать учетные данные Windows при соединении с источником данных**устанавливать не следует. Если сервер базы данных поддерживает олицетворение или делегирование, можно выбрать параметр **Выполнять в контексте этой учетной записи**.  
  
8.  Чтобы проверить возможность соединения для источника данных с использованием новых учетных данных, щелкните **Проверить соединение**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>Настройка общего источника данных на использование сохраненных учетных данных  
  
1.  Перейдите к библиотеке документов SharePoint, в которой сохранен общий источник данных.  
  
2.  Щелкните значок, чтобы развернуть раскрывающееся меню для общего источника данных, и выберите пункт **Редактировать определение источника данных**.  
  
     Откроется страница «Источник данных».  
  
3.  Оставьте в полях **Тип источника данных** и **Строка подключения** исходные значения, если вам не нужно, чтобы общий источник данных подключался к другому типу источника данных, другому серверу или хранилищу данных.  
  
4.  В поле **Учетные данные**, выберите вариант **Сохраненные учетные данные**.  
  
     Вариант **Учетные данные не требуются** также можно использовать в определенных обстоятельствах. Этот вариант работает, только если источник данных не принимает учетные данные или если учетные данные передаются каким-то другим способом.  
  
     Для некоторых типов источников данных необходимо настроить на сервере отчетов учетную запись автоматического выполнения. Дополнительные сведения см. в подразделе по соответствующему типу источника данных: [Добавление данных из внешних источников данных (службы SSRS)](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) и [Настройка учетной записи автоматического выполнения (диспетчер конфигурации служб SSRS)](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
5.  Введите имя пользователя и пароль.  
  
    -   Если учетная запись является учетной записью пользователя домена Windows, укажите его в следующем формате: \<домена >\\< учетная запись\>, а затем выберите **использовать учетные данные Windows при подключении к источнику данных.**  
  
    -   Если имя пользователя и пароль являются учетными данными базы данных, флажок **Использовать учетные данные Windows при соединении с источником данных**устанавливать не следует. Если сервер базы данных поддерживает олицетворение или делегирование, можно выбрать параметр **Выполнять в контексте этой учетной записи**.  
  
6.  Чтобы проверить возможность соединения для источника данных с использованием новых учетных данных, щелкните **Проверить соединение**.  
  
7.  Убедитесь, что установлен флажок «Включить этот источник данных».  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Передать документы в библиотеку SharePoint &#40; Службы Reporting Services в режиме интеграции с SharePoint &#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  