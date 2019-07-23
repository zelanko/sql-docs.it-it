---
title: 'Passaggio 3: Modello di verifica per la connessione a SQL tramite pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87faa60456dd6d03f23d45346ab0dd103dc07c82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992512"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Passaggio 3: Modello di verifica per la connessione a SQL tramite pyodbc

Questo esempio deve essere considerato solo un modello di prova.  Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft.  

**Esegui script di esempio di seguito**  Creare un file denominato test.py e aggiungere ogni frammento di codice man mano che si procede. 

```
> python test.py
```
  
## <a name="step-1--connect"></a>Passaggio 1: connettersi  
  
```python

import pyodbc 
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="step-2--execute-query"></a>Passaggio 2: eseguire la query  
  
Cursor. ExecuteFunction può essere utilizzato per recuperare un set di risultati da una query sul database SQL. Questa funzione accetta essenzialmente qualsiasi query e restituisce un set di risultati su cui è possibile eseguire l'iterazione con l'uso di Cursor. fetchOne ()
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>Passaggio 3: inserire una riga  
  
In questo esempio si vedrà come eseguire un'istruzione [Insert](../../../t-sql/statements/insert-transact-sql.md) in modo sicuro, passare i parametri che proteggono l'applicazione da un valore [SQL injection](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) .    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  
  `      
  ## <a name="next-steps"></a>Passaggi successivi  
  
Per ulteriori informazioni, vedere il [centro per sviluppatori Python](https://azure.microsoft.com/develop/python/).
