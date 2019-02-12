---
title: Conversione del tipo di dati (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- converting data types [SQL Server]
- CONVERT function
- data types [SQL Server], converting
- implicit data type conversions
- explicit data type conversions [SQL Server]
- converting data types [SQL Server], about converting data types
ms.assetid: ffacf45e-a488-48d0-9bb0-dcc7fd365299
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 76db4e710c2bd3d6eac25383a1db66a3720280ca
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014503"
---
# <a name="data-type-conversion-database-engine"></a>Conversione del tipo di dati (motore di database)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

I tipi di dati possono essere convertiti negli scenari seguenti:
-   Quando i dati di un oggetto vengono spostati, confrontati o combinati con i dati di un altro oggetto, può essere necessario convertirli nel tipo di dati del secondo oggetto.  
-   Quando i dati di una colonna di risultati, di un codice restituito o di un parametro di output di [!INCLUDE[tsql](../../includes/tsql-md.md)] vengono spostati in una variabile di programma, è necessario convertirli dal tipo di dati di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in quello della variabile.  
  
Le conversioni del tipo di dati supportate tra una variabile di applicazione e una colonna del set di risultati, un codice restituito, un parametro o un marcatore di parametro di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono definite dall'API di database.
  
## <a name="implicit-and-explicit-conversion"></a>Conversione implicita ed esplicita
I tipi di dati possono essere convertiti in modo implicito o esplicito.
  
Le conversioni implicite non sono visibili all'utente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte automaticamente i dati da un tipo all'altro. Se ad esempio un valore **smallint** viene confrontato con un valore **int**, il valore **smallint** viene implicitamente convertito in un valore **int** prima dell'esecuzione del confronto.
  
**GETDATE()** esegue la conversione implicita in stile di data 0. **SYSDATETIME()** esegue la conversione implicita in stile di data 21.
  
Nelle conversioni esplicite vengono utilizzate le funzioni CAST e CONVERT.
  
Le funzioni [CAST e CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) consentono di convertire un valore, ad esempio una variabile locale, una colonna o un'altra espressione, da un tipo di dati a un altro. Ad esempio, la funzione `CAST` seguente converte il valore numerico `$157.27` nella stringa di caratteri `'157.27'`:
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
Utilizzare CAST invece di CONVERT per rendere il codice di programma [!INCLUDE[tsql](../../includes/tsql-md.md)] compatibile con lo standard ISO. Utilizzare CONVERT invece di CAST per trarre vantaggio dalla funzionalità degli stili disponibile in CONVERT.
  
Nella figura seguente vengono illustrate le conversioni di tipi di dati esplicite e implicite consentite per i tipi di dati di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questi includono **xml**, **bigint** e **sql_variant**. Non è possibile eseguire una conversione implicita in un'assegnazione dal tipo di dati **sql_variant**, ma è possibile eseguire una conversione implicita verso il tipo di dati **sql_variant**.
  
![Tabella di conversione dei tipi di dati](../../t-sql/data-types/media/lrdatahd.png "Tabella di conversione dei tipi di dati")
  
## <a name="data-type-conversion-behaviors"></a>Funzionamento della conversione dei tipi di dati
Alcune conversioni implicite ed esplicite non sono supportate quando si converte il tipo di dati di un oggetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un altro tipo di dati. Non è ad esempio possibile convertire un valore **nchar** in un valore **image**. Un valore **nchar** può essere convertito in un valore **binary** solo tramite una conversione esplicita, in quanto la conversione implicita in valore **binary** non è supportata. È tuttavia possibile convertire in modo esplicito o implicito un valore **nchar** in valore **nvarchar**.
  
Negli argomenti seguenti viene descritto il funzionamento della conversione dei tipi di dati corrispondenti:
  
 - [binary e varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money e smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit &#40;Transact-SQL&#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char e varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal e numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float e real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int, bigint, smallint e tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40;Transact-SQL&#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>Conversione del tipo di dati mediante stored procedure di automazione OLE  
Poiché in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono utilizzati tipi di dati [!INCLUDE[tsql](../../includes/tsql-md.md)] e nell'automazione OLE vengono utilizzati tipi di dati [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], i dati che vengono trasferiti da un sistema all'altro devono essere convertiti tramite le stored procedure di automazione OLE.
  
Nella tabella seguente vengono descritte le conversioni dei tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nei tipi di dati [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].
  
|Tipo di dati di SQL Server|Tipo di dati di Visual Basic|  
|--------------------------|----------------------------|  
|**char**, **varchar**, **text**, **nvarchar**, **ntext**|**String**|  
|**decimal**, **numeric**|**String**|  
|**bit**|**Boolean**|  
|**binary**, **varbinary**, **image**|Matrice di **Byte()** unidimensionale|  
|**int**|**Long**|  
|**smallint**|**Integer**|  
|**tinyint**|**Byte**|  
|**float**|**Double**|  
|**real**|**Singolo**|  
|**money**, **smallmoney**|**Currency**|  
|**datetime**, **smalldatetime**|**Data**|  
|Qualsiasi tipo impostato su NULL|**Variant** impostato su Null|  
  
Tutti i singoli valori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono convertiti in un singolo valore di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], ad eccezione dei valori **binary**, **varbinary** e **image**. Questi valori vengono convertiti in una matrice di **Byte()** unidimensionale in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Questa matrice ha un intervallo di **Byte(** 0 to *length*1 **)** dove *length* è il numero di byte nei valori **binary**, **varbinary** o **image** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Di seguito sono riportate le conversioni dai tipi di dati [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] nei tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
|Tipo di dati di Visual Basic|Tipo di dati di SQL Server|  
|----------------------------|--------------------------|  
|**Long**, **Integer**, **Byte**, **Boolean**, **Object**|**int**|  
|**Double**, **Single**|**float**|  
|**Currency**|**money**|  
|**Data**|**datetime**|  
|**String** con 4000 caratteri o meno|**varchar**/**nvarchar**|  
|**String** con più di 4000 caratteri|**text**/**ntext**|  
|Matrice di **Byte()** unidimensionale con numero di byte minore o uguale a 8000|**varbinary**|  
|Matrice di **Byte()** unidimensionale con un numero di byte maggiore di 8000|**image**|  
  
## <a name="see-also"></a>Vedere anche
[Stored procedure di automazione &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  
