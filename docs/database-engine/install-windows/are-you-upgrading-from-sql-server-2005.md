---
title: Вы выполняете обновление с версии SQL Server 2005? | Документы Майкрософт
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ad40e66f-71fe-4ee6-9ce3-17127e7b1d7a
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: d33917267f50b12b0088c62ae56ab8024e40e917
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753962"
---
# <a name="are-you-upgrading-from-sql-server-2005"></a>Вы выполняете обновление с версии SQL Server 2005?

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 Окончание расширенной поддержки для SQL Server 2005 — еще одна причина выполнить обновление до более новой версии SQL Server и базы данных SQL Azure. Обновление позволяет обеспечить безопасность и соответствие требованиям, достичь высокой производительности и оптимизировать инфраструктуру платформы данных.  
  
 Дополнительные сведения, руководство и средства для планирования и автоматизации обновления или миграции см. в разделе [Прекращение поддержки SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## <a name="why-upgrade"></a>Зачем выполнять обновление  
  
> [!IMPORTANT]  
>  Расширенная поддержка SQL Server 2005 закончилась 12 апреля 2016 г. Если SQL Server 2005 будет использоваться после 12 апреля 2016 г., вы больше не будете получать обновления для системы безопасности.  
  
## <a name="choose-your-upgrade-option"></a>Выберите вариант обновления  
При обновлении реляционных баз данных SQL Server 2005 доступны следующие варианты реляционного хранилища на платформе Майкрософт.  
  
Чтобы просмотреть более подробный анализ этих вариантов, [щелкните здесь](http://sql05upgrade.azurewebsites.net/).  
  
|Вариант реляционного хранилища|Преимущества|Другие факторы, которые следует учитывать|  
|-------------------------------|--------------|-------------------------------|  
|**SQL Server на локальном компьютере**<br /><br /> Этот вариант рекомендуется для приложений баз данных любого типа: от транзакционных систем до хранилищ данных.|У вас есть полный контроль над возможностями и масштабируемостью, так как вы управляете и оборудованием, и программным обеспечением.<br /><br /> Эта среда наиболее близка к обновляемой среде SQL Server 2005.|Необходимо сделать максимальные первоначальные инвестиции и обеспечить наиболее тщательное управление, поскольку необходимо приобрести собственное оборудование и программное обеспечение, поддерживать его и управлять им.<br /><br /> Дополнительные сведения см. на странице [SQL Server](https://www.microsoft.com/EN-US/server-cloud/products/sql-server-2017/).|  
|**SQL Server, размещенный на виртуальных машинах Azure**<br /><br /> Рекомендуется использовать этот вариант, если требуется следующее.<br /><br /> Преимущества миграции в размещенную среду.<br /><br /> Управление операционной средой.<br /><br /> Набор знакомых функций SQL Server.|Можно быстро выполнить развертывание из библиотеки образов виртуальных машин.<br /><br /> Вы получаете полный набор функций SQL Server.<br /><br /> Можно сэкономить на стоимости оборудования и серверного программного обеспечения. Вы платите только за почасовое использование.|Необходимо настроить программное обеспечение SQL Server и операционной системы и управлять им.<br /><br /> <br /><br /> Дополнительные сведения см. в статье [Обзор SQL Server на виртуальных машинах Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/).<br /><br /> Сведения о миграции см. в разделе [Перенос базы данных в SQL Server на виртуальной машине Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/).|  
|**Размещенная служба базы данных SQL Azure**<br /><br /> Рекомендуется использовать этот вариант, если требуется экономичное решение с меньшим объемом обслуживания.<br /><br /> Этот вариант особенно хорошо подходит для приложений, которым не требуется постоянное выделение одинаковых мощностей или для которых необходим внешний доступ.|Можно быстро выполнить развертывание и масштабирование.<br /><br /> Вы платите только за почасовое использование.<br /><br /> Стоимость обслуживания включает не только хранилище, но и высокую доступность и автоматическое резервное копирование.|В базе данных SQL Azure отсутствуют некоторые функции SQL Server, которые не применяются в размещенной облачной среде. Дополнительные сведения см. в разделе [Сведения о Transact-SQL Базы данных SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/).<br /><br /> Кроме того, база данных SQL Azure имеет максимальный размер 500 ГБ, а SQL Server — 524 ПБ.<br /><br /> Дополнительные сведения см. на странице [База данных SQL](https://azure.microsoft.com/services/sql-database/).<br /><br /> Сведения о миграции см. в статье, посвященной [переносу базы данных SQL Server в базу данных Azure SQL](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/).|  
  
 Возможно, для некоторых данных и приложений следует использовать нереляционное решение или решение, отличное от SQL.  
  
|Нереляционное решение|Преимущества|  
|------------------------------|--------------|  
|**Azure Cosmos DB**<br /><br /> Рекомендуется использовать этот вариант для современных, масштабируемых, мобильных и веб-приложений, использующих данные JSON и требующих сочетания надежного выполнения запросов и обработки транзакционных данных.<br /><br /> Дополнительные сведения см. в разделе [Cosmos DB](http://azure.microsoft.com/services/cosmos-db/).<br /><br /> Сведения об импорте данных см. в статье [Импорт данных в Cosmos DB](http://docs.microsoft.com/azure/cosmos-db/import-data/).|Документы индексируются, и для запросов к ним можно использовать знакомый синтаксис SQL.<br /><br /> База данных является бессхемной.<br /><br /> Можно добавлять свойства в документы без необходимости перестроения индексов.<br /><br /> Поддержка JSON и JavaScript осуществляется прямо внутри ядра СУБД.<br /><br /> Вы получаете встроенную поддержку геопространственных данных и интеграции с другими службами Azure, включая поиск Azure, HDInsight и фабрику данных.<br /><br /> Вы получаете высокопроизводительное хранилище с низкими задержками, имеющее зарезервированные уровни пропускной способности.|  
|**Табличное хранилище Azure**<br /><br /> Рекомендуется использовать этот вариант для хранения петабайт частично структурированных данных в экономичном решении.<br /><br /> Дополнительные сведения см. в разделе [Табличное хранилище](https://azure.microsoft.com/services/storage/tables/).|Можно развивать приложения и табличную схему без перевода данных в автономный режим.<br /><br /> Можно увеличивать масштаб без сегментирования набора данных.<br /><br /> Вы получаете географически избыточное хранилище, которое реплицирует данные по нескольким регионам.|  
  
## <a name="plan-your-upgrade"></a>Планирование обновления  
  
-   Ознакомьтесь с рядом сообщений о планировании обновления в блоге группы разработчиков SQL Server.  
  
    -   [Планирование эффективного обновления SQL Server 2005: шаг 1 из 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [Планирование эффективного обновления SQL Server 2005: шаг 2 из 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [Планирование эффективного обновления SQL Server 2005: шаг 3 из 3](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   Ознакомьтесь с требованиями и рекомендациями в разделе [Планирование установки SQL Server](../../sql-server/install/planning-a-sql-server-installation.md), включая [Требования к оборудованию и программному обеспечению для установки SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   Ознакомьтесь со способами обновления.  
  
    -   Просмотрите доступные методы обновления и узнайте о способах планирования и тестирования в статье [Обновление [компонент ядра СУБД]](../../database-engine/install-windows/upgrade-database-engine.md).  
  
        > [!IMPORTANT]  
        >  Обновить экземпляр SQL Server 2005 до SQL Server 2017 на месте нельзя. Необходимо установить экземпляр SQL Server 2017, а затем перенести базы данных SQL Server 2005 в новую установку. Дополнительные сведения см. в разделе "Обновление новой установки" статьи [Выбор метода обновления компонента Database Engine](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
   
  
-   Дополнительные сведения, руководство и средства для планирования и автоматизации обновления или миграции см. в разделе [Прекращение поддержки SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
## <a name="get-sql-server"></a>Получить SQL Server  
 Чтобы скачать пробную версию SQL Server, [щелкните здесь](http://www.microsoft.com/evalcenter/evaluate-sql-server-2016).  
  
## <a name="next-steps"></a>Next Steps  
 [SQL Server 2017](http://www.microsoft.com/sql-server/sql-server-2017)   
 [Прекращение поддержки SQL Server 2005](http://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
  
  
