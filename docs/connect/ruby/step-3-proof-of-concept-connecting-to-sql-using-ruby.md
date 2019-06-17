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
manager: jroth
ms.openlocfilehash: 20b63a0ffbe12f43ff943b9588e8392a90cff7e0
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66800812"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>Passaggio 3: Modello di verifica per la connessione a SQL tramite Ruby

In questo esempio deve essere considerato un modello di verifica solo.  Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft.  
  
## <a name="step-1--connect"></a>Passaggio 1: connettersi  
  
Il [tinytds:: client](https://github.com/rails-sqlserver/tiny_tds) funzione viene utilizzata per connettersi al Database SQL.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>Passaggio 2: Eseguire una query  
  
Copiare e incollare il codice seguente in un file vuoto. La chiamata RB. Quindi eseguirlo immettendo il comando seguente dal prompt dei comandi:  
  
    ruby test.rb  
  
Nell'esempio di codice, il [tinytds:: result](https://github.com/rails-sqlserver/tiny_tds) funzione viene utilizzata per recuperare un set di risultati da una query sul Database SQL. Questa funzione accetta una query e restituisce un set di risultati. Il set di risultati è iterato usando [result si | righe |](https://github.com/rails-sqlserver/tiny_tds).  
  
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
  
## <a name="step-3--insert-a-row"></a>Passaggio 3: Inserire una riga  
  
In questo esempio illustra come eseguire un' [inserire](../../t-sql/statements/insert-transact-sql.md) istruzione in modo sicuro, passare i parametri che proteggono l'applicazione dal [attacchi SQL injection](../../relational-databases/tables/primary-and-foreign-key-constraints.md) valore.    
  
Per usare TinyTDS con Azure, si consiglia di eseguire diverse `SET` istruzioni per modificare la modalità di gestione di informazioni specifiche della sessione corrente. Consigliato `SET` vengono fornite le istruzioni nel codice di esempio. Ad esempio, `SET ANSI_NULL_DFLT_ON` consentirà le nuove colonne create di autorizzare valori nulli anche se lo stato di supporto di valori null della colonna non viene dichiarato in modo esplicito.  
  
Per la compatibilità con Microsoft SQL Server [data/ora](../../t-sql/data-types/datetime-transact-sql.md) formattare, utilizzare il [strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) funzione per eseguire il cast nel formato datetime corrispondente.  
  
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
