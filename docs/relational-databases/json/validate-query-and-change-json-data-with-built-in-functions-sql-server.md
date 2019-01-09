---
title: Convalidare, eseguire query e modificare i dati JSON con funzioni predefinite (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, built-in functions
- functions (JSON)
ms.assetid: 6b6c7673-d818-4fa9-8708-b4ed79cb1b41
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 02e8a7e05bfb1de4deb6a9c4b5d95902e7ee6a67
ms.sourcegitcommit: 0330cbd1490b63e88334a9f9e421f4bd31a6083f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2018
ms.locfileid: "52886746"
---
# <a name="validate-query-and-change-json-data-with-built-in-functions-sql-server"></a>Convalidare, eseguire query e modificare i dati JSON con funzioni predefinite (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Il supporto integrato per JSON include le funzioni predefinite seguenti descritte brevemente in questo argomento.  
  
-   [ISJSON](#ISJSON) verifica se una stringa include contenuto JSON valido.  
  
-   [JSON_VALUE](#VALUE) estrae un valore scalare da una stringa JSON.  
  
-   [JSON_QUERY](#QUERY) estrae un oggetto o una matrice da una stringa JSON.  
  
-   [JSON_MODIFY](#MODIFY) aggiorna il valore di una proprietà in una stringa JSON e restituisce la stringa JSON aggiornata.  
 
## <a name="json-text-for-the-examples-on-this-page"></a>Testo JSON per gli esempi in questa pagina
Gli esempi in questa pagina usano il testo JSON seguente, che contiene un elemento complesso.

```sql 
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }' 
``` 

##  <a name="ISJSON"></a> Convalidare il testo JSON tramite la funzione ISJSON  
 La funzione **ISJSON** verifica se una stringa include contenuto JSON valido.  
  
L'esempio seguente restituisce le righe in cui la colonna `json_col` include contenuto JSON valido.  
  
```sql  
SELECT id, json_col
FROM tab1
WHERE ISJSON(json_col) > 0 
```  

Per altre informazioni, vedere [ISJSON &#40;Transact-SQL&#41;](../../t-sql/functions/isjson-transact-sql.md).  
  
##  <a name="VALUE"></a> Estrarre un valore dal testo JSON tramite la funzione JSON_VALUE  
La funzione **JSON_VALUE** estrae un valore scalare da una stringa JSON.  
  
Nell'esempio seguente viene estratto il valore della proprietà JSON annidata `town` in una variabile locale.  
  
```sql  
SET @town = JSON_VALUE(@jsonInfo, '$.info.address.town')  
```  
  
Per altre informazioni, vedere [JSON_VALUE &#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md).  
  
##  <a name="QUERY"></a> Estrarre un oggetto o una matrice dal testo JSON tramite la funzione JSON_QUERY  
La funzione **JSON_QUERY** estrae un oggetto o una matrice da una stringa JSON.  
 
Nell'esempio seguente viene illustrato come restituire un frammento JSON nei risultati della query.  
  
```sql  
SELECT FirstName, LastName, JSON_QUERY(jsonInfo,'$.info.address') AS Address
FROM Person.Person
ORDER BY LastName
```  
  
Per altre informazioni, vedere [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md).  
  
##  <a name="JSONCompare"></a> Confronto tra JSON_VALUE e JSON_QUERY  
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
  
## <a name="test-jsonvalue-and-jsonquery-with-the-adventureworks-sample-database"></a>Test di JSON_VALUE e JSON_QUERY con il database di esempio AdventureWorks  
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
  
##  <a name="MODIFY"></a> Aggiornare i valori delle proprietà in testo JSON tramite la funzione JSON_MODIFY  
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
  
  
