---
title: "Преобразование «Копирование столбца» | Документы Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.copycolumntrans.f1
- sql13.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: d05d290cd9468eb7fd0b208e00a88db76cfae61a
ms.contentlocale: ru-ru
ms.lasthandoff: 08/19/2017

---
# <a name="copy-column-transformation"></a>преобразование «Копирование столбца»
  Преобразование «Копирование столбца» позволяет создавать новые столбцы путем копирования входных столбцов и добавления новых к выходу преобразования. На более поздних этапах потока данных к копиям столбцов могут применяться различные преобразования. Например, преобразование «Копирование столбца» можно использовать для создания копии столбца и дальнейшего перевода символов скопированных данных в верхний регистр с помощью преобразования «Таблица символов» или для статистической обработки нового столбца с помощью преобразования «Агрегатная обработка».  
  
## <a name="configuration-of-the-copy-column-transformation"></a>Настройка преобразования «Копирование столбца»  
 Преобразование «Копирование столбца» настраивается путем определения входных столбцов, которые необходимо скопировать. Можно создать несколько копий столбца или же копии нескольких столбцов в одной операции.  
  
 Это преобразование имеет один вход и один выход. Вывод ошибок не поддерживается.  
  
 Свойства могут устанавливаться через конструктор служб [!INCLUDE[ssIS](../../../includes/ssis-md.md)] или с помощью программных средств.  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Пользовательские свойства преобразований](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Дополнительные сведения о настройке свойств см. в разделе [Установление свойств компонента потока данных](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="copy-column-transformation-editor"></a>редактор преобразования «Копирование столбца»
  Диалоговое окно **Редактор преобразования «Копирование столбцов»** используется для выбора копируемых столбцов и присвоения имен новым выходным столбцам.  
  
> [!NOTE]  
>  При простом копировании всех данных из источника в назначение использовать преобразование «Копирование столбцов» необязательно. В некоторых ситуациях можно напрямую соединить источник с назначением, если преобразование данных не требуется. В некоторых ситуациях часто бывает предпочтительнее использовать мастер импорта и экспорта SQL Server, который создаст пакет. Позже пакет можно расширить и изменить его конфигурацию. Дополнительные сведения см. в разделе [SQL Server Import and Export Wizard](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md).  
  
### <a name="options"></a>Параметры  
 **Доступные входные столбцы**  
 Выберите копируемые столбцы с помощью флажков. Выбранные столбцы добавляются в качестве входных столбцов в таблицу, представленную ниже.  
  
 **Входной столбец**  
 Выберите столбцы для копирования из списка доступных входных столбцов. Выбранные столбцы обозначаются флажками в таблице **Доступные входные столбцы** .  
  
 **Псевдоним вывода**  
 Введите псевдоним для каждого нового выходного столбца. По умолчанию, используется **Копия**и далее имя входного столбца, однако можно выбрать любое уникальное описательное имя.  
  
## <a name="see-also"></a>См. также:  
 [Поток данных](../../../integration-services/data-flow/data-flow.md)   
 [Преобразования служб Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  