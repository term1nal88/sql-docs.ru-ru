---
title: Параметры проекта (база данных Azure SQL) (SybaseToSQL) | Документация Майкрософт
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f26c89839c1ae4ff958aa65d293a1bb18962eb76
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47807922"
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>Параметры проекта (база данных SQL Azure) (SybaseToSQL)
Параметры проекта базы данных SQL Azure позволяют настраивать суффикс базы данных Azure SQL DB для добавляться в диалоговом окне соединения, а также позволяет реализовать механизм пульса в соединении базы данных SQL Azure.  
  
В области базы данных SQL Azure доступна в **параметры проекта** и **параметры проекта по умолчанию** диалоговым окнам.  
  
-   Используйте диалоговое окно параметров проекта, чтобы задать параметры конфигурации для текущего проекта. Для доступа к параметрам базы данных SQL Azure, на **средства** меню, выберите **параметры проекта**, нажмите кнопку **Общие** в нижней части левой панели, а затем выберите  **База данных Azure SQL**.  
  
-   Используйте диалоговое окно Параметры проекта по умолчанию, чтобы задать параметры конфигурации для всех проектов. Для доступа к параметрам базы данных SQL Azure, на **средства** меню, выберите **параметры DefaultProject**, нажмите кнопку **Общие** в нижней части левой панели, а затем выберите **База данных azure SQL**.  
  
## <a name="connectivity"></a>Соединение  
**Интервал подтверждения**  
  
Задает интервал времени, используемый для механизма пульса для поддержки подключения базы данных SQL Azure в "минуты: секунды формат.  
  
**Значение по умолчанию**: "4:45 '  
  
Значение должно быть указано в меня: ss формат (например, "4:45 ' или ' 0:50 ').  
  
**Суффикс сервера базы данных Azure SQL**  
  
Указывает суффикс сервера базы данных SQL Azure  
  
**Значение по умолчанию**: «database.windows.net».  
  
