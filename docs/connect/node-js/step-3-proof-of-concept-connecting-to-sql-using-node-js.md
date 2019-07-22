---
title: 'Passaggio 3: Modello di verifica per la connessione a SQL con Node.js | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5d5b41b6-129a-40b1-af8b-7e8fbd4a84bb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7a462fcb1e8fe91cc2a140716968bd6b6f188ac1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003749"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-nodejs"></a>Passaggio 3: Modello di verifica per la connessione a SQL con Node.js

![Download-FrecciaGIÙ-Circled](../../ssdt/media/download.png)[per scaricare il driver SQL node. js](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Questo esempio deve essere considerato solo un modello di prova.  Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft. Altri esempi che usano le stesse funzioni cruciali sono disponibili in GitHub:

- [https://github.com/tediousjs/tedious/blob/master/examples/](https://github.com/tediousjs/tedious/blob/master/examples/)
  
## <a name="step-1-connect"></a>Passaggio 1: connettersi  
  
La **nuova** funzione di connessione viene utilizzata per la connessione al database SQL.  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        userName: 'yourusername',  
        password: 'yourpassword',  
        server: 'yourserver.database.windows.net',  
        // If you are on Microsoft Azure, you need this:  
        options: {encrypt: true, database: 'AdventureWorks'}  
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
    // If no error, then good to proceed.  
        console.log("Connected");  
    });  
```  
  
## <a name="step-2--execute-a-query"></a>Passaggio 2: Eseguire una query  
  
  
Tutte le istruzioni SQL vengono eseguite utilizzando la **nuova funzione Request ()** . Se l'istruzione restituisce righe, ad esempio un'istruzione SELECT, è possibile recuperarle utilizzando la funzione **Request. on ()** . Se non sono presenti righe, la funzione request. on () restituisce elenchi vuoti.  
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        userName: 'yourusername',  
        password: 'yourpassword',  
        server: 'yourserver.database.windows.net',  
        // When you connect to Azure SQL Database, you need these next options.  
        options: {encrypt: true, database: 'AdventureWorks'}  
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement();  
    });  
  
    var Request = require('tedious').Request;  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement() {  
        request = new Request("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;", function(err) {  
        if (err) {  
            console.log(err);}  
        });  
        var result = "";  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                result+= column.value + " ";  
              }  
            });  
            console.log(result);  
            result ="";  
        });  
  
        request.on('done', function(rowCount, more) {  
        console.log(rowCount + ' rows returned');  
        });  
        connection.execSql(request);  
    }  
```  
  
## <a name="step-3-insert-a-row"></a>Passaggio 3: inserire una riga  
  
In questo esempio si vedrà come eseguire un'istruzione [Insert](../../t-sql/statements/insert-transact-sql.md) in modo sicuro, passare i parametri che proteggono l'applicazione da un valore [SQL injection](../../relational-databases/tables/primary-and-foreign-key-constraints.md) .    
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        userName: 'yourusername',  
        password: 'yourpassword',  
        server: 'yourserver.database.windows.net',  
        // If you are on Azure SQL Database, you need these next options.  
        options: {encrypt: true, database: 'AdventureWorks'}  
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement1();  
    });  
  
    var Request = require('tedious').Request  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement1() {  
        request = new Request("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES (@Name, @Number, @Cost, @Price, CURRENT_TIMESTAMP);", function(err) {  
         if (err) {  
            console.log(err);}  
        });  
        request.addParameter('Name', TYPES.NVarChar,'SQL Server Express 2014');  
        request.addParameter('Number', TYPES.NVarChar , 'SQLEXPRESS2014');  
        request.addParameter('Cost', TYPES.Int, 11);  
        request.addParameter('Price', TYPES.Int,11);  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                console.log("Product id of inserted item is " + column.value);  
              }  
            });  
        });       
        connection.execSql(request);  
    }  
```  
