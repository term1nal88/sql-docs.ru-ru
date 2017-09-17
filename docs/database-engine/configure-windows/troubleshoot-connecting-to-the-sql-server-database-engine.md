---
title: "Устранение неполадок при соединении с компонентом SQL Server Database Engine | Документы Майкрософт"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- troubleshooting, connecting to Database Engine
- connecting to Database Engine, troubleshooting
ms.assetid: 474c365b-c451-4b07-b636-1653439f4b1f
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ec8d27f68672ddbb93bbf22624345ecb59e9bb79
ms.contentlocale: ru-ru
ms.lasthandoff: 08/02/2017

---
# <a name="troubleshoot-connecting-to-the-sql-server-database-engine"></a>Устранение неполадок при соединении с компонентом SQL Server Database Engine
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Здесь приводится полный список методов поиска и устранения неполадок, которые можно использовать в случае неудачных попыток соединения с компонентом SQL Server Database Engine. Порядок этих действий не соответствует последовательности, в которой решаются наиболее вероятные проблемы. Сначала указываются шаги по устранению базовых ошибок, а затем рассматриваются более сложные вопросы. При выполнении этих действий предполагается, что вы подключаетесь к SQL Server с другого компьютера по протоколу TCP/IP — такая ситуация является наиболее распространенной. Эти действия предназначены для SQL Server 2016 с SQL Server и клиентскими приложениями под управлением Windows 10. Однако с незначительными изменениями их также можно применять к другим версиям SQL Server и другим операционным системам.

Эти инструкции особенно полезны при устранении неполадок, связанных с ошибкой "**Подключение к серверу**" с номером 11001 (или 53), серьезностью 20, состоянием 0 и сообщениями об ошибках, такими как:

*   "При установке соединения с SQL Server возникла ошибка, связанная с сетью или экземпляром. Сервер не найден или недоступен. Убедитесь, что указано правильное имя сервера и SQL Server разрешает удаленные подключения. " 

*   "(поставщик: поставщик именованных каналов, ошибка: 40 — невозможно открыть соединение с SQL Server) (Microsoft SQL Server, ошибка: 53)" или "(поставщик: поставщик TCP, ошибка: 0 — такой узел не существует.) (Microsoft SQL Server, ошибка: 11001)" 

Эта ошибка обычно означает, что не удается найти компьютер SQL Server либо номер TCP-порта неизвестен, или является неправильным, или заблокирован брандмауэром.

>  [!TIP]
>  Интерактивную страницу по устранению неполадок можно найти на сайте службы технической поддержки [!INCLUDE[msCoName_md](../../includes/msconame-md.md)] на странице [Solving Connectivity errors to SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server) (Устранение ошибок подключения к SQL Server).

### <a name="not-included"></a>Ошибки, не описанные в статье

* В этой статье отсутствуют сведения об ошибках SSPI. Сведения об ошибках SSPI см. в разделе [How to troubleshoot the "Cannot generate SSPI context" error message](http://support.microsoft.com/kb/811889)(Исправление ошибки "Не удается создать контекст SSPI").  
* В этой статье отсутствуют сведения об ошибках Kerberos. Справочные сведения см. в разделе [Диспетчер конфигурации Microsoft Kerberos для SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).
* В этой статье отсутствуют сведения о подключения к SQL Azure. Справочные сведения см. в разделе [Устранение неполадок подключения с базой данных SQL Microsoft Azure](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database). 

## <a name="gathering-information-about-the-instance-of-sql-server"></a>Сбор сведений об экземпляре SQL Server

Сначала необходимо собрать основные сведения о компоненте Database Engine.

1. Убедитесь, что экземпляр SQL Server Database Engine установлен и запущен.
    1.  Войдите на компьютер, где размещен экземпляр SQL Server.
    2.  Запустите диспетчер конфигурации SQL Server. (Диспетчер конфигурации автоматически устанавливается на компьютер при установке SQL Server. Инструкции по запуску диспетчера конфигурации могут незначительно отличаться в зависимости от версии SQL Server и Windows. Сведения о запуске диспетчера конфигурации см. в статье [Диспетчер конфигурации SQL Server](https://msdn.microsoft.com/library/ms174212.aspx).)
    3.  В диспетчере конфигурации на левой панели выберите **Службы SQL Server**. На правой панели убедитесь, что экземпляр компонента Database Engine существует и запущен. Экземпляр с именем **SQL Server (MSSQLSERVER)** является экземпляром по умолчанию (безымянным). Может существовать только один экземпляр по умолчанию. Имена других (именованных) экземпляров будут указаны в круглых скобках. SQL Server Express будет использовать имя **SQL Server (SQLEXPRESS)** как имя экземпляра до тех пор, пока кто-либо не изменит его во время установки. Запишите имя экземпляра, к которому вы пытаетесь подключиться. Кроме того, убедитесь, что экземпляр запущен, посмотрев на зеленую стрелку. Если экземпляр обозначен красным квадратом, щелкните экземпляр правой кнопкой мыши и выберите команду **Запустить**. Цвет должен измениться на зеленый.
     4. При попытке подключения к именованному экземпляру убедитесь, что запущена служба обозревателя SQL Server.
 

2.  Получите IP-адрес компьютера.
    1. В меню "Пуск" щелкните **Выполнить**. В окне **Выполнить** введите **cmd**, а затем нажмите кнопку **ОК**.
    2.  В окне командной строки введите **ipconfig** и нажмите клавишу ВВОД. Запишите **IPv4** -адрес и **IPv6** -адрес. (SQL Server может использовать для подключения старый IP-протокол версии 4 или более новый IP-протокол версии 6. В вашей сети может быть разрешен один из них или оба. Большинство пользователей начинает устранение неполадок с **IPv4** -адреса. Он короче и проще для ввода.)


3.  Получите номер TCP-порта, используемого SQL Server. В большинстве случаев соединение с компонентом Database Engine с другого компьютера устанавливается по протоколу TCP.
    1.  Используя SQL Server Management Studio на компьютере с SQL Server, подключитесь к экземпляру SQL Server. В обозревателе объектов разверните узел **Управление**, разверните **Журналы SQL Server**, а затем дважды щелкните текущий журнал.
    2.  В средстве просмотра журнала нажмите кнопку **Фильтр** на панели инструментов. В поле **Сообщение содержит текст** введите **Сервер прослушивает**, нажмите кнопку **Применить фильтр**, а затем кнопку **ОК**.
    3.  Должно быть введено сообщение с текстом, аналогичным следующему: **Сервер прослушивает ['any' \<ipv4> 1433]**. Сообщение означает, что этот экземпляр SQL Server прослушивает все IP-адреса на этом компьютере (для IP-протокола версии 4) и TCP-порт 1433. (TCP-порт 1433 — это порт, обычно используемый компонентом Database Engine. Использовать порт может только один экземпляр SQL Server, поэтому если установлено несколько экземпляров SQL Server, некоторые из них должны работать с другими номерами портов.) Запишите имя экземпляра [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], к которому вы пытаетесь подключиться. 

    >    [!NOTE] 
    >    Возможно, указан IP-адрес 127.0.0.1. Он называется адресом адаптера замыкания на себя и может использоваться только для подключения из процессов на том же компьютере. Он может быть полезен при устранения неполадок, но не подходит для соединения с другого компьютера.

## <a name="enable-protocols"></a>Включение протоколов

В некоторых установках SQL Server соединение с компонентом Database Engine с другого компьютера не включено. Администратор может разрешить соединение с помощью диспетчера конфигурации. Чтобы разрешить соединения с других компьютеров, нужно выполнить указанные ниже действия.

1.  Запустите диспетчер конфигурации SQL Server, как описано выше. 
2.  В диспетчере конфигурации на левой панели разверните узел **Сетевая конфигурация SQL Server**, а затем выберите экземпляр SQL Server, к которому нужно подключиться. На правой панели перечислены доступные протоколы соединений. Как правило, включена общая память. Ее можно использовать только на том же компьютере, поэтому в большинстве установок общая память остается включенной. Для подключения к SQL Server с другого компьютера обычно используется протокол TCP/IP. Если TCP/IP не включен, правой кнопкой мыши щелкните **TCP/IP**и выберите команду **Включить**. 
3.  Если включенный параметр для протокола был изменен, необходимо перезапустить компонент Database Engine. На левой панели щелкните **Службы SQL Server**. На правой панели щелкните экземпляр Database Engine правой кнопкой мыши и выберите команду **Перезапустить**. 

## <a name="testing-tcpip-connectivity"></a>Тестирование подключения TCP/IP

Для подключения к SQL Server по протоколу TCP/IP требуется возможность установки соединения в Windows. Для тестирования TCP-подключения воспользуйтесь средством `ping` .
1.  В меню "Пуск" щелкните **Выполнить**. В окне **Выполнить** введите **cmd**, а затем нажмите кнопку **ОК**. 
2.  В окне командной строки введите `ping` и IP-адрес компьютера, на котором запущен SQL Server. Например `ping 192.168.1.101` с IPv4-адресом или `ping fe80::d51d:5ab5:6f09:8f48%11` с IPv6-адресом. (Цифры после ping необходимо заменить IP-адресами, собранными ранее.) 
3.  Если сеть настроена должным образом, вы получите ответ, такой как **Ответ от \<IP-адрес>**, за которым следует ряд дополнительных сведений. Если появляется сообщение об ошибке, такое как **Заданный узел недоступен.** или **Истекло время ожидания запроса.**, значит TCP/IP настроен неправильно. (Проверьте правильность IP-адреса и правильность его ввода.) На этом этапе ошибка может указывать на проблему с клиентским компьютером, компьютером сервера или сетевую проблему, например ошибку маршрутизатора. В Интернете существует множество ресурсов для устранения неполадок с TCP/IP. Рекомендуется обратиться к статье 2006 г. [How to Troubleshoot Basic TCP/IP Problems](http://support.microsoft.com/kb/169790)(Устранение основных проблем с TCP/IP).
4.  Затем, в случае успешной проверки связи с использованием IP-адреса, убедитесь, что имя компьютера может быть разрешено в TCP/IP-адрес. На клиентском компьютере в окне командной строки введите `ping` и имя компьютера, на котором запущен SQL Server. Например `ping newofficepc` 
5.  Если вы могли проверить связь с IP-адресом, но теперь появляется сообщение об ошибке, такое как **Заданный узел недоступен.** или **Истекло время ожидания запроса.**, возможно, на клиентском компьютере кэшированы старые сведения о разрешении имен. Введите `ipconfig /flushdns` , чтобы очистить кэш DNS. Затем проверьте связь с компьютером по имени еще раз. Клиентский компьютер с пустым кэшем DNS будет проверять наличие последних сведения об IP-адресе компьютера сервера. 
6.  Если сеть настроена должным образом, вы получите ответ, такой как **Ответ от \<IP-адрес>**, за которым следует ряд дополнительных сведений. Если проверка связи с компьютером сервера по IP-адресу выполняется успешно, но при проверке по имени компьютера выводится сообщение об ошибке, такое как **Заданный узел недоступен.** или **Истекло время ожидания запроса.**, значит разрешение имен настроено неправильно. (Дополнительные сведения см. в упомянутой ранее статье 2006 г. [How to Troubleshoot Basic TCP/IP Problems](http://support.microsoft.com/kb/169790) (Устранение основных проблем с TCP/IP).) Для подключения к SQL Server успешное разрешение имен не требуется, но если не удается разрешить имя компьютера в IP-адрес, выполнять подключения следует с указанием IP-адреса. Это не идеальное решение, но проблему с разрешением имен можно устранить позднее.
  
  
## <a name="testing-a-local-connection"></a>Тестирование локального подключения

Перед устранением неполадки, связанной с подключением с другого компьютера, нужно проверить возможность подключения из клиентского приложения, установленного на компьютере,где запущен SQL Server. (Это позволит не принимать в расчет проблемы с брандмауэром.) В этой процедуре используется среда SQL Server Management Studio. Если среда Management Studio не установлена, см. раздел [Скачивание SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). (Если установить среду Management Studio невозможно, можно проверить соединение с использованием служебной программы `sqlcmd.exe` , которая устанавливается вместе с компонентом Database Engine. Дополнительные сведения о `sqlcmd.exe`см. в разделе [Программа sqlcmd](https://msdn.microsoft.com/library/ms162773.aspx).)
1.  Войдите на компьютер, где установлен SQL Server, с помощью имени входа с разрешением на доступ к SQL Server. (Во время установки для SQL Server требуется задать по меньшей мере одно имя входа в качестве администратора SQL Server. Если администратор неизвестен, см. сведения в статье [Подключение к SQL Server в случае, если доступ системных администраторов заблокирован](http://msdn.microsoft.com/library/dd207004.aspx).)
2.   На начальной странице введите **SQL Server Management Studio**. В более старых версиях Windows в меню "Пуск" выберите **Все программы**, **Microsoft SQL Server**, а затем щелкните **SQL Server Management Studio**.
3.  В диалоговом окне **Соединение с сервером** в списке **Тип сервера** выберите **Ядро СУБД**. В поле **Проверка подлинности** выберите **Проверка подлинности Windows**. В поле **Имя сервера** введите один из указанных далее вариантов.

|Подключение к|Тип:|Пример|
|-----------------|---------------|-----------------|
|Экземпляр по умолчанию|Имя компьютера|ACCNT27|
|Именованный экземпляр|Имя компьютера или имя экземпляра|ACCNT27\PAYROLL|

>  [!NOTE] 
>  При подключении к SQL Server из клиентского приложения на том же компьютере используется протокол общей памяти. Общая память — это тип локального именованного канала, поэтому иногда возникают ошибки, связанные с каналами.

Если на данном этапе происходит ошибка, ее необходимо устранить и только затем продолжать работу. Существует целый ряд потенциальных проблем. Имя входа может не иметь разрешений для подключения. Может отсутствовать база данных по умолчанию.

>    [!NOTE] 
>    В некоторых сообщениях об ошибках, передаваемых клиенту, намеренно отсутствуют сведения, необходимые для устранения неполадок. Это связано с обеспечением безопасности, так как в этом случае злоумышленник не может получить данные о SQL Server. Чтобы просмотреть полные сведения об ошибке, обратитесь к журналу ошибок SQL Server. Там вы найдете все подробности. Если возникает ошибка **18456 Ошибка входа пользователя**, дополнительные сведения о кодах ошибок см. в статье [MSSQLSERVER_18456](http://msdn.microsoft.com/library/cc645917) электронной документации. Очень большой список кодов ошибок приведен в блоке Аарона Бертрана (Aaron Bertrand) в статье [Troubleshooting Error 18456](http://www2.sqlblog.com/blogs/aaron_bertrand/archive/2011/01/14/sql-server-v-next-denali-additional-states-for-error-18456.aspx). Журнал ошибок можно просмотреть помощью среды SSMS (при наличии соединения) в разделе "Управление" обозревателя объектов. В противном случае журнал можно просмотреть с помощью программы Блокнот Windows. Расположение по умолчанию зависит от версии и может быть изменено во время установки. Расположением по умолчанию для [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] является `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\ERRORLOG`.  

4.   Если соединение устанавливается с помощью общей памяти, проверьте его с использованием TCP. Чтобы активировать TCP-подключение, укажите **tcp:** перед именем. Например:

|Подключение к|Тип:|Пример|
|-----------------|---------------|-----------------|
|Экземпляр по умолчанию|tcp: имя компьютера|tcp:ACCNT27|
|Именованный экземпляр|tcp: имя компьютера или имя экземпляра|tcp:ACCNT27\PAYROLL|
  
Если соединение устанавливается с помощью общей памяти, но не TCP, необходимо устранить проблему с TCP. Скорее всего, проблема в том, что TCP-протокол отключен. Сведения о включении TCP см. в разделе **Включение протоколов** выше.

5.   Если вы хотите установить соединение с использованием учетной записи, отличной от учетной записи администратора, после соединения с правами администратора повторите попытку, используя имя входа для проверки подлинности Windows или имя входа для проверки подлинности SQL Server, которое будет применять клиентское приложение.

## <a name="opening-a-port-in-the-firewall"></a>Открытие порта в брандмауэре

Начиная с Windows XP с пакетом обновления 2 (SP2), брандмауэр Windows находится во включенном состоянии и блокирует подключения с другого компьютера. Чтобы подключиться с использованием протокола TCP/IP с другого компьютера, на компьютере SQL Server необходимо настроить брандмауэр для разрешения подключений к TCP-порту, используемому компонентом Database Engine. Как упоминалось ранее, экземпляр по умолчанию обычно прослушивает TCP-порт 1433. Если имеются именованные экземпляры или вы изменили значение по умолчанию, TCP-порт [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] может прослушивать другой порт. См. описание сбора сведений для определения порта в начальном разделе.  
При подключении к именованному экземпляру или порту, отличному от TCP-порта 1433, необходимо также открыть UDP-порт 1434 для службы обозревателя SQL Server. Пошаговые инструкции об открытии порта в брандмауэре Windows см. в разделе [Настройка брандмауэра Windows для доступа к компоненту Database Engine](https://msdn.microsoft.com/library/ms175043).

## <a name="testing-the-connection"></a>Тестирование соединения

После того как появилась возможность соединения с использованием TCP на том же компьютере, нужно проверить подключение с клиентского компьютера. Теоретически можно использовать любое клиентское приложение, но чтобы избежать дополнительных сложностей, установите средства управления SQL Server на клиентском компьютере и попытайтесь запустить среду SQL Server Management Studio.

1. На клиентском компьютере с помощью среды SQL Server Management Studio попробуйте подключиться, используя IP-адрес и номер TCP-порта в формате "IP-адрес, номер порта". Например, **192.168.1.101,1433** . Если этот вариант не работает, вероятно, возникла одна из указанных далее проблем.

    * **Проверка связи** по IP-адресу не работает, что указывает на наличие общей проблемы конфигурации TCP. Вернитесь к разделу **Тестирование подключения TCP/IP**. 
    *   SQL Server не прослушивает протокол TCP. Вернитесь к разделу **Включение протоколов**. 
    *   SQL Server прослушивает порт, отличный от указанного порта. Вернитесь к разделу **Сбор сведений об экземпляре SQL Server**. 
    *   TCP-порт SQL Server блокируется брандмауэром. Вернитесь к разделу **Открытие порта в брандмауэре**.


2. Если вы можете подключиться с помощью IP-адреса и номера порта, попробуйте подключиться, используя IP-адрес без указания номера порта. Для экземпляра по умолчанию просто используйте IP-адрес. Для именованного экземпляра используйте IP-адрес и имя экземпляра в формате "IP-адрес\имя экземпляра", например **192.168.1.101\PAYROLL** . Если этот вариант не работает, вероятно, возникла одна из указанных далее проблем.

    *   Если вы подключаетесь к экземпляру по умолчанию, оно может прослушивать порт, отличный от TCP-порта 1433, и клиент не пытается подключиться к правильному номеру порта.
    *   Если вы подключаетесь к именованному экземпляру, номер порта не возвращается клиенту.  

Обе эти проблемы связаны со службой обозревателя SQL Server, которая предоставляет клиенту номер порта. Далее приводятся возможные решения.

  * Запустите службу обозревателя SQL Server. Вернитесь к разделу **Сбор сведений об экземпляре SQL Server**(подраздел 1.г).
  * Служба обозревателя SQL Server блокируется брандмауэром. Откройте UDP-порт 1434 в брандмауэре. Вернитесь к разделу **Открытие порта в брандмауэре**. (Убедитесь, что открываете UDP-порт, а не TCP-порт. Это разные порты.)
  * Данные о UDP-порте 1434 блокируются маршрутизатором. UDP-соединения (протокол UDP) не предназначены для передачи через маршрутизаторы. Это исключает попадание трафика с низким приоритетом в сеть. Вы можете настроить маршрутизатор для пересылки UDP-трафика или же всегда указывать номер порта при подключении.
  * Если клиентский компьютер работает под управлением Windows 7 или Windows Server 2008 (или более поздней операционной системы), ОС может отбрасывать UDP-трафик, поскольку ответ с сервера возвращается с IP-адреса, отличного от запрошенного. Это функция безопасности, блокирующая свободное сопоставление источника. Дополнительные сведения см. в разделе **Сервер с несколькими IP-адресами** статьи электронной документации [Устранение неполадок. Время ожидания истекло](http://msdn.microsoft.com/library/ms190181.aspx). Это статья о SQL Server 2008 R2, но ее основные тезисы можно применить также к рассматриваемому вопросу. Вы можете настроить клиент для использования правильного IP-адреса или же всегда указывать номер порта при подключении.
     
3. Если вы можете установить соединение с помощью IP-адреса (или IP-адреса и имени экземпляра имени для именованного экземпляра), попробуйте подключиться с помощью имени компьютера (или имени компьютера и имени экземпляра для именованного экземпляра). Чтобы принудительно установить подключение TCP/IP, укажите `tcp:` перед именем компьютера. Например, для экземпляра по умолчанию на компьютере с именем `ACCNT27`используйте `tcp:ACCNT27` . Для именованного экземпляра `PAYROLL`на этом компьютере используйте `tcp:ACCNT27\PAYROLL` . Если можно подключиться с помощью IP-адреса, но не имени компьютера, то существует проблема с разрешением имени. Вернитесь к разделу **Тестирование подключения TCP/IP**, подраздел 4.

4. Если вы можете подключиться с помощью имени компьютера, активирующего TCP, попробуйте подключиться с использованием имени компьютера, но без принудительной активации TCP. Например, для экземпляра по умолчанию используйте только имя компьютера, например `CCNT27`. Для именованного экземпляра используйте имя компьютера и имя экземпляра, например `ACCNT27\PAYROLL`. Если вы можете установить соединение с активацией TCP, но не можете без активации TCP, возможно, клиент использует другой протокол (например, именованные каналы).

    1. На клиентском компьютере в левой панели диспетчера конфигурации SQL Server разверните узел **Конфигурация клиента Native Client SQL версии** *версия*****, а затем выберите **Клиентские протоколы**.
    2. Убедитесь, что протокол TCP/IP на правой панели включен. Если протокол TCP/IP не включен, правой кнопкой мыши щелкните **TCP/IP** и выберите команду **Включить**.
    3. Убедитесь в том, что в последовательности протоколов TCP/IP используются значения, меньше чем для протоколов именованных каналов (или протоколов VIA в более старых версиях). Обычно общая память должна быть указана как первый порядок, а TCP/IP — как второй. Общая память используется только в том случае, когда клиент и сервер SQL выполняются на том же компьютере. Все включенные протоколы опрашиваются в указанном порядке до получения успешного результата. Следует отметить, что при установке соединения с другим компьютером общая память пропускается. 

