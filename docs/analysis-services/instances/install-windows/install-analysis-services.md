---
title: "Установка служб Analysis Services | Документы Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ba3bacb78e49319db1e458d776cead3429e6c60
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="install-sql-server-analysis-services"></a>Установка SQL Server Analysis Services
  SQL Server Analysis Services является сервер аналитических баз данных, на котором размещена табличных моделей, многомерных кубов и моделей интеллектуального анализа данных, можно получить из отчетов, электронных таблиц и панелей мониторинга.  
  
 Службы Analysis Services имеет несколько экземпляров, это означает, что можно установить несколько копий на одном компьютере или запустить новые и старые версии side-by-side. Все установленные экземпляры работают в одном из трех режимов, определяемых во время установки: многомерный и интеллектуальный анализ данных, а также режим для работы с табличными моделями или моделями SharePoint. Если вы хотите использовать несколько режимов, вам потребуется отдельный экземпляр для каждого из них.  
  
 После установки сервера в определенном режиме вы можете использовать его для размещения решений, поддерживаемых этим режимом. Например, сервер в табличном режиме необходим, если требуется сетевой доступ к данным табличной модели.  
  
## <a name="get-tools-and-designers"></a>Получение средств и конструкторов  
 Программа установки SQL Server больше не устанавливает конструкторы моделей и средства управления, используемые для разработки решений и администрирования сервера. В этом выпуске для средств предусмотрена отдельная установка — см. следующие ссылки:  
  
-   [Скачивание SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)  
  
-   [Скачать SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)  
  
 Вам потребуется среда SSMS и SSDT, для работы с данными и экземплярами служб Analysis Services. Средства можно установить в любом месте, но не забудьте настроить порты на сервере перед подключением. Дополнительные сведения см. в разделе [Configure the Windows Firewall to Allow Analysis Services Access](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) .  
  
## <a name="install-using-a-wizard"></a>Установка с помощью мастера  
 В следующем списке приведены страницы в мастере установки SQL Server, используемые при установке служб Analysis Services.  
  
1.  Выберите **Службы Analysis Services** в дереве компонентов в программе установки.  
  
     ![Дерево компонентов программы установки со службами Analysis Services](../../../analysis-services/instances/install-windows/media/ssas-setupas.gif "дерево компонентов программы установки со службами Analysis Services")  
  
2.  На странице «Конфигурация служб Analysis Services» выберите режим. Значение по умолчанию — в табличном режиме...  
  
     ![Страница установки с параметрами конфигурации служб Analysis Services](../../../analysis-services/instances/install-windows/media/ssas-setupasconfig.png "страница установки с параметрами конфигурации служб Analysis Services")  
  
  Табличный режим использует подсистему аналитики в памяти xVelocity (VertiPaq), которая является хранилищем по умолчанию для табличных моделей. После развертывания табличных моделей на сервере, можно выборочно настроить табличных решениях использование дискового хранилища DirectQuery в качестве альтернативы для хранения с памятью.  
 
 Многомерный и интеллектуальный анализ данных режим использования MOLAP хранения по умолчанию для моделей, развертываемых в службах Analysis Services. После развертывания на сервере вы можете настроить решение для использования ROLAP, если планируете выполнять запросы непосредственно к реляционной базе данных, а не хранить данные запроса в многомерной базе данных служб Analysis Services.  
  

  
 Управление памятью и параметры ввода-вывода можно настраивать, чтобы добиться более высокой производительности при использовании нестандартных режимов хранения. Дополнительные сведения см. в статье [Свойства сервера в службах Analysis Services](../../../analysis-services/server-properties/server-properties-in-analysis-services.md) .  
  
## <a name="command-line-setup"></a>Установка из командной строки  
 В программе установки SQL Server предусмотрен новый параметр (**ASSERVERMODE**), который определяет режим сервера. В приведенном ниже примере показана установка служб Analysis Services в табличном режиме сервера из командной строки.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 Значение**INSTANCENAME** должно иметь длину менее 17 символов.  
  
 Все заполнители значений учетных записей должны быть заменены на действительные учетные записи и пароли.  
  
 Параметр**ASSERVERMODE** учитывает регистр.  Все значения должны задаваться в верхнем регистре. В следующей таблице приведены допустимые значения параметра **ASSERVERMODE**.  
  
|Значение|Описание|  
|-----------|-----------------|  
|TABULAR|Это значение по умолчанию. Если вы не установите **ASSERVERMODE**, сервер будет установлен в табличном режиме.|
|MULTIDIMENSIONAL|Это значение является необязательным.|  
|POWERPIVOT|Это значение является необязательным. На практике, если задан параметр **ROLE** , режим сервера автоматически получает значение 1, что делает **ASSERVERMODE** необязательным в установке [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] для SharePoint. Дополнительные сведения см. в статье [Установка Power Pivot из командной строки](http://msdn.microsoft.com/en-us/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328).|  
  
  
## <a name="see-also"></a>См. также:  
 [Определение режима работы сервера экземпляра служб Analysis Services](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Табличное моделирование (табличные службы SSAS)](https://msdn.microsoft.com/library/hh212945(v=sql.110).aspx)  
  
  
