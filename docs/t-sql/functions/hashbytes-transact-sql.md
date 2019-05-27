---
title: HASHBYTES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HASHBYTES_TSQL
- HASHBYTES
dev_langs:
- TSQL
helpviewer_keywords:
- hash input
- HASHBYTES
ms.assetid: 0ea6a4d1-313e-4f70-b939-dd2cd570f6d6
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aeb87d4408f1fbe1ba269d8373e8cc648efba55e
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948375"
---
# <a name="hashbytes-transact-sql"></a>HASHBYTES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce l'hash MD2, MD4, MD5, SHA1 o SHA2 del relativo input in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
HASHBYTES ( '<algorithm>', { @input | 'input' } )  
  
<algorithm>::= MD2 | MD4 | MD5 | SHA | SHA1 | SHA2_256 | SHA2_512   
```  
  
## <a name="arguments"></a>Argomenti  
 **'** \<algorithm> **'**  
 Identifica l'algoritmo di hash da utilizzare per eseguire l'hashing dell'input. Si tratta di un argomento obbligatorio in assenza di impostazioni predefinite. Le virgolette singole sono obbligatorie. A partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], tutti gli algoritmi diversi da SHA2_256 e SHA2_512 sono deprecati.  
  
 **@input**  
 Specifica una variabile contenente i dati di cui eseguire l'hashing. **@input** è di tipo **varchar**, **nvarchar** o **varbinary**.  
  
 **'** *input* **'**  
 Specifica un'espressione che restituisce un carattere o una stringa binaria di cui eseguire l'hashing.  
  
 L'output è conforme allo standard dell'algoritmo: 128 bit (16 byte) per MD2, MD4 e MD5; 160 bit (20 byte) per SHA e SHA1; 256 bit (32 byte) per SHA2_256 e 512 bit (64 byte) per SHA2_512.  
  
**Si applica a**: da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Per [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e versioni precedenti, la dimensione dei valori di input consentiti è limitata a 8.000 byte.  
  
## <a name="return-value"></a>Valore restituito  
 **varbinary** (non più di 8000 byte)  

## <a name="remarks"></a>Remarks  
È consigliabile usare `CHECKSUM` o `BINARY_CHECKSUM` come alternative per calcolare un valore hash.

Gli algoritmi MD2, MD4, MD5, SHA e SHA1 sono deprecati a partire da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Usare invece SHA2_256 o SHA2_512. Gli algoritmi precedenti continueranno a funzionare, ma genereranno un evento Deprecation.

## <a name="examples"></a>Esempi  
### <a name="return-the-hash-of-a-variable"></a>Restituire l'hash di una variabile  
 Nell'esempio seguente viene restituito l'hash `SHA1` dei dati **nvarchar** archiviati nella variabile `@HashThis`.  
  
```sql  
DECLARE @HashThis nvarchar(4000);  
SET @HashThis = CONVERT(nvarchar(4000),'dslfdkjLK85kldhnv$n000#knf');  
SELECT HASHBYTES('SHA1', @HashThis);  
```  
  
### <a name="return-the-hash-of-a-table-column"></a>Restituire l'hash di una colonna di tabella  
 Nell'esempio seguente viene restituito l'hash SHA1 dei valori della colonna `c1` nella tabella `Test1`.  
  
```sql  
CREATE TABLE dbo.Test1 (c1 nvarchar(50));  
INSERT dbo.Test1 VALUES ('This is a test.');  
INSERT dbo.Test1 VALUES ('This is test 2.');  
SELECT HASHBYTES('SHA1', c1) FROM dbo.Test1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------------  
0x0E7AAB0B4FF0FD2DFB4F0233E2EE7A26CD08F173  
0xF643A82F948DEFB922B12E50B950CEE130A934D6  
  
(2 row(s) affected)  
```  
  
## <a name="see-also"></a>Vedere anche  
[Scelta di un algoritmo di crittografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)  
  
