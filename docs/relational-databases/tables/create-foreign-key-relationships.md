---
title: Creare relazioni di chiave esterna | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], creating
ms.assetid: 867a54b8-5be4-46e6-9702-49ae6dabf67c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a8277582639ebb5ae507c320c38f9ffbe7e0da43
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019537"
---
# <a name="create-foreign-key-relationships"></a>Creare relazioni di chiave esterna
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  > [!div class="nextstepaction"]
  > [Condividi il feedback sul sommario della documentazione SQL](https://aka.ms/sqldocsurvey)

  In questo argomento si illustra come creare relazioni di chiave esterna in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Una relazione tra due tabelle consente di stabilire un'associazione tra le righe di una tabella e le righe di un'altra tabella.    
     
##  <a name="BeforeYouBegin"></a> Prima di iniziare Limitazioni e restrizioni
 
-   Un vincolo di chiave esterna può anche non essere collegato esclusivamente al vincolo di chiave primaria di un'altra tabella. Può infatti essere definito in modo da fare riferimento alle colonne di un vincolo UNIQUE in un'altra tabella.    
    
-   I valori diversi da NULL immessi nella colonna di un vincolo FOREIGN KEY devono essere presenti nella colonna a cui viene fatto riferimento. In caso contrario, viene restituito un messaggio di errore di violazione della chiave esterna. Per assicurarsi che tutti i valori di un vincolo di chiave esterna composto vengano verificati, specificare NOT NULL in tutte le colonne coinvolte.    
    
-   I vincoli FOREIGN KEY possono fare riferimento solo a tabelle di un singolo database nello stesso server. L'integrità referenziale tra database diversi deve essere implementata tramite trigger. Per altre informazioni, vedere [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).    
    
-   I vincoli FOREIGN KEY possono fare riferimento a un'altra colonna nella stessa tabella. Questo tipo di vincolo viene definito autoreferenziale.    
    
-   Un vincolo FOREIGN KEY specificato a livello di colonna può includere una sola colonna di riferimento. Il tipo di dati di tale colonna deve essere uguale al tipo di dati della colonna in cui viene definito il vincolo.    
    
-   Un vincolo FOREIGN KEY specificato a livello di tabella deve includere lo stesso numero di colonne di riferimento di quelle presenti nell'elenco di colonne del vincolo. Il tipo di dati di ogni colonna di riferimento deve inoltre essere uguale a quello della colonna corrispondente nell'elenco di colonne.    
    
-   Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non prevede un limite predefinito per il numero di vincoli FOREIGN KEY che possono essere inclusi in una tabella e che fanno riferimento ad altre tabelle o per il numero di vincoli FOREIGN KEY di proprietà di altre tabelle che fanno riferimento a una tabella specifica. Il numero effettivo di vincoli FOREIGN KEY che è possibile usare, tuttavia, è limitato dalla configurazione hardware e dalla progettazione del database e dell'applicazione.  Una tabella può fare riferimento a un massimo di 253 altre tabelle e colonne come chiavi esterne (riferimenti in uscita). [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] incrementa da 253 a 10.000 il limite per il numero di altre tabelle e colonne che possono fare riferimento alle colonne in una singola tabella (riferimenti in ingresso).  (richiede almeno il livello di compatibilità 130). All'incremento vengono applicate le seguenti restrizioni:    
    
    -   I riferimenti di chiave esterna maggiori di 253 sono supportati per le operazioni DELETE e UPDATE DML. Le operazioni MERGE non sono supportate.    
    
    -   Una tabella con un riferimento di chiave esterna a se stessa è comunque limitata a 253 riferimenti di chiave esterna.    
    
    -   I riferimenti di chiave esterna maggiori di 253 non sono attualmente disponibili per gli indici columnstore, le tabelle ottimizzate per la memoria o l'estensione database.    
    
-   I vincoli FOREIGN KEY non vengono applicati nelle tabelle temporanee.    
    
-   Se si definisce una chiave esterna su una colonna di tipo CLR definito dall'utente, è necessario che l'implementazione del tipo supporti l'ordinamento binario. Per altre informazioni, vedere [Tipi CLR definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).    
    
-   Una colonna di tipo **varchar(max)** può far parte di un vincolo FOREIGN KEY solo se anche la chiave primaria a cui fa riferimento è definita come tipo **varchar(max)**.    
    

    
##   <a name="permissions"></a>Permissions    
 Per la creazione di una nuova tabella con una chiave esterna è richiesta l'autorizzazione CREATE TABLE per il database e l'autorizzazione ALTER per lo schema in cui viene creata la tabella.    
    
 Per la creazione di una chiave esterna in una tabella esistente è richiesta l'autorizzazione ALTER per la tabella.    
       
    
## <a name="create-a-foreign-key-relationship-in-table-designer"></a>Creare una relazione di chiave esterna in Progettazione tabelle 
####  <a name="using-sql-server-management-studio"></a>Utilizzo di SQL Server Management Studio    
    
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sulla tabella che si troverà sul lato chiave esterna della relazione e scegliere **Progetta**.    
    
     La tabella verrà aperta in **Progettazione tabelle**.    
    
2.  Scegliere **Relazioni** dal menu **Progettazione tabelle**.    
    
3.  Nella finestra di dialogo **Relazioni chiavi esterne** fare clic su **Aggiungi**.    
    
     La relazione verrà visualizzata nell'elenco **Relazione selezionata** con un nome specificato dal sistema nel formato FK_\<*nometabella*>_\<*nometabella*>, dove *nometabella* è il nome della tabella di chiave esterna.    
    
4.  Fare clic sulla relazione nell'elenco **Relazione selezionata** .    
    
5.  Fare clic su **Specifica tabelle e colonne** nella griglia a destra e quindi sul pulsante con i puntini di sospensione (**...**) a destra della proprietà.    
    
6.  Nella finestra di dialogo **Tabelle e colonne** selezionare dall'elenco a discesa **Chiave primaria** la tabella che si troverà sul lato chiave primaria della relazione.    
    
7.  Nella griglia sottostante selezionare le colonne che contribuiranno alla chiave primaria della tabella. Nella cella adiacente alla sinistra di ciascuna colonna selezionare la corrispondente colonna chiave esterna della tabella di chiave esterna.    
    
     **Progettazione tabelle** suggerisce automaticamente un nome da assegnare alla relazione. Per specificare un nome diverso, modificare il contenuto della casella di testo **Nome relazione** .    
    
8.  Scegliere **OK** per creare la relazione.    
       
## <a name="create-a-foreign-key-in-a-new-table"></a>Creare una chiave esterna in una nuova tabella  
####  <a name="using-transact-sql"></a>Utilizzo di Transact-SQL   
    
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].    
    
2.  Sulla barra Standard fare clic su **Nuova query**.    
    
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**. Nell'esempio si crea una tabella e si definisce un vincolo di chiave esterna nella colonna `TempID` alla quale fa riferimento la colonna `SalesReasonID` nella tabella `Sales.SalesReason` . Le clausole ON DELETE CASCADE e ON UPDATE CASCADE vengono utilizzate per garantire che le modifiche apportate alla tabella `Sales.SalesReason` vengano propagate automaticamente alla tabella `Sales.TempSalesReason` .    
    
    ```    
    USE AdventureWorks2012;    
    GO    
    CREATE TABLE Sales.TempSalesReason (TempID int NOT NULL, Name nvarchar(50),     
    CONSTRAINT PK_TempSales PRIMARY KEY NONCLUSTERED (TempID),     
    CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)     
        REFERENCES Sales.SalesReason (SalesReasonID)     
        ON DELETE CASCADE    
        ON UPDATE CASCADE    
    );
    GO    
    
    ```    
    
## <a name="create-a-foreign-key-in-an-existing-table"></a>Creare una chiave esterna in una tabella esistente 
#### <a name="using-transact-sql"></a>Utilizzo di Transact-SQL   
    
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].    
    
2.  Sulla barra Standard fare clic su **Nuova query**.    
    
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**. Nell'esempio si crea una chiave esterna nella colonna `TempID` e si fa riferimento alla colonna `SalesReasonID` nella tabella `Sales.SalesReason`.    
    
    ```    
    USE AdventureWorks2012;    
    GO    
    ALTER TABLE Sales.TempSalesReason     
    ADD CONSTRAINT FK_TempSales_SalesReason FOREIGN KEY (TempID)     
        REFERENCES Sales.SalesReason (SalesReasonID)     
        ON DELETE CASCADE    
        ON UPDATE CASCADE    
    ;    
    GO    
    
    ```    
    
     Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md), [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) e [table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md).    
    
  
