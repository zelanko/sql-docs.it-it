---
title: VERIFYSIGNEDBYASYMKEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VERIFYSIGNEDBYASYMKEY_TSQL
- VERIFYSIGNEDBYASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- verifying digitally signed data for changes
- VERIFYSIGNEDBYASYMKEY
- testing digitally signed data for changes
- checking digitally signed data for changes
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 9f7c6e0b-5ba4-4dbb-994d-5bd59f4908de
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7d32728a6c8dd282628642739cfbf67a79bba0bd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85709824"
---
# <a name="verifysignedbyasymkey-transact-sql"></a>VERIFYSIGNEDBYASYMKEY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Verifica se i dati con firma digitale sono stati modificati dopo la firma.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
VerifySignedByAsymKey( Asym_Key_ID , clear_text , signature )  
```  
  
## <a name="arguments"></a>Argomenti  
 *Asym_Key_ID*  
 ID di un certificato con chiave asimmetrica nel database.  
  
 *clear_text*  
 Dati non crittografati che si desidera verificare.  
  
 *signature*  
 Firma allegata ai dati firmati. *signature* è di tipo **varbinary**.  
  
## <a name="return-types"></a>Tipi restituiti  
 **int**  
  
 Restituisce 1 se le firme corrispondono. In caso contrario, 0.  
  
## <a name="remarks"></a>Osservazioni  
 **VerifySignedByAsymKey** decrittografa la firma dei dati usando la chiave pubblica della chiave asimmetrica specificata e confronta il valore decrittografato con un nuovo hash MD5 dei dati calcolato. Se i valori corrispondono, viene confermata la validità della firma.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW DEFINITION per la chiave asimmetrica.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-testing-for-data-with-a-valid-signature"></a>R. Verifica dei dati contenenti una firma valida  
 Nell'esempio seguente viene restituito 1 se i dati selezionati non sono stati modificati dopo la firma tramite la chiave asimmetrica `WillisKey74`. Viene restituito 0 se invece i dati sono stati alterati.  
  
```  
SELECT Data,  
     VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), SignedData,  
     DataSignature ) as IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
RETURN;  
```  
  
### <a name="b-returning-a-result-set-that-contains-data-with-a-valid-signature"></a>B. Restituzione di un set di risultati contenente dati con una firma valida  
 Nell'esempio seguente vengono restituite le righe di `SignedData04` contenenti dati che non sono stati modificati dopo la firma con la chiave asimmetrica `WillisKey74`. Nell'esempio viene chiamata la funzione `AsymKey_ID` per recuperare l'ID della chiave asimmetrica dal database.  
  
```  
SELECT Data   
FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), Data,  
     DataSignature ) = 1  
AND Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
