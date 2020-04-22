---
title: 'Passaggio 3: Connessione a SQL tramite pyodbc'
description: Il passaggio 3 è un modello di prova che illustra come è possibile connettersi a SQL Server usando Python e pyODBC. Gli esempi di base illustrano la selezione e l'inserimento dei dati.
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: arob98
ms.author: angrobe
ms.openlocfilehash: 971f89f9748ab8f31c234f872e817b0b474dcbe0
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528475"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Passaggio 3: Modello di verifica per la connessione a SQL tramite pyodbc

Questo esempio è un modello di verifica. Il codice di esempio è semplificato per maggiore chiarezza e non rappresenta necessariamente le procedure consigliate da Microsoft.  

Per iniziare, eseguire lo script di esempio seguente. Creare un file denominato test.py e aggiungere ogni frammento di codice man mano che si procede. 

```
> python test.py
```
  
## <a name="connect"></a>Connessione  
  
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
  
  
## <a name="run-query"></a>Esegui query  
  
Per recuperare un set di risultati di una query sul database SQL è possibile usare la funzione cursor.execute. Questa funzione accetta una query e restituisce un set di risultati su cui è possibile eseguire l'iterazione tramite cursor.fetchone()
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="insert-a-row"></a>Inserire una riga  
  
Questo esempio illustra come eseguire un'istruzione [INSERT](../../../t-sql/statements/insert-transact-sql.md) in modo sicuro e come passare i parametri che proteggono l'applicazione da attacchi [SQL injection](../../../relational-databases/tables/primary-and-foreign-key-constraints.md).    
  
  
```python
#Sample insert query
cursor.execute("""
INSERT INTO SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) 
VALUES (?,?,?,?,?)""",
'SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP) 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print('Inserted Product key is ' + str(row[0]))
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-and-the-connection-string"></a>Azure Active Directory e la stringa di connessione

pyODBC usa Microsoft ODBC Driver for SQL Server.
Se la versione del driver ODBC è 17.1 o successiva, è possibile usare la modalità interattiva di Azure Active Directory del driver ODBC tramite pyODBC.
L'opzione interattiva funziona se Python e pyODBC consentono al driver ODBC di visualizzare la finestra di dialogo. L'opzione è disponibile solo nel sistema operativo Windows. 

### <a name="example-connection-string-for-azure-active-directory-interactive-authentication"></a>Stringa di connessione di esempio per l'autenticazione interattiva di Azure Active Directory

Di seguito è riportata una stringa di connessione di esempio ODBC che specifica l'autenticazione interattiva di Azure Active Directory:

`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

Per altre informazioni sulle opzioni di autenticazione del driver ODBC, vedere [Uso di Azure Active Directory con il driver ODBC](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords).

## <a name="next-steps"></a>Passaggi successivi
  
Per ulteriori informazioni, vedere il [Centro per sviluppatori di Python](https://azure.microsoft.com/develop/python/).
