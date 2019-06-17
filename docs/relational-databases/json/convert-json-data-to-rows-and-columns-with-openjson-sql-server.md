---
title: Analizzare e trasformare i dati JSON con OPENJSON (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- OPENJSON
- JSON, importing
- importing JSON
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||= azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9260a04673ecdf4de8090bf6582fa9c674d9cf2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570991"
---
# <a name="parse-and-transform-json-data-with-openjson-sql-server"></a>Analizzare e trasformare i dati JSON con OPENJSON (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

La funzione dei set di righe **OPENJSON** consente di convertire testo JSON in un set di righe e colonne. Dopo aver trasformato una raccolta JSON in un set di righe con **OPENJSON**, è possibile eseguire qualsiasi query SQL sui dati restituiti o inserirli in una tabella di SQL Server. 
  
La funzione **OPENJSON** accetta un singolo oggetto JSON o una raccolta di oggetti JSON e li trasforma in una o più righe. Per impostazione predefinita la funzione **OPENJSON** restituisce i dati seguenti:
-   Da un oggetto JSON la funzione restituisce tutte le coppie chiave-valore trovate al primo livello.
-   Da una matrice JSON la funzione restituisce tutti gli elementi della matrice con i rispettivi indici.  

È possibile aggiungere una clausola **WITH** facoltativa per specificare uno schema che definisce in modo esplicito la struttura dell'output.  
  
## <a name="option-1---openjson-with-the-default-output"></a>Opzione 1: OPENJSON con l'output predefinito
Quando si usa la funzione **OPENJSON** senza specificare uno schema esplicito per i risultati, ovvero senza una clausola **WITH** dopo **OPENJSON**, la funzione restituisce una tabella con le tre colonne seguenti:
1.  Il **nome** della proprietà nell'oggetto di input o l'indice dell'elemento nella matrice di input.
2.  Il **valore** della proprietà o l'elemento della matrice.
3.  Il **tipo**, ad esempio stringa, numero, valore booleano, matrice o oggetto.

**OPENJSON** restituisce ogni proprietà dell'oggetto JSON o ogni elemento della matrice come riga separata.  

Il breve esempio che segue usa la funzione **OPENJSON** con lo schema predefinito, ovvero senza la clausola **WITH** facoltativa, e restituisce una riga per ogni proprietà dell'oggetto JSON.  

**Esempio**

```sql
DECLARE @json NVARCHAR(MAX)

SET @json='{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';

SELECT *
FROM OPENJSON(@json);
```  
  
**Risultati**
  
|Key|Valore|Tipo|  
|---------|-----------|----------|  
|NAME|John|1|  
|surname|Doe|1|  
|age|45|2|  
|skills|["SQL","C#","MVC"]|4|

### <a name="more-info-about-openjson-with-the-default-schema"></a>Altre informazioni su OPENJSON con lo schema predefinito

Per altre info e altri esempi, vedere [Use OPENJSON with the Default Schema &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md) (Usare OPENJSON con lo schema predefinito (SQL Server)).

Per la sintassi e l'utilizzo, vedere [OPENJSON &#40; Transact-SQL &#41;](../../t-sql/functions/openjson-transact-sql.md). 

## <a name="option-2---openjson-output-with-an-explicit-structure"></a>Opzione 2: output di OPENJSON con una struttura esplicita

Quando si specifica uno schema per i risultati tramite la clausola **WITH** della funzione **OPENJSON**, la funzione restituisce una tabella che include solo le colonne definite nella clausola **WITH**. Nella clausola **WITH** facoltativa specificare un set di colonne di output, i relativi tipi e i percorsi delle proprietà di origine JSON per ogni valore di output. **OPENJSON** esegue l'iterazione della matrice di oggetti JSON, legge il valore nel percorso specificato per ogni colonna e converte il valore nel tipo specificato.  

L'esempio seguente usa **OPENJSON** con uno schema per l'output specificato in modo esplicito nella clausola **WITH**.  
  
**Esempio**
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json =   
  N'[  
       {  
         "Order": {  
           "Number":"SO43659",  
           "Date":"2011-05-31T00:00:00"  
         },  
         "AccountNumber":"AW29825",  
         "Item": {  
           "Price":2024.9940,  
           "Quantity":1  
         }  
       },  
       {  
         "Order": {  
           "Number":"SO43661",  
           "Date":"2011-06-01T00:00:00"  
         },  
         "AccountNumber":"AW73565",  
         "Item": {  
           "Price":2024.9940,  
           "Quantity":3  
         }  
      }  
 ]'  
   
SELECT * FROM  
 OPENJSON ( @json )  
WITH (   
              Number   varchar(200) '$.Order.Number' ,  
              Date     datetime     '$.Order.Date',  
              Customer varchar(200) '$.AccountNumber',  
              Quantity int          '$.Item.Quantity'  
 ) 
```  
  
**Risultati**
  
|Number|date|Customer|Quantity|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
Questa funzione restituisce e formatta gli elementi di una matrice JSON.  
  
-   Per ogni elemento nella matrice JSON la funzione **OPENJSON** genera una nuova riga nella tabella di output. I due elementi nella matrice JSON vengono convertiti in due righe nella tabella restituita.  
  
-   Per ogni colonna, specificata usando la sintassi `colName type json_path`, **OPENJSON** converte il valore trovato in ogni elemento della matrice nel percorso specificato del tipo specificato. In questo esempio i valori per la colonna `Date` sono ricavati da ogni elemento nel percorso `$.Order.Date` e convertiti in valori datetime.  
  
### <a name="more-info-about-openjson-with-an-explicit-schema"></a>Altre informazioni su OPENJSON con uno schema esplicito

Per altre info e altri esempi, vedere [Usare OPENJSON con uno schema esplicito &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md).

Per la sintassi e l'utilizzo, vedere [OPENJSON &#40; Transact-SQL &#41;](../../t-sql/functions/openjson-transact-sql.md).

## <a name="openjson-requires-compatibility-level-130"></a>OPENJSON richiede il livello di compatibilità 130

La funzione **OPENJSON** è disponibile per il **livello di compatibilità 130**. Se il livello di compatibilità del database è inferiore a 130, SQL Server non riesce a trovare e a eseguire la funzione **OPENJSON**. Altre funzioni JSON predefinite sono disponibili in tutti i livelli di compatibilità.

È possibile controllare il livello di compatibilità nella vista `sys.databases` o nelle proprietà del database.

È possibile modificare il livello di compatibilità di un database usando il comando seguente:   
`ALTER DATABASE <DatabaseName> SET COMPATIBILITY_LEVEL = 130`  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere i video seguenti:

- [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 e supporto JSON)

- [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)

- [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON come ponte tra NoSQL e gli ambienti relazionali)
  
## <a name="see-also"></a>Vedere anche  
 [OPENJSON &#40; Transact-SQL &#41;](../../t-sql/functions/openjson-transact-sql.md)  
  