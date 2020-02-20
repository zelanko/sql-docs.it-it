---
title: 'Passaggio 3: Modello di verifica per la connessione a SQL con pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 10/09/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e241d84ebc60acceafe09b1a9240711a72d2067
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "72798323"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Passaggio 3: Modello di verifica per la connessione a SQL tramite pyodbc

Questo esempio deve essere considerato solo un modello di verifica.  Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft.  

**Eseguire lo script di esempio seguente** Creare un file denominato test.py e aggiungere ogni frammento di codice man mano che si procede. 

```
> python test.py
```
  
## <a name="step-1--connect"></a>Passaggio 1:  Connessione  
  
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
  
  
## <a name="step-2--execute-query"></a>Passaggio 2:  Eseguire la query  
  
Per recuperare un set di risultati di una query sul database SQL è possibile usare la funzione cursor.execute. Questa funzione accetta essenzialmente qualsiasi query e restituisce un set di risultati su cui è possibile eseguire l'iterazione usando cursor.fetchone().
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>Passaggio 3:  Inserire una riga  
  
Questo esempio illustra come eseguire un'istruzione [INSERT](../../../t-sql/statements/insert-transact-sql.md) in modo sicuro e come passare i parametri che proteggono l'applicazione da attacchi [SQL injection](../../../relational-databases/tables/primary-and-foreign-key-constraints.md).    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-aad-and-the-connection-string"></a>Azure Active Directory (AAD) e la stringa di connessione

pyODBC usa Microsoft ODBC Driver for SQL Server.
Se la versione del driver ODBC è 17.1 o successiva, è possibile usare la modalità interattiva di AAD del driver ODBC con pyODBC.
L'opzione interattiva di AAD funziona se Python e pyODBC consentono al driver ODBC di visualizzare la finestra di dialogo.
Questa opzione è disponibile solo nel sistema operativo Windows.

### <a name="example-connection-string-for-aad-interactive-authentication"></a>Esempio di stringa di connessione per l'autenticazione interattiva di AAD

Di seguito è riportato un esempio di stringa di connessione ODBC che specifica l'autenticazione interattiva di AAD:

- `server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

Per informazioni dettagliate sulle opzioni di autenticazione di AAD per il driver ODBC, vedere l'articolo seguente:

- [Uso di Azure Active Directory con ODBC Driver](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords)

## <a name="next-steps"></a>Passaggi successivi
  
Per ulteriori informazioni, vedere il [Centro per sviluppatori di Python](https://azure.microsoft.com/develop/python/).
