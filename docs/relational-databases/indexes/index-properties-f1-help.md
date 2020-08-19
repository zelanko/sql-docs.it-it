---
description: Guida sensibile al contesto di Proprietà indice
title: Guida sensibile al contesto di Proprietà indice | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: reference
f1_keywords:
- sql13.swb.indexproperties.filter.f1
- sql13.swb.indexproperties.partitions.f1
- sql13.swb.indexproperties.general.f1
- sql13.swb.indexproperties.storage.f1
- sql13.swb.indexproperties.columns.f1
- sql13.swb.indexproperties.options.f1
- sql13.swb.indexproperties.spatial.f1
ms.assetid: 45efd81a-3796-4b04-b0cc-f3deec94c733
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 43ef52303110cb26b145348edc6aa9ec09bf38de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88408137"
---
# <a name="index-properties-f1-help"></a>Guida sensibile al contesto di Proprietà indice
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Le sezioni in questo argomento fanno riferimento a varie proprietà di indice disponibili tramite le finestre di dialogo di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 **Contenuto dell'argomento:**  
  
 [Pagina Generale di Proprietà indice](#General)  
  
 [Finestra di dialogo Seleziona colonne (Indice)](#Columns)  
  
 [Pagina Archiviazione di Proprietà indice](#Storage)  
  
 [Pagina Spaziale di Proprietà indice](#Spatial)  
  
 [Pagina Filtro di Proprietà indice](#Filter)  
  
##  <a name="index-properties-general-page"></a><a name="General"></a> Pagina Generale di Proprietà indice  
 Usare la pagina Generale per visualizzare o modificare le proprietà di indice per la tabella o la vista selezionata. Le opzioni per ogni pagina possono cambiare a seconda del tipo di indice selezionato.  
  
 **Nome tabella**  
 Visualizza il nome della tabella o della vista in cui l'indice è stato creato. Questo campo è di sola lettura. Per selezionare una tabella diversa chiudere la pagina Proprietà indice, selezionare la tabella corretta e quindi riaprire la pagina Proprietà indice.  
  
 Non è possibile specificare indici spaziali in viste indicizzate. È possibile definire indici spaziali solo per una tabella con chiave primaria. Il numero massimo di colonne chiave primaria in una tabella è pari a 15. La dimensione combinata per riga delle colonne chiave primaria non può essere superiore a 895 byte.  
  
 **Nome indice**  
 Consente di visualizzare il nome dell'indice. Per un indice esistente questo campo è di sola lettura. Quando si crea un nuovo indice, digitare il nome dell'indice.  
  
 **Tipo di indice**  
 Indica il tipo di indice. Per i nuovi indici, indica il tipo di indice selezionato all'apertura della finestra di dialogo. Gli indici possono essere: **Cluster**, **Non cluster**, **XML primario**, **XML secondario**, **Spaziale**, **Columnstore cluster** o **Columnstore non cluster**.  
  
 **Nota** È consentito un solo indice cluster per ogni tabella. È consentito un solo indice columnstore con ottimizzazione per la memoria xVelocity per ogni tabella.  
  
 **Univoco**  
 Selezionando questa casella di controllo, si rende l'indice univoco. Due righe non potranno avere lo stesso valore di indice. Per impostazione predefinita, tale casella di controllo è deselezionata. Se due righe hanno lo stesso valore durante la modifica di un indice esistente, la creazione dell'indice avrà esito negativo. Per le colonne in cui sono consentiti valori Null, un indice univoco consente un solo valore Null.  
  
 Se nel campo **Tipo di indice** si seleziona **Spaziale** , la casella di controllo **Univoco** è visualizzata in grigio.  
  
 **Colonne chiave indice**  
 Consente di aggiungere le colonne desiderate alla griglia **Colonne chiave indice** . Quando viene aggiunta più di una colonna, le colonne devono essere elencate nell'ordine desiderato. L'ordine delle colonne in un indice può influenzare notevolmente le prestazioni dell'indice.  
  
 Non è possibile includere più di 16 colonne in un solo indice composto. Per un numero di colonne maggiore di 16, vedere la sezione dedicata a included_columns alla fine di questo argomento.  
  
 È possibile definire un indice spaziale solo in una colonna che contiene un tipo di dati spaziali ( *colonna spaziale*).  
  
 **Nome**  
 Consente di visualizzare il nome della colonna che partecipa alla chiave dell'indice.  
  
 **Ordinamento**  
 Consente di specificare la direzione di ordinamento, **Crescente** o **Decrescente**, della colonna dell'indice selezionata.  
  
> [!NOTE]  
>  Se il tipo di indice è **XML primario** o **Spaziale**, questa colonna non viene visualizzata nella tabella.  
  
 **Tipo di dati**  
 Consente di visualizzare informazioni sul tipo di dati.  
  
> [!NOTE]  
>  Se la colonna della tabella è una colonna calcolata, l'opzione **Tipo di dati** visualizza "colonna calcolata".  
  
 **Dimensione**  
 Consente di visualizzare il numero massimo di byte necessari per archiviare il tipo di dati della colonna. In caso di colonna spaziale o XML, il valore visualizzato è zero (0).  
  
 **Identità**  
 Indica se la colonna che partecipa alla chiave dell'indice è una colonna Identity.  
  
 **Consenti valori Null**  
 Indica se la colonna che partecipa alla chiave dell'indice consente l'archiviazione di valori Null nella colonna della tabella o della vista.  
  
 **Aggiungere**  
 Consente di aggiungere una colonna alla chiave dell'indice. Selezionare le colonne della tabella nella finestra di dialogo **Seleziona colonne da** *\<table name>* che viene visualizzata quando si fa clic su **Aggiungi**. In caso di indice spaziale, questo pulsante viene visualizzato in grigio dopo la selezione di una colonna.  
  
 **Rimuovi**  
 Consente di rimuovere la colonna selezionata dalla partecipazione alla chiave dell'indice.  
  
 **Sposta su**  
 Consente di spostare verso l'alto la colonna selezionata nella griglia della chiave dell'indice.  
  
 **Sposta giù**  
 Consente di spostare verso il basso la colonna selezionata nella griglia della chiave dell'indice.  
  
 **Colonne columnstore**  
 Fare clic su **Aggiungi** per selezionare le colonne per l'indice columnstore. Per le limitazioni in un indice columnstore, vedere [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-columnstore-index-transact-sql.md).  
  
 **included_columns**  
 Consente di includere colonne non chiave nell'indice non cluster. Questa opzione consente di ignorare i limiti dell'indice corrente relativi alle dimensioni totali di una chiave di indice e il numero massimo di colonne che fanno parte di una chiave di indice aggiungendo colonne come colonne non chiave nel livello foglia dell'indice non cluster. Per altre informazioni, vedere [Creare indici con colonne incluse](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
##  <a name="select-index-columns-dialog-box"></a><a name="Columns"></a> Finestra di dialogo Seleziona colonne (Indice)  
 Usare questa pagina per aggiungere colonne alla pagina Generale di **Proprietà indice** durante la creazione o la modifica di un indice.  
  
 **Casella di controllo**  
 È possibile selezionare le caselle di controllo per aggiungere le colonne desiderate.  
  
 **Nome**  
 Nome della colonna.  
  
 **Tipo di dati**  
 Tipo di dati della colonna.  
  
 **Byte**  
 Dimensioni in byte della colonna.  
  
 **Identità**  
 Il valore indicato è **Sì** per le colonne Identity oppure **No** se la colonna non è di tipo Identity.  
  
 **Consenti valori NULL**  
 Il valore indicato è **Sì** se la definizione della tabella consente valori Null per la colonna. oppure **No** se la definizione della tabella non consente valori Null per la colonna.  

##  <a name="options-page-options"></a><a name="Options"></a> Opzioni nella pagina Opzioni
 Usare questa pagina per visualizzare o modificare le varie opzioni per l'indice.

### <a name="general-options"></a>Opzioni generali
**Ricalcola statistiche automaticamente**<br>
Specifica se le statistiche di distribuzione vengono ricalcolate automaticamente. L'impostazione predefinita è **True**, equivalente all'impostazione di STATISTICS_NORECOMPUTE su OFF. L'impostazione **False** imposta STATISTICS_NORECOMPUTE su ON.

**Ignora valori duplicati** <br>
Specifica l'errore restituito quando un'operazione di inserimento tenta di inserire valori di chiave duplicati in un indice univoco.

True<br>
Viene visualizzato un messaggio di avviso quando i valori di chiave duplicati vengono inseriti in un indice univoco. Avranno esito negativo solo le righe che violano il vincolo di unicità.

False<br>
Viene visualizzato un messaggio di errore quando i valori di chiave duplicati vengono inseriti in un indice univoco. Viene eseguito il rollback dell'intera operazione INSERT.

### <a name="locks-options"></a>Opzioni per i blocchi

**Consenti blocchi di riga**<br>
Specifica se sono consentiti blocchi di riga.

**Consenti blocchi di pagina**<br>
Specifica se sono consentiti blocchi a livello di pagina.

### <a name="operation-options"></a>Opzioni per le operazioni

 **Consenti elaborazione DML online**  
 Consente agli utenti di accedere ai dati della tabella o dell'indice cluster sottostanti e a eventuali indici non cluster associati durante un'operazione sull'indice, come CREATE o ALTER. Per altre informazioni, vedere [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).  
  
> [!NOTE]  
>  Questa opzione non è disponibile per gli indici XML o se l'indice è un indice cluster disabilitato.  
  
 **Massimo grado di parallelismo**  
 Consente di limitare il numero di processori da usare durante l'esecuzione di piani paralleli. Il valore predefinito è 0 e corrisponde al numero effettivo di CPU disponibili. L'impostazione del valore su 1 impedisce la generazione di piani paralleli. L'impostazione del valore su un numero maggiore di 1 limita il numero massimo di processori usati da una singola esecuzione della query. Questa opzione diventa disponibile solo se la finestra di dialogo è nello stato **Ricompila** o **Ricrea** . Per altre informazioni, vedere [Impostazione dell'opzione relativa al massimo grado di parallelismo per ottenere prestazioni ottimali](../../relational-databases/policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md).  
  
> [!NOTE]  
>  Se viene specificato un valore maggiore del numero di CPU disponibili, verrà usato l'effettivo numero di CPU disponibili.  


**Optimize for sequential key** (Ottimizza per chiave sequenziale)<br>
Specifica se eseguire o meno l'ottimizzazione per la contesa di inserimento dell'ultima pagina. Per altre informazioni, vedere [Chiavi sequenziali](../../t-sql/statements/create-index-transact-sql.md#sequential-keys).

### <a name="storage-options"></a>Opzioni di archiviazione

**Ordina in tempdb**<br>
Specifica se i risultati temporanei dell'ordinamento devono essere archiviati in tempdb.

True<br>
I risultati intermedi dell'ordinamento utilizzati per la compilazione dell'indice vengono archiviati in tempdb. Questo potrebbe ridurre il tempo necessario per creare un indice se tempdb si trova in un set di dischi diverso rispetto al database utente. La quantità di spazio su disco utilizzata durante la compilazione dell'indice sarà tuttavia maggiore.

False<br>
I risultati intermedi dell'ordinamento vengono archiviati nello stesso database dell'indice. Per altre informazioni, vedere [Opzione SORT_IN_TEMPDB per gli indici](./sort-in-tempdb-option-for-indexes.md).

**Fattore di riempimento**<br>
Specifica una percentuale che indica il livello di riempimento del livello foglia di ogni pagina di indice da parte del motore di database durante la creazione o la ricompilazione dell'indice. fillfactor deve essere un valore intero compreso tra 1 e 100. Se fillfactor è 100, il motore di database crea indici con pagine foglia riempite fino alla capacità massima.
L'impostazione di FILLFACTOR viene applicata solo in fase di creazione o di ricompilazione dell'indice. La percentuale specificata di spazio vuoto delle pagine non viene mantenuta in modo dinamico dal motore di database.

Per altre informazioni, vedere [Specificare un fattore di riempimento per un indice](./specify-fill-factor-for-an-index.md).

**Riempi indice**<br>
Specifica il riempimento dell'indice.

True<br>
La percentuale di spazio disponibile specificata da fillfactor viene applicata alle pagine di livello intermedio dell'indice.

False o fillfactor non è specificato<br>
Le pagine di livello intermedio vengono riempite poco al di sotto della capacità massima, in modo che lo spazio residuo sia sufficiente per almeno una riga della dimensione massima supportata dall'indice, in base al set di chiavi nelle pagine intermedie.


##  <a name="storage-page-options"></a><a name="Storage"></a> Opzioni della pagina Archiviazione  
 Usare questa pagina per visualizzare o modificare proprietà di filegroup o di schemi di partizione per l'indice selezionato. Vengono mostrate solo le opzioni correlate al tipo di indice.  
  
 **Filegroup**  
 Archivia l'indice nel filegroup specificato. Nell'elenco sono visualizzati solo filegroup standard (ROW). La selezione predefinita nell'elenco è il filegroup PRIMARY del database. Per altre informazioni, vedere [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
 **Filegroup FILESTREAM**  
 Specifica il filegroup per i dati FILESTREAM. Questo elenco visualizza solo i filegroup FILESTREAM. La selezione predefinita nell'elenco è il filegroup PRIMARY FILESTREAM del database. Per altre informazioni, vedere [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
 **Schema di partizione**  
 Archivia l'indice in uno schema di partizione. Facendo clic su **Schema partizione** si abilita la griglia sottostante. La selezione predefinita nell'elenco è lo schema di partizione usato per archiviare i dati di tabella. Selezionando uno schema di partizione diverso nell'elenco si aggiornano le informazioni visualizzate nella griglia. Per ulteriori informazioni, vedere [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 L'opzione relativa allo schema di partizione non è disponibile se il database non contiene schemi di partizione.  
  
 **Schema di partizione FILESTREAM**  
 Specifica lo schema di partizione per i dati FILESTREAM. Lo schema di partizione deve essere simmetrico con la combinazione specificata nell'opzione **Schema partizione** .  
  
 Se la tabella non è partizionata, il campo è vuoto.  
  
 **Parametro schema partizione**  
 Consente di visualizzare il nome della colonna che partecipa allo schema di partizione.  
  
 **Colonne della tabella**  
 Consente di selezionare la tabella o la vista su cui eseguire il mapping allo schema di partizione.  
  
 **Tipo di dati colonna**  
 Consente di visualizzare le informazioni sul tipo di dati relative alla colonna.  
  
> [!NOTE]  
>  Se la colonna della tabella è una colonna calcolata, l'opzione **Tipo di dati colonna** visualizza "colonna calcolata".  
  
##  <a name="spatial-page-index-options"></a><a name="Spatial"></a> Opzioni di indice della pagina Spaziale  
 Usare la pagina **Spaziale** per visualizzare o specificare i valori delle proprietà spaziali. Per altre informazioni, vedere [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md).  
  
### <a name="bounding-box"></a>Riquadro  
 Si definisce *riquadro* il perimetro della griglia di livello principale di un piano geometrico. I parametri del riquadro sono presenti solo nello schema a mosaico griglia geometrica. Questi parametri non sono disponibili se **Schema a mosaico** è impostato su **Griglia geografica**.  
  
 Nel pannello sono visualizzate le coordinate **(** _X-min_ **,** _Y-min_ **)** e **(** _X-max_ **,** _Y-max_ **)** del rettangolo di selezione. Non esistono valori predefiniti, Quando si crea un indice spaziale nuovo su una colonna di tipo **geometry** , è quindi necessario specificare i valori delle coordinate.  
  
 **X-min**  
 La coordinata X dell'angolo inferiore sinistro del riquadro.  
  
 **Y-min**  
 La coordinata Y dell'angolo inferiore sinistro del riquadro.  
  
 **X-max**  
 La coordinata X dell'angolo superiore destro del riquadro.  
  
 **Y-max**  
 La coordinata Y dell'angolo superiore destro del riquadro.  
  
### <a name="general"></a>Generale  
 **Schema a mosaico**  
 Indica lo schema a mosaico dell'indice. Sono supportati gli schemi a mosaico seguenti.  
  
 **Griglia geometrica**  
 Specifica lo schema a mosaico per griglia geometrica che viene applicato a una colonna con il tipo di dati **geometry** .  
  
 **Griglia geometrica automatica**  
 Questa opzione è abilitata per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando il livello di compatibilità del database è impostato su 110 o su un valore maggiore.  
  
 **Griglia geografica**  
 Specifica lo schema a mosaico per griglia geografica che viene applicato a una colonna con il tipo di dati **geography** .  
  
 **Griglia geografica automatica**  
 Questa opzione è abilitata per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando il livello di compatibilità del database è impostato su 110 o su un valore maggiore.  
  
 Per informazioni sull'implementazione dello schema a mosaico in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Dati spaziali &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md).  
  
 **Celle per oggetto**  
 Indica il numero di celle per oggetto di mosaico utilizzabile per un singolo oggetto spaziale nell'indice. È possibile usare qualsiasi numero intero compreso tra 1 e 8192. Quando il livello di compatibilità del database è impostato su 110 o su un valore maggiore, il valore predefinito è 16, mentre è 8 per le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Se al livello principale un oggetto include più celle rispetto a quanto specificato da *n*, l'indicizzazione usa il numero di celle necessario per offrire uno schema a mosaico di livello principale completo. In tali casi un oggetto può ricevere un numero di celle maggiore di quello specificato: il numero massimo è il numero di celle generate dalla griglia di livello principale che dipende dalla densità di **Livello 1** .  
  
### <a name="grids"></a>Griglie  
 In questo pannello è visualizzata la densità della griglia a ogni livello dello schema a mosaico. Le opzioni disponibili sono **Bassa**, **Media**o **Alta**. Il valore predefinito è **Media**. **Bassa** rappresenta una griglia 4x4 (16 celle), **Media** una griglia 8x8 (64 celle) e **Alta** una griglia 16x16 (256 celle). Queste opzioni non sono disponibili se si scelgono le opzioni di schema a mosaico **Griglia geometrica automatica** o **Griglia geografica automatica** .  
  
 **Livello 1**  
 Densità della griglia di primo livello (principale).  
  
 **Livello 2**  
 Densità della griglia di secondo livello.  
  
 **Livello 3**  
 Densità della griglia di terzo livello.  
  
 **Livello 4**  
 Densità della griglia di quarto livello.  
  
##  <a name="filter-page"></a><a name="Filter"></a> Pagina Filtro  
 Usare questa pagina per immettere il predicato del filtro per un indice filtrato. Per altre informazioni, vedere [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
 **Espressione filtro**  
 Definisce le righe di dati da includere nell'indice filtrato. Ad esempio, usare `StartDate > '20000101' AND EndDate IS NOT NULL'.`  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare le opzioni di indice](../../relational-databases/indexes/set-index-options.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
