---
title: ASYMKEYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASYMKEYPROPERTY_TSQL
- ASYMKEYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASYMKEYPROPERTY
ms.assetid: a30581f2-e1b1-4996-93e6-527ff96b7c42
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a5e11aef47752b1e58543b593f15df3d1dd470f6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827145"
---
# <a name="asymkeyproperty-transact-sql"></a>ASYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Questa funzione restituisce le proprietà di una chiave asimmetrica.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
ASYMKEYPROPERTY (Key_ID , 'algorithm_desc' | 'string_sid' | 'sid')  
```  
  
## <a name="arguments"></a>Argomenti  
*Key_ID*  
Key_ID di una chiave asimmetrica nel database. Per trovare il Key_ID quando si conosce solo il nome della chiave, usare ASYMKEY_ID. *Key_ID* è un tipo di dati **int**.
  
**'** algorithm_desc **'**  
Specifica che l'output restituisce la descrizione dell'algoritmo della chiave asimmetrica. Disponibile solo per le chiavi asimmetriche create da un modulo EKM.
  
**'** string_sid **'**  
Specifica che l'output restituisce il SID della chiave asimmetrica in formato **nvarchar()** .
  
**'** sid **'**  
Specifica che l'output restituisce il SID della chiave asimmetrica in formato binario.
  
## <a name="return-types"></a>Tipi restituiti  
**sql_variant**
  
## <a name="permissions"></a>Autorizzazioni  
Sono richieste le autorizzazioni appropriate per la chiave asimmetrica ed è necessario che al chiamante non sia stata negata l'autorizzazione VIEW per la chiave asimmetrica. Per altre informazioni sulle autorizzazioni per le chiavi asimmetriche, vedere [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md).
  
## <a name="examples"></a>Esempi  
L'esempio seguente restituisce le proprietà della chiave asimmetrica con Key_ID 256.
  
```sql
SELECT   
ASYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm,  
ASYMKEYPROPERTY(256, 'string_sid') AS String_SID,  
ASYMKEYPROPERTY(256, 'sid') AS SID ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[sys.asymmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
[SYMKEYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/symkeyproperty-transact-sql.md)
  
  
