---
description: 'Esercitazione di T-SQL: Creare ed eseguire query di oggetti di database'
title: 'Esercitazione di T-SQL: Creare ed eseguire query per oggetti di database | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 9fb8656b-0e4e-4ada-b404-4db4d3eea995
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3a489da04d7a65bf854cebf06e8103e22c1abc12
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88459175"
---
# <a name="lesson-1-create-and-query-database-objects"></a>Lezione 1: Creare ed eseguire query per oggetti di database
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

In questa lezione vengono illustrate le procedure per creare un database, creare in quest'ultimo una tabella, nonché come accedere ai dati della tabella e modificarli. Poiché l'obiettivo di questa lezione è offrire un'introduzione all'uso di [!INCLUDE[tsql](../includes/tsql-md.md)], non verranno usate né descritte le numerose opzioni disponibili per le istruzioni.  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] Le istruzioni possono essere scritte e inviate a [!INCLUDE[ssDE](../includes/ssde-md.md)] nei modi seguenti:  
  
-   Mediante [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. In questa esercitazione si presuppone che venga usato [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], ma è anche possibile usare [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Express, disponibile come download gratuito nell' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=14630).  
  
-   Mediante l' [utilità sqlcmd](../tools/sqlcmd-utility.md).  
  
-   Mediante la connessione da un'applicazione creata dall'utente.  
  
Il codice viene eseguito in [!INCLUDE[ssDE](../includes/ssde-md.md)] nello stesso modo e con le stesse autorizzazioni, indipendentemente dalla modalità di invio delle istruzioni di codice.  
  
Per eseguire le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] in [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], aprire [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] e connettersi a un'istanza di [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)].  

## <a name="prerequisites"></a>Prerequisiti
Per completare questa esercitazione è necessario avere SQL Server Management Studio e l'accesso a un'istanza di SQL Server. 

- Installare [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Se non è disponibile un'istanza di SQL Server, crearne una. Per crearne una, selezionare la piattaforma nei collegamenti seguenti. Se si sceglie Autenticazione SQL, usare le credenziali di accesso di SQL Server.
- **Windows**: [scaricare SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [scaricare SQL Server 2017 in Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

## <a name="create-a-database"></a>Creazione di un database
Analogamente a molte altre istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)], l'istruzione [`CREATE DATABASE`](statements/create-database-transact-sql.md) ha un parametro obbligatorio, ovvero il nome del database. ` CREATE DATABASE` include anche molti parametri facoltativi, ad esempio il percorso su disco in cui si vogliono inserire i file del database. Quando si esegue `CREATE DATABASE` senza parametri facoltativi, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa i valori predefiniti per molti di tali parametri.

1.  In una finestra dell'editor di query digitare ma non eseguire il codice seguente:  
  
    ```sql  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  Usare il puntatore per selezionare le parole `CREATE DATABASE`e quindi premere **F1**. Verrà aperto l'argomento relativo all'istruzione `CREATE DATABASE` nella documentazione online di SQL Server. È possibile usare questa tecnica per trovare la sintassi completa di `CREATE DATABASE` e delle altre istruzioni usate in questa esercitazione.  
  
3.  Nell'editor di query premere **F5** per eseguire l'istruzione e creare un database denominato `TestData`.  
  
Quando si crea un database, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esegue una copia del database **model** e le assegna il nome del database specificato. L'operazione dovrebbe richiedere solo alcuni secondi a meno che non si specifichi una dimensione iniziale per il database particolarmente grande come parametro facoltativo.  
  
> [!NOTE]  
> La parola chiave GO separa le istruzioni inviate in un singolo batch. GO è un elemento facoltativo se il batch contiene un'unica istruzione.  

## <a name="create-a-table"></a>Creare una tabella

[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

Per creare una tabella, è necessario specificare un nome per la tabella e i nomi e i tipi di dati di ogni colonna di quest'ultima. È inoltre consigliabile indicare se sono consentiti valori Null in ogni colonna. Per creare una tabella è necessario avere l'autorizzazione `CREATE TABLE` e l'autorizzazione `ALTER SCHEMA` per lo schema che conterrà la tabella. Il ruolo predefinito del database [`db_ddladmin`](../relational-databases/security/authentication-access/database-level-roles.md) dispone di tali autorizzazioni.  
  
La maggior parte delle tabelle dispone di una chiave primaria costituita da una o più colonne. La chiave primaria è sempre univoca. In [!INCLUDE[ssDE](../includes/ssde-md.md)] è applicata la limitazione per la quale nessun valore di chiave primaria può essere ripetuto nella tabella.  
  
Per un elenco di tipi di dati e collegamenti alle relative descrizioni, vedere [Tipi di dati &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
> [!NOTE]  
> È possibile installare [!INCLUDE[ssDE](../includes/ssde-md.md)] in modo che venga fatta o meno distinzione tra maiuscole e minuscole. Se in [!INCLUDE[ssDE](../includes/ssde-md.md)] tale distinzione è rilevante, i nomi degli oggetti devono essere sempre indicati con le lettere maiuscole e minuscole appropriate. Una tabella denominata OrderData è ad esempio diversa da una tabella denominata ORDERDATA. Se nel [!INCLUDE[ssDE](../includes/ssde-md.md)] non viene fatta distinzione tra maiuscole e minuscole, tali nomi sono considerati equivalenti e quindi il nome stesso può essere utilizzato una sola volta.  
  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>Connessione dell'editor di query al database TestData  

Nella finestra dell'editor di query digitare ed eseguire il codice seguente per connettersi al database `TestData` .  
  
  ```sql  
  USE TestData  
  GO  
  ```  
  
### <a name="create-the-table"></a>Creare la tabella

Nella finestra dell'editor di query digitare ed eseguire il codice seguente per creare una tabella denominata `Products`. Le colonne nella tabella vengono denominate `ProductID`, `ProductName`, `Price`e `ProductDescription`. La colonna `ProductID` rappresenta la chiave primaria della tabella. `int`, `varchar(25)`, `money`e `varchar(max)` sono tutti tipi di dati. Le uniche colonne che possono non contenere dati quando viene inserita o modificata un riga sono `Price` e `ProductionDescription` . Questa istruzione contiene un elemento facoltativo (`dbo.`) che corrisponde a uno schema. Lo schema rappresenta l'oggetto di database a cui appartiene la tabella. Se si è un amministratore, `dbo` è lo schema predefinito. `dbo` corrisponde al proprietario del database.  
  
  ```sql  
  CREATE TABLE dbo.Products  
     (ProductID int PRIMARY KEY NOT NULL,  
     ProductName varchar(25) NOT NULL,  
     Price money NULL,  
     ProductDescription varchar(max) NULL)  
  GO  
 ```  

## <a name="insert-and-update-data-in-a-table"></a>Inserire e aggiornare dati in una tabella
Dopo aver creato la tabella **Products** è possibile inserirvi dati con l'istruzione INSERT. Dopo aver inserito i dati, si procederà alla modifica del contenuto di una riga mediante l'istruzione UPDATE. Per limitare l'operazione di aggiornamento a una sola riga verrà utilizzata la clausola WHERE dell'istruzione UPDATE. Le quattro istruzioni immetteranno i dati seguenti.  
  
|ProductID|ProductName|Prezzo|ProductDescription|  
|-------------|---------------|---------|----------------------|  
|1|Clamp|12.48|Workbench clamp|  
|50|Screwdriver|3,17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3 mm Bracket|0.52||  
  
La sintassi di base è INSERT, nome tabella, elenco colonne, VALUES, a cui segue quindi un elenco dei valori da inserire. I due trattini davanti a una riga indicano che si tratta di un commento il cui testo verrà ignorato dal compilatore. In questo caso il commento descrive una variazione consentita della sintassi.  
  
### <a name="insert-data-into-a-table"></a>Inserire dati in una tabella  
  
1.  Eseguire l'istruzione seguente per inserire una riga nella tabella `Products` creata nell'attività precedente.
  
   ```sql 
   -- Standard syntax  
   INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
       VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
   GO   
   ```  

   > [!NOTE]
   > Se l'inserimento ha esito positivo, procedere con il passaggio successivo.
   >
   > Se l'inserimento non riesce, è possibile che la tabella `Product` includa già una riga con tale ID prodotto. Per continuare, eliminare tutte le righe della tabella e ripetere il passaggio precedente. [`TRUNCATE TABLE`](statements/truncate-table-transact-sql.md) elimina tutte le righe nella tabella. 
   >
   > Eseguire il comando seguente per eliminare tutte le righe nella tabella:
   > 
   > ```sql
   >TRUNCATE TABLE TestData.dbo.Products;
   > GO
   >```
   >
   > Dopo aver troncato la tabella, ripetere il comando `INSERT` in questo passaggio.

2.  L'istruzione seguente illustra come modificare l'ordine in cui vengono specificati i parametri scambiando la posizione di `ProductID` e `ProductName` in entrambi gli elenchi di campi (tra parentesi) e nell'elenco dei valori.  
  
   ```sql  
   -- Changing the order of the columns  
   INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
       VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
   GO    
   ```  
  
3.  L'istruzione seguente illustra che i nomi delle colonne sono facoltativi a condizione che i valori siano elencati nell'ordine corretto. Questa sintassi comune non è tuttavia consigliata poiché potrebbe rendere il codice di difficile comprensione per gli altri utenti. `NULL` viene specificato per la colonna `Price` perché il prezzo del prodotto corrispondente non è ancora noto.  
  
   ```sql  
   -- Skipping the column list, but keeping the values in order  
   INSERT dbo.Products  
       VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
   GO  
  ```  
  
4.  Il nome dello schema è facoltativo a condizione che si acceda per la modifica a una tabella inclusa nello schema predefinito. Poiché la colonna `ProductDescription` supporta valori Null e non viene specificato alcun valore, il nome e il valore della colonna `ProductDescription` verranno eliminati completamente dall'istruzione.  
  
   ```sql  
   -- Dropping the optional dbo and dropping the ProductDescription column  
   INSERT Products (ProductID, ProductName, Price)  
       VALUES (3000, '3 mm Bracket', 0.52)  
   GO  
   ```  
  
### <a name="update-the-products-table"></a>Aggiornare la tabella dei prodotti  
Digitare ed eseguire l'istruzione `UPDATE` seguente per modificare il valore `ProductName` del secondo prodotto da `Screwdriver`in `Flat Head Screwdriver`.  
  
  ```sql  
  UPDATE dbo.Products  
      SET ProductName = 'Flat Head Screwdriver'  
      WHERE ProductID = 50  
  GO  
  ```  

## <a name="read-data-from-a-table"></a>Leggere dati da una tabella
Utilizzare l'istruzione SELECT per leggere i dati archiviati in una tabella. L'istruzione SELECT è una delle più importanti istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] e la relativa sintassi presenta numerose variazioni. Ai fini di questa esercitazione ne verranno utilizzate cinque semplici versioni.  
  
### <a name="read-the-data-in-a-table"></a>Leggere i dati di una tabella  
  
1.  Per leggere i dati archiviati nella tabella `Products` , digitare ed eseguire le istruzioni seguenti.  
  
  ```sql 
  -- The basic syntax for reading data from a single table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
  GO  
  ```  
  
2.  È possibile usare un asterisco (`*`) per selezionare tutte le colonne nella tabella. L'asterisco è per le query ad hoc. Specificare l'elenco delle colonne nel codice permanente in modo che l'istruzione restituisca le colonne previste anche se viene successivamente aggiunta una nuova colonna alla tabella.  
  
  ```sql  
  -- Returns all columns in the table  
  -- Does not use the optional schema, dbo  
  SELECT * FROM Products  
  GO   
  ```  
  
3.  È possibile omettere le colonne che non si desidera vengano restituite. Le colonne verranno restituite nell'ordine specificato.  
  
  ```sql  
  -- Returns only two of the columns from the table  
  SELECT ProductName, Price  
      FROM dbo.Products  
  GO    
  ```  
  
4.  Utilizzare una clausola `WHERE` per limitare le righe restituite.  
  
  ``` sql 
  -- Returns only two of the records in the table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
      WHERE ProductID < 60  
  GO    
  ```  
  
5.  È possibile utilizzare i valori nelle colonne quando vengono restituiti. L'esempio seguente esegue un'operazione matematica sulla colonna `Price` . Alle colonne modificate in questo modo non verrà assegnato un nome a meno che non se ne specifichi uno utilizzando la parola chiave `AS` .  
  
  ```sql  
  -- Returns ProductName and the Price including a 7% tax  
  -- Provides the name CustomerPays for the calculated column  
  SELECT ProductName, Price * 1.07 AS CustomerPays  
      FROM dbo.Products  
  GO  
  ```  
  
### <a name="useful-functions-in-a-select-statement"></a>Funzioni utili in un'istruzione SELECT  
Per informazioni su alcune funzioni che consentono di utilizzare i dati in un'istruzione SELECT, vedere gli argomenti seguenti:  

:::row:::
    :::column:::
        [Funzioni per i valori stringa &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)
    :::column-end:::
    :::column:::
        [Funzioni e tipi di dati di data e ora &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [Funzioni matematiche &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)
    :::column-end:::
    :::column:::
        [Funzioni per i valori text e image &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)
    :::column-end:::
:::row-end:::

## <a name="create-views-and-stored-procedures"></a>Creare viste e stored procedure
Una vista è costituita da un'istruzione SELECT, mentre una stored procedure da una o più istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] eseguite in un batch.  
  
Sulle viste è possibile eseguire query come con le tabelle, ad eccezione del fatto che le viste non accettano parametri. Le stored procedure sono più complesse delle viste e possono avere parametri di input e output, nonché contenere istruzioni per controllare il flusso del codice, ad esempio istruzioni IF e WHILE. È consigliabile dal punto di vista della programmazione utilizzare le stored procedure per tutte le azioni ripetitive sul database.  
  
In questo esempio si userà CREATE VIEW per creare una vista che seleziona solo due delle colonne incluse nella tabella **Products** . Si utilizzerà quindi CREATE PROCEDURE per creare una stored procedure che accetta un parametro di prezzo e restituisce solo i prodotti il cui costo è inferiore al valore di tale parametro.  
  
### <a name="create-a-view"></a>Creare una visualizzazione  
  
Eseguire l'istruzione seguente per creare un vista che esegue un'istruzione SELECT e restituisce i nomi e i prezzi dei prodotti.  
  
  ```sql  
  CREATE VIEW vw_Names  
     AS  
     SELECT ProductName, Price FROM Products;  
  GO    
  ```  
  
### <a name="test-the-view"></a>Test della vista  
  
Le viste vengono utilizzate in modo analogo alle tabelle. Utilizzare un'istruzione `SELECT` per accedere a una vista.  
  
  ```sql  
  SELECT * FROM vw_Names;  
  GO   
  ```  
  
### <a name="create-a-stored-procedure"></a>Creare una stored procedure  
  
L'istruzione seguente crea una stored procedure denominata `pr_Names`che accetta un parametro di input denominato `@VarPrice` con tipo di dati `money`. La stored procedure visualizza il testo `Products less than` concatenata al parametro di input modificato da tipo di dati `money` in tipo di dati carattere `varchar(10)` . La procedura esegue quindi un'istruzione `SELECT` sulla vista, passando il parametro di input come parte della clausola `WHERE` . Ciò restituisce tutti i prodotti il cui costo è inferiore al valore del parametro di input.  
  
  ```sql  
  CREATE PROCEDURE pr_Names @VarPrice money  
     AS  
     BEGIN  
        -- The print statement returns text to the user  
        PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
        -- A second statement starts here  
        SELECT ProductName, Price FROM vw_Names  
              WHERE Price < @varPrice;  
     END  
  GO    
  ```  
  
### <a name="test-the-stored-procedure"></a>Test della stored procedure  
  
Per testare la stored procedure, digitare ed eseguire l'istruzione seguente. La procedura restituirà i nomi di due prodotti immessi nella tabella `Products` nella lezione 1 con prezzo inferiore a `10.00`.  
  
  ```sql  
  EXECUTE pr_Names 10.00;  
  GO  
  ```  

## <a name="next-steps"></a>Passaggi successivi
L'articolo successivo illustra come configurare autorizzazioni per gli oggetti di database. Gli oggetti creati nella lezione 1 verranno usati anche nella lezione 2. 

Per altre informazioni, vedere l'articolo successivo:
> [!div class="nextstepaction"]
> [Passaggi successivi](../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
  
  
