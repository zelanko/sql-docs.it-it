---
title: CERTPRIVATEKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERTPRIVATEKEY
- CERTPRIVATEKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTPRIVATEKEY
ms.assetid: 33e0f01e-39ac-46da-94ff-fe53b1116df4
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e409d5064cb0e807d12a76b42055a6a43c9cb7c1
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948822"
---
# <a name="certprivatekey-transact-sql"></a>CERTPRIVATEKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Questa funzione restituisce la chiave privata di un certificato in formato binario. Questa funzione accetta tre argomenti.
-   ID certificato.  
-   Password di crittografia, usata per crittografare i bit della chiave privata restituiti dalla funzione. Questo approccio non espone le chiavi come testo non crittografato agli utenti.  
-   Password di decrittografia facoltativa. Per decrittografare la chiave privata del certificato viene usata una password di decrittografia specifica. Altrimenti viene usata la chiave master del database.  
  
Solo gli utenti con accesso alla chiave privata del certificato possono usare questa funzione. Questa funzione restituisce la chiave privata nel formato PVK.
  
## <a name="syntax"></a>Sintassi  
  
```sql
CERTPRIVATEKEY   
    (  
          cert_ID   
        , ' encryption_password '   
      [ , ' decryption_password ' ]  
    )  
```  
  
## <a name="arguments"></a>Argomenti  
*certificate_ID*  
**certificate_id** del certificato. Ottenere questo valore da sys.certificates o dalla funzione [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md). *cert_id* è un tipo di dati **int**.
  
*encryption_password*  
Password utilizzata per crittografare il valore binario restituito.
  
*decryption_password*  
Password utilizzata per decrittografare il valore binario restituito.
  
## <a name="return-types"></a>Tipi restituiti
**varbinary**
  
## <a name="remarks"></a>Remarks  
Usare **CERTENCODED** e **CERTPRIVATEKEY** insieme per restituire parti diverse di un certificato in formato binario.
  
## <a name="permissions"></a>Autorizzazioni  
**CERTPRIVATEKEY** è disponibile pubblicamente.
  
## <a name="examples"></a>Esempi  
  
```sql
CREATE DATABASE TEST1;  
GO  
USE TEST1  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Use 5tr0ng P^55Words'  
GO  
CREATE CERTIFICATE Shipping04   
WITH SUBJECT = 'Sammamish Shipping Records',   
EXPIRY_DATE = '20401031';  
GO  
SELECT CERTPRIVATEKEY(CERT_ID('Shipping04'), 'jklalkaa/; uia3dd');  
```  
  
Vedere [CERTENCODED &#40;Transact-SQL&#41;](../../t-sql/functions/certencoded-transact-sql.md), esempio B, per un esempio più complesso che usa **CERTPRIVATEKEY** e **CERTENCODED** per copiare un certificato in un altro database.
  
## <a name="see-also"></a>Vedere anche
[Funzioni di sicurezza &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)
[Funzioni di sicurezza &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)
[sys.certificates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
