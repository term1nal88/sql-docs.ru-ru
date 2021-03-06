---
title: Включение и отключение "песочницы" для языка определения отчетов для служб Reporting Services в режиме интеграции с SharePoint | Документы Майкрософт
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1cf64bf1e07a83defbc3553535251f51fa96f839
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50032123"
---
# <a name="enable-and-disable-rdl-sandboxing-for-reporting-services-in-sharepoint-integrated-mode"></a>Включение и отключение "песочницы" для языка определения отчетов для служб Reporting Services в режиме интеграции с SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Функция "песочницы" для языка определения отчетов позволяет обнаруживать и ограничивать использование определенных типов ресурсов отдельными пользователями в среде с многочисленными пользователями, которые используют единственную веб-ферму серверов отчетов. Примером этого является сценарий услуг хост-сервера, в котором может поддерживаться единственная веб-ферма серверов отчетов, применяемая несколькими пользователями, а также, возможно, другими компаниями. Администратор сервера отчетов может включить эту функцию для выполнения следующих задач.  
  
-   Ограничение размера внешних ресурсов. Внешние ресурсы включают изображения, XSLT-файлы и данные карт.  
  
-   Во время публикации отчета ограничить типы и члены, используемые в тексте выражения.  
  
-   Во время выполнения ограничить длину текста и размер возвращаемых значений для выражений.

> [!NOTE]
> Интеграция служб Reporting Services с SharePoint больше не доступна после выхода SQL Server 2016.

 При включении функции «песочницы» для языка определения отчетов отключаются следующие функции:  
  
-   пользовательский код в элементе определения отчета **\<Code>**;  
  
-   режим обратной совместимости выражений языка определения отчетов для пользовательских элементов отчета [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] ;  
  
-   именованные параметры в выражениях.  
  
 В этом разделе описывается каждый из элементов, вложенных в элемент \<**RDLSandboxing**> в файле RSReportServer.Config. Дополнительные сведения об изменении файла см. в разделе [Изменение файла конфигурации служб Reporting Services (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md). Операции с записями журнала трассировки сервера, связанные с функцией «песочницы» для выражений языка определения отчетов. Дополнительные сведения о журналах трассировки см. в разделе [Журнал трассировки службы сервера отчетов](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## <a name="example-configuration"></a>Пример конфигурации
 В следующем примере показаны параметры и примерные значения элемента \<**RDLSandboxing**> в файле RSReportServer.Config.  
  
```  
<RDLSandboxing>  
   <MaxExpressionLength>5000</MaxExpressionLength>  
   <MaxResourceSize>5000</MaxResourceSize>  
   <MaxStringResultLength>3000</MaxStringResultLength>  
   <MaxArrayResultLength>250</MaxArrayResultLength>  
   <Types>  
      <Allow Namespace=”System.Drawing” AllowNew=”True”>Bitmap</Allow>  
      <Allow Namespace=”TypeConverters.Custom” AllowNew=”True”>*</Allow>  
   </Types>  
   <Members>  
      <Deny>Format</Deny>  
      <Deny>StrDup</Deny>  
   </Members>  
</RDLSandboxing>  
```

## <a name="configuration-settings"></a>Параметры конфигурации

 Сведения о параметрах настройки приведены в следующей таблице. Параметры представлены в том порядке, в котором они следуют в файле конфигурации.  
  
|Настройка|Описание|  
|-------------|-----------------|  
|**MaxExpressionLength**|Максимально допустимое число символов в выражении языка определения отчетов.<br /><br /> По умолчанию — 1000|  
|**MaxResourceSize**|Максимально допустимый размер внешнего ресурса (КБ).<br /><br /> По умолчанию — 100|  
|**MaxStringResultLength**|Максимально допустимое число символов для возвращаемого значения выражения языка определения отчетов.<br /><br /> По умолчанию — 1000|  
|**MaxArrayResultLength**|Максимальное число элементов для возвращаемого значения выражения языка определения отчетов, допустимое в массиве.<br /><br /> По умолчанию — 100|  
|**Типы**|Список членов, разрешенных для выражений языка определения отчетов.|  
|**Allow**|Тип или набор типов, разрешенных для выражений языка определения отчетов.|  
|**Пространство имен**|Атрибут для элемента **Allow** , представляющий пространство имен, содержащее один или несколько типов, применимых к атрибуту Value. Это свойство учитывает регистр символов.|  
|**AllowNew**|Логический атрибут элемента **Allow**, указывающий, разрешено ли создание новых экземпляров этого типа в выражениях языка определения отчетов или в элементах языка определения отчетов **\<Class>**.<br /><br /> Если режим **RDLSandboxing** включен, то новые массивы не могут создаваться в выражениях языка определения отчетов, независимо от значения **AllowNew**.|  
|**Value**|Значение элемента **Allow** , представляющее имя типа, разрешенного в выражениях языка определения отчетов. Значение **\*** показывает, что разрешены все типы в пространстве имен. Это свойство учитывает регистр символов.|  
|**Члены**|Для списка типов, включенных в элемент **\<Types>**, представляет список имен членов, запрещенных в выражениях языка определения отчетов.|  
|**Запретить**|Имя члена, запрещенного в выражении языка определения отчетов. Это свойство учитывает регистр символов.<br /><br /> Если для члена указано **Deny**, то все члены всех типов с этим именем будут запрещены.|  
  
## <a name="working-with-expressions-when-rdl-sandboxing-is-enabled"></a>Работа с выражениями в режиме "песочницы" для выражений языка определения отчетов

Функцию «песочницы» для выражений языка определения отчетов можно изменить, чтобы обеспечить управление ресурсами, используемыми в выражении, следующим образом:  
  
-   ограничение количества символов, используемых в выражении;  
  
-   ограничение размера результата, возвращаемого выражением;  
  
-   разрешение списка определенных типов, которые могут быть использованы в выражении;  
  
-   ограничение списка членов по именам для списка разрешенных типов, которые могут быть использованы в выражении;  
  
-   функция «песочницы» для выражений языка определения отчетов позволяет создать список разрешенных типов и список запрещенных членов. Список разрешенных типов называется списком разрешений. Список запрещенных членов называется списком блокировок.  
  
> [!NOTE]  
>  В определении отчета компьютеру неизвестны типы всех экземпляров в справочниках выражений служб. При добавлении члена к списку блокировок в списке разрешений блокируются все члены всех типов с этим именем.  
  
 Проверка результатов выражений языка определения отчетов производится во время выполнения. Выражения языка определения отчетов проверяются в определении отчета при публикации отчета. Наблюдение за журналом трассировки сервера отчетов на наличие нарушений. Дополнительные сведения см. в статье [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
### <a name="working-with-types"></a>Работа с типами

 При добавлении типа к списку разрешений осуществляется управление следующими точками входа, используемыми для доступа к выражениям языка определения отчетов:  
  
-   статические члены этого типа;  
  
-   метод [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **New** method.  
  
-   элемент **\<Classes>** в определении отчета;  
  
-   члены, добавленные к списку блокировок, для типа в списке разрешений.  
  
 Список разрешений не управляет следующими точками входа:  
  
-   наборы данных отчетов. Поля в наборах данных отчетов, возвращаемые при запросах, могут содержать любой допустимый тип выражения языка определения отчетов;  
  
-   параметры отчета; Указанные пользователем значения параметров могут содержать любой допустимый тип выражения языка определения отчетов;  
  
-   члены разрешенного типа, не состоящие в списке блокировок. По умолчанию разрешены все члены всех типов в списке разрешений. При добавлении имени члена к списку блокировок в списке разрешений блокируются все члены всех типов с этим именем.  
  
 Чтобы разрешить член одного типа и запретить член другого типа с тем же именем, необходимо выполнить следующие действия:  
  
-   добавить к имени члена элемент **\<Deny>**;  
  
-   в пользовательской сборке создать в классе член-посредник с другим именем для того члена, который необходимо разрешить;  
  
-   добавить этот новый класс к списку разрешений.  
  
 Чтобы добавить функции [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework к списку разрешений, добавьте к списку разрешений соответствующие типы из пространства имен Microsoft.VisualBasic.  
  
 Чтобы добавить ключевые слова, определяющие тип [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework, добавьте к списку разрешений соответствующий тип CLR. Например, чтобы использовать ключевое слово [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].NET Framework **Integer**, добавьте к элементу **\<RDLSandboxing>** следующий фрагмент XML:  
  
```  
<Allow Namespace="System">Int32</Allow>  
```  
  
 Чтобы добавить универсальный или допускающий значения NULL тип .NET Framework [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] к списку разрешений, выполните следующие действия:  
  
-   создайте тип-посредник для универсального или допускающего значения NULL типа .NET Framework [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ;  
  
-   добавьте тип-посредник к списку разрешений.  
  
 При добавлении типа из пользовательской сборки к списку разрешений для сборки неявное предоставление разрешения на выполнение не выполняется. Необходимо специально изменить файл управления доступом для кода, предоставив разрешение на выполнение для данной сборки. Дополнительные сведения см. в статье [Code Access Security in Reporting Services](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md).  
  
#### <a name="maintaining-the-deny-list-of-members"></a>Обслуживание списка \<Deny> для членов

 В следующем списке показано, когда необходимо обновление списка заблокированных членов при добавлении нового типа к списку разрешений:  
  
-   при обновлении пользовательской сборки до версии, в которой вводятся новые типы;  
  
-   при добавлении новых членов к типам в списке разрешений;  
  
-   при обновлении [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] на сервере отчетов;  
  
-   при обновлении сервера отчетов до последней версии служб [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)];  
  
-   при обновлении сервера отчетов для обработки последней схемы языка определения отчетов при добавлении новых членов к типам языка определения отчетов.  
  
### <a name="working-with-operators-and-new"></a>Работа с операторами и оператором New

 По умолчанию все операторы языка [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework, кроме **New**, всегда разрешены. Оператор **New** управляется атрибутом **AllowNew** элемента **\<Allow>**. Другие операторы языка, такие как оператор метода доступа коллекции по умолчанию, оператор **!** и макросы приведения [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework, такие как **CInt**, всегда разрешены.  
  
 Добавление операторов к списку заблокированных, включая пользовательские, не поддерживается. Чтобы исключить тип операторов, выполните следующие действия:  
  
-   создайте тип-посредник, не реализующий операторы, которые необходимо исключить;.  
  
-   добавьте тип-посредник к списку разрешений.  
  
 Чтобы создать новый массив в выражении языка определения отчетов, создайте массив в определяемом классе и добавьте этот класс к списку разрешений.  
  
 Чтобы создать новый массив в выражении языка определения отчетов, необходимо выполнить следующие действия:  
  
-   определите новый класс и создайте массив в методе в этом классе;  
  
-   добавьте этот класс к списку разрешений.  
  
## <a name="see-also"></a>См. также раздел

 [Файл конфигурации RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Журнал трассировки службы сервера отчетов](../../reporting-services/report-server/report-server-service-trace-log.md)  

Остались вопросы? [Посетите форум служб Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
