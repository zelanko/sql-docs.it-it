---
title: KEY_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KEY_NAME_TSQL
- KEY_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- KEY_NAME function
ms.assetid: 7b693e5d-2325-4bf9-9b45-ad6a23374b41
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bd2246ed1a6c2c03e3a9f5c1989ce9e544c8b199
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109328"
---
# <a name="keyname-transact-sql"></a>KEY_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce il nome della chiave simmetrica dal GUID di una chiave simmetrica o da un testo crittografato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
KEY_NAME ( ciphertext | key_guid )   
```  
  
## <a name="arguments"></a>Argomenti  
 *ciphertext*  
 Testo crittografato dalla chiave simmetrica. *cyphertext* è di tipo **varbinary(8000)** .  
  
 *key_guid*  
 GUID della chiave simmetrica. *key_guid* è di tipo **uniqueidentifier**.  
  
## <a name="returned-types"></a>Tipi restituiti  
 **varchar(128)**  
  
## <a name="permissions"></a>Autorizzazioni  
 A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] la visibilità dei metadati è limitata alle entità a sicurezza diretta di cui l'utente è proprietario o per le quali dispone di autorizzazioni. Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-displaying-the-name-of-a-symmetric-key-using-the-keyguid"></a>A. Visualizzazione del nome di una chiave simmetrica mediante key_guid  
 Il database **master** contiene una chiave simmetrica denominata ##MS_ServiceMasterKey##. Nell'esempio seguente il GUID di tale chiave viene recuperato dalla vista a gestione dinamica sys.symmetric_keys e viene assegnato a una variabile che viene quindi passata alla funzione KEY_NAME per illustrare come restituire il nome corrispondente al GUID.  
  
```  
USE master;  
GO  
DECLARE @guid uniqueidentifier ;  
SELECT @guid = key_guid FROM sys.symmetric_keys  
WHERE name = '##MS_ServiceMasterKey##' ;  
-- Demonstration of passing a GUID to KEY_NAME to receive a name  
SELECT KEY_NAME(@guid) AS [Name of Key];  
```  
  
### <a name="b-displaying-the-name-of-a-symmetric-key-using-the-cipher-text"></a>B. Visualizzazione del nome di una chiave simmetrica mediante il testo crittografato  
 Nell'esempio seguente viene illustrato l'intero processo di creazione di una chiave simmetrica e popolamento di una tabella con i dati. Nell'esempio viene quindi mostrata la restituzione del nome della chiave da KEY_NAME quando viene passato il testo crittografato.  
  
```  
-- Create a symmetric key  
CREATE SYMMETRIC KEY TestSymKey   
   WITH ALGORITHM = AES_128,  
   KEY_SOURCE = 'The square of the hypotenuse is equal to the sum of the squares of the sides',  
   IDENTITY_VALUE = 'Pythagoras'  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y' ;  
GO  
-- Create a table for the demonstration  
CREATE TABLE DemoKey  
(IDCol int IDENTITY PRIMARY KEY,  
SecretCol varbinary(256) NOT NULL)  
GO  
-- Open the symmetric key if not already open  
OPEN SYMMETRIC KEY TestSymKey   
    DECRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
-- Insert a row into the DemoKey table  
DECLARE @key_GUID uniqueidentifier;  
SELECT @key_GUID = key_guid FROM sys.symmetric_keys  
WHERE name LIKE 'TestSymKey' ;  
INSERT INTO DemoKey(SecretCol)  
VALUES ( ENCRYPTBYKEY (@key_GUID, 'EncryptedText'))  
GO  
-- Verify the DemoKey data  
SELECT * FROM DemoKey;  
GO  
-- Decrypt the data  
DECLARE @ciphertext varbinary(256);  
SELECT @ciphertext = SecretCol  
FROM DemoKey WHERE IDCol = 1 ;  
SELECT CAST (  
DECRYPTBYKEY( @ciphertext)  
AS varchar(100) ) AS SecretText ;  
-- Use KEY_NAME to view the name of the key  
SELECT KEY_NAME(@ciphertext) AS [Name of Key] ;  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEYAUTOASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykeyautoasymkey-transact-sql.md)  
  
  
