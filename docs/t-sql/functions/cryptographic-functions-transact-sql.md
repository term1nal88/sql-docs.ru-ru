---
title: "Криптографические функции (Transact-SQL) | Документы Microsoft"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], cryptographic
- crypto functions
- cryptography [SQL Server], functions
- decryption [SQL Server], functions
- security functions
- encryption [SQL Server], functions
ms.assetid: 0be5626b-5a25-4d8c-9f44-7abbfccf816c
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 65c62cefdff83f40f730ee9125687377af8a64ba
ms.contentlocale: ru-ru
ms.lasthandoff: 09/01/2017

---
# <a name="cryptographic-functions-transact-sql"></a>Криптографические функции (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Следующие функции поддерживают шифрование, расшифровку, цифровые подписи и их проверку.
  
## <a name="symmetric-encryption-and-decryption"></a>Симметричное шифрование и расшифровка
  
|||  
|-|-|  
|[ENCRYPTBYKEY](../../t-sql/functions/encryptbykey-transact-sql.md)|[DECRYPTBYKEY](../../t-sql/functions/decryptbykey-transact-sql.md)|  
|[ENCRYPTBYPASSPHRASE](../../t-sql/functions/encryptbypassphrase-transact-sql.md)|[DECRYPTBYPASSPHRASE](../../t-sql/functions/decryptbypassphrase-transact-sql.md)|  
|[ИДЕНТИФИКАТОР KEY_ID](../../t-sql/functions/key-id-transact-sql.md)|[KEY_GUID](../../t-sql/functions/key-guid-transact-sql.md)|  
|[DECRYPTBYKEYAUTOASYMKEY](../../t-sql/functions/decryptbykeyautoasymkey-transact-sql.md)|[KEY_NAME](../../t-sql/functions/key-name-transact-sql.md)|  
|[SYMKEYPROPERTY](../../t-sql/functions/symkeyproperty-transact-sql.md)||  
  
## <a name="asymmetric-encryption-and-decryption"></a>Асимметричное шифрование и расшифровка
  
|||  
|-|-|  
|[ENCRYPTBYASYMKEY](../../t-sql/functions/encryptbyasymkey-transact-sql.md)|[DECRYPTBYASYMKEY](../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
|[Функция ENCRYPTBYCert](../../t-sql/functions/encryptbycert-transact-sql.md)|[DECRYPTBYCERT](../../t-sql/functions/decryptbycert-transact-sql.md)|  
|[ASYMKEYPROPERTY](../../t-sql/functions/asymkeyproperty-transact-sql.md)|[ASYMKEY_ID](../../t-sql/functions/asymkey-id-transact-sql.md)|  
  
## <a name="signing-and-signature-verification"></a>Подписывание и проверка подписи
  
|||  
|-|-|  
|[SIGNBYASYMKEY](../../t-sql/functions/signbyasymkey-transact-sql.md)|[ИНСТРУКЦИЯ VERIFYSIGNEDBYASMKEY](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)|  
|[SIGNBYCERT](../../t-sql/functions/signbycert-transact-sql.md)|[VERIGYSIGNEDBYCERT](../../t-sql/functions/verifysignedbycert-transact-sql.md)|  
|[IS_OBJECTSIGNED](../../t-sql/functions/is-objectsigned-transact-sql.md)||  
  
## <a name="symmetric-decryption-with-automatic-key-handling"></a>Симметричная расшифровка с автоматическим управлением ключами
  
|||  
|-|-|  
|[DecryptByKeyAutoCert](../../t-sql/functions/decryptbykeyautocert-transact-sql.md)||  
  
## <a name="encryption-hashing"></a>Криптографическое хеширование
  
|||  
|-|-|  
|[HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md)||  
  
## <a name="copying-certificates"></a>Копирование сертификатов
  
|||  
|-|-|  
|[CERTENCODED &#40; Transact-SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md)||  
|[CERTPRIVATEKEY &#40; Transact-SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)||  
  
## <a name="see-also"></a>См. также:
[Функции](../../t-sql/functions/functions.md)  
[Иерархия шифрования](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[Иерархия разрешений (компонент Database Engine)](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[CREATE CERTIFICATE (Transact-SQL)](../../t-sql/statements/create-certificate-transact-sql.md)  
[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[Представления каталога безопасности &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)
  
  
