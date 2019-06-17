---
title: ENCRYPTBYPASSPHRASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYPASSPHRASE
- ENCRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYPASSPHRASE function
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYPASSPHRASE function
ms.assetid: f8dbb9e6-94d6-40d7-8b38-6833a409d597
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 310c734a8b2bd72c0d2217540ce9fb303a87df77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948871"
---
# <a name="encryptbypassphrase-transact-sql"></a>ENCRYPTBYPASSPHRASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Esegue la crittografia dei dati con una passphrase, usando l'algoritmo TRIPLE DES con una lunghezza della chiave pari a 128 bit.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
EncryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'cleartext' | @cleartext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *passphrase*  
 Passphrase dalla quale generare una chiave simmetrica.  
  
 @passphrase  
 Variabile di tipo **nvarchar**, **char**, **varchar**, **binary**, **varbinary** o **nchar** contenente una passphrase da cui generare una chiave simmetrica.  
  
 *cleartext*  
 Testo non crittografato da crittografare.  
  
 @cleartext  
 Variabile di tipo **nvarchar**, **char**, **varchar**, **binary**, **varbinary** o **nchar** contenente il testo non crittografato. Le dimensioni massime sono pari a 8.000 byte.  
  
 *add_authenticator*  
 Indica se un autenticatore verrà crittografato insieme al testo non crittografato. 1 se verrà aggiunto un autenticatore. **int**.  
  
 @add_authenticator  
 Indica se un hash verrà crittografato insieme al testo non crittografato.  
  
 *authenticator*  
 Dati da cui derivare un autenticatore. **sysname**.  
  
 @authenticator  
 Variabile contenente i dati dai quali derivare un autenticatore.  
  
## <a name="return-types"></a>Tipi restituiti  
 **varbinary** con un valore massimo di 8.000 byte.  
  
## <a name="remarks"></a>Remarks  
 Una passphrase è una password contenente spazi. Il vantaggio dell'uso di una passphrase consiste nel fatto che è più facile ricordare una frase significativa che una stringa di caratteri di pari lunghezza.  
  
 Questa funzione non controlla la complessità delle password.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene aggiornato un record della tabella `SalesCreditCard` e viene crittografato il valore del numero della carta di credito archiviato nella colonna `CardNumber_EncryptedbyPassphrase`, usando la chiave primaria come autenticatore.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard   
    ADD CardNumber_EncryptedbyPassphrase varbinary(256);   
GO  
-- First get the passphrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
    = 'A little learning is a dangerous thing!';  
  
-- Update the record for the user's credit card.  
-- In this case, the record is number 3681.  
UPDATE Sales.CreditCard  
SET CardNumber_EncryptedbyPassphrase = EncryptByPassPhrase(@PassphraseEnteredByUser  
    , CardNumber, 1, CONVERT( varbinary, CreditCardID))  
WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DECRYPTBYPASSPHRASE &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbypassphrase-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
