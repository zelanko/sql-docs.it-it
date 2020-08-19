---
description: Convalidare, eseguire query e modificare i dati JSON con funzioni predefinite (SQL Server)
title: Convalidare, eseguire query e modificare i dati JSON con funzioni predefinite
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 76644f677a03f34312e6731f5a973167313ad22a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424093"
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>Convalidare, eseguire query e modificare i dati JSON con funzioni predefinite (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Il supporto integrato per JSON include le funzioni predefinite seguenti descritte brevemente in questo argomento.  
  
-   [ISJSON](#ISJSON) verifica se una stringa include contenuto JSON valido.  
  
-   [JSON_VALUE](#VALUE) estrae un valore scalare da una stringa JSON.  
  
-   [JSON_QUERY](#QUERY) estrae un oggetto o una matrice da una stringa JSON.  
  
-   [JSON_MODIFY](#MODIFY) aggiorna il valore di una proprietà in una stringa JSON e restituisce la stringa JSON aggiornata.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>Testo JSON per gli esempi in questa pagina

Gli esempi in questa pagina usano il testo JSON simile al contenuto illustrato nell'esempio seguente:

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller",
         "givenName": "Lisa",
         "gender": "female",
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

Questo documento JSON, che contiene elementi complessi annidati, viene archiviato nella tabella di esempio seguente:

```sql
CREATE TABLE Families (
   id int identity constraint PK_JSON_ID primary key,
   doc nvarchar(max)
)
``` 

##  <a name="validate-json-text-by-using-the-isjson-function"></a><a name="ISJSON"></a> Convalidare il testo JSON tramite la funzione ISJSON  
 La funzione **ISJSON** verifica se una stringa include contenuto JSON valido.  
  
L'esempio seguente restituisce le righe in cui la colonna JSON include testo JSON valido. Si noti che senza un vincolo JSON esplicito, è possibile immettere qualsiasi testo nella colonna NVARCHAR:  
  
```sql  
SELECT *
FROM Families
WHERE ISJSON(doc) > 0 
```  

Per altre informazioni, vedere [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md).  
  
##  <a name="extract-a-value-from-json-text-by-using-the-json_value-function"></a><a name="VALUE"></a> Estrarre un valore dal testo JSON tramite la funzione JSON_VALUE  
La funzione **JSON_VALUE** estrae un valore scalare da una stringa JSON. La query seguente restituirà i documenti in cui il campo JSON `id` corrisponde al valore `AndersenFamily`, ordinati in base ai campi JSON `city` e `state`:

```sql  
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       JSON_VALUE(f.doc, '$.address.county') AS County
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
ORDER BY JSON_VALUE(f.doc, '$.address.city') DESC, JSON_VALUE(f.doc, '$.address.state') ASC
```  

I risultati di questa query sono riportati nella tabella seguente:

| Nome | city | Contea |
| --- | --- | --- |
| AndersenFamily | NY | Manhattan |

Per altre informazioni, vedere [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
##  <a name="extract-an-object-or-an-array-from-json-text-by-using-the-json_query-function"></a><a name="QUERY"></a> Estrarre un oggetto o una matrice dal testo JSON tramite la funzione JSON_QUERY  

La funzione **JSON_QUERY** estrae un oggetto o una matrice da una stringa JSON. Nell'esempio seguente viene illustrato come restituire un frammento JSON nei risultati della query.  
  
```sql
SELECT JSON_QUERY(f.doc, '$.address') AS Address,
       JSON_QUERY(f.doc, '$.parents') AS Parents,
       JSON_QUERY(f.doc, '$.parents[0]') AS Parent0
FROM Families f 
WHERE JSON_VALUE(f.doc, '$.id') = N'AndersenFamily'
```  
I risultati di questa query sono riportati nella tabella seguente:

| Indirizzo | Parents | Parent0 |
| --- | --- | --- |
| { "state": "NY", "county": "Manhattan", "city": "NY" } | [{ "familyName": "Wakefield", "givenName": "Robin" }, {"familyName": "Miller", "givenName": "Ben" } ]| { "familyName": "Wakefield", "givenName": "Robin" } |

Per altre informazioni, vedere [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  

## <a name="parse-nested-json-collections"></a>Analizzare raccolte JSON annidate

La funzione `OPENJSON` consente di trasformare la sottomatrice JSON nel set di righe e quindi di unirla in join all'elemento padre. È ad esempio possibile restituire tutti i documenti della famiglia e "unirli in join" ai relativi oggetti `children` archiviati come una matrice JSON interna:

```sql
SELECT JSON_VALUE(f.doc, '$.id')  AS Name, 
       JSON_VALUE(f.doc, '$.address.city') AS City,
       c.givenName, c.grade
FROM Families f
        CROSS APPLY OPENJSON(f.doc, '$.children')
            WITH(grade int, givenName nvarchar(100))  c
```

I risultati di questa query sono riportati nella tabella seguente:

| Nome | city | givenName | grade |
| --- | --- | --- | --- |
| AndersenFamily | NY | Jesse | 1 |
| AndersenFamily | NY | Lisa | 8 |

Si ottengono due righe come risultato perché una riga padre viene unita in join con due righe figlio generate analizzando due elementi della sottomatrice degli elementi figlio. La funzione `OPENJSON` analizza il frammento `children` dalla colonna `doc` e restituisce `grade` e `givenName` da ogni elemento come set di righe. Questo set di righe può essere unito in join al documento padre.
 
## <a name="query-nested-hierarchical-json-sub-arrays"></a>Eseguire query in sottomatrici JSON gerarchiche annidate

È possibile applicare più chiamate `CROSS APPLY OPENJSON` per eseguire query in strutture JSON annidate. Il documento JSON usato in questo esempio include una matrice annidata denominata `children`, in cui ogni elemento figlio ha una matrice annidata di `pets`. La query seguente analizzerà gli elementi figlio di ogni documento, restituirà ogni oggetto della matrice come riga e quindi analizzerà la matrice `pets`:

```sql
SELECT  familyName,
    c.givenName AS childGivenName,
    c.firstName AS childFirstName,
    p.givenName AS petName 
FROM Families f 
    CROSS APPLY OPENJSON(f.doc) 
        WITH (familyName nvarchar(100), children nvarchar(max) AS JSON)
        CROSS APPLY OPENJSON(children) 
        WITH (givenName nvarchar(100), firstName nvarchar(100), pets nvarchar(max) AS JSON) as c
            OUTER APPLY OPENJSON (pets)
            WITH (givenName nvarchar(100))  as p
```

La prima chiamata di `OPENJSON` restituirà un frammento della matrice `children`usando la clausola AS JSON. Questo frammento di matrice verrà fornito alla seconda funzione `OPENJSON` che restituirà `givenName`, `firstName` di ogni figlio, nonché la matrice di `pets`. La matrice di `pets` verrà fornita alla terza funzione `OPENJSON` che restituirà `givenName` dell'animale domestico.
I risultati di questa query sono riportati nella tabella seguente:

| familyName | childGivenName | childFirstName | petName |
| --- | --- | --- | --- |
| AndersenFamily | Jesse | Merriam | Goofy |
| AndersenFamily | Jesse | Merriam | Ombreggiatura |
| AndersenFamily | Lisa | Miller| `NULL` |

Il documento radice viene unito in join alle due righe `children` restituite dalla prima chiamata di `OPENJSON(children)` che crea due righe (o tuple). Ogni riga viene quindi unita in join alle nuove righe generate da `OPENJSON(pets)` tramite l'operatore `OUTER APPLY`. Jesse ha due animali domestici, quindi `(AndersenFamily, Jesse, Merriam)` viene unito in join alle due righe generate per Goofy e Shadow. Lisa non ha animali domestici, quindi non sono presenti righe restituite da `OPENJSON(pets)` per questa tupla. Tuttavia, dal momento che si usa `OUTER APPLY`, si ottiene `NULL` nella colonna. Specificando `CROSS APPLY` invece di `OUTER APPLY`, Lisa non verrebbe inclusa nel risultato perché non sono presenti righe di animali domestici che possono essere unite in join con questa tupla.

##  <a name="compare-json_value-and-json_query"></a><a name="JSONCompare"></a> Confronto tra JSON_VALUE e JSON_QUERY  
La differenza principale tra **JSON_VALUE** e **JSON_QUERY** consiste nel fatto che **JSON_VALUE** restituisce un valore scalare, mentre **JSON_QUERY** restituisce un oggetto o una matrice.  
  
Si consideri il testo JSON di esempio seguente.  
  
```json  
{
    "a": "[1,2]",
    "b": [1, 2],
    "c": "hi"
}  
```  
  
In questo testo JSON di esempio i membri dati "a" e "c" sono valori stringa, mentre il membro dati "b" è una matrice. **JSON_VALUE** e **JSON_QUERY** restituiscono i risultati seguenti:  
  
|Percorso|**JSON_VALUE** restituisce|**JSON_QUERY** restituisce|  
|-----------|-----------------------------|-----------------------------|  
|**$**|NULL o errore|`{ "a": "[1,2]", "b": [1,2], "c":"hi"}`|  
|**$.a**|[1,2]|NULL o errore|  
|**$.b**|NULL o errore|[1,2]|  
|**$.b[0]**|1|NULL o errore|  
|**$.c**|hi|NULL o errore|  
  
## <a name="test-json_value-and-json_query-with-the-adventureworks-sample-database"></a>Test di JSON_VALUE e JSON_QUERY con il database di esempio AdventureWorks  
Testare le funzioni predefinite descritte in questo argomento eseguendo gli esempi seguenti con il database di esempio AdventureWorks. Per informazioni su come ottenere il database AdventureWorks e su come aggiungere i dati JSON per il testing eseguendo uno script, vedere [Test drive del supporto JSON integrato](json-data-sql-server.md#test-drive-built-in-json-support-with-the-adventureworks-sample-database).
  
Negli esempi seguenti la colonna `Info` nella tabella `SalesOrder_json` contiene testo JSON.  
  
### <a name="example-1---return-both-standard-columns-and-json-data"></a>Esempio 1: restituire colonne standard e dati JSON  
La query seguente restituisce valori sia dalle colonne relazionali standard sia da una colonna JSON.  
  
```sql  
SELECT SalesOrderNumber, OrderDate, Status, ShipDate, Status, AccountNumber, TotalDue,
 JSON_QUERY(Info,'$.ShippingInfo') ShippingInfo,
 JSON_QUERY(Info,'$.BillingInfo') BillingInfo,
 JSON_VALUE(Info,'$.SalesPerson.Name') SalesPerson,
 JSON_VALUE(Info,'$.ShippingInfo.City') City,
 JSON_VALUE(Info,'$.Customer.Name') Customer,
 JSON_QUERY(OrderItems,'$') OrderItems
FROM Sales.SalesOrder_json
WHERE ISJSON(Info) > 0
```  
  
### <a name="example-2--aggregate-and-filter-json-values"></a>Esempio 2: aggregare e filtrare valori JSON  
La query seguente aggrega i subtotali in base al nome del cliente (archiviato in JSON) e in base allo stato (archiviato in una colonna normale), quindi filtra i risultati in base alla città (archiviata in JSON) e in base al valore OrderDate (archiviato in una colonna normale).  
  
```sql  
DECLARE @territoryid INT;
DECLARE @city NVARCHAR(32);

SET @territoryid=3;

SET @city=N'Seattle';

SELECT JSON_VALUE(Info, '$.Customer.Name') AS Customer, Status, SUM(SubTotal) AS Total
FROM Sales.SalesOrder_json
WHERE TerritoryID=@territoryid
 AND JSON_VALUE(Info, '$.ShippingInfo.City') = @city
 AND OrderDate > '1/1/2015'
GROUP BY JSON_VALUE(Info, '$.Customer.Name'), Status
HAVING SUM(SubTotal)>1000
```  
  
##  <a name="update-property-values-in-json-text-by-using-the-json_modify-function"></a><a name="MODIFY"></a> Aggiornare i valori delle proprietà in testo JSON tramite la funzione JSON_MODIFY  
La funzione **JSON_MODIFY** aggiorna il valore di una proprietà in una stringa JSON e restituisce la stringa JSON aggiornata.  
  
Nell'esempio seguente viene aggiornato il valore di una proprietà JSON in una variabile che include contenuto JSON.  
  
```sql  
SET @info = JSON_MODIFY(@jsonInfo, "$.info.address[0].town", 'London')    
```  
  
 Per altre informazioni, vedere [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md).  
  
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere i video seguenti:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 e supporto JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON come ponte tra NoSQL e gli ambienti relazionali)
  
## <a name="see-also"></a>Vedere anche  
 [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md)   
 [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)   
 [JSON_MODIFY &#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)   
 [JSON Path Expressions (Espressioni di percorso JSON) &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)  
  
  
