---
title: "Импорт базы знаний из файла .dqs | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
caps.latest.revision: 17
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 17
---
# Импорт базы знаний из файла .dqs
  В этом разделе описывается, как импортировать всю базу знаний из файла данных DQS в службах [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Создайте файл данных путем экспорта существующей базы знаний изнутри [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] приложения (см. [Экспорт базы знаний в файл .dqs](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)).  
  
 Использование файла DQS для экспорта содержания базы знаний и последующего импорта содержимого в другую базу знаний на том же [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] или на другом [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] упрощает процесс создания набора знаний, экономя время и усилия. Это позволяет совместно использовать базу знаний и ее знания, экономя время. Файл DQS будет содержать все сведения базы знаний, включая домены и политику сопоставления, кроме присоединенных ссылочных данных. Будут импортированы опубликованные и неопубликованные данные.  
  
 Файл данных .dqs зашифрован, поэтому его нельзя просмотреть.  
  
 При импорте базы знаний вы можете использовать то же самое имя, если только это имя базы знаний уже не существует в клиентском приложении; в этом случае базу знаний следует переименовать.  
  
##  <a name="BeforeYouBegin"></a> Перед началом  
  
###  <a name="Prerequisites"></a> Предварительные требования  
 Чтобы импортировать базу знаний из файла данных DQS, необходимо предварительно экспортировать базу знаний в файл DQS.  
  
###  <a name="Security"></a> Безопасность  
  
####  <a name="Permissions"></a> Разрешения  
 Для импорта базы знаний из файла DQS необходимо иметь роль dqs_kb_editor или dqs_administrator в базе данных DQS_MAIN.  
  
##  <a name="Import"></a> Импорт базы знаний из файла DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Запустите клиентское приложение DQS](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  На главном экране [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] нажмите кнопку **Создать базу знаний**.  
  
3.  Введите имя для базы знаний.  
  
4.  Нажмите стрелку вниз **Создать базу знаний из**и выберите **Импорт из файла DQS**.  
  
5.  Чтобы **Выбрать файл данных**, нажмите кнопку **Обзор**.  
  
6.  В диалоговом окне **Импорт из файла данных** перейдите к папке, содержащей файл DQS, который надо импортировать, и щелкните имя этого файла. Нажмите кнопку **Открыть**.  
  
7.  Убедитесь, что база знаний и домены правильно отображаются в списке **Домен** .  
  
8.  Выберите действия, которые требуется выполнить, и нажмите кнопку **Создать**.  
  
9. В диалоговом окне **Импорт базы знаний** убедитесь, что строка состояния указывает, что импорт завершен. Нажмите кнопку **ОК**.  
  
10. Завершите задачи обнаружения знаний, управления доменами или политики сопоставления, которые необходимо выполнить, и нажмите кнопку **Готово**.  
  
11. Нажмите кнопку **Опубликовать** , чтобы опубликовать знания в базе знаний, или кнопку **Нет** , чтобы не публиковать.  
  
12. Если вы опубликовали базу знаний, нажмите кнопку **ОК**.  
  
13. На домашней странице служб Data Quality Services убедитесь, что база знаний содержится в списке **Недавние базы знаний**.  
  
##  <a name="FollowUp"></a> Дальнейшие действия. После импорта базы знаний из файла DQS  
 После импорта базы знаний из файла DQS можно добавить набор знаний в базу знаний или использовать базу знаний в проекте очистки или сопоставления данных в зависимости от содержимого базы знаний. Дополнительные сведения см. в разделе [Обнаружение знаний](../data-quality-services/perform-knowledge-discovery.md), [Управление доменом](../data-quality-services/managing-a-domain.md), [Управление составным доменом](../data-quality-services/managing-a-composite-domain.md), [Создание политики сопоставления](../data-quality-services/create-a-matching-policy.md), [очистки данных](../data-quality-services/data-cleansing.md), или [Сопоставление данных](../data-quality-services/data-matching.md).  
  
  