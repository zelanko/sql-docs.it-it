---
title: binary e varbinary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- binary_TSQL
- varbinary_TSQL
- binary
- varbinary
dev_langs:
- TSQL
helpviewer_keywords:
- varbinary data type
- binary [SQL Server], about binary data type
ms.assetid: bcce65f9-10db-4b3e-bfaf-dfc06c6f820f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 22ea90a5876c6c824f7e80683503f1f8bf863675
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017072"
---
# <a name="binary-and-varbinary-transact-sql"></a>binary e varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipi di dati binary a lunghezza fissa o variabile.
  
## <a name="arguments"></a>Argomenti  
**binary** [ ( *n* ) ] Dati binari a lunghezza fissa con lunghezza di *n* byte, dove *n* rappresenta un valore compreso tra 1 e 8.000. Le dimensioni di archiviazione corrispondono a *n* byte.
  
**varbinary** [ ( *n* | **max**) ] Dati binari a lunghezza variabile. *n* può essere un valore compreso tra 1 e 8.000. **max** indica che la capacità di memorizzazione massima è di 2^31-1 byte. Le dimensioni dello spazio di archiviazione corrispondono alla lunghezza effettiva dei dati immessi + 2 byte. È possibile che la lunghezza dei dati immessi sia pari a 0 byte. L'equivalente di ANSI SQL per **varbinary** è **binary varying**.
  
## <a name="remarks"></a>Remarks  
Se *n* viene omesso in un'istruzione di definizione dei dati o di dichiarazione di variabili, la lunghezza predefinita è 1. Se *n* viene omesso in una funzione CAST, la lunghezza predefinita è 30.

| Tipo di dati | Usare se... |
| --- | --- |
| **binary** | le dimensioni delle voci di dati delle colonne sono consistenti.|
| **varbinary** | le dimensioni delle voci di dati delle colonne presentano notevoli differenze.|
| **varbinary(max)** | le voci di dati delle colonne superano gli 8.000 byte.|


## <a name="converting-binary-and-varbinary-data"></a>Conversione dei dati di tipo binary e varbinary
Nella conversione da un tipo di dati string (**char**, **varchar**, **nchar**, **nvarchar**, **binary**, **varbinary**, **text**, **ntext** o **image**) a un tipo di dati **binary** o **varbinary** di lunghezza variabile, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue il riempimento o il troncamento dei dati a destra. Nella conversione di altri tipi di dati nel tipo **binary** o **varbinary**, viene eseguito il riempimento o il troncamento dei dati a sinistra. Il riempimento viene eseguito utilizzando zero esadecimali.
  
La conversione nei tipi di dati **binary** e **varbinary** è utile quando i dati **binary** risultano i dati più semplici da spostare. Quando un valore di qualsiasi tipo viene convertito in un valore binario di dimensioni sufficienti e successivamente riconvertito nel tipo di dati iniziale, si ottiene sempre lo stesso valore se entrambe le conversioni vengono eseguite nella stessa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La rappresentazione binaria di un valore può variare da una versione all'altra di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
La conversione del tipo di dati **int**, **smallint** e **tinyint** nel tipo di dati **binary** o **varbinary** è supportata. Se è stato eseguito il troncamento e il valore **binary** viene riconvertito in un valore integer, il valore ottenuto sarà diverso dal valore integer originale. L'istruzione SELECT seguente, ad esempio, mostra che il valore intero `123456` viene in genere archiviato come un dato di tipo binary `0x0001e240`:
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
L'istruzione `SELECT` seguente illustra il troncamento automatico delle cifre iniziali se il valore di destinazione **binary** è troppo piccolo per l'archiviazione dell'intero valore, in modo che lo stesso numero possa essere archiviato sotto forma di `0xe240`:
  
```sql
SELECT CAST( 123456 AS BINARY(2) );  
```  
  
Il batch seguente illustra come il troncamento automatico possa influire sulle operazioni aritmetiche senza tuttavia generare errori:
  
```sql
DECLARE @BinaryVariable2 BINARY(2);  
  
SET @BinaryVariable2 = 123456;  
SET @BinaryVariable2 = @BinaryVariable2 + 1;  
  
SELECT CAST( @BinaryVariable2 AS INT);  
GO  
```  
  
Il risultato finale è `57921`, non `123457`.
  
> [!NOTE]  
>  È possibile che le conversioni da un tipo di dati ai tipi di dati **binary** e viceversa eseguite in versioni diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] producano risultati diversi.  
  
## <a name="see-also"></a>Vedere anche
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Conversione del tipo di dati &#40;motore di database&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
