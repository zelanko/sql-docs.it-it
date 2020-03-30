---
title: Costanti (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- bit data type
- constants [SQL Server]
- scalar values
- money data type, constants
- binary [SQL Server], constants
- float data type
- Unicode [SQL Server], constants
- constants [Transact-SQL]
- integer constants
- decimal data type, constants
- character strings [SQL Server], constants
- positive values [SQL Server]
- formats [SQL Server], constants
- datetime data type [SQL Server]
- literals [SQL Server], constants
- real data type
- negative values
ms.assetid: 58ae3ff3-b1d5-41b2-9a2f-fc7ab8c83e0e
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f469222ff5d511447574c1bfb1e0bc2500cfae6d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68125974"
---
# <a name="constants-transact-sql"></a>Costanti (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Una costante, denominata anche valore letterale o scalare, è un simbolo che rappresenta un valore di dati specifico. Il formato di una costante dipende dal tipo di dati del valore che essa rappresenta.
  
## <a name="character-string-constants"></a>Costanti di stringhe di caratteri
Le costanti di stringhe di caratteri sono racchiuse tra virgolette singole e includono caratteri alfanumerici (a-z, A-Z e 0-9) e caratteri speciali, ad esempio il punto esclamativo (!), il simbolo di chiocciola (@) e il simbolo di cancelletto (#). A queste costanti vengono assegnate le regole di confronto predefinite del database corrente, a meno che non siano state specificate regole di confronto specifiche tramite la clausola COLLATE. Le stringhe di caratteri immesse dagli utenti vengono valutate in base alla tabella codici in uso nel computer e, se necessario, vengono convertite in base alla tabella codici predefinita del database.
  
Se per una connessione l'opzione QUOTED_IDENTIFIER è impostata su OFF, le stringhe di caratteri possono essere racchiuse tra virgolette doppie. Il provider Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e il driver ODBC tuttavia utilizzano automaticamente l'opzione SET QUOTED_IDENTIFIER ON. È consigliabile utilizzare le virgolette singole.
  
Se una stringa di caratteri racchiusa tra virgolette singole include virgolette singole, queste devono essere rappresentare con due virgolette singole. Ciò non è necessario nel caso di stringhe tra virgolette doppie.
  
Di seguito sono riportati esempi di stringhe di caratteri.
  
```sql
'Cincinnati'  
'O''Brien'  
'Process X is 50% complete.'  
'The level for job_id: %d should be between %d and %d.'  
"O'Brien"  
```  
  
Le stringhe vuote vengono rappresentate da due virgolette singole che non racchiudono alcun contenuto. In modalità di compatibilità 6.x, una stringa vuota viene gestita come spazio singolo.
  
Le costanti di stringhe di caratteri supportano regole di confronto avanzate.
  
> [!NOTE]  
>  Le costanti carattere di dimensioni superiori a 8000 byte vengono tipizzate come dati **varchar(max)** .  
  
## <a name="unicode-strings"></a>Stringhe Unicode
Il formato delle stringhe Unicode è simile a quello delle stringhe di caratteri, ma sono precedute da un identificatore N, che nello standard SQL-92 sta per National Language. Il prefisso N deve essere maiuscolo. 'Michél', ad esempio, è una costante di caratteri, mentre N'Michél' è una costante Unicode. Le costanti Unicode vengono interpretate come dati Unicode e non vengono valutate in base a una tabella codici. Alle costanti Unicode vengono associate regole di confronto, la cui funzione principale è il controllo dei confronti e la rilevanza di maiuscole e minuscole. Non vi sono assegnate tuttavia le regole di confronto predefinite del database corrente, a meno che non siano state specificate regole di confronto specifiche tramite la clausola COLLATE. I dati Unicode vengono archiviati utilizzando 2 byte per carattere, mentre per i dati di caratteri viene utilizzato 1 byte per carattere. Per altre informazioni, vedere [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md).
  
Le costanti di stringa Unicode supportano le regole di confronto avanzate.
  
> [!NOTE]  
>  Le costanti Unicode superiori a 8000 byte vengono tipizzate come dati **nvarchar(max)** .  
  
## <a name="binary-constants"></a>Costanti binarie
Le costanti binarie hanno il prefisso `0x` e sono stringhe di numeri esadecimali non racchiuse tra virgolette.
  
Di seguito sono riportati esempi di stringhe binarie.
  
```sql
0xAE  
0x12Ef  
0x69048AEFDD010E  
0x  (empty binary string)  
```  
  
> [!NOTE]  
>  Le costanti binarie superiori a 8000 byte vengono tipizzate come dati **varbinary(max)** .  
  
## <a name="bit-constants"></a>Costanti bit
Le costanti **bit** vengono rappresentate dai numeri 0 o 1 e non sono racchiuse tra virgolette. I numeri maggiori di uno vengono convertiti nel numero uno.
  
## <a name="datetime-constants"></a>Costanti datetime
Le costanti **datetime** vengono rappresentate tramite valori di data di tipo carattere in formati specifici e sono racchiuse tra virgolette singole.
  
Di seguito sono riportati esempi di costanti **datetime**:
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
Esempi di costanti datetime:
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>costanti Integer
Le costanti **integer** sono rappresentate da una stringa di numeri non racchiusa tra virgolette e priva di separatori decimali. Le costanti **integer** devono essere numeri interi e non includere decimali.
  
Di seguito sono riportati esempi di costanti **integer**:
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>Costanti decimal
Le costanti **decimal** sono rappresentate da una stringa di numeri non racchiusa tra virgolette e con un separatore decimale.
  
Di seguito sono riportati esempi di costanti **decimal**:
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>Costanti float e real
Le costanti **float** e **real** sono rappresentate tramite la notazione scientifica.
  
Di seguito sono riportati esempi di valori **float** o **real**:
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>Costanti money
Le costanti **money** vengono rappresentate come stringhe di numeri con separatore decimale facoltativo e un simbolo di valuta come prefisso facoltativo. Le costanti **money** non vengono racchiuse tra virgolette.
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non vengono imposte regole di raggruppamento quali, ad esempio, l'inserimento di un punto (.) ogni tre cifre nelle stringhe che rappresentano valori monetari.
  
> [!NOTE]  
>  I punti vengono ignorati in qualsiasi posizione nella costante letterale **money** specificata.  
  
Di seguito sono riportati esempi di costanti **money**:
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>Costanti uniqueidentifier
Le costanti **uniqueidentifier** sono stringhe che rappresentano un identificatore univoco globale (GUID). Possono essere specificate in formato di stringa binaria o di caratteri.
  
In entrambi gli esempi seguenti viene specificato lo stesso GUID.
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>Specificazione di numeri negativi e positivi  
Per indicare se un numero è positivo o negativo, è necessario includere l'operatore unario **+** o **-** in una costante numerica. In tal modo viene creata un'espressione numerica che rappresenta il valore numerico con segno. Se l'operatore unario **+** o **-** non viene applicato, le costanti numeriche usano il segno positivo.
  
Espressioni **integer** con segno:  
  
```sql
+145345234
-2147483648
```
Espressioni **decimal** con segno:  
  
```sql
+145345234.2234
-2147483648.10
```
  
Espressioni **float** con segno:  
  
```sql
+123E-3
-12E5
```
  
Espressioni **money** con segno:  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>Regole di confronto avanzate  
SQL Server supporta le costanti di stringhe di caratteri e Unicode che supportano regole di confronto avanzate. Per altre informazioni, vedere la clausola [COLLATE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9).
  
## <a name="see-also"></a>Vedere anche
[Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Espressioni &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Operatori &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)
  
  
