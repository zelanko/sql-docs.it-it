---
title: ENCRYPTBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3510c94a80f0ba7cf06817afd62d6d29e1878f1e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65948904"
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Questa funzione crittografa i dati con una chiave asimmetrica.  
  
 ![Icona di collegamento a un articolo](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un articolo")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>Argomenti  
*asym_key_ID*  
ID di una chiave asimmetrica nel database. *asym_key_ID* ha un tipo di dati **int**.  
  
*cleartext*  
Stringa di dati che verrà crittografata da `ENCRYPTBYASYMKEY` con la chiave asimmetrica. *cleartext* può avere
 
+ **binary**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
o Gestione configurazione
  
+ **varchar**
 
come tipo di dati.  
  
**@plaintext**  
Variabile contenente un valore che verrà crittografato da `ENCRYPTBYASYMKEY` con la chiave asimmetrica. **@plaintext** può avere
  
+ **binary**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
o Gestione configurazione
  
+ **varchar**
 
come tipo di dati.  
  
## <a name="return-types"></a>Tipi restituiti  
**varbinary** con un valore massimo di 8.000 byte.  
  
## <a name="remarks"></a>Remarks  
Le operazioni di crittografia e decrittografia che usano chiavi asimmetriche usano una quantità elevata di risorse e diventano quindi molto costose rispetto alla crittografia e alla decrittografia a chiavi simmetriche. È consigliabile che gli sviluppatori evitino le operazioni di crittografia e decrittografia con chiavi asimmetriche su set di dati di grandi dimensioni, ad esempio nel caso di set di dati utente archiviati in tabelle di database. Si consiglia invece agli sviluppatori di crittografare prima i dati con una chiave simmetrica avanzata e quindi di crittografare tale chiave simmetrica con una chiave asimmetrica.  
  
A seconda dell'algoritmo, `ENCRYPTBYASYMKEY` restituisce **NULL** se l'input supera un determinato numero di byte. Limiti specifici:

+ una chiave RSA a 512 bit può crittografare fino a 53 byte
+ una chiave a 1024 bit può crittografare fino a 117 byte
+ una chiave a 2048 bit può crittografare fino a 245 byte

In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sia i certificati che le chiavi asimmetriche fungono da wrapper sulle chiavi RSA.  
  
## <a name="examples"></a>Esempi  
Questo esempio crittografa il testo archiviato in `@cleartext` con la chiave asimmetrica `JanainaAsymKey02`. L'istruzione inserisce i dati crittografati nella tabella `ProtectedData04`.  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  