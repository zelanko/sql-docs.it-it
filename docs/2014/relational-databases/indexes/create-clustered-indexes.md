---
title: Creare indici cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index creation [SQL Server], clustered indexes
- clustered indexes, creating
- clustered indexes, PRIMARY KEY constraint
- clustered indexes, UNIQUE constraint
- indexes [SQL Server], clustered
ms.assetid: 47148383-c2c7-4f08-a9e4-7016bf2d1d13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3cea4731ee665e401429679d764832247b2a2242
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63155376"
---
# <a name="create-clustered-indexes"></a>Creare indici cluster
  È possibile creare indici cluster nelle tabelle di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A parte poche eccezioni, ogni tabella deve disporre di un indice cluster. Oltre a migliorare le prestazioni di esecuzione delle query, un indice può essere ricompilato o riorganizzato su richiesta per controllare la frammentazione della tabella. È inoltre possibile creare un indice cluster in una vista. Gli indici cluster sono descritti nell'argomento [Descrizione di indici cluster e non cluster](clustered-and-nonclustered-indexes-described.md).  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Modalità di implementazione tipiche](#Implementations)  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un indice cluster in una tabella tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="typical-implementations"></a><a name="Implementations"></a> Modalità di implementazione tipiche  
 Gli indici cluster vengono implementati nei modi seguenti:  
  
-   **Vincoli PRIMARY KEY e UNIQUE**  
  
     Quando si crea un vincolo PRIMARY KEY, viene automaticamente creato un indice cluster univoco nella colonna o nelle colonne se nella tabella non esiste già un indice cluster e non si specifica un indice non cluster univoco. La colonna chiave primaria non può supportare i valori NULL.  
  
     Quando si crea un vincolo UNIQUE, viene creato un indice non cluster univoco per applicare un vincolo UNIQUE per impostazione predefinita. È possibile specificare un indice cluster univoco se nella tabella non ne esiste già uno.  
  
     A un indice creato come parte del vincolo viene automaticamente assegnato lo stesso nome del vincolo. Per ulteriori informazioni, vedere [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md) e [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
-   **Indice indipendente da un vincolo**  
  
     È possibile creare un indice cluster in una colonna diversa dalla colonna chiave primaria a condizione che sia stato specificato un vincolo di chiave primaria non cluster.  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Quando viene creata una struttura dell'indice cluster, è necessario spazio su disco per la struttura vecchia (origine) e per quella nuova (destinazione) nei file e filegroup appropriati. La struttura vecchia non viene deallocata fino a quando non viene eseguito il commit della transazione completa. Potrebbe inoltre essere necessario spazio su disco aggiuntivo temporaneo per l'ordinamento. Per altre informazioni, vedere [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md).  
  
-   Se viene creato un indice cluster in un heap con molti indici non cluster esistenti, tutti gli indici non cluster devono essere ricompilati in modo che contengano il valore della chiave di clustering anziché l'identificatore di riga (RID, Row Identifier). In modo analogo, se viene eliminato un indice cluster di una tabella con molti indici non cluster, tutti gli indici non cluster verranno ricompilati durante l'operazione DROP. Per tabelle di grandi dimensioni, la ricostruzione degli indici potrebbe richiedere una notevole quantità di tempo.  
  
     La strategia ottimale per la compilazione di indici per tabelle di grandi dimensioni consiste nel compilare innanzitutto l'indice cluster e quindi eventuali indici non cluster. Quando si creano gli indici in tabelle esistenti, impostare l'opzione ONLINE su ON. In questo modo, i blocchi di lunga durata a livello di tabella non vengono mantenuti, al fine di consentire l'esecuzione di query o l'aggiornamento della tabella sottostante. Per altre informazioni, vedere [Perform Index Operations Online](perform-index-operations-online.md).  
  
-   La chiave di indice di un indice cluster non può contenere colonne di tipo `varchar` con dati esistenti nell'unità di allocazione ROW_OVERFLOW_DATA. Se viene creato un indice cluster in una colonna `varchar` e i dati esistenti si trovano nell'unità di allocazione IN_ROW_DATA, le azioni di inserimento o aggiornamento successive eseguite nella colonna che comporterebbero lo spostamento dei dati all'esterno di righe non verranno eseguite correttamente. Per ottenere informazioni sulle tabelle che potrebbero contenere dati di overflow della riga, usare la funzione a gestione dinamica [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per la tabella o la vista. L'utente deve essere un membro del ruolo predefinito del server **sysadmin** o dei ruoli predefiniti del database **db_ddladmin** e **db_owner** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-create-a-clustered-index-by-using-object-explorer"></a>Per creare un indice cluster tramite Esplora oggetti  
  
1.  In Esplora oggetti espandere la tabella in cui si desidera creare un indice cluster.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Indici**, scegliere **Nuovo indice** e selezionare **Indice cluster**.  
  
3.  Nella pagina **Generale** della finestra di dialogo **Nuovo indice** immettere il nome del nuovo indice nella casella **Nome indice** .  
  
4.  In **Colonne chiave indice**fare clic su **Aggiungi**.  
  
5.  Nella finestra di dialogo **Seleziona colonne da**_table_name_ Selezionare la casella di controllo della colonna della tabella da aggiungere all'indice cluster.  
  
6.  Fare clic su **OK**.  
  
7.  Nella finestra di dialogo **Nuovo indice** fare clic su **OK**.  
  
#### <a name="to-create-a-clustered-index-by-using-the-table-designer"></a>Per creare un indice cluster tramite Progettazione tabelle  
  
1.  In Esplora oggetti espandere il database in cui si desidera creare una tabella con un indice cluster.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Tabelle** e scegliere **Nuova tabella**.  
  
3.  Creare una nuova tabella con il metodo tradizionale. Per altre informazioni, vedere [Creare tabelle &#40;Motore di database&#41;](../tables/create-tables-database-engine.md).  
  
4.  Fare clic con il pulsante destro del mouse sulla nuova tabella creata e scegliere **Progetta**.  
  
5.  Scegliere **Indici/chiavi** nel menu **Progettazione tabelle**.  
  
6.  Nella finestra di dialogo **Indici/chiavi** fare clic su **Aggiungi**.  
  
7.  Selezionare il nuovo indice dalla casella di testo **Chiave o indice primario/univoco selezionato** .  
  
8.  Nella griglia selezionare **Crea come CLUSTERED**, quindi selezionare **Sì** dall'elenco a discesa a destra della proprietà.  
  
9. Fare clic su **Close**.  
  
10. Nel menu **File** scegliere **Salva**_table_name_.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-create-a-clustered-index"></a>Per creare un indice cluster  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Create a new table with three columns.  
    CREATE TABLE dbo.TestTable  
        (TestCol1 int NOT NULL,  
         TestCol2 nchar(10) NULL,  
         TestCol3 nvarchar(50) NULL);  
    GO  
    -- Create a clustered index called IX_TestTable_TestCol1  
    -- on the dbo.TestTable table using the TestCol1 column.  
    CREATE CLUSTERED INDEX IX_TestTable_TestCol1   
        ON dbo.TestTable (TestCol1);   
    GO  
    ```  
  
 Per altre informazioni, vedere [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di chiavi primarie](../tables/create-primary-keys.md)   
 [Creare vincoli UNIQUE](../tables/create-unique-constraints.md)  
  
  
