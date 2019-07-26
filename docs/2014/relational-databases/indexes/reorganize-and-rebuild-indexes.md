---
title: Riorganizzare e ricompilare gli indici | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.indexproperties.fragmentation.f1
- sql12.swb.index.reorg.f1
- sql12.swb.index.rebuild.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2de93079289ffda8ff6287ad09aa4dea150932d7
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68475963"
---
# <a name="reorganize-and-rebuild-indexes"></a>Riorganizzare e ricompilare gli indici
  In questo argomento viene descritto come riorganizzare o ricompilare un indice frammentato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Tramite il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] la manutenzione degli indici viene automaticamente eseguita dopo ogni operazione di modifica, inserimento o eliminazione dei dati sottostanti. Nel tempo, queste modifiche possono provocare la frammentazione dell'indice nel database. La frammentazione si verifica quando negli indici sono presenti pagine in cui l'ordinamento logico, basato sul valore chiave, non corrisponde all'ordinamento fisico all'interno del file di dati. Gli indici con un alto grado di frammentazione possono essere causa del calo delle prestazioni delle query e rallentare l'applicazione.  
  
 È possibile porre rimedio alla frammentazione eseguendo la riorganizzazione o la ricompilazione dell'indice. Per gli indici partizionati compilati in base a uno schema di partizione è possibile procedere in uno dei metodi seguenti sull'intero indice o su una singola partizione. La ricompilazione di un indice consiste nell'eliminazione e nella ricreazione dell'indice. Questa operazione consente di rimuovere la frammentazione, rendere disponibile spazio su disco grazie alla compattazione delle pagine in base all'impostazione del fattore di riempimento esistente o specificata e riordinare le righe dell'indice in pagine contigue. Quando viene specificata la parola chiave ALL, tutti gli indici della tabella vengono eliminati e ricompilati in una singola transazione. La riorganizzazione di un indice richiede una quantità minima di risorse di sistema. Questa operazione deframmenta il livello foglia di indici cluster e non cluster di tabelle e viste tramite il riordinamento fisico delle pagine al livello foglia in base all'ordine logico, da sinistra verso destra, dei nodi foglia. La riorganizzazione consente inoltre di compattare le pagine di indice in base al valore del fattore di riempimento esistente.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Rilevamento della frammentazione](#Fragmentation)  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per controllare la frammentazione di un indice usando:**  
  
     [SQL Server Management Studio](#SSMSProcedureFrag)  
  
     [Transact-SQL](#TsqlProcedureFrag)  
  
-   **Per riorganizzare o ricompilare un indice usando:**  
  
     [SQL Server Management Studio](#SSMSProcedureReorg)  
  
     [Transact-SQL](#TsqlProcedureReorg)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Fragmentation"></a> Rilevamento della frammentazione  
 Il primo passaggio per decidere il metodo di deframmentazione da usare consiste nell'eseguire un'analisi dell'indice per determinare il grado di frammentazione. La funzione di sistema [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)consente di rilevare la frammentazione in un indice specifico, in tutti gli indici di una tabella o vista indicizzata, in tutti gli indici di un database o in tutti gli indici di tutti i database. Per gli indici partizionati, **sys.dm_db_index_physical_stats** fornisce anche informazioni sulla frammentazione per ogni partizione.  
  
 Il set di risultati restituito dalla funzione **sys.dm_db_index_physical_stats** include le colonne seguenti.  
  
|Colonna|Descrizione|  
|------------|-----------------|  
|**avg_fragmentation_in_percent**|Percentuale di frammentazione logica (pagine non ordinate nell'indice).|  
|**fragment_count**|Numero di frammenti (pagine foglia fisicamente consecutive) nell'indice.|  
|**avg_fragment_size_in_pages**|Numero medio di pagine in un frammento di un indice.|  
  
 Una volta noto il grado di frammentazione, usare la tabella seguente per determinare il metodo migliore per la correzione della frammentazione.  
  
|Valore di**avg_fragmentation_in_percent**|Istruzione correttiva|  
|-----------------------------------------------|--------------------------|  
|> 5% e \< = 30%|ALTER INDEX REORGANIZE|  
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|

<sup>1</sup> È possibile eseguire la ricompilazione di un indice online oppure offline. La riorganizzazione di un indice viene sempre eseguita online. Per ottenere una disponibilità simile a quella offerta dall'opzione di riorganizzazione è necessario ricompilare gli indici in modalità online.  
  
> [!TIP]
> Questi valori costituiscono un'indicazione approssimativa per determinare il punto in cui passare da `ALTER INDEX REORGANIZE` a `ALTER INDEX REBUILD`. I valori effettivi, in realtà, variano da caso a caso. È importante riuscire a determinare la soglia migliore per l'ambiente in uso. Se, ad esempio, un determinato indice viene utilizzato principalmente per le operazioni di analisi, la rimozione della frammentazione può migliorare le prestazioni di tali operazioni. Il vantaggio in merito alle prestazioni è meno evidente per gli indici utilizzati principalmente per le operazioni di ricerca. Analogamente, la rimozione della frammentazione in un heap, ovvero una tabella senza un indice cluster, è particolarmente utile per le operazioni di analisi degli indici non cluster, ma ha un effetto ridotto nelle operazioni di ricerca.

Non è in genere consigliabile usare questi comandi per livelli di frammentazione ridotti (inferiori al 5%), poiché i vantaggi offerti dalla rimozione di una frammentazione così limitata sono praticamente annullati dal costo della riorganizzazione o della ricompilazione dell'indice. 

> [!NOTE]
> La ricompilazione o la riorganizzazione degli indici di dimensioni ridotte spesso non riduce la frammentazione. Le pagine di indici di dimensioni ridotte vengono talvolta archiviate in extent misti. Poiché gli extent misti possono essere condivisi al massimo da otto oggetti, la frammentazione in un indice di dimensioni ridotte potrebbe non ridursi dopo la riorganizzazione o la ricompilazione dell'indice.

### <a name="index-defragmentation-considerations"></a>Considerazioni sulla deframmentazione dell'indice
In determinate condizioni, la ricompilazione di un indice cluster ricreerà automaticamente tutti gli indici non cluster che fanno riferimento alla chiave di clustering, se è necessario modificare gli identificatori fisici o logici contenuti nei record degli indici non cluster.

Scenari che forzano la ricompilazione automatica di tutti gli indici non cluster in una tabella:

-  Creazione di un indice cluster in una tabella
-  Rimozione di un indice cluster, causa dell'archiviazione della tabella come heap
-  Modifica della chiave di clustering per includere o escludere colonne

Scenari che non richiedono la ricompilazione automatica di tutti gli indici non cluster in una tabella:

-  Ricompilazione di un indice cluster univoco
-  Ricompilazione di un indice cluster non univoco
-  Modifica dello schema dell'indice, ad esempio l'applicazione di uno schema di partizionamento a un indice cluster o il trasferimento dell'indice cluster in un filegroup diverso
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
Gli indici con più di 128 extent vengono ricompilati in due fasi separate, logica e fisica. Nella fase logica, le unità di allocazione esistenti usate dall'indice vengono contrassegnate per la deallocazione, le righe di dati vengono copiate e ordinate, quindi spostate nelle nuove unità di allocazione create per archiviare l'indice ricompilato. Nella fase fisica, le unità di allocazione precedentemente contrassegnate per la deallocazione vengono fisicamente eliminate nelle transazioni brevi eseguite in background e non richiedono molti blocchi. Per altre informazioni sugli extent, vedere la [Guida all'architettura di pagine ed extent](https://docs.microsoft.com/sql/relational-databases/pages-and-extents-architecture-guide).

L'istruzione `ALTER INDEX REORGANIZE` richiede che nel file di dati che include l'indice sia disponibile spazio, perché l'operazione può allocare solo pagine di lavoro temporanee nello stesso file, non in un altro file nel filegroup. Anche se nel filegroup possono essere disponibili pagine libere, è tuttavia possibile che l'utente incontri l'errore 1105: `Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`

La creazione e la ricompilazione di indici non allineati per una tabella con oltre 1000 partizioni sono possibili, ma non consigliate. Questo tipo di operazioni può causare riduzioni delle prestazioni e un eccessivo consumo della memoria.

Non è possibile riorganizzare o ricompilare indici contenuti in un filegroup offline o di sola lettura. Quando viene specificata la parola chiave `ALL` e uno o più indici si trovano in un filegroup offline o di sola lettura, l'istruzione ha esito negativo.
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione `ALTER` per la tabella o la vista. L'utente deve essere un membro del ruolo predefinito del server **sysadmin** o dei ruoli predefiniti del database **db_ddladmin** e **db_owner** .  
  
##  <a name="SSMSProcedureFrag"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>Per controllare la frammentazione di un indice  
  
1.  In Esplora oggetti espandere il database contenente la tabella in cui si desidera controllare la frammentazione di un indice.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Espandere la tabella in cui si desidera controllare la frammentazione di un indice.  
  
4.  Espandere la cartella **Indici** .  
  
5.  Fare clic con il pulsante destro del mouse sull'indice di cui si vuole controllare la frammentazione e scegliere **Proprietà**.  
  
6.  In **Selezione pagina**selezionare **Frammentazione**.  
  
     Le informazioni seguenti sono disponibili nella pagina **Frammentazione** :  
  
     **Livello di riempimento pagina**  
     Indica il livello medio di riempimento delle pagine di indice, espresso come percentuale. Il valore 100% indica che le pagine di indice sono completamente piene. Il valore 50% indica che ogni pagina di indice è piena all'incirca per metà.  
  
     **Frammentazione totale**  
     Percentuale di frammentazione logica. Indica il numero di pagine di un indice che non sono archiviate in ordine.  
  
     **Dimensioni medie delle righe**  
     Dimensioni medie di una riga al livello foglia.  
  
     **Livello nidificazione**  
     Numero di livelli dell'indice, compreso il livello foglia.  
  
     **Record inoltrati**  
     Numero di record in un heap che hanno inoltrato puntatori a un altro percorso dei dati. Questo stato si verifica durante un aggiornamento, nel caso in cui non vi sia spazio sufficiente per archiviare la riga nel percorso originale.  
  
     **Righe fantasma**  
     Numero di righe contrassegnate come eliminate ma non ancora rimosse. Queste righe verranno rimosse da un thread di pulitura nel momento in cui il server non è occupato. Questo valore non comprende le righe mantenute a causa di una transazione di isolamento dello snapshot in attesa.  
  
     **Tipo di indice**  
     Tipo di indice. I valori possibili sono **Indice cluster**, **Indice non cluster**e **XML primario**. È inoltre possibile archiviare le tabelle come heap (senza indici), ma in questo caso non sarà possibile aprire la pagina Proprietà indice.  
  
     **Righe al livello foglia**  
     Numero di righe al livello foglia.  
  
     **Dimensioni massime righe**  
     Dimensioni massime delle righe al livello foglia.  
  
     **Dimensioni minime righe**  
     Dimensioni minime delle righe al livello foglia.  
  
     **Pagine**  
     Numero totale di pagine di dati.  
  
     **Partition ID**  
     ID partizione dell'albero B contenente l'indice.  
  
     **Righe fantasma versione**  
     Numero di record fantasma mantenuti a causa di una transazione di isolamento dello snapshot in attesa.  
  
##  <a name="TsqlProcedureFrag"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-check-the-fragmentation-of-an-index"></a>Per controllare la frammentazione di un indice  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Find the average fragmentation percentage of all indexes  
    -- in the HumanResources.Employee table.   
    SELECT a.index_id, name, avg_fragmentation_in_percent  
    FROM sys.dm_db_index_physical_stats (DB_ID(N'AdventureWorks2012'), OBJECT_ID(N'HumanResources.Employee'), NULL, NULL, NULL) AS a  
        JOIN sys.indexes AS b ON a.object_id = b.object_id AND a.index_id = b.index_id;   
    GO  
    ```  
  
     L'istruzione potrebbe restituire un set di risultati simile al seguente.  
  
    ```  
    index_id    name                                                  avg_fragmentation_in_percent  
    ----------- ----------------------------------------------------- ----------------------------  
    1           PK_Employee_BusinessEntityID                          0  
    2           IX_Employee_OrganizationalNode                        0  
    3           IX_Employee_OrganizationalLevel_OrganizationalNode    0  
    5           AK_Employee_LoginID                                   66.6666666666667  
    6           AK_Employee_NationalIDNumber                          50  
    7           AK_Employee_rowguid                                   0  
  
    (6 row(s) affected)  
    ```  
  
 Per altre informazioni, vedere [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql).  
  
##  <a name="SSMSProcedureReorg"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-reorganize-or-rebuild-an-index"></a>Per riorganizzare o ricompilare un indice  
  
1.  In Esplora oggetti espandere il database che contiene la tabella in cui si desidera riorganizzare un indice.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Espandere la tabella in cui si desidera riorganizzare un indice.  
  
4.  Espandere la cartella **Indici** .  
  
5.  Fare clic con il pulsante destro del mouse sull'indice che si vuole riorganizzare e scegliere **Riorganizza**.  
  
6.  Nella finestra di dialogo **Riorganizza indici** verificare che nella griglia **Indici da riorganizzare** sia presente l'indice corretto, quindi scegliere **OK**.  
  
7.  Selezionare la casella di controllo **Compatta dati di colonne LOB** per specificare che tutte le pagine che contengono dati LOB vengano compattate.  
  
8.  Scegliere **OK.**  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>Per riorganizzare tutti gli indici in una tabella  
  
1.  In Esplora oggetti espandere il database che contiene la tabella in cui si desidera riorganizzare gli indici.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Espandere la tabella in cui si desidera riorganizzare gli indici.  
  
4.  Fare clic con il pulsante destro del mouse sulla cartella **Indici** e scegliere **Riorganizza tutto**.  
  
5.  Nella finestra di dialogo **Riorganizza indici** verificare che nella griglia **Indici da riorganizzare**siano presenti gli indici corretti. Per rimuovere un indice dalla griglia **Indici da riorganizzare** , selezionare l'indice desiderato e premere CANC.  
  
6.  Selezionare la casella di controllo **Compatta dati di colonne LOB** per specificare che tutte le pagine che contengono dati LOB vengano compattate.  
  
7.  Fare clic su **OK**.  
  
#### <a name="to-rebuild-an-index"></a>Per ricompilare un indice  
  
1.  In Esplora oggetti espandere il database che contiene la tabella in cui si desidera riorganizzare un indice.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Espandere la tabella in cui si desidera riorganizzare un indice.  
  
4.  Espandere la cartella **Indici** .  
  
5.  Fare clic con il pulsante destro del mouse sull'indice che si vuole riorganizzare e scegliere **Riorganizza**.  
  
6.  Nella finestra di dialogo **Ricompila indici** verificare che nella griglia **Indici da ricompilare** sia presente l'indice corretto, quindi scegliere **OK**.  
  
7.  Selezionare la casella di controllo **Compatta dati di colonne LOB** per specificare che tutte le pagine che contengono dati LOB vengano compattate.  
  
8.  Scegliere **OK.**  
  
##  <a name="TsqlProcedureReorg"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-reorganize-a-defragmented-index"></a>Per riorganizzare un indice deframmentato  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize the IX_Employee_OrganizationalLevel_OrganizationalNode index on the HumanResources.Employee table.   
  
    ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-reorganize-all-indexes-in-a-table"></a>Per riorganizzare tutti gli indici in una tabella  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- Reorganize all indexes on the HumanResources.Employee table.  
    ALTER INDEX ALL ON HumanResources.Employee  
    REORGANIZE ;   
    GO  
    ```  
  
#### <a name="to-rebuild-a-defragmented-index"></a>Per ricompilare un indice deframmentato  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Nell'esempio viene ricompilato un solo indice nella tabella `Employee` .  
  
     [!code-sql[IndexDDL#AlterIndex1](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex1)]  
  
#### <a name="to-rebuild-all-indexes-in-a-table"></a>Per ricompilare tutti gli indici in una tabella  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query. Nell'esempio viene specificata la parola chiave `ALL`. In questo modo vengono ricompilati tutti gli indici associati alla tabella. Vengono inoltre specificate tre opzioni.  
  
     [!code-sql[IndexDDL#AlterIndex2](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex2)]  
  
 Per altre informazioni, vedere [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure consigliate relative alla deframmentazione degli indici in Microsoft SQL Server 2000](https://technet.microsoft.com/library/cc966523.aspx)  
  
  
