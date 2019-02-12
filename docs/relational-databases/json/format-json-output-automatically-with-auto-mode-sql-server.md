---
title: Formattare automaticamente l'output JSON con la modalità AUTO (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON AUTO
ms.assetid: 178a2a4e-e0f6-49b9-9895-396956d3c7d9
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b0578b06a83b1a3af7ab86f4800e64e56472f071
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033532"
---
# <a name="format-json-output-automatically-with-auto-mode-sql-server"></a>Formattare automaticamente l'output JSON con la modalità AUTO (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Per formattare l'output della clausola **FOR JSON** automaticamente in base alla struttura dell'istruzione **SELECT**, specificare l'opzione **AUTO**.  
  
Quando si specifica l'opzione **AUTO** il formato dell'output JSON viene determinato automaticamente in base all'ordine delle colonne nell'elenco SELECT e delle relative tabelle di origine. Non è possibile modificare questo formato.
 
L'alternativa consiste nell'usare l'opzione **PATH** per mantenere il controllo sull'output.
-   Per altre informazioni sull'opzione **PATH**, vedere [Formattare l'output JSON annidato con la modalità PATH](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).
-   Per una panoramica di entrambe le opzioni, vedere [Formattare i risultati delle query in formato JSON con FOR JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).

Una query che usa l'opzione **FOR JSON AUTO** deve avere una clausola **FROM** .  
  
Di seguito sono riportati alcuni esempi della clausola **FOR JSON** con l'opzione **AUTO** .  
  
## <a name="examples"></a>Esempi

### <a name="example-1"></a>Esempio 1
 **Query**  
  
Quando una query fa riferimento a una sola tabella, i risultati della clausola FOR JSON AUTO sono simili a quelli di FOR JSON PATH. In questo caso, FOR JSON AUTO non crea oggetti annidati. L'unica differenza è che FOR JSON AUTO genera come output alias separati da punti (come `Info.MiddleName` nell'esempio seguente) come chiavi con punti e non come oggetti annidati.  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON AUTO  
```  
  
 **Result**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sánchez",
    "Info.MiddleName": "J"
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info.MiddleName": "Lee"
}, {
    "Id": 3,
    "FirstName": "Roberto",
    "LastName": "Tamburello"
}, {
    "Id": 4,
    "FirstName": "Rob",
    "LastName": "Walters"
}, {
    "Id": 5,
    "FirstName": "Gail",
    "LastName": "Erickson",
    "Info.Title": "Ms.",
    "Info.MiddleName": "A"
}]
```  

### <a name="example-2"></a>Esempio 2

**Query**  
  
Quando si uniscono più tabelle, le colonne della prima tabella vengono generate come proprietà dell'oggetto radice. Le colonne della seconda tabella vengono generate come proprietà di un oggetto annidato. Il nome della tabella o l'alias della seconda tabella (ad esempio `D` nell'esempio seguente) viene usato come nome della matrice annidata.  
  
```sql  
SELECT TOP 2 SalesOrderNumber,  
        OrderDate,  
        UnitPrice,  
        OrderQty  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON AUTO   
```  
  
**Result**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO43659",
    "D": [{
        "UnitPrice": 34.40
    }, {
        "UnitPrice": 134.24,
        "OrderQty": 5
    }]
}]
```  

### <a name="example-3"></a>Esempio 3
 
**Query**  
Invece di usare FOR JSON AUTO è possibile annidare una sottoquery FOR JSON PATH nell'istruzione SELECT, come illustrato nell'esempio seguente. Questo esempio genera lo stesso risultato dell'esempio precedente.  
  
```sql  
SELECT TOP 2  
    SalesOrderNumber,  
    OrderDate,  
    (SELECT UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail AS D  
      WHERE H.SalesOrderID = D.SalesOrderID  
     FOR JSON PATH) AS D  
FROM Sales.SalesOrderHeader AS H  
FOR JSON PATH  
```  
  
**Result**  
  
```json  
[{
    "SalesOrderNumber": "SO43659",
    "OrderDate": "2011-05-31T00:00:00",
    "D": [{
        "UnitPrice": 24.99,
        "OrderQty": 1
    }]
}, {
    "SalesOrderNumber": "SO4390",
    "D": [{
        "UnitPrice": 24.99
    }]
}]
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Altre informazioni su JSON in SQL Server e nel database SQL di Azure  
  
### <a name="microsoft-videos"></a>Video Microsoft

Per un'introduzione visiva al supporto JSON predefinito in SQL Server e nel database SQL di Azure, vedere i video seguenti:

-   [SQL Server 2016 and JSON Support](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support) (SQL Server 2016 e supporto JSON)

-   [Using JSON in SQL Server 2016 and Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database) (Uso di JSON in SQL Server 2016 e nel database SQL di Azure)

-   [JSON as a bridge between NoSQL and relational worlds](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) (JSON come ponte tra NoSQL e gli ambienti relazionali)

## <a name="see-also"></a>Vedere anche  
 [Clausola FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
