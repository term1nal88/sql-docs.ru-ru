---
title: Передача файла или отчета (диспетчер отчетов) | Документы Майкрософт
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bc1a807ed81ffb0b0aa5482d2fe3a09e70eb7908
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116185"
---
# <a name="upload-a-file-or-report-report-manager"></a>Передача файла или отчета (диспетчер отчетов)
  В диспетчере отчетов предусмотрена функция передачи, позволяющая добавлять отчеты, модели и другие файлы к серверу отчетов без публикации этих элементов из клиентского приложения. Файлы, переданные из файловой системы, сохраняются на сервере отчетов как элементы. Способ сохранения зависит от типа передаваемого файла.  
  
-   RDL-файлы сохраняются как отчеты.  
  
-   SMDL-файлы сохраняются как модели отчетов.  
  
-   Все другие файлы, включая файлы общих источников данных (RDS), передаются как ресурсы. Ресурсы не обрабатываются сервером отчетов, но могут быть просмотрены в диспетчере отчетов, если сервер отчетов поддерживает тип MIME файла.  
  
### <a name="to-upload-a-file-or-report"></a>Передача файла или отчета  
  
1.  Запустите [диспетчер отчетов (службы SSRS в собственном режиме)](../report-manager-ssrs-native-mode.md).  
  
2.  В диспетчере отчетов перейдите на страницу **Содержимое** . Перейдите к папке, в которую нужно добавить элемент.  
  
3.  Щелкните **Передать файл**.  
  
4.  Нажмите кнопку **Обзор** для выбора передаваемого файла. Можно выгружать файл определения отчета, изображение, документ и любой другой файл, который нужно сделать доступным на сервере отчетов.  
  
5.  Введите имя нового элемента. Имя элемента может включать пробелы, но не может включать зарезервированные символы: ; ? : \@ & = +, $ / * \< > |.  
  
6.  Если нужно заменить существующий элемент новым, установите флажок **Перезаписывать существующие элементы**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Создание, удаление и изменение общего источника данных &#40;диспетчера отчетов&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Содержимое страницы &#40;диспетчера отчетов&#41;](../contents-page-report-manager.md)   
 [Страница "Передача файла" (диспетчер отчетов)](../upload-file-page-report-manager.md)   
 [Передача файлов в папку](../report-server/upload-files-to-a-folder.md)  
  
  
