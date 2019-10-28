---
title: Popolare gli indici full-text | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- index populations [full-text search]
- incremental populations [full-text search]
- populations [full-text search]
- full-text search [SQL Server], populations
- crawls [full-text search]
- automatic full-text index updates
- change tracking-based populations [full-text search]
- manual updates [full-text search]
- manual populations [full-text search]
- auto populations [full-text search]
- full-text indexes [SQL Server], key column
- full populations [full-text search]
- full-text indexes [SQL Server], populations
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 52fc7d3d43c1f0adcf7ab94d78cf301254a9a18d
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903875"
---
# <a name="populate-full-text-indexes"></a>Popolamento degli indici full-text
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La creazione e la gestione di un indice full-text comporta il popolamento dell'indice con un processo denominato *popolamento* , noto anche con il termine *ricerca per indicizzazione*.  
  
##  <a name="types"></a> Types of population  
Un indice full-text supporta i tipi di popolamento seguenti:
-   Popolamento **completo**
-   Popolamento automatico o manuale basato sul **rilevamento delle modifiche**
-   Popolamento incrementale basato su **timestamp**
  
## <a name="full-population"></a>Popolamento completo  
 Durante un popolamento completo, vengono compilate voci di indice per tutte le righe di una tabella o di una vista indicizzata. Durante un popolamento completo di un indice full-text, vengono compilate voci di indice per tutte le righe di una tabella di base o di una vista indicizzata.  
  
Per impostazione predefinita, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un nuovo indice full-text viene popolato completamente non appena viene creato.
-   D'altra parte un popolamento completo può richiedere una quantità significativa di risorse. Di conseguenza, quando si crea un indice full-text durante periodi di intensa attività è spesso consigliabile rimandare il popolamento completo a un periodo di attività meno intensa, in particolare se la tabella di base di un indice full-text è di grandi dimensioni.
-   Tuttavia, il catalogo full-text a cui appartiene l'indice non può essere usato finché non vengono popolati tutti i relativi indici full-text.

Per creare un indice full-text senza popolarlo immediatamente, specificare la clausola `CHANGE_TRACKING OFF, NO POPULATION` nell'istruzione `CREATE FULLTEXT INDEX`. Se si specifica `CHANGE_TRACKING MANUAL`, il motore di ricerca full-text non popola il nuovo indice full-text finché non viene eseguita l'istruzione `ALTER FULLTEXT INDEX` usando la clausola `START FULL POPULATION` o `START INCREMENTAL POPULATION`. 

### <a name="example---create-a-full-text-index-without-running-a-full-population"></a>Esempio: creare un indice full-text senza eseguire un popolamento completo  
 Nell'esempio seguente viene creato un indice full-text nella tabella `Production.Document` del database di esempio `AdventureWorks` . Questo esempio usa `WITH CHANGE_TRACKING OFF, NO POPULATION` per ritardare il popolamento completo iniziale.  
  
```sql
CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
CREATE FULLTEXT CATALOG AW_Production_FTCat;  
CREATE FULLTEXT INDEX ON Production.Document  
(  
    Document                         --Full-text index column name   
        TYPE COLUMN FileExtension    --Name of column that contains file type information  
        Language 1033                 --1033 is LCID for the English language  
)  
    KEY INDEX ui_ukDoc  
    ON AW_Production_FTCat  
    WITH CHANGE_TRACKING OFF, NO POPULATION;  
GO  
  
```  
  
### <a name="example---run-a-full-population-on-a-table"></a>Esempio: eseguire un popolamento completo in una tabella  
 Nell'esempio seguente viene eseguito un popolamento completo nella tabella `Production.Document` del database di esempio `AdventureWorks` .  
  
```sql
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
   
## <a name="population-based-on-change-tracking"></a>Popolamento basato sul rilevamento delle modifiche
 Facoltativamente, è possibile utilizzare il rilevamento delle modifiche per gestire un indice full-text dopo il popolamento completo iniziale. Al rilevamento delle modifiche è associato un overhead perché in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è presente una tabella nella quale vengono rilevate le modifiche apportate alla tabella di base dopo l'ultimo popolamento. Quando si usa il rilevamento delle modifiche, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene mantenuto un record delle righe della tabella di base o della vista indicizzata modificate tramite aggiornamenti, eliminazioni o inserimenti. Le modifiche apportate ai dati tramite WRITETEXT e UPDATETEXT non vengono riflesse nell'indice full-text e pertanto non vengono registrate dalla funzione di rilevamento delle modifiche.  
  
> [!NOTE]  
>  Per le tabelle che contengono una colonna **timestamp** , è possibile usare il popolamento incrementale anziché il rilevamento delle modifiche.  
  
 Quando il rilevamento delle modifiche viene abilitato durante la creazione dell'indice, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue il popolamento completo del nuovo indice full-text subito dopo la creazione. Le modifiche vengono quindi rilevate e propagate all'indice full-text.

### <a name="enable-change-tracking"></a>Abilita rilevamento modifiche
Esistono due tipi di rilevamento delle modifiche:
-   Automatico (opzione `CHANGE_TRACKING AUTO`). Il rilevamento delle modifiche automatico è il comportamento predefinito.
-   Manuale (opzione `CHANGE_TRACKING MANUAL`).   
  
 La modalità di popolamento dell'indice full-text dipende dal tipo di rilevamento delle modifiche:  
  
-   **Popolamento automatico**  
  
     Per impostazione predefinita o se si specifica `CHANGE_TRACKING AUTO`, il motore di ricerca full-text usa il popolamento automatico per l'indice full-text. Al termine del popolamento completo iniziale, le modifiche vengono rilevate man mano che i dati vengono modificati nella tabella di base e le modifiche rilevate vengono propagate automaticamente. L'indice full-text viene aggiornato in background, pertanto le modifiche propagate potrebbero non venire riflesse immediatamente nell'indice.  
  
     **Per avviare il rilevamento delle modifiche con il popolamento automatico**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) ... WITH CHANGE_TRACKING AUTO  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ... SET CHANGE_TRACKING AUTO  
  
    **Esempio: modificare un indice full-text per l'uso del rilevamento delle modifiche automatico**  
    Nell'esempio seguente viene creato un indice full-text della tabella `HumanResources.JobCandidate` del database di esempio `AdventureWorks` per l'utilizzo del rilevamento delle modifiche con il popolamento automatico.  
  
    ```sql  
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
    GO   
    ```  
  
-   **Popolamento manuale**  
  
     Se si specifica CHANGE_TRACKING MANUAL, il motore di ricerca full-text utilizza il popolamento manuale per l'indice full-text. Al termine del popolamento completo iniziale, le modifiche vengono rilevate man mano che i dati vengono modificati nella tabella di base. Non vengono invece propagate nell'indice full-text finché non viene eseguita un'istruzione ALTER FULLTEXT INDEX ... START UPDATE POPULATION . Per chiamare questa istruzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] periodicamente, è possibile utilizzare [!INCLUDE[tsql](../../includes/tsql-md.md)] Agent.  
  
     **Per avviare il rilevamento delle modifiche con il popolamento manuale**  
  
    -   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) ... WITH CHANGE_TRACKING MANUAL  
  
    -   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ... SET CHANGE_TRACKING MANUAL  
  
    **Esempio: creare un indice full-text con il rilevamento delle modifiche manuale**  
    Nell'esempio seguente viene creato un indice full-text che utilizzerà il rilevamento delle modifiche con popolamento manuale nella tabella `HumanResources.JobCandidate` del database di esempio `AdventureWorks` .  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
    CREATE FULLTEXT CATALOG ft AS DEFAULT;  
    CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
       KEY INDEX ui_ukJobCand   
       WITH CHANGE_TRACKING=MANUAL;  
    GO  
    ```  
  
    **Esempio: eseguire un popolamento manuale**  
    Nell'esempio seguente viene eseguito un popolamento manuale nell'indice full-text con rilevamento delle modifiche della tabella `HumanResources.JobCandidate` del database di esempio `AdventureWorks` .  
  
    ```sql 
    USE AdventureWorks;  
    GO  
    ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
    GO  
    ```
   
### <a name="disable-change-tracking"></a>Disabilitare il rilevamento delle modifiche 
  
-   [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) ... WITH CHANGE_TRACKING OFF  
  
-   [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ... SET CHANGE_TRACKING OFF  
   
  
## <a name="incremental-population-based-on-a-timestamp"></a>Popolamento incrementale basato su timestamp  
 Un popolamento incrementale è un meccanismo alternativo per il popolamento manuale di un indice full-text. Se in una tabella vengono eseguiti molti inserimenti, l'utilizzo del popolamento incrementale può rivelarsi più efficiente dell'utilizzo del popolamento manuale.
 
 È possibile eseguire un popolamento incrementale per un indice full-text per il quale CHANGE_TRACKING è impostato su MANUAL o OFF. 
  
 Per eseguire il popolamento incrementale, è necessario che la tabella indicizzata contenga una colonna del tipo di dati **timestamp** . Se non è disponibile una colonna **timestamp** , il popolamento incrementale non può essere eseguito.   

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la colonna **timestamp** per identificare le righe che sono state modificate dopo l'ultimo popolamento. Il popolamento incrementale aggiorna l'indice full-text per le righe aggiunte, eliminate o modificate dopo l'ultimo popolamento o durante la sua esecuzione. Al termine di un popolamento, il motore di ricerca full-text registra un nuovo valore **timestamp** , che corrisponde al valore **timestamp** maggiore rilevato da SQL Gatherer. Questo valore verrà usato all'avvio del successivo popolamento incrementale.  
 
In alcuni casi una richiesta di popolamento incrementale comporta un popolamento completo.
-   Se viene richiesto un popolamento incrementale per una tabella senza una colonna **timestamp** , verrà eseguito un popolamento completo.
-   Se il primo popolamento di un indice full-text è incrementale, vengono indicizzate tutte le righe e il risultato è equivalente a un popolamento completo. 
-   Se alcuni metadati che interessano l'indice full-text della tabella sono stati modificati dopo l'ultimo popolamento, le richieste di popolamento vengono implementate come popolamenti completi. Sono incluse le modifiche ai metadati causate dall'alterazione di qualsiasi definizione di colonna, indice o indice full-text. 

### <a name="run-an-incremental-population"></a>Eseguire un popolamento incrementale
  
 Per eseguire un popolamento incrementale, eseguire un'istruzione `ALTER FULLTEXT INDEX` usando la clausola `START INCREMENTAL POPULATION`.  
  
###  <a name="create"></a> Creare o modificare una pianificazione per un popolamento incrementale   
  
1.  In Management Studio espandere il server in Esplora oggetti.  
  
2.  Espandere **Database**e quindi il database contenente l'indice full-text.  
  
3.  Espandere **Tabelle**.  
  
    Fare clic con il pulsante destro del mouse sulla tabella in cui viene definito l'indice full-text, scegliere **Indice full-text**e quindi **Proprietà** dal menu di scelta rapida **Indice full-text**. Verrà visualizzata la finestra di dialogo **Proprietà indice full-text** .  

    > [!IMPORTANT]  
    >  Se la tabella o la vista di base non contiene una colonna di dati di tipo **timestamp**, non è possibile eseguire un popolamento incrementale.
      
1.  Nel riquadro **Seleziona una pagina** selezionare **Pianificazioni**.  
  
     Utilizzare questa pagina per creare o gestire le pianificazioni per un processo di SQL Server Agent che consente di avviare un popolamento incrementale della tabella di base o della vista indicizzata dell'indice full-text.  

     Sono disponibili le opzioni seguenti:  
  
    -   Per **creare** una nuova pianificazione, fare clic su **Nuova**.  
  
        Verrà visualizzata la finestra di dialogo **Nuova pianificazione tabella indicizzazione full-text** , in cui è possibile creare una pianificazione. Per salvare la pianificazione, fare clic su **OK**.  
  
        > [!IMPORTANT]  
        >  Dopo la chiusura della finestra di dialogo *Proprietà indice full-text*, alla nuova pianificazione viene associato un processo di SQL Server Agent, Start Incremental Table Population on*database_name*. **table_name** (Avvio popolamento incrementale tabella in nome_database.nome_tabella). Se vengono create più pianificazioni per lo stesso indice full-text, tutte usano lo stesso processo.  
  
    -   Per **modificare** una pianificazione esistente, selezionare la pianificazione esistente e quindi fare clic su **Modifica**.  
  
         Verrà visualizzata la finestra di dialogo **Nuova pianificazione tabella indicizzazione full-text** , in cui è possibile modificare la pianificazione.  
  
        > [!NOTE]  
        >  Per informazioni sulla modifica di un processo di SQL Server Agent, vedere [Modificare un processo](../../ssms/agent/modify-a-job.md).  
  
    -   Per **rimuovere** una pianificazione esistente, selezionare la pianificazione esistente e quindi fare clic su **Elimina**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]   

##  <a name="crawl"></a> Risolvere i problemi relativi agli errori in un popolamento full-text (ricerca per indicizzazione)  
Quando si verifica un errore durante una ricerca per indicizzazione, la funzionalità di registrazione corrispondente per la ricerca full-text crea e gestisce un log di tipo ricerca per indicizzazione in formato testo normale. Ogni log di tipo ricerca per indicizzazione corrisponde a un catalogo full-text specifico. Per impostazione predefinita, i log di ricerca per indicizzazione per un'istanza specifica, ad esempio l'istanza predefinita, si trovano nella cartella `%ProgramFiles%\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\LOG`.
 
Il file del log di tipo ricerca per indicizzazione segue lo schema di denominazione seguente:  
  
`SQLFT<DatabaseID><FullTextCatalogID>.LOG[<n>]`
  
Di seguito sono riportate le parti variabili del nome del file del log di ricerca per indicizzazione.
-   <**IDDatabase**>: ID di un database. \<**dbid**> è un numero a cinque cifre con zeri iniziali.  
-   <**IDCatalogoFullText**>: ID del catalogo full-text. \<**catid**> è un numero a cinque cifre con zeri iniziali.  
-   <**n**>: numero intero che indica l'esistenza di uno o più log di ricerca per indicizzazione per lo stesso catalogo full-text.  
  
 Ad esempio, `SQLFT0000500008.2` è il file del log di ricerca per indicizzazione per un database con ID database = 5 e ID catalogo full-text = 8. Il 2 alla fine del nome file indica che sono disponibili due file del log di tipo ricerca per indicizzazione per questa coppia di database/catalogo.  

## <a name="see-also"></a>Vedere anche  
 [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)   
 [Introduzione alla ricerca full-text](../../relational-databases/search/get-started-with-full-text-search.md)   
 [Creazione e gestione di indici full-text](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
