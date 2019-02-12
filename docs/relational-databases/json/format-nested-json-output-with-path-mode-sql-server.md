---
title: Formattare l'output JSON annidato con la modalità PATH (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
ms.assetid: 032761b0-6358-42e4-b05c-dbfd663ac881
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d90637fb98635c16029be7fb81bb384e08edd34
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033182"
---
# <a name="format-nested-json-output-with-path-mode-sql-server"></a>Formattare l'output JSON annidato con la modalità PATH (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Per mantenere il controllo completo sull'output della clausola **FOR JSON**, specificare l'opzione **PATH**.  
  
La modalità**PATH** consente di creare oggetti wrapper e annidare proprietà complesse. I risultati vengono formattati sotto forma di matrice di oggetti JSON.  
  
L'alternativa prevede l'uso dell'opzione **AUTO** per formattare l'output automaticamente in base alla struttura dell'istruzione **SELECT**.
 -   Per altre informazioni sull'opzione **AUTO**, vedere [Formattare automaticamente l'output JSON con la modalità AUTO](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md) .
 -   Per una panoramica di entrambe le opzioni, vedere [Formattare i risultati delle query in formato JSON con FOR JSON](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).
 
Di seguito sono riportati alcuni esempi della clausola **FOR JSON** con l'opzione **PATH** . Per formattare risultati annidati, usare nomi di colonna separati da punti oppure query annidate, come illustrato negli esempi seguenti. Per impostazione predefinita, i valori null non vengono inclusi nell'output **FOR JSON**.  

## <a name="example---dot-separated-column-names"></a>Esempio: nomi di colonna separati da punti  
La query seguente formatta le prime cinque righe della tabella `Person` di AdventureWorks come JSON.  

La clausola **FOR JSON PATH** usa l'alias o il nome di colonna per determinare il nome della chiave nell'output JSON. Se un alias contiene punti, l'opzione PATH crea oggetti annidati.  

 **Query**  
  
```sql  
SELECT TOP 5   
       BusinessEntityID As Id,  
       FirstName, LastName,  
       Title As 'Info.Title',  
       MiddleName As 'Info.MiddleName'  
   FROM Person.Person  
   FOR JSON PATH   
```  
  
 **Result**  
  
```json  
[{
    "Id": 1,
    "FirstName": "Ken",
    "LastName": "Sanchez",
    "Info": {
        "MiddleName": "J"
    }
}, {
    "Id": 2,
    "FirstName": "Terri",
    "LastName": "Duffy",
    "Info": {
        "MiddleName": "Lee"
    }
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
    "Info": {
        "Title": "Ms.",
        "MiddleName": "A"
    }
}]
```  
   
## <a name="example---multiple-tables"></a>Esempio: più tabelle  
Se nella query si fa riferimento a più tabelle, **FOR JSON PATH** annida ogni colonna usando il relativo alias. La query seguente crea un oggetto JSON per ogni coppia (OrderHeader,OrderDetails) unita in join nella query. 
  
 **Query**  
  
```sql  
SELECT TOP 2 SalesOrderNumber AS 'Order.Number',  
        OrderDate AS 'Order.Date',  
        UnitPrice AS 'Product.Price',  
        OrderQty AS 'Product.Quantity'  
FROM Sales.SalesOrderHeader H  
   INNER JOIN Sales.SalesOrderDetail D  
     ON H.SalesOrderID = D.SalesOrderID  
FOR JSON PATH   
```  
  
 **Result**  
  
```json  
[{
    "Order": {
        "Number": "SO43659",
        "Date": "2011-05-31T00:00:00"
    },
    "Product": {
        "Price": 2024.9940,
        "Quantity": 1
    }
}, {
    "Order": {
        "Number": "SO43659"
    },
    "Product": {
        "Price": 2024.9940
    }
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
