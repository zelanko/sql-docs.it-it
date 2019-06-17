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
manager: jroth
ms.openlocfilehash: e8f4c34c1b6b945c28193a549a06546ec952a5d9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780370"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Passaggio 3: Modello di verifica per la connessione a SQL tramite pyodbc

In questo esempio deve essere considerato un modello di verifica solo.  Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft.  

**Eseguire script di esempio riportato di seguito** creare un file denominato test.py e aggiungere ogni frammento di codice mentre si procede. 

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
  
  
## <a name="step-2--execute-query"></a>Passaggio 2: Eseguire query  
  
Il cursor.executefunction utilizzabile per recuperare un set di risultati da una query sul Database SQL. Questa funzione accetta qualsiasi query essenzialmente e restituisce un set di risultati che può eseguire l'iterazione tramite l'uso di fetchone)
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>Passaggio 3: Inserire una riga  
  
In questo esempio illustra come eseguire un' [inserire](../../../t-sql/statements/insert-transact-sql.md) istruzione in modo sicuro, passare i parametri che proteggono l'applicazione dal [attacchi SQL injection](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) valore.    
  
  
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
  
Per altre informazioni, vedere la [Centro per sviluppatori Python](https://azure.microsoft.com/develop/python/).
