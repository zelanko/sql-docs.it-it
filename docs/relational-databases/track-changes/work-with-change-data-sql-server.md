---
title: Usare i dati delle modifiche (SQL Server) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data [SQL Server]
- change data capture [SQL Server], query function scenarios
- change data capture [SQL Server], LSN boundaries
- change data capture [SQL Server], query functions
ms.assetid: 5346b852-1af8-4080-b278-12efb9b735eb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 62c705432367b8d2ad7b5de7de30c840be368aac
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405236"
---
# <a name="work-with-change-data-sql-server"></a>Utilizzare i dati delle modifiche (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  I dati delle modifiche vengono resi disponibili ai consumer della funzionalità Change Data Capture tramite funzioni con valori di tabella. Per tutte le query di queste funzioni sono necessari due parametri che definiscono l'intervallo di numeri di sequenza del file di log (LSN) idonei durante lo sviluppo del set di risultati restituito. Entrambi i valori LSN che rappresentano il limite inferiore e quello superiore dell'intervallo sono inclusi nell'intervallo stesso.  
  
 Per stabilire i valori LSN appropriati da utilizzare per l'esecuzione di query su una funzione con valori di tabella, sono disponibili numerose funzioni. La funzione [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) restituisce il valore LSN meno elevato associato a un intervallo di validità di un'istanza di acquisizione, ovvero all'intervallo di tempo durante il quale i dati delle modifiche rimangono disponibili per le relative istanze di acquisizione. La funzione [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) restituisce il valore LSN più elevato nell'intervallo di validità. Le funzioni [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) e [sys.fn_cdc_map_lsn_to_time](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) possono essere usate per includere i valori LSN in una cronologia convenzionale. Poiché in Change Data Capture vengono utilizzati intervalli di query chiusi, talvolta risulta necessario generare il valore LSN successivo in una sequenza per garantire che le modifiche non vengano duplicate in finestre di query consecutive. Le funzioni [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) e [sys.fn_cdc_decrement_lsn](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md) sono utili quando è necessario modificare in modo incrementale un valore LSN.  
  
##  <a name="LSN"></a> Convalida dei limiti LSN  
 È consigliabile convalidare i limiti LSN da utilizzare in una query con funzione con valori di tabella prima dell'utilizzo. Endpoint con valore Null oppure endpoint esterni all'intervallo di validità per un'istanza di acquisizione provocheranno la restituzione di un errore da parte di una funzione con valori di tabella relativa a Change Data Capture.  
  
 L'errore seguente viene ad esempio restituito per una query per tutte le modifiche quando un parametro utilizzato per definire l'intervallo di query non è valido, non è compreso nell'intervallo oppure l'opzione del filtro di riga non è valida.  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_all_changes_ ...`  
  
 L'errore corrispondente restituito per una query **net changes** è il seguente:  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_net_changes_ ...`  
  
> [!NOTE]  
>  È noto che il messaggio 313 è fuorviante e non indica la causa effettiva dell'errore. Questo utilizzo non opportuno del messaggio deriva dall'impossibilità di generare un errore esplicito dall'interno di una funzione con valori di tabella. Si è tuttavia ritenuto preferibile restituire un errore riconoscibile, sebbene inaccurato, rispetto a non restituire alcun risultato. Un set di risultati vuoto non sarebbe infatti distinguibile da una query valida che non restituisce alcuna modifica.  
  
 Quando viene eseguita una query per tutte le modifiche, gli errori di autorizzazione negata restituiranno altri errori, come illustrato di seguito:  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object 'fn_cdc_get_all_changes_...', database 'MyDB', schema 'cdc'.`  
  
 Lo stesso messaggio è valido in caso di esecuzione di una query per le modifiche totali:  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object fn_cdc_get_net_changes_...', database 'MyDB', schema 'cdc'.`  
  
 Vedere il modello Enumerate Net Changes Using TRY CATCH per una dimostrazione di come vengono intercettati questi errori noti relativi alle funzioni con valori di tabella e come vengono restituite informazioni più significative relative all'errore.  
  
> [!NOTE]  
>  Per trovare i modelli di Change Data Capture in SQL Server Management Studio, scegliere **Esplora modelli** dal menu **Visualizza**, espandere **Modelli di SQL Server** , quindi espandere la cartella **Change Data Capture** .  
  
##  <a name="Functions"></a> Funzioni di query  
 A seconda delle caratteristiche della tabella di origine per cui viene eseguito il rilevamento delle modifiche e del modo in cui la relativa istanza di acquisizione viene configurata, vengono generate una o due funzioni con valori di tabella per l'esecuzione di query sui dati delle modifiche.  
  
-   La funzione [cdc.fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) restituisce tutte le modifiche che si sono verificate per l'intervallo specificato. Questa funzione viene sempre generata. Le voci vengono restituite sempre in modo ordinato, prima in base al valore LSN del commit della transazione e successivamente in base a un valore che ordina in sequenza la modifica all'interno della transazione. A seconda dell'opzione del filtro di riga scelta, un aggiornamento può comportare la restituzione della riga finale (opzione del filtro di riga "all") o dei valori nuovi e precedenti (opzione del filtro di riga "all update old").  
  
-   La funzione [cdc.fn_cdc_get_net_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) viene generata quando il parametro @supports_net_changes è impostato su 1 e la tabella di origine è abilitata.  
  
    > [!NOTE]  
    >  Questa opzione è supportata solo se la tabella di origine contiene una chiave primaria definita o se il parametro @index_name è stato usato per identificare un indice univoco.  
  
     La funzione **netchanges** restituisce una modifica per ogni riga della tabella di origine modificata. Se durante l'intervallo specificato viene registrata più di una modifica relativa alla riga, i valori della colonna rifletteranno i contenuti finali della riga. Per identificare correttamente l'operazione necessaria all'aggiornamento dell'ambiente di destinazione, è necessario che nella funzione con valori di tabella vengano considerate sia l'operazione iniziale sulla riga durante l'intervallo sia l'operazione finale sulla riga stessa. Quando viene specificata l'opzione del filtro di riga 'all', le operazioni restituite da una query **net changes** vengono inserite, eliminate o aggiornate con valori nuovi. Questa opzione restituisce sempre un valore Null per la maschera di aggiornamento perché al calcolo di una maschera di aggregazione è associato un costo. Se è necessaria una maschera di aggregazione che rifletta tutte le modifiche apportate a una riga, utilizzare l'opzione 'all with mask'. Se l'elaborazione a valle non richiede la distinzione tra operazioni di inserimento e di aggiornamento, utilizzare l'opzione 'all with merge'. In questo caso, il valore dell'operazione accetterà solo due valori, 1 per l'eliminazione e 5 per un'operazione che potrebbe essere un inserimento o un aggiornamento. Questa opzione elimina le operazioni di elaborazione aggiuntive necessarie per determinare se l'operazione derivata deve essere un inserimento o un aggiornamento e può migliorare le prestazioni della query quando questa differenziazione non è necessaria.  
  
 La maschera di aggiornamento restituita da una funzione della query è una rappresentazione compatta che identifica tutte le colonne modificate in una riga di dati delle modifiche. Generalmente, queste informazioni sono necessarie solo per un subset delle colonne acquisite di dimensioni ridotte. Le funzioni sono disponibili per consentire l'estrazione delle informazioni dalla maschera in una forma utilizzabile dalle applicazioni in modo più diretto. La funzione [sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) restituisce la posizione ordinale di una colonna denominata per una determinata istanza di acquisizione, mentre la funzione [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) restituisce la parità del bit nella maschera fornita in base al numero ordinale passato nella chiamata alla funzione. Se utilizzate insieme, queste due funzioni consentono l'estrazione e la restituzione efficienti delle informazioni dalla maschera di aggiornamento con la richiesta dei dati delle modifiche. Vedere il modello Enumerate Net Changes Using All With Mask per una dimostrazione di come utilizzare queste funzioni.  
  
##  <a name="Scenarios"></a> Scenari di funzioni di query  
 Nelle sezioni seguenti vengono descritti scenari comuni per l'esecuzione di query sui dati di Change Data Capture tramite le funzioni di query cdc.fn_cdc_get_all_changes_<capture_instance> e cdc.fn_cdc_get_net_changes_<capture_instance>.  
  
### <a name="querying-for-all-changes-within-the-capture-instance-validity-interval"></a>Esecuzione di query per tutte le modifiche comprese nell'intervallo di validità dell'istanza di acquisizione  
 La richiesta più diretta di dati delle modifiche consiste nella restituzione di tutti i dati delle modifiche correnti compresi nell'intervallo di validità di un'istanza di acquisizione. Per eseguire questa richiesta, determinare innanzitutto i limiti LSN superiore e inferiore dell'intervallo di validità. Usare quindi questi valori per identificare i parametri @from_lsn e@to_lsn passati alla funzione di query cdc.fn_cdc_get_all_changes_<capture_instance> o cdc.fn_cdc_get_net_changes_<capture_instance>. Usare la funzione [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) per ottenere il limite inferiore e [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) per ottenere il limite superiore. Vedere il modello Enumerate All Changes for the Valid Range affinché nel codice di esempio venga eseguita una query per tutte le modifiche valide correnti tramite la funzione di query cdc.fn_cdc_get_all_changes_<capture_instance>. Vedere il modello Enumerate Net Changes for the Valid Range per un esempio simile relativo all'utilizzo della funzione cdc.fn_cdc_get_net_changes_<capture_instance>.  
  
### <a name="querying-for-all-new-changes-since-the-last-set-of-changes"></a>Esecuzione di query per tutte le nuove modifiche successive all'ultimo set di modifiche  
 Per applicazioni tipiche, il processo di esecuzione di query per i dati delle modifiche è continuo, con richieste periodiche di tutte le modifiche apportate dopo l'ultima richiesta. Per query di questo tipo, è possibile usare la funzione [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) per dedurre il limite inferiore della query corrente dal limite superiore della query precedente. Tramite questo metodo è possibile garantire che nessuna riga venga ripetuta perché l'intervallo di query viene sempre considerato come un intervallo chiuso dove entrambi gli endpoint sono inclusi nell'intervallo. Usare la funzione [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) per ottenere l'endpoint alto per il nuovo intervallo della richiesta. Vedere il modello Enumerate All Changes Since Previous Request affinché nel codice di esempio la finestra Query venga spostata sistematicamente per ottenere tutte le modifiche apportate dopo l'ultima richiesta.  
  
### <a name="querying-for-all-new-changes-up-until-now"></a>Esecuzione di query per tutte le nuove modifiche apportate finora  
 Un vincolo tipico posto sulle modifiche restituite da una funzione di query consiste nella necessità di dover includere solo le modifiche che si sono verificate tra la richiesta precedente e la data e l'ora correnti. Per questa query, applicare la funzione sys.fn_cdc_increment_lsn al valore @from_lsn usato nella richiesta precedente per determinare il limite inferiore. Poiché il limite superiore dell'intervallo di tempo viene espresso come momento specifico nel tempo, è necessario convertirlo in un valore LSN prima che possa essere utilizzato da una funzione di query. Prima di poter convertire il valore datetime in un valore LSN corrispondente, è necessario assicurarsi che il processo di acquisizione abbia elaborato tutte le modifiche di cui è stato eseguito il commit attraverso il limite superiore specificato. Solo così è possibile assicurarsi che tutte le modifiche valide siano state propagate alla tabella delle modifiche. Un modo possibile per eseguire questa operazione consiste nel strutturare un ciclo di attesa che controlli periodicamente se il valore LSN di commit massimo corrente registrato per qualsiasi tabella delle modifiche del database supera l'ora di fine desiderata dell'intervallo della richiesta.  
  
 Dopo che il ciclo di ritardo verifica se il processo di acquisizione abbia già elaborato tutte le voci di log rilevanti, usare la funzione [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) per determinare il nuovo endpoint alto espresso come un valore LSN. Per assicurarsi che tutte le voci di cui è stato eseguito il commit nel periodo di tempo specificato siano state recuperate, chiamare la funzione sys.fn_cdc_map_time_to_lsn e utilizzare l'opzione 'largest less than or equal'.  
  
> [!NOTE]  
>  In periodi di inattività, viene aggiunta una voce fittizia alla tabella cdc.lsn_time_mapping per contrassegnare il fatto che il processo di acquisizione ha elaborato le modifiche entro un periodo di commit specificato. Ciò evita che il processo sembri in ritardo con l'acquisizione, quando invece semplicemente non esistono modifiche recenti da elaborare.  
  
 Il modello Enumerate All Changes Up Until Now è una dimostrazione di come utilizzare la strategia precedente per eseguire query per i dati delle modifiche.  
  
### <a name="adding-a-commit-time-to-an-all-changes-result-set"></a>Aggiunta di un'ora di commit a un set di risultati di tutte le modifiche  
 L'ora di commit di ogni transazione con una voce associata in una tabella delle modifiche del database è disponibile nella tabella [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md). Unendo in join il valore __$start_lsn restituito in una richiesta di tutte le modifiche al valore start_lsn di una voce della tabella cdc.lsn_time_mapping, è possibile restituire il valore tran_end_time insieme ai dati delle modifiche per contrassegnare la modifica con l'ora di commit della transazione all'origine. Il modello Append Commit Time to All Changes Result Set è una dimostrazione di come eseguire questo join.  
  
### <a name="joining-change-data-with-other-data-from-the-same-transaction"></a>Join dei dati delle modifiche con altri dati della stessa transazione  
 È talvolta utile creare un join dei dati delle modifiche con altre informazioni raccolte sulla transazione quando il relativo commit viene eseguito all'origine. Nella colonna tran_begin_lsn della tabella cdc.lsn_time_mapping sono contenute le informazioni necessarie per eseguire questo join. Quando si verifica l'aggiornamento dell'origine, il valore di database_transaction_begin_lsn della vista dinamica del sistema [sys.dm_tran_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) deve essere salvato insieme a qualsiasi altra informazione da unire con i dati delle modifiche. Utilizzare la funzione fn_convertnumericlsntobinary per confrontare i valori database_transaction_begin_lsn e tran_begin_lsn. Il codice per creare questa funzione è disponibile nel modello Create Function fn_convertnumericlsntobinary. Il modello Return All Changes with a Given tran_begin_lsn è una dimostrazione di come attuare il join.  
  
### <a name="querying-using-datetime-wrapper-functions"></a>Esecuzione di query utilizzando le funzioni del wrapper datetime  
 Un tipico scenario dell'applicazione relativo all'esecuzione di query per i dati delle modifiche consiste nel richiedere periodicamente i dati delle modifiche tramite una finestra temporale scorrevole delimitata da valori datetime. Per questa classe di consumer, Change Data Capture fornisce la stored procedure [sys.sp_cdc_generate_wrapper_function](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md) che consente di generare script per creare funzioni wrapper personalizzate per le funzioni di query di Change Data Capture. Questi wrapper personalizzati consentono di esprimere l'intervallo di query come coppia datetime.  
  
 Le opzioni di chiamata per la stored procedure consentono di generare wrapper per tutte le istanze di acquisizione a cui può accedere il chiamante o per una sola istanza di acquisizione specificata. Le opzioni supportate includono inoltre la possibilità di specificare se l'endpoint alto dell'intervallo di acquisizione deve essere aperto o chiuso, quale colonna acquisita disponibile deve essere inclusa nel set di risultati e a quali colonne incluse è necessario associare flag di aggiornamento. La procedura restituisce un set di risultati con due colonne: il nome della funzione generata, derivabile dal nome dell'istanza di acquisizione, e l'istruzione CREATE per la stored procedure del wrapper. La funzione per eseguire il wrapping della query di tutte le modifiche viene sempre generata. Se il parametro @supports_net_changes è stato impostato in fase di creazione dell'istanza di acquisizione, viene anche generata la funzione di wrapping della query per le modifiche delta.  
  
 È responsabilità del progettista dell'applicazione chiamare la stored procedure per la generazione dello script per generare le istruzioni CREATE per le stored procedure del wrapper ed eseguire gli script di creazione risultanti per creare le funzioni. Questo processo non viene eseguito automaticamente alla creazione di un'istanza di acquisizione.  
  
 I wrapper datetime sono di proprietà dell'utente e non vengono creati nello schema predefinito del chiamante. La funzione generata è utilizzabile dalla maggior parte degli utenti senza necessità di apportare modifiche. Lo script generato può comunque essere ulteriormente personalizzato prima di creare la funzione.  
  
 Il nome della funzione di wrapping della query per tutte le modifiche è fn_all_changes_ seguito dal nome dell'istanza di acquisizione. Il prefisso utilizzato per il wrapper delle modifiche delta è fn_net_changes_. Entrambe le funzioni accettano tre argomenti, proprio come le funzioni con valori di tabella di Change Data Capture associate. Tuttavia, l'intervallo di query per i wrapper è limitato da due valori datetime e non da due valori LSN. Il parametro @row_filter_option è identico per entrambi i set di funzioni.  
  
 Le funzioni wrapper generate supportano la convenzione seguente per l'esame sistematico della cronologia di Change Data Capture: si prevede che il parametro @end_time dell'intervallo precedente venga usato come parametro @start_time dell'intervallo successivo. La funzione wrapper esegue il mapping dei valori datetime ai valori LSN e si assicura che nessun dato venga perso o ripetuto se viene seguita questa convenzione.  
  
 È possibile generare i wrapper affinché supportino un limite superiore chiuso o un limite superiore aperto nella finestra di query specificata. Il chiamante può quindi specificare se le voci con un'ora di commit corrispondente al limite superiore dell'intervallo di estrazione debbano essere incluse nell'intervallo. Per impostazione predefinita, il limite superiore è incluso.  
  
 Se le funzioni con valori di tabella della query generata hanno esito negativo nel caso in cui venga fornito un valore Null per @from_lsn o @to_lsn, le funzioni del wrapper datetime usano Null per consentire ai wrapper datetime di restituire tutte le modifiche correnti. Se Null viene passato come endpoint basso della finestra di query al wrapper datetime, l'endpoint basso dell'intervallo di validità dell'istanza di acquisizione viene utilizzato nell'istruzione SELECT sottostante applicata alla funzione con valori di tabella della query. Analogamente, se Null viene passato come endpoint alto della finestra di query, l'endpoint alto dell'intervallo di validità dell'istanza di acquisizione viene utilizzato per la selezione eseguita dalla funzione con valori di tabella della query.  
  
 Il set di risultati restituito da una funzione wrapper include tutte le colonne richieste seguite da una colonna dell'operazione, registrata come uno o due caratteri per identificare l'operazione associata alla riga. Se sono stati richiesti flag di aggiornamento, vengono visualizzati come colonne bit dopo il codice dell'operazione, nell'ordine specificato nel parametro @update_flag_list. Per informazioni sulle opzioni di chiamata per la personalizzazione dei wrapper datetime generati, vedere [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md).  
  
 Il modello Instantiate a Wrapper TVF With Update Flag è una dimostrazione di come personalizzare una funzione wrapper generata per aggiungere un flag di aggiornamento per una colonna specificata al set di risultati restituito da una query delle modifiche delta. Il modello Instantiate CDC Wrapper TVFs for a Schema è una dimostrazione di come creare un'istanza dei wrapper datetime per le funzioni con valori di tabella delle query per tutte le istanze di acquisizione create per le tabelle di origine in un determinato schema del database.  
  
 Per un esempio di utilizzo di un wrapper datetime per eseguire una query per i dati delle modifiche, vedere il modello Get Net Changes Using Wrapper With Update Flags. Questo modello è una dimostrazione di come eseguire query per le modifiche delta con una funzione wrapper quando il wrapper è configurato per la restituzione di flag di aggiornamento. Si noti che l'opzione del filtro di riga 'all with mask' è necessaria affinché la funzione di query sottostante restituisca una maschera di aggiornamento non Null all'aggiornamento. I valori Null vengono passati per i limiti inferiore e superiore dell'intervallo datetime per indicare alla funzione di utilizzare l'endpoint basso e l'endpoint alto dell'intervallo di validità per l'istanza di acquisizione durante l'esecuzione della query basata su LSN sottostante. La query restituisce una riga per ogni modifica a una riga di origine che si è verificata nell'intervallo valido per l'istanza di acquisizione.  
  
### <a name="using-the-datetime-wrapper-functions-to-transition-between-capture-instances"></a>Utilizzo delle funzioni wrapper datetime per la transizione tra istanze di acquisizione  
 Change Data Capture supporta fino a due istanze di acquisizione per una singola tabella di origine in cui viene eseguito il rilevamento delle modifiche. L'utilizzo principale di questa funzionalità consiste nell'inserire una transizione tra più istanze di acquisizione quando le modifiche DDL (Data Definition Language) apportate alla tabella di origine espandono il set di colonne disponibili per il rilevamento. Durante la transizione a una nuova istanza di acquisizione, è possibile proteggere i livelli dell'applicazione più elevati dalle modifiche ai nomi delle funzioni di query sottostanti eseguendo il wrapping della chiamata sottostante tramite un'apposita funzione. Assicurarsi che il nome della funzione wrapper rimanga invariato. Al momento della transizione, è possibile eliminare la funzione wrapper precedente e crearne una nuova con lo stesso nome che faccia riferimento alle nuove funzioni di query. Modificando lo script generato per creare una funzione wrapper con lo stesso nome, è possibile passare a una nuova istanza di acquisizione senza influire sui livelli dell'applicazione più elevati.  
  
## <a name="see-also"></a>Vedere anche  
 [Tenere traccia delle modifiche ai dati &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Informazioni su Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Abilitare e disabilitare Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [Amministrare e monitorare Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
