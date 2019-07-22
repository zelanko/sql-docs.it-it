---
title: 'Passaggio 3: Modello di verifica per la connessione a SQL tramite pymssql | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b56a20a0456bef04553c614432bde270d8e98d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935779"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>Passaggio 3: Modello di verifica per la connessione a SQL con pymssql
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

Questo esempio deve essere considerato solo un modello di prova.  Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft.  
  
## <a name="step-1--connect"></a>Passaggio 1: connettersi  
  
Per la connessione al database SQL viene usata la funzione [pymssql. Connect](https://pymssql.org/en/latest/ref/pymssql.html) .  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>Passaggio 2: eseguire la query  
  
È possibile utilizzare la funzione [Cursor. Execute](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute) per recuperare un set di risultati da una query sul database SQL. Questa funzione accetta essenzialmente qualsiasi query e restituisce un set di risultati su cui è possibile eseguire l'iterazione con l'uso di [Cursor. fetchOne ()](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone).  
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute('SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;')  
    row = cursor.fetchone()  
    while row:  
        print str(row[0]) + " " + str(row[1]) + " " + str(row[2])     
        row = cursor.fetchone()  
```  
  
## <a name="step-3--insert-a-row"></a>Passaggio 3: inserire una riga  
  
In questo esempio si vedrà come eseguire un'istruzione [Insert](../../../t-sql/statements/insert-transact-sql.md) in modo sicuro, passare i parametri che proteggono l'applicazione da un valore [SQL injection](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) .    
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express', 'SQLEXPRESS', 0, 0, CURRENT_TIMESTAMP)")  
    row = cursor.fetchone()  
    while row:  
        print "Inserted Product ID : " +str(row[0])  
        row = cursor.fetchone()  
    conn.commit()
    conn.close()
```  
  
## <a name="step-4--rollback-a-transaction"></a>Passaggio 4: eseguire il rollback di una transazione  
  
In questo esempio di codice viene illustrato l'utilizzo delle transazioni in cui è possibile:  
  
* Inizia una transazione  
* Inserire una riga di dati  
* Eseguire il rollback della transazione per annullare l'inserimento  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("BEGIN TRANSACTION")  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, CURRENT_TIMESTAMP)")  
    conn.rollback()  
    conn.close()
```  
    
  ## <a name="next-steps"></a>Passaggi successivi  
  
Per ulteriori informazioni, vedere il [centro per sviluppatori Python](https://azure.microsoft.com/develop/python/).
