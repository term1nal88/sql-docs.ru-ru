---
title: "Установка диспетчера драйверов | Документы Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
caps.latest.revision: 59
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ca46eb4fbb6203191a7aace3946daad8361b224
ms.contentlocale: ru-ru
ms.lasthandoff: 09/09/2017

---
# <a name="installing-the-driver-manager"></a>Установка диспетчера драйверов
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Этот раздел содержит инструкции по установке диспетчера драйверов unixODBC для использования с Microsoft ODBC Driver 11, 13 или 13.1 for SQL Server в Linux и macOS.  

> [!IMPORTANT]  
> Перед установкой диспетчера драйверов unixODBC удалите с компьютера все установленные пакеты диспетчера драйверов. Установка диспетчера драйверов unixODBC может вызвать сбой существующего диспетчера драйверов.  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-130-and-131"></a>Установка диспетчера драйверов для Microsoft ODBC Driver 13.0 и 13.1
Зависимости диспетчера драйверов автоматически разрешено системой управления пакета при установке 13.0 драйвера Microsoft ODBC или 13.1 for SQL Server в Linux или macOS, следуя инструкциям в разделе [установки драйвера Microsoft ODBC для SQL Server в Linux или macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>Установка диспетчера драйверов для Microsoft ODBC Driver 11 for SQL Server  

(SUSE и только в Red Hat Linux).

**С помощью сценария установки**  
  
> [!IMPORTANT]  
> Эти инструкции относятся к `msodbcsql-11.0.2270.0.tar.gz`, который представляет собой файл установки для Red Hat Linux. При установке предварительной версии для SUSE Linux файл имеет имя `msodbcsql-11.0.2260.0.tar.gz`.  

Порядок установки диспетчера драйверов:  
  
1.  Убедитесь, что у вас есть корневое разрешение.  
  
2.  Перейдите в каталог где [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] загрузки драйвера ODBC поместил файл с именем `msodbcsql-11.0.2270.0.tar.gz`. Убедитесь в наличии файла \*.TAR.GZ, который соответствует вашей версии Linux. Чтобы извлечь файлы, выполните следующую команду: **tar xvzf msodbcsql-11.0.2270.0.tar.gz**.  

3.  Измените `msodbcsql-11.0.2270.0` каталог должен находиться файл с именем `build_dm.sh`. Можно запустить `build_dm.sh` для установки диспетчера драйверов unixODBC.

4.  Чтобы просмотреть список доступных параметров, выполните следующую команду: **./build_dm.sh--справки**.  
  
5.  Когда вы готовы к установке, а ваш компьютер имеет доступ к внешнему узлу по протоколу FTP, выполните следующую команду: **./build_dm.sh**.

Если компьютер не может получить доступ к внешнему узлу по протоколу FTP, получите `unixODBC-2.3.0.tar.gz`. Вы можете получить `unixODBC-2.3.0.tar.gz` из [http://www.unixodbc.org](http://www.unixodbc.org/). Нажмите кнопку **загрузки** ссылку в левой части страницы, чтобы перейти на страницу загрузки. Щелкните соответствующую ссылку для скачивания unixODBC-2.3.0 (не unixODBC-2.3.1). unixODBC-2.3.1 не поддерживается в этом выпуске [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Выполните следующую команду, чтобы начать установки диспетчера драйверов unixODBC: **./build_dm.sh--URL-адрес загрузки = file://unixODBC-2.3.0.tar.gz**.  

6.  Тип **Да** Чтобы приступить к распаковке файлов. Эта часть процесса может занять около 5 минут.  

7.  После завершения выполнения скрипта следуйте инструкциям на экране, чтобы установить диспетчер драйверов unixODBC

Теперь все готово для установки драйвера. В разделе [Установка Microsoft ODBC Driver for SQL Server для Linux и macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) для получения дополнительной информации.  

**Установка вручную**

Если скрипту установки не удалось завершить работу, самостоятельно выполните настройку и сборку подходящего диспетчера драйверов.

1.  Удалите все старые установленные версии unixODBC (например, unixODBC 2.2.11). В Red Hat Enterprise Linux 5 или 6, выполните следующую команду: **yum удалить unixODBC**. В SUSE Linux Enterprise **zypper удалить unixODBC**.  
  
2.  Последовательно выберите пункты [http://www.unixodbc.org](http://www.unixodbc.org/). Нажмите кнопку **загрузки** ссылку в левой части страницы, чтобы перейти на страницу загрузки. Щелкните соответствующую ссылку, чтобы сохранить файл unixODBC-2.3.0.tar.gz на компьютере. UnixODBC-2.3.1 не поддерживается в этом выпуске [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
3.  На компьютере Linux, выполните команду: **tar xvzf unixODBC-2.3.0.tar.gz**.  
  
4.  Перейдите в каталог unixODBC-2.3.0.  
  
5.  В командной строке выполните команду: **CPPFLAGS = "-DSIZEOF_LONG_INT = 8»**.  
  
6.  В командной строке выполните команду: **Экспорт CPPFLAGS**.  
  
7.  В командной строке выполните команду: **«. / настройки--префикса = usr--libdir = / usr/lib64--sysconfdir = и т. д--enable gui = нет — включить драйверы = нет--enable iconv с iconv-char-enc = UTF8 - с iconv-ucode-enc = UTF16LE»**.  
  
8.  В командной строке (выполнив вход в корень) выполните команду: **сделать**.  
  
9. В командной строке (выполнив вход в корень) выполните команду: **сделать установить**.  

Теперь все готово для установки драйвера. В разделе [Установка Microsoft ODBC Driver for SQL Server для Linux и macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) для получения дополнительной информации.  
  
## <a name="see-also"></a>См. также:
[Установка Microsoft ODBC Driver for SQL Server для Linux и macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[Известные проблемы в данной версии драйвера](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Заметки о выпуске](../../../connect/odbc/linux-mac/release-notes.md)
