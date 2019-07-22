---
title: 'Passaggio 3: Modello di verifica per la connessione a SQL tramite Ruby | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9724fb48f6ae896d9026bfec63056070e2180a8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992494"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>Passaggio 3: Modello di verifica per la connessione a SQL tramite Ruby

Questo esempio deve essere considerato solo un modello di prova.  Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft.  
  
## <a name="step-1--connect"></a>Passaggio 1: connettersi  
  
La funzione [funzione tinytds:: client](https://github.com/rails-sqlserver/tiny_tds) viene usata per connettersi al database SQL.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>Passaggio 2: Eseguire una query  
  
Copiare e incollare il codice seguente in un file vuoto. Chiamare test. RB. Quindi eseguirlo immettendo il comando seguente dal prompt dei comandi:  
  
    ruby test.rb  
  
Nell'esempio di codice viene usata la funzione [funzione tinytds:: result](https://github.com/rails-sqlserver/tiny_tds) per recuperare un set di risultati da una query sul database SQL. Questa funzione accetta una query e restituisce un set di risultati. Il set di risultati viene iterato utilizzando [result. each do | Row |](https://github.com/rails-sqlserver/tiny_tds).  
  
``` ruby 
    require 'tiny_tds'    
    print 'test'       
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC")  
    results.each do |row|  
    puts row  
    end  
```  
  
## <a name="step-3--insert-a-row"></a>Passaggio 3: inserire una riga  
  
In questo esempio si vedrà come eseguire un'istruzione [Insert](../../t-sql/statements/insert-transact-sql.md) in modo sicuro, passare i parametri che proteggono l'applicazione da un valore [SQL injection](../../relational-databases/tables/primary-and-foreign-key-constraints.md) .    
  
Per usare funzione tinytds con Azure, è consigliabile eseguire diverse `SET` istruzioni per modificare la modalità di gestione delle informazioni specifiche da parte della sessione corrente. Nell' `SET` esempio di codice vengono fornite istruzioni consigliate. Ad esempio, `SET ANSI_NULL_DFLT_ON` consentirà la creazione di nuove colonne per consentire valori null, anche se lo stato di supporto dei valori null della colonna non viene dichiarato in modo esplicito.  
  
Per allineare il formato [datetime](../../t-sql/data-types/datetime-transact-sql.md) Microsoft SQL Server, utilizzare la funzione [strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) per eseguire il cast al formato DateTime corrispondente.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SET ANSI_NULLS ON")  
    results = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")  
    results = client.execute("SET ANSI_NULL_DFLT_ON ON")  
    results = client.execute("SET IMPLICIT_TRANSACTIONS OFF")  
    results = client.execute("SET ANSI_PADDING ON")  
    results = client.execute("SET QUOTED_IDENTIFIER ON")  
    results = client.execute("SET ANSI_WARNINGS ON")  
    results = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")  
    require 'date'  
    t = Time.now  
    curr_date = t.strftime("%Y-%m-%d %H:%M:%S.%L")  
    results = client.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate)  
    OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, '#{curr_date}' )")  
    results.each do |row|  
    puts row  
    end  
```
