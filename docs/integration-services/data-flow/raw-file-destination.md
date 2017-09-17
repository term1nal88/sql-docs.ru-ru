---
title: "Необработанный файл назначения | Документы Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.rawfiledest.f1
- sql13.dts.designer.rawfiledestinationconnectionmanager.f1
- sql13.dts.designer.rawfiledestinationcolumns.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: d92f79e7a43f8d8368ec44b33aef7297749eb351
ms.contentlocale: ru-ru
ms.lasthandoff: 08/17/2017

---
# <a name="raw-file-destination"></a>назначение «Необработанный файл»
  Назначение «Необработанный файл» записывает необработанные данные в файл. Так как формат данных является собственным для назначения, данные не требуют перевода и нуждаются лишь в небольшом анализе. Это значит, что назначение «Необработанный файл» может записывать данные быстрее, чем другие назначения, такие как «Неструктурированный файл» или «OLE DB».  
  
 Помимо записи необработанных данных в файл, можно также использовать назначение «Необработанный файл» для создания пустого необработанного файла, содержащего только столбцы (файла только с метаданными), без необходимости запуска пакета. Источник «Необработанный файл» используется для извлечения необработанных данных, записанных ранее одноименным назначением. Также в качестве источника «Необработанный файл» вы можете указать файл, который содержит только метаданные.  
  
 В формате необработанного файла содержатся сведения о сортировке. Назначение «Необработанный файл» сохраняет все сведения о сортировке, включая флаги сравнения для строковых столбцов. Источник «Необработанный файл» считывает и учитывает сведения о сортировке. С помощью расширенного редактора можно настроить источник «Необработанный файл» так, что флаги сортировки в файле не будут учитываться. Дополнительные сведения о флагах сравнения см. в разделе [Comparing String Data](../../integration-services/data-flow/comparing-string-data.md).  
  
 Можно настроить назначение «Необработанный файл» следующим образом.  
  
-   Задайте режим доступа, являющийся либо именем файла, либо переменной, содержащей имя файла, в который записывает данные назначение «Необработанный файл».  
  
-   Укажите, будет ли назначение «Необработанный файл» дозаписывать данные в существующий файл с таким именем или создавать новый файл.  
  
 Назначение «Необработанный файл» часто используется для записи промежуточных результатов частичной обработки данных между запусками пакетов. Хранение необработанных данных означает, что данные можно быстро считать с использованием источника «Необработанный файл», а затем преобразовать перед загрузкой в окончательное назначение. Например, пакет может запускаться несколько раз, каждый раз записывая в файлы необработанные данные. Позднее другой пакет сможет использовать источник «Необработанный файл» для считывания из каждого файла, использовать преобразование «Объединить все» для слияния данных в один набор, а затем применить дополнительные преобразования, окончательно обрабатывающие данные перед загрузкой данных в окончательное назначение, такое как таблица [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Назначение «Необработанный файл» поддерживает данные типа NULL, но не поддерживает данные типа BLOB.  
  
> [!NOTE]  
>  Назначение «Необработанный файл» не использует диспетчер соединений.  
  
 Этот источник имеет один стандартный вход. Вывод ошибок не поддерживается.  
  
## <a name="append-and-new-file-options"></a>Параметры Append и New File  
 Свойство WriteOption включает возможности дозаписи данных в существующий файл или создания нового файла.  
  
 В следующей таблице описаны доступные значения свойства WriteOption.  
  
|Параметр|Description|  
|------------|-----------------|  
|Append|Дозаписывает данные в существующий файл. Метаданные присоединенных данных должны соответствовать формату файла.|  
|Create always|Всегда создает новый файл.|  
|Create once|Создает новый файл. Если файл существует, то работа компонента завершается аварийно.|  
|Truncate and append|Усекает существующий файл и затем записывает данные. Метаданные присоединенных данных должны соответствовать формату файла.|  
  
 Ниже приведены важные вопросы о добавлении данных.  
  
-   Добавление данных в существующий необработанный файл не приводит к повторной сортировке данных.  
  
     Необходимо убедиться, что ключи сортировки остаются в правильном порядке.  
  
-   Добавление данных в существующий необработанный файл не меняет метаданные этого файла (сведения о сортировке).  
  
 Например, пакет считывает данные, отсортированные по ключу продукта (ProductKey, PK). Пакетный поток данных добавляет данные в существующий необработанный файл. При первом запуске пакета будут получены три строки (PK 1000, 1100, 1200). Теперь необработанный файл содержит следующие данные.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
 При втором запуске пакета будут получены две новые строки (PK 1001, 1300). Теперь необработанный файл содержит следующие данные.  
  
-   1000, productA  
  
-   1100, productB  
  
-   1200, productC  
  
-   1001, productD  
  
-   1300, productE  
  
 Новые данные добавляются в конец необработанного файла, и порядок сортируемых ключей (PK) нарушается. Кроме того, операция добавления не меняет метаданные файла (сведения о сортировке). Если файл был считан с использованием источника «Необработанный файл», компонент указывает, что файл все еще сортируется по PK, даже несмотря на то, что данные в файле больше не следуют в правильном порядке.  
  
 Чтобы сохранить сортируемые ключи в правильном порядке после добавления данных, можно разработать пакетный поток данных следующим образом:  
  
1.  Извлечение новых строк с использованием источника A.  
  
2.  Извлечение существующих строк из файла RawFile1 с помощью источника B.  
  
3.  Объединение входных данных из источников A и B с помощью преобразования «Объединить все».  
  
4.  Сортировка по PK.  
  
5.  Запись в файл RawFile2 с использованием назначения «Необработанный файл».  
  
     Файл RawFile1 заблокирован, поскольку из него выполняется чтение в потоке данных.  
  
6.  Замените RawFile1 на RawFile2.  
  
### <a name="using-the-raw-file-destination-in-a-loop"></a>Использование назначения «Необработанный файл» в цикле  
 Если поток данных, использующий назначение «Необработанный файл», является циклом, файл создается один раз, а затем данные дозаписываются в файл по мере повторения цикла. Чтобы добавить данные в файл, формат этих данных должен соответствовать формату существующего файла.  
  
 Чтобы создать файл в первой итерации цикла, а затем в последующих итерациях цикла добавлять в него строки, в процессе разработки необходимо выполнить следующие действия.  
  
1.  Установите для свойства WriteOption значение **CreateOnce** или **CreateAlways**и запустите одну итерацию цикла. Файл будет создан. Это будет гарантией того, что добавляемые метаданные и файл будут соответствовать друг другу.  
  
2.  Сбросьте свойство WriteOption до значения **Append** и установите для свойства ValidateExternalMetadata значение **False**.  
  
 Если используется параметр **TruncateAppend** вместо параметра **Append** , то строки, которые были добавлены в любой предыдущей итерации, будут усечены, и только затем будет добавлена новая строка. Использование параметра **TruncateAppend** также требует, чтобы данные соответствовали формату файла.  
  
## <a name="configuration-of-the-raw-file-destination"></a>Настройка назначения «Необработанный файл»  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Диалоговое окно **Расширенный редактор** содержит свойства, которые можно установить с помощью программных средств. Дополнительные сведения о свойствах, которые вы можете задать в диалоговом окне **Расширенный редактор** или программными средствами, см. в следующих разделах.  
  
-   [Общие свойства](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Пользовательские свойства необработанного файла](../../integration-services/data-flow/raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Связанные задачи  
 Дополнительные сведения о настройке свойств компонента см. в разделе [Установление свойств компонента потока данных](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>См. также  
 Запись в блоге [Необработанные файлы ― это здорово](http://www.sqlservercentral.com/blogs/stratesql/archive/2011/1/1/31-days-of-ssis-_1320_-raw-files-are-awesome-_2800_1_2F00_31_2900_.aspx)на сайте sqlservercentral.com.  
  
## <a name="raw-file-destination-editor-connection-manager-page"></a>Редактор назначения «Необработанный файл» (страница «Диспетчер соединений»)
  Для настройки назначения «Необработанный файл» на запись необработанных данных в файл используйте редактор назначения «Необработанный файл».  
  
 **Выбор действия**  
  
-   [Открытие редактора назначения «Необработанный файл»](#open)  
  
-   [Задание параметров на вкладке «Диспетчер соединений»](#connection)  
  
-   [Задание параметров на вкладке «Столбцы»](#mapping)  
  
###  <a name="open"></a> Открытие редактора назначения «Необработанный файл»  
  
1.  Добавление назначения «Необработанный файл» в пакет [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Щелкните правой кнопкой мыши компонент и выберите команду **Изменить**.  
  
###  <a name="connection"></a> Задание параметров на вкладке «Диспетчер соединений»  
 **Режим доступа**  
 Выберите порядок указания имени файла. Выберите пункт **Имя файла** , чтобы ввести имя файла и путь непосредственно, или пункт **Имя файла из переменной** , чтобы указать переменную, содержащую имя файла.  
  
 **Имя файла** или **Имя переменной**  
 Введите имя необработанного файла и путь к нему или выберите переменную, содержащую имя файла.  
  
 **Параметр записи**  
 Выберите метод, используемый для создания файла и записи в файл.  
  
 **Создание исходного необработанного файла**  
 Нажмите эту кнопку для создания пустого необработанного файла, который содержит только столбцы (файл только с метаданными), без необходимости запуска пакета. Файл содержит столбцы, выбранные на странице **Столбцы** окна **Редактор назначения «Необработанный файл»**. Можно указать источник «Необработанный файл» в файле, который содержит только эти метаданные.  
  
 После нажатия **Создать исходный необработанный файл**появляется окно сообщения. Щелкните **ОК** , чтобы продолжить создание файла. Щелкните **Отмена** , чтобы выбрать другой список столбцов на странице **Столбцы** .  
  
###  <a name="mapping"></a> Задание параметров на вкладке «Столбцы»  
 **Доступные входные столбцы**  
 Выберите один или несколько входных столбцов для записи в необработанный файл.  
  
 **Входной столбец**  
 Входной столбец автоматически добавляется в эту таблицу во время выбора в списке **Доступные входные столбцы**. Также можно выбрать входной столбец непосредственно в этой таблице.  
  
 **Псевдоним вывода**  
 Укажите альтернативное имя для выходного столбца.  
  
## <a name="raw-file-destination-editor-columns-page"></a>Редактор назначения «Строковый файл» (страница «Столбцы»)
  Для настройки назначения «Необработанный файл» на запись необработанных данных в файл используйте редактор назначения «Необработанный файл».  
  
 **Выбор действия**  
  
-   [Открытие редактора назначения «Необработанный файл»](#open)  
  
-   [Задание параметров на вкладке «Диспетчер соединений»](#connection)  
  
-   [Задание параметров на вкладке «Столбцы»](#mapping)  
  
###  <a name="open"></a> Открытие редактора назначения «Необработанный файл»  
  
1.  Добавление назначения «Необработанный файл» в пакет [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] в среде [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Щелкните правой кнопкой мыши компонент и выберите команду **Изменить**.  
  
###  <a name="connection"></a> Задание параметров на вкладке «Диспетчер соединений»  
 **Режим доступа**  
 Выберите порядок указания имени файла. Выберите пункт **Имя файла** , чтобы ввести имя файла и путь непосредственно, или пункт **Имя файла из переменной** , чтобы указать переменную, содержащую имя файла.  
  
 **Имя файла** или **Имя переменной**  
 Введите имя необработанного файла и путь к нему или выберите переменную, содержащую имя файла.  
  
 **Параметр записи**  
 Выберите метод, используемый для создания файла и записи в файл.  
  
 **Создание исходного необработанного файла**  
 Нажмите эту кнопку для создания пустого необработанного файла, который содержит только столбцы (файл только с метаданными), без необходимости запуска пакета. Можно указать источник «Необработанный файл» в файле, который содержит только метаданные.  
  
 После нажатия этой кнопки появляется список столбцов. Можно нажать кнопку «Отмена» и изменить столбцы или нажать кнопку «ОК», чтобы продолжить создание файла.  
  
###  <a name="mapping"></a> Задание параметров на вкладке «Столбцы»  
 **Доступные входные столбцы**  
 Выберите один или несколько входных столбцов для записи в необработанный файл.  
  
 **Входной столбец**  
 Входной столбец автоматически добавляется в эту таблицу во время выбора в списке **Доступные входные столбцы**. Также можно выбрать входной столбец непосредственно в этой таблице.  
  
 **Псевдоним вывода**  
 Укажите альтернативное имя для выходного столбца.  
  
## <a name="see-also"></a>См. также:  
 [Источник «Необработанный файл»](../../integration-services/data-flow/raw-file-source.md)   
 [Поток данных](../../integration-services/data-flow/data-flow.md)  
  
  