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
ms.openlocfilehash: c1dfce515eeadbdbaf1fd96e6dcf1a08cd536ab5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "74200453"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>Passaggio 3: Modello di verifica per la connessione a SQL con pymssql
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

Questo esempio deve essere considerato solo un modello di verifica.  Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft.  
  
## <a name="step-1--connect"></a>Passaggio 1:  Connessione  
  
Per connettersi al database SQL viene usata la funzione [pymssql.connect](https://pypi.org/project/pymssql/) .  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>Passaggio 2:  Eseguire la query  
  
Per recuperare un set di risultati di una query sul database SQL è possibile usare la funzione [cursor.execute](https://pypi.org/project/pymssql/) . Questa funzione accetta essenzialmente qualsiasi query e restituisce un set di risultati su cui è possibile eseguire l'iterazione mediante [cursor.fetchone()](https://pypi.org/project/pymssql/).  
  
  
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
  
## <a name="step-3--insert-a-row"></a>Passaggio 3:  Inserire una riga  
  
Questo esempio illustra come eseguire un'istruzione [INSERT](../../../t-sql/statements/insert-transact-sql.md) in modo sicuro e come passare i parametri che proteggono l'applicazione da attacchi [SQL injection](../../../relational-databases/tables/primary-and-foreign-key-constraints.md).    
  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>Passaggio 4:  Eseguire il rollback di una transazione  
  
Questo esempio di codice illustra l'uso di transazioni con le operazioni seguenti:  
  
* Avvio di una transazione  
* Inserimento di una riga di dati  
* Rollback della transazione per annullare l'inserimento  
  
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
  
Per ulteriori informazioni, vedere il [Centro per sviluppatori di Python](https://azure.microsoft.com/develop/python/).
