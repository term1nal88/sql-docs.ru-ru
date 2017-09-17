---
title: "Изменение пакета развертывания модели | Документы Майкрософт"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6b0fdb7d-83dd-4392-9011-4ae642c471f1
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: a5b5a850ad5f21670776629c4bc85c5d82b587d1
ms.contentlocale: ru-ru
ms.lasthandoff: 09/07/2017

---
# <a name="edit-a-model-deployment-package"></a>Изменение пакета развертывания модели
  В этом разделе описывается развертывание в MDS выбранных частей модели вместо всей модели. Для этого пакет модели MDS необходимо изменить в редакторе пакетов моделей.  
  
 Мастер редактора пакетов моделей позволяет выбирать в модели отдельные сущности, производные иерархии, представления подписок и бизнес-правила, которые будут включены в пакет MDS и впоследствии развернуты. Части модели, развертывать которые не требуется, вы можете оставить невыбранными. При выборе сущности также автоматически выбираются все зависимые объекты в этой сущности.  
  
 С помощью редактора пакетов моделей можно выбирать части модели в файле пакета, созданном либо средством MDSModelDeploy (оно создает файл пакета, включающий объекты и данные), либо мастером развертывания моделей (он создает файл, включающий только структуру модели). После редактирования модели в пакете используйте средство MDSModelDeploy для развертывания объектов и данных или мастер развертывания моделей для развертывания лишь структуры модели.  
  
## <a name="prerequisites"></a>Предварительные требования  
 Чтобы выполнить эту процедуру:  
  
-   необходимо быть администратором модели. Дополнительные сведения см. в статье [Администраторы (службы Master Data Services)](../master-data-services/administrators-master-data-services.md).  
  
-   Должен существовать пакет модели для изменения. Дополнительные сведения см. в разделах [Развертывание моделей (службы Master Data Services)](../master-data-services/deploying-models-master-data-services.md) и [Создание пакета развертывания модели с помощью мастера](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md) или [Создание пакета развертывания модели при помощи MDSModelDeploy](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md).  
  
### <a name="to-edit-a-model-deployment-package"></a>Изменения пакета развертывания модели  
  
1.  В проводнике Windows на сервере MDS перейдите в папку *диск*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration.  
  
2.  Запустите ModelPackageEditor.exe.  
  
3.  В мастере редактора пакетов моделей нажмите кнопку **Обзор**, перейдите к папке, в которой содержатся пакеты, выберите пакет и нажмите кнопку **Открыть**. Нажмите кнопку **Далее**.  
  
4.  Выберите сущности, производные иерархии, представления подписок или бизнес-правила, которые необходимо развернуть. Снимите выбор тех из них, которые не требуется развертывать. Нажмите кнопку **Далее**.  
  
5.  Проверьте список выбранных объектов для развертывания. Чтобы изменить его, нажмите кнопку **Назад** и повторите шаг 4.  
  
6.  Нажмите кнопку **Обзор**, перейдите к папке, в которой следует сохранить частичный пакет, и введите имя файла частичного пакета (с расширением .pkg). Нажмите кнопку **Сохранить**.  
  
7.  Нажмите кнопку **Готово**.  
  
## <a name="next-steps"></a>Следующие шаги  
  
-   [Развертывание пакета развертывания модели с помощью мастера](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)  
  
-   [Развертывание пакета развертывания модели при помощи MDSModelDeploy](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  