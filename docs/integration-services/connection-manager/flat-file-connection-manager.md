---
title: "Flat File Connection Manager | Документы Microsoft"
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
- sql13.dts.designer.ffileconnection.general.f1
- sql13.dts.designer.ffileconnection.columns.f1
- sql13.dts.designer.ffileconnection.columnproperties.f1
- sql13.dts.designer.ffileconnection.preview.f1
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 2b3f4c303b1d60cbbe23c639c36a6336ca07447f
ms.contentlocale: ru-ru
ms.lasthandoff: 08/09/2017

---
# <a name="flat-file-connection-manager"></a>Диспетчер соединений с неструктурированными файлами
  Диспетчер соединений с неструктурированными файлами дает возможность пакету получить доступ к данным неструктурированного файла. Например, исходные и целевые неструктурированные файлы могут использоваться диспетчерами соединений с неструктурированными файлами для извлечения и загрузки данных.  
  
 Диспетчер соединений с неструктурированными файлами получает доступ только к одному файлу. Чтобы ссылаться на несколько файлов, воспользуйтесь диспетчером соединений с несколькими неструктурированными файлами вместо обычного диспетчера соединений с неструктурированными файлами. Дополнительные сведения см. в разделе [Multiple Flat Files Connection Manager](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="column-length"></a>Длина столбца  
 По умолчанию диспетчер соединений с неструктурированными файлами устанавливает длину строки столбцов, равную 50 символам. В диалоговом окне **Редактор диспетчера соединений с неструктурированными файлами** можно оценить образец данных и автоматически изменить длину этих столбцов во избежание обрезки данных или чрезмерной ширины столбцов. Пока не будет изменена длина столбцов в источнике неструктурированного файла или преобразования, длина строки столбца останется неизменной. Если эти строки столбцов сопоставляются с более узкими целевыми столбцами, интерфейс пользователя выдаст предупреждение. Более того, во время выполнения могут появляться ошибки вследствие усечения данных. Во избежание ошибок или усечения можно изменить размер столбцов, чтобы они были совместимы с целевыми столбцами в диспетчере соединений с неструктурированными файлами, в источнике неструктурированного файла или в преобразовании. Чтобы изменить длину выходных столбцов, используйте свойство **Length** выходных столбцов на вкладке **Свойства входов и выходов** диалогового окна **Расширенный редактор** .  
  
 Изменять выходные столбцы в источнике неструктурированного файла вручную нет необходимости, если обновить длину столбцов в диспетчере соединений с неструктурированными файлами после того, как будет добавлен и настроен источник неструктурированного файла, который использует диспетчер соединения. При открытии диалогового окна **Источник «Неструктурированный файл»** источник неструктурированного файла предоставляет параметр для синхронизации метаданных столбца.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>Настройка диспетчера соединения с неструктурированными файлами  
 При добавлении диспетчера соединений с неструктурированными файлами в пакет служба [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] создает диспетчер соединений, который устанавливает соединение с неструктурированными файлами во время выполнения, определяет свойства этого соединения и добавляет диспетчер соединений с неструктурированными файлами в коллекцию **Соединения** пакета.  
  
 Свойству **ConnectionManagerType** диспетчера соединений присваивается значение **FLATFILE**.  
  
 По умолчанию диспетчер соединений с неструктурированными файлами всегда проверяет наличие разделителя строки в данных без кавычек и начинает новую строку при нахождении разделителя строки. Что позволяет диспетчеру соединений правильно анализировать файлы со строками, в которых пропущены поля столбцов.  
  
 В некоторых случаях отключение этой функции может улучшить производительность пакета. Эту функцию вы можете отключить, задав свойству **AlwaysCheckForRowDelimiters**диспетчера соединений с неструктурированными файлами значение **False**.  
  
 Настройте диспетчер соединений с неструктурированными файлами одним из следующих способов.  
  
-   Укажите файл, локаль и используемую кодовую страницу. Локаль используется для интерпретации данных, зависящих от локаля, например дат, а кодовая страница используется для конвертации строковых данных в формат Юникод.  
  
-   Укажите формат файла. Можно использовать форматы с разделителями, фиксированной шириной или без выравнивания по правому краю.  
  
-   Укажите строку заголовка, строку данных и разделители столбцов. Разделители столбцов могут указываться на уровне файла и перезаписываться на уровне столбцов.  
  
-   Определите, будет ли первая строка файла содержать имена столбцов.  
  
-   Укажите символ ограничителя текста. Каждый столбец может быть настроен на распознавание текстового ограничителя.  
  
     Для внедрения символа ограничителя в заданную строку диспетчер подключений к неструктурированным файлам теперь поддерживает использование символа ограничителя. Двойной экземпляр ограничителя текста интерпретируется как литерал, один экземпляр строки ограничителя. Например, если ограничитель текста — одинарная кавычка, а входные данные — 'abc', 'def', 'g'hi', то выходные данные будут иметь вид abc, def, g'hi. Однако экземпляр ограничителя, внедренный в заданную строку, вызывает сбой источника неструктурированного файла с ошибкой DTS_E_PRIMEOUTPUTFAILED.
  
-   Установите свойства, например имя, тип данных и максимальную ширину отдельных столбцов.  
  
 Можно задать свойство ConnectionString для диспетчера соединений с неструктурированными файлами, указывая выражение в окне "Свойства" [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Для предотвращения ошибок проверки выполните следующие действия.  
  
-   Если для указания файла используется выражение, введите путь к файлу в поле **Имя файла** в **редакторе диспетчера соединений с неструктурированными файлами**.  
  
-   Задайте свойство **DelayValidation** в диспетчере соединений с неструктурированными файлами равным **True**.  
  
 Можно использовать выражение для создания имени файла во время выполнения, применяя диспетчер соединений с неструктурированными файлами с назначением «Неструктурированный файл».  
  
 Значения свойств можно задавать с помощью конструктора [!INCLUDE[ssIS](../../includes/ssis-md.md)] или программными средствами.  
  
 Дополнительные сведения о программной настройке диспетчера подключений см. в разделах <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> и [Добавление соединений программным образом](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="flat-file-connection-manager-editor-general-page"></a>Редактор диспетчера соединений с неструктурированными файлами (страница «Общие»)
  Используйте страницу **Общие** диалогового окна **Редактор диспетчера соединений с неструктурированными файлами** , чтобы выбрать файл и формат данных. Соединение с неструктурированным файлом дает пакету возможность установить соединение с текстовым файлом.  
  
 Дополнительные сведения о диспетчере соединений с неструктурированными файлами см. в разделе [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Параметры  
 **Имя диспетчера соединений**  
 Укажите уникальное имя для соединения с неструктурированным файлом в рабочем процессе. Выбранное имя будет отображаться в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Опишите соединение. Рекомендуется описать цель соединения, чтобы пакеты самодокументировались и их проще было обслуживать.  
  
 **Имя файла**  
 Введите путь и имя файла для использования в соединении с неструктурированным файлом.  
  
 **Обзор**  
 Укажите имя файла для использования в соединении с неструктурированным файлом.  
  
 **Локаль**  
 Укажите локаль, чтобы предоставить определяемые языком правила для сортировки данных и формата даты и времени.  
  
 **Юникод**  
 Укажите, следует ли использовать Юникод. При использовании Юникод невозможно указать кодовую страницу.  
  
 **Кодовая страница**  
 Укажите кодовую страницу для текста не в Юникоде.  
  
 **Формат**  
 Укажите, используется ли в файле форматирование с разделителями, с фиксированной шириной столбцов или форматирование без ограничения длины строк.  
  
|Значение|Description|  
|-----------|-----------------|  
|С разделителями|Столбцы отделены друг от друга с помощью разделителей, указанных на странице **Столбцы** .|  
|Фиксированная ширина|Столбцы имеют фиксированную ширину.|  
|Переменная ширина|В файлах с текстом без выравнивания вправо каждый столбец имеет фиксированную ширину, за исключением последнего столбца. Он отделяется разделителем строк.|  
  
 **Ограничитель текста**  
 Укажите ограничитель текста, который следует использовать. Например, можно указать, что текстовые поля должны быть заключены в кавычки.  
  
> [!NOTE]  
>  После выбора ограничителя текста невозможно повторно выбрать параметр **None** . Тип **None** предназначен для отмены выбора ограничителя текста.  
  
 **Разделитель строки заголовка**  
 Выберите разделитель из списка разделителей строк заголовка или введите текст разделителя.  
  
|Значение|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|В качестве разделителей для строки заголовка используются сочетания символов возврата каретки и перевода строки.|  
|**{CR}**|В качестве разделителей для строки заголовка используются символы возврата каретки.|  
|**{LF}**|В качестве разделителей для строки заголовка используются символы перевода строки.|  
|**Точка с запятой {;}**|В качестве разделителя для строки заголовка используется точка с запятой.|  
|**Двоеточие {:}**|В качестве разделителя для строки заголовка используется двоеточие.|  
|**Запятая {,}**|В качестве разделителя для строки заголовка используется запятая.|  
|**Табуляция {t}**|В качестве разделителя для строки заголовка используется символ табуляции.|  
|**Вертикальная черта {&#124;}**|В качестве разделителя для строки заголовка используется вертикальная черта.|  
  
 **Пропускаемые строки заголовка**  
 Укажите количество строк заголовка или строк начальных данных, которые следует пропускать при необходимости.  
  
 **Имена столбцов в первой строке данных**  
 Укажите, ожидать или задать имена столбцов в первой строке данных.  
## <a name="flat-file-connection-manager-editor-columns-page"></a>Редактор диспетчера соединений с неструктурированными файлами (страница «Столбцы»)
  Страница **Столбцы** диалогового окна **Редактор диспетчера соединений с неструктурированными файлами** используется для задания данных о строках и столбцах и для предварительного просмотра файла.  
  
 Дополнительные сведения о диспетчере соединений с неструктурированными файлами см. в разделе [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="static-options"></a>Статические параметры  
 **Имя диспетчера соединений**  
 Укажите уникальное имя для соединения с неструктурированным файлом в рабочем процессе. Выбранное имя будет отображаться в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Опишите соединение. Рекомендуется описать цель соединения, чтобы пакеты самодокументировались и их проще было обслуживать.  
  
### <a name="flat-file-format-dynamic-options"></a>Динамические параметры формата неструктурированных файлов  
  
#### <a name="format--delimited"></a>Формат = Разделитель  
 **Разделитель строк**  
 Выберите из списка доступных разделителей строк или введите текст разделителя.  
  
|Значение|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Строки разделяются сочетанием символов возврата каретки и перевода строки.|  
|**{CR}**|Строки разделяются символом возврата каретки.|  
|**{LF}**|Строки разделяются символом перевода строки.|  
|**Точка с запятой {;}**|Строки разделяются точкой с запятой.|  
|**Двоеточие {:}**|Строки разделяются двоеточием.|  
|**Запятая {,}**|Строки разделяются запятой.|  
|**Табуляция {t}**|Строки разделяются символом табуляции.|  
|**Вертикальная черта {&#124;}**|Строки разделяются вертикальной чертой.|  
  
 **Разделитель столбцов**  
 Выберите из списка доступных разделителей столбцов или введите текст разделителя.  
  
|Значение|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Столбцы разделяются парой символов возврата каретки и перевода строки.|  
|**{CR}**|Столбцы разделяются символом возврата каретки.|  
|**{LF}**|Столбцы разделяются символом перевода строки.|  
|**Точка с запятой {;}**|Столбцы разделяются символом точки с запятой.|  
|**Двоеточие {:}**|Столбцы разделяются символом двоеточия.|  
|**Запятая {,}**|Столбцы разделяются символом запятой.|  
|**Табуляция {t}**|Столбцы разделяются символом табуляции.|  
|**Вертикальная черта {&#124;}**|Столбцы разделяются символом вертикальной черты.|  
  
 **Обновить**  
 Просмотрите результаты изменения разделителей, нажав кнопку **Обновить**. Эта кнопка становится видимой только после изменения других параметров соединения.  
  
 **Предварительный просмотр строк**  
 Просмотр образца данных в неструктурированном файле, разделенном на столбцы и строки с помощью выбранных параметров.  
  
 **Сбросить столбцы**  
 При нажатии кнопки **Сбросить столбцы**удаляются все столбцы, кроме исходных.  
  
#### <a name="format--fixed-width"></a>Формат = Фиксированная ширина  
 **Шрифт**  
 Выбор шрифта для предварительного просмотра данных.  
  
 **Столбцы источника данных**  
 Настройте ширину строк, перемещая красный вертикальный маркер, а также ширину столбцов, щелкнув линейку в верхней части окна предварительного просмотра  
  
 **Ширина строки**  
 Задайте длину строки перед добавлением разделителей для отдельных столбцов. Или переместите красный вертикальный маркер в окне предварительного просмотра, чтобы отметить конец строки. Значение ширины строки автоматически обновляется.  
  
 **Сбросить столбцы**  
 При нажатии кнопки **Сбросить столбцы**удаляются все столбцы, кроме исходных.  
  
#### <a name="format--ragged-right"></a>Формат = Выравнивание по левому краю  
  
> [!NOTE]  
>  В файлах с текстом без выравнивания вправо каждый столбец имеет фиксированную ширину, за исключением последнего столбца. Он отделяется разделителем строк.  
  
 **Шрифт**  
 Выбор шрифта для предварительного просмотра данных.  
  
 **Столбцы источника данных**  
 Настройте ширину строк, перемещая красный вертикальный маркер, а также ширину столбцов, щелкнув линейку в верхней части окна предварительного просмотра  
  
 **Разделитель строк**  
 Выберите из списка доступных разделителей строк или введите текст разделителя.  
  
|Значение|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Строки разделяются сочетанием символов возврата каретки и перевода строки.|  
|**{CR}**|Строки разделяются символом возврата каретки.|  
|**{LF}**|Строки разделяются символом перевода строки.|  
|**Точка с запятой {;}**|Строки разделяются точкой с запятой.|  
|**Двоеточие {:}**|Строки разделяются двоеточием.|  
|**Запятая {,}**|Строки разделяются запятой.|  
|**Табуляция {t}**|Строки разделяются символом табуляции.|  
|**Вертикальная черта {&#124;}**|Строки разделяются вертикальной чертой.|  
  
 **Сбросить столбцы**  
 При нажатии кнопки **Сбросить столбцы**удаляются все столбцы, кроме исходных.  
## <a name="flat-file-connection-manager-editor-advanced-page"></a>Редактор диспетчера соединений с неструктурированными файлами (страница «Дополнительно»)
  Страница **Дополнительно** диалогового окна **Редактор диспетчера соединения с неструктурированными файлами** используется для установки свойств, указывающих, как службы Integration Services считывают и записывают данные в неструктурированные файлы. Можно изменить имена столбцов неструктурированного файла и установить свойства, включающие тип данных и разделители для каждого столбца файла.  
  
 По умолчанию, длина строковых столбцов составляет 50 символов. Чтобы не допустить усечения данных или установки избыточной ширины столбца, можно изменить длину столбцов. Также можно обновить другие метаданные, чтобы обеспечить совместимость с целевыми столбцами. Например, можно изменить тип данных столбца, который содержит только целые данные, на числовой тип данных, например DT_I2. Эти изменения можно выполнить вручную или нажать кнопку **Выбор типов** , чтобы вывести диалоговое окно **Предлагаемые типы столбцов** , оценить образец данных и выполнить некоторые из этих изменений автоматически.  
  
 Дополнительные сведения о диспетчере соединений с неструктурированными файлами см. в разделе [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Параметры  
 **Имя диспетчера соединений**  
 Введите уникальное имя для диспетчера соединений с неструктурированными файлами в рабочем процессе. Выбранное имя будет отображаться в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Задайте описание диспетчера соединений. Рекомендуется описать назначение диспетчера соединений, чтобы сделать пакеты самодокументируемыми и более простыми в использовании.  
  
 **Настройте свойства каждого столбца**  
 Выберите столбец в левой панели для просмотра его свойств в правой панели. В нижеследующей таблице приведены описания свойств типов данных. Некоторые перечисленные свойства могут настраиваться только для некоторых форматов неструктурированных файлов.  
  
|Свойство|Description|  
|--------------|-----------------|  
|**ColumnType**|Указывает, ограничен ли столбец специальным символом, фиксированной шириной или оборван по правому краю. Это свойство предназначено только для чтения. В файлах с текстом без выравнивания вправо каждый столбец имеет фиксированную ширину, за исключением последнего столбца. Он отделяется разделителем строк.|  
|**OutputColumnWidth**|Укажите значение, которое будет храниться как количество байтов. Для файлов в кодировке Юникод это будет соответствовать количеству символов. В задаче потока данных это значение используется для задания ширины выходных столбцов для источника неструктурированного файла. В объектной модели это свойство имеет имя MaximumWidth.|  
|**DataType**|Выберите из списка доступных типов данных. Дополнительные сведения см. в статье [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**TextQualified**|Указывает, окружены ли текстовые данные символами-квалификаторами текста, например кавычками.<br /><br /> True: текстовые данные в неструктурированном файле обработаны квалификатором. False: текстовые данные в неструктурированном файле НЕ обработаны квалификатором.|  
|**Название**|Введите описательное имя столбца. Если не вводить имя, службы [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] автоматически создадут его в формате «Столбец 0», «Столбец 1» и так далее.|  
|**DataScale**|Укажите масштаб числовых данных. Масштаб представляет собой количество разрядов в числе. Дополнительные сведения см. в статье [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Выберите из списка допустимых разделителей столбцов. Выберите разделители, которые не могут встретиться в тексте. Это значение пропускается для столбцов фиксированной ширины.<br /><br /> **{CR}{LF}**. Столбцы разделяются парой символов возврата каретки и перевода строки.<br /><br /> **{CR}**. Столбцы разделяются символом возврата каретки.<br /><br /> **{LF}**. Столбцы разделяются символом перевода строки.<br /><br /> **Точка с запятой {;}**. Столбцы разделяются символом точки с запятой.<br /><br /> **Двоеточие {:}**. Столбцы разделяются символом двоеточия.<br /><br /> **Запятая {,}**. Столбцы разделяются символом запятой.<br /><br /> **Табуляция {t}**. Столбцы разделяются символом табуляции.<br /><br /> **Вертикальная черта {&#124;}**. Столбцы разделяются символом вертикальной черты.|  
|**DataPrecision**|Укажите точность числовых данных. Точность представляет собой число разрядов. Дополнительные сведения см. в статье [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Укажите значение, которое будет храниться как количество байтов; для файлов в кодировке Юникод это будет отображаться как количество символов. Это значение пропускается для столбцов, ограниченных разделителями.<br /><br /> **Примечание** . В объектной модели это свойство имеет имя ColumnWidth.|  
  
 **Создать**  
 Добавьте новый столбец, нажав кнопку **Создать**. По умолчанию, кнопка **Создать** добавляет новый столбец в конец списка. Эта кнопка также имеет следующие параметры, доступные в раскрывающемся списке.  
  
|Значение|Description|  
|-----------|-----------------|  
|**Добавить столбец**|Добавить новый столбец в конец списка.|  
|**Вставить до**|Вставить новый столбец перед выделенным столбцом.|  
|**Вставить после**|Вставить новый столбец после выделенного столбца.|  
  
 **Удалить**  
 Выберите столбец и затем удалите его, нажав кнопку **Удалить**.  
  
 **Предложить типы**  
 Используйте диалоговое окно **Предлагаемые типы столбцов** , чтобы оценить образец данных в файле и получить предложения для типа данных и длины каждого столбца. Дополнительные сведения см. в разделе [Диалоговое окно "Предложение типов столбцов" справочника по пользовательскому интерфейсу](../../integration-services/connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
## <a name="flat-file-connection-manager-editor-preview-page"></a>Редактор диспетчера соединения с неструктурированными файлами (страница «Предварительный просмотр»)
  Узел **Предварительный просмотр** диалогового окна **Редактор диспетчера соединения с неструктурированными файлами** предназначен для просмотра содержимого исходного файла в табличном формате.  
  
 Дополнительные сведения о диспетчере соединений с неструктурированными файлами см. в разделе [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
### <a name="options"></a>Параметры  
 **Имя диспетчера соединений**  
 Укажите уникальное имя для соединения с неструктурированным файлом в рабочем процессе. Выбранное имя будет отображаться в конструкторе служб [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Опишите соединение. Рекомендуется описать цель соединения, чтобы пакеты самодокументировались и их проще было обслуживать.  
  
 **Количество пропускаемых строк данных**  
 Укажите, сколько строк необходимо пропустить в начале неструктурированного файла.  
  
 **Обновить**  
 Просмотрите эффект от изменения числа пропускаемых строк, нажав кнопку **Обновить**. Эта кнопка становится видимой только после изменения других параметров соединения.  
  
 **Предварительный просмотр строк**  
 Просмотр данных выборки в неструктурированном файле, разделенном на столбцы и строки согласно выбранным параметрам.  
 