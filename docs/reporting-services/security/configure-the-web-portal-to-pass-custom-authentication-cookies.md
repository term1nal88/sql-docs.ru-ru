---
title: "Настройка веб-портал для передачи файлов cookie нестандартной проверки подлинности | Документы Microsoft"
ms.custom: 
ms.date: 04/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- authentication [Reporting Services]
- extensions [Reporting Services], custom security
ms.assetid: 91aeb053-149e-4562-ae4c-a688d0e1b2ba
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0f1131c191fa64c6dc6f2a074a9cd5db7a8b0e1b
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="configure-the-web-portal-to-pass-custom-authentication-cookies"></a>Настройка передачи файлов cookie для пользовательской проверки подлинности на веб-портале

При использовании пользовательского модуля проверки подлинности, следует настроить веб-портал для передачи файлов cookie нестандартной проверки подлинности. В противном случае веб-портал будет передавать только куки-файлов через HTTP-запрос для сервера отчетов. Чтобы передать дополнительные куки-файлы, необходимо изменить файл RSReportServer.Config.

## <a name="modifying-the-rsreportserverconfig-file"></a>Изменение файла RSReportServer.Config

Можно включить [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] передать дополнительные куки-файлов через сервер отчетов путем добавления \< **PassThroughCookies**> элемент параметры веб-портала конфигурации в файле RSReportServer.config. Использование дополнительных куки-файлов удобно в решениях однократной проверки подлинности при входе, когда требуются не только куки-файлы проверки подлинности сервера отчетов, но также куки-файлы от сторонних систем проверки подлинности.

Чтобы включить дополнительные куки-файлы могут передаваться через HTTP-запрос при использовании веб-портале, установите следующие элементы в файле RSReportServer.config:
  
```  
<UI>  
   <CustomAuthenticationUI>  
      ...  
      <PassThroughCookies>  
         <PassThroughCookie>cookiename1</PassThroughCookie>  
         <PassThroughCookie>cookiename2</PassThroughCookie>  
      </PassThroughCookies>  
   </CustomAuthenticationUI>  
      ...  
</UI>  
```  
  
## <a name="see-also"></a>См. также:

[Проверка подлинности с использованием сервера отчетов](../../reporting-services/security/authentication-with-the-report-server.md)   
[Файл конфигурации RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Общие сведения о модулях безопасности](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[Настройка и администрирование сервера отчетов &#40; Собственный режим служб SSRS &#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)  
Дополнительные вопросы? [Повторите форум служб Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)