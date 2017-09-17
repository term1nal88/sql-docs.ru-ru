---
title: "Диспетчер конфигурации (собственный режим) служб Reporting Services | Документы Microsoft"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
- components [Reporting Services], Reporting Services Configuration tool
ms.assetid: 379eab68-7f13-4997-8d64-38810240756e
caps.latest.revision: 49
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ab787456bd3fdbc727ac1727188edd8ab5db0caa
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---

# <a name="reporting-services-configuration-manager-native-mode"></a>Использование диспетчера конфигурации служб Reporting Services (собственный режим)

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

Используйте диспетчер конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] для настройки установленных служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] в собственном режиме. Если сервер отчетов был установлен в режиме «только файлы», то перед использованием сервера необходимо воспользоваться диспетчером конфигурации. Если сервер отчетов устанавливался в режиме по умолчанию, используйте диспетчер настройки для проверки или изменения настроек, заданных во время установки. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] может использоваться для настройки экземпляра локального или удаленного сервера отчетов.

> [!NOTE]
> Начиная с выпуска [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , диспетчер конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] не предназначен для управления серверами отчетов, работающими в режиме интеграции с SharePoint. Управление и настройка режима интеграции с SharePoint осуществляются с использованием центра администрирования SharePoint и скриптов PowerShell.  
  
##  <a name="bkmk_scenarios"></a> Сценарии использования диспетчера конфигурации служб Reporting Services  
 С помощью программы настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] можно выполнять следующие задачи.  
  
-   Настройка учетной записи службы сервера отчетов. Учетная запись службы сервера отчетов изначально настраивается в процессе установки, но может быть изменена с помощью программы настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , если требуется обновить пароль или использовать другую учетную запись.  
  
-   Создание и настройка URL-адресов. Сервер отчетов и [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] являются приложениями [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] , доступ к которым осуществляется через URL-адреса. URL-адрес сервера отчетов обеспечивает доступ к конечным точкам SOAP сервера отчетов. URL-адрес [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] используется, чтобы открыть [!INCLUDE[ssRSWebPortal-Non-Markdown](../../includes/ssrswebportal-non-markdown-md.md)] . Для каждого приложения можно настроить один или несколько URL-адресов.  
  
-   Создание и настройка базы данных сервера отчетов. Сервер отчетов представляет собой сервер без сохранения состояния, которому необходима база данных [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] в качестве внутреннего хранилища. Программу настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] можно использовать для создания базы данных сервера отчетов и настройки соединения с сервером отчетов. Можно также выбрать существующую базу данных сервера отчетов, содержащую нужные данные.  
  
-   Настройка масштабного развертывания в собственном режиме. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] поддерживают топологию развертывания, которая позволяет всем экземплярам сервера отчетов использовать одну и ту же общую базу данных сервера отчетов. В случае масштабного развертывания сервера отчетов используйте программу настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , чтобы подключить каждый сервер отчетов к общей базе данных сервера отчетов.  
  
-   Резервное копирование, восстановление или замена симметричного ключа, используемого для шифрования хранимых строк соединения и учетных данных. Если изменяется учетная запись службы или база данных сервера отчетов перемещается на другой компьютер, необходимо иметь резервную копию симметричного ключа.  
  
-   Настройка учетной записи автоматического выполнения. Эта учетная запись используется для удаленных соединений при запланированных операциях или в случае, если недоступны учетные данные пользователя.  
  
-   Настройка электронной почты сервера отчетов. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] включают модуль доставки электронной почты сервера отчетов, в котором для доставки отчетов или уведомлений об обработке отчетов по электронной почте используется протокол SMTP. С помощью диспетчера конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] можно указать SMTP-сервер или сетевой шлюз, который используется для доставки электронной почты.  
  
 Программа настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] не предназначена для управления содержимым сервера отчетов, включения дополнительных компонентов или предоставления доступа к серверу. Полное развертывание требует также использования [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] включить дополнительные компоненты или изменить значения по умолчанию и веб-портале, чтобы предоставить пользователю доступ к серверу.

##  <a name="bkmk_requirements"></a> Требования

Диспетчер конфигурации работает только с конкретной версией служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Диспетчер конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , который устанавливается вместе с этой версией [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , не может применяться для настройки более ранней версии служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Если на одном компьютере работает нескольких версий служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , для настройки каждого экземпляра должен использоваться диспетчер конфигурации служб Reporting Services, который поставляется с соответствующей версией.  

Для использования диспетчера настройки служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] необходимо иметь следующее.

- Разрешения локального системного администратора на компьютере, размещающем сервер отчетов, который нужно настроить. Для настройки удаленного компьютера необходимы также разрешения администратора локальной системы на этом компьютере.

- Разрешение на создание баз данных в компоненте [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , размещающем базу данных сервера отчетов.

- На каждом настраиваемом сервере отчетов должна быть включена и запущена служба инструментария управления Windows (WMI). Диспетчер конфигурации служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] производит подключение к локальным и удаленным серверам отчетов через поставщик WMI сервера отчетов. Если настраивается удаленный сервер отчетов, на компьютере должен быть разрешен удаленный доступ к инструментарию WMI. Дополнительные сведения о подготовке сервера отчетов для удаленного администрирования см. в разделе [Настройка сервера отчетов для удаленного администрирования](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md).  

- Перед подключением к удаленному экземпляру сервера отчетов для его настройки необходимо обеспечить пропускание удаленных вызовов инструментария управления Windows (WMI) через брандмауэр Windows. Дополнительные сведения см. в разделе [Настройка сервера отчетов для удаленного администрирования](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md) электронной документации по [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Диспетчер конфигурации служб Reporting Services устанавливается автоматически при установке SQL Server Reporting Services.

##  <a name="bkmk_start_configuration_manager"></a> Запуск диспетчера конфигурации служб Reporting Services

1.  Следующий шаг должен соответствовать версии ОС Microsoft Windows.

    - На начальном экране Windows введите **отчетов** и выберите **диспетчер конфигурации служб Reporting Services** в результатах поиска.

    - Нажмите кнопку **Пуск**и последовательно наведите указатель на пункты **Все программы**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]и **Средства настройки**.

         Если необходимо настроить экземпляр сервера отчетов предыдущей версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], откройте соответствующую ей папку установки. Например, укажите [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] вместо [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] , чтобы открыть средства настройки для компонентов сервера [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .

         Выберите **Диспетчер конфигурации служб Reporting Services**.

2. Появится диалоговое окно **Подключение для конфигурации служб Reporting Services** , в котором можно выбрать настраиваемый экземпляр сервера отчетов. Выберите **Подключиться**.

3. В поле **Имя сервера**укажите имя компьютера, на котором установлен экземпляр сервера отчетов. По умолчанию это поле содержит имя локального компьютера, но если необходимо подключиться к серверу отчетов, установленному на другом компьютере, в него можно ввести имя удаленного экземпляра [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

4. Если указан удаленный компьютер, для установления соединения нажмите кнопку **Найти** .

5. В списке **Report Server В спискеstance**выберите экземпляр служб [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , который необходимо настроить. В списке отображаются только экземпляры сервера отчетов для данной версии [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Более ранние версии служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]настраивать нельзя.

6. Выберите **Подключиться**.

## <a name="next-steps"></a>Следующие шаги

[Веб-портал](../../reporting-services/web-portal-ssrs-native-mode.md)   
[Средства служб отчетов](../../reporting-services/tools/reporting-services-tools.md)   
[Настройка подключения к базе данных сервера отчетов](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
[Диспетчер конфигурации SQL Server](../../relational-databases/sql-server-configuration-manager.md)   
[Настройка и администрирование сервера отчетов](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  

Дополнительные вопросы? [Попробуйте задать вопрос на форуме служб Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)