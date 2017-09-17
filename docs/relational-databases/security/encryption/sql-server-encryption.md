---
title: "Шифрование в SQL Server | Документация Майкрософт"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption [SQL Server], about encryption
- security [SQL Server], encryption
- cryptography [SQL Server], about cryptography
ms.assetid: ead0150e-4943-4ad5-84c8-36f85c7278f4
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 7b4f037616e0559ac62bbae5dbe04aeffe529b06
ms.openlocfilehash: 8c449858a5f72cb7647c32a22b7a5906754d23bf
ms.contentlocale: ru-ru
ms.lasthandoff: 08/28/2017

---
# <a name="sql-server-encryption"></a>Шифрование SQL Server
  Шифрование представляет собой способ скрытия данных с помощью ключа или пароля. Это делает данные бесполезными без соответствующего ключа или пароля для дешифрования. Шифрование не решает проблемы управления доступом. Однако оно повышает защиту за счет ограничения потери данных даже при обходе системы управления доступом. Например, если компьютер, на котором установлена база данных, был настроен неправильно и злоумышленник смог получить конфиденциальные данные, то украденная информация будет бесполезна, если она была предварительно зашифрована.  
  

> [!IMPORTANT]  
>  Несмотря на то, что шифрование является полезным средством обеспечения безопасности, его не следует применять ко всем данным или соединениям. При решении о внедрении шифрования необходимо проанализировать, как пользователи получают доступ к данным. Если пользователи получают доступ к данным через открытую сеть, то шифрование может потребоваться для повышения безопасности. Однако если весь доступ осуществляется по безопасной внутренней сети, то шифрование не требуется. Использование шифрования включает политику управления паролями, ключами и сертификатами.  
  
> [!NOTE]  
>  Последние сведения о безопасности уровня транспорта (TSL1.2) см. по адресу [Поддержка TLS 1.2 для Microsoft SQL Server](https://support.microsoft.com/kb/3135244).  

В [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] можно шифровать соединения, данные и хранимые процедуры. В следующих разделах содержатся дополнительные сведения о шифровании в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

 [Иерархия средств шифрования](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
 Сведения об иерархии шифрования в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Выбор алгоритма шифрования](../../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
 Сведения о выборе эффективного алгоритма шифрования.  
  
 [Прозрачное шифрование данных (TDE)](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
 Общие сведения о прозрачном шифровании данных.  
  
 [Ключи шифрования базы данных и SQL Server (компонент Database Engine)](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  
 Используемые в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]ключи шифрования представляют собой сочетание открытых, закрытых и симметричных ключей, которые используются для защиты конфиденциальных данных. В этом разделе рассказывается о внедрении и управлении ключами шифрования.  
  
 [Постоянное шифрование (компонент Database Engine)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
 Предотвращение доступа локальных администраторов баз данных, операторов облачных баз данных и других неавторизованных пользователей с высоким уровнем привилегий к зашифрованным данным.  
  
 [Маскирование динамических данных](../../../relational-databases/security/dynamic-data-masking.md)  
 Ограничение возможности раскрытия конфиденциальных данных за счет маскирования этих данных для непривилегированных пользователей.  
  
 [Сертификаты SQL Server и асимметричные ключи](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)  
 Сведения об использовании шифрования с открытым ключом.  
  
## <a name="related-content"></a>См. также  
 [Обеспечение безопасности SQL Server](../../../relational-databases/security/securing-sql-server.md)  
 Общие сведения о способах обеспечения безопасности платформы [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] и способах работы с пользователями и защищаемыми объектами.  
  
 [Криптографические функции (Transact-SQL)](../../../t-sql/functions/cryptographic-functions-transact-sql.md)  
 Сведения о внедрении криптографических функций.  
  
 [ENCRYPTBYPASSPHRASE (Transact-SQL)](../../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
 Сведения об использовании паролей для шифрования данных.  
  
 [ENCRYPTBYKEY (Transact-SQL)](../../../t-sql/functions/encryptbykey-transact-sql.md)  
 Сведения об использовании симметричных ключей для шифрования данных.  
  
 [ENCRYPTBYASYMKEY (Transact-SQL)](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)  
 Сведения об использовании асимметричных ключей для шифрования данных.  
  
 [ENCRYPTBYCERT (Transact-SQL)](../../../t-sql/functions/encryptbycert-transact-sql.md)  
 Сведения об использовании сертификатов для шифрования данных.  
  
## <a name="external-resources"></a>Внешние ресурсы  
 [Microsoft TechNet, технический центр SQL Server: "SQL Server 2012 — безопасность и защита"](http://download.microsoft.com/download/8/F/A/8FABACD7-803E-40FC-ADF8-355E7D218F4C/SQL_Server_2012_Security_Best_Practice_Whitepaper_Apr2012.docx)  
 Текущие сведения о безопасности в [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>См. также:  
 [sys.key_encryptions (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)   
 [Ключи шифрования базы данных и SQL Server (компонент Database Engine)](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Резервное копирование и восстановление ключей шифрования служб Reporting Services](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
  
  
