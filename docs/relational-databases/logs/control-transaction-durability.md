---
title: Controllare la durabilità delle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 09/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- delayed durability
- Lazy Commit
ms.assetid: 3ac93b28-cac7-483e-a8ab-ac44e1cc1c76
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ac96a7ea691a02c61aa132ea0efcdf5bc2d68ab1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62707129"
---
# <a name="control-transaction-durability"></a>Controllo della durabilità delle transazioni
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Il commit delle transazioni di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere completamente durevole, l'impostazione predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , oppure con durabilità ritardata (noto come Lazy Commit).    
    
 Il commit delle transazioni completamente durevole è sincrono e segnala il completamento del commit restituendo il controllo al client solo dopo che i record del log per la transazione vengono scritti su disco. Il commit delle transazioni con durabilità ritardata è asincrono e segnala il completamento del commit prima che i record del log per la transazione vengano scritti su disco. La scrittura delle voci di log delle transazioni su disco è necessaria affinché una transazione sia durevole. Le transazioni con durabilità ritardata diventano durevoli quando le voci di log delle transazioni vengono scaricate su disco.    
    
 In questo argomento vengono descritte in dettaglio le transazioni con durabilità ritardata.    
    
## <a name="full-vs-delayed-transaction-durability"></a>Transazioni completamente durevoli e  transazioni con durabilità ritardata    
 Le transazioni con durabilità completa e quelle con durabilità ritardata hanno sia vantaggi che svantaggi. Un'applicazione può contenere una combinazione di transazioni completamente durevoli e transazioni con durabilità ritardata. È necessario valutare attentamente le esigenze aziendali e determinare quale dei due tipi vi si adatti meglio.    
    
### <a name="full-transaction-durability"></a>Transazioni con durabilità completa    
 Le transazioni completamente durevoli scrivono il log delle transazioni su disco prima di restituire il controllo al client. Utilizzare le transazioni con durabilità completa ogni volta che:    
    
-   Il sistema non può tollerare alcuna perdita di dati.     
    Per informazioni sul momento in cui può verificarsi una perdita di dati, vedere la sezione [Quando può verificarsi una perdita di dati?](../../relational-databases/logs/control-transaction-durability.md#bkmk_DataLoss) .    
    
-   Il collo di bottiglia non è causato dalla latenza di scrittura del log delle transazioni.    
    
 Le transazioni con durabilità ritardata riducono la latenza causata dall'I/O del log mantenendo i record del log delle transazioni in memoria e scrivendo nel log delle transazioni in batch, richiedendo pertanto un numero minore di operazioni di I/O. Le transazioni con durabilità ritardata riducono potenzialmente la contesa di I/O del log, riducendo pertanto le attese del sistema.    
    
 **Garanzie delle transazioni con durabilità completa**    
    
-   Una volta completato il commit della transazione, le modifiche apportate dalla transazione sono visibili alle altre transazioni nel sistema. Per altre informazioni sui livelli di isolamento delle transazioni, vedere [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md) o [Transactions with Memory-Optimized Tables](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md) (Transazioni con tabelle con ottimizzazione per la memoria).    
    
-   La durabilità è garantita in fase di commit. I record di log corrispondenti vengono salvati in modo permanente sul disco prima del completamento del commit delle transazioni restituendo il controllo al client.    
    
### <a name="delayed-transaction-durability"></a>Transazioni con durabilità ritardata    
 Le transazioni con durabilità ritardata vengono eseguite utilizzando scritture del log su disco asincrone. I record del log delle transazioni vengono mantenuti in un buffer e vengono scritti su disco quando il buffer si riempie o quando si verifica un evento di scaricamento del buffer. Le transazioni con durabilità ritardata riducono la latenza e la contesa nel sistema in quanto:    
    
-   L'elaborazione del commit delle transazioni non attende il completamento delle operazioni di I/O del log e la restituzione del controllo al client.    
    
-   La contesa di I/O del log da parte delle transazioni simultanee è meno probabile; al contrario, il buffer del log può essere scaricato su disco in blocchi più grandi, riducendo la contesa e aumentando la velocità effettiva.    
    
    > [!NOTE]    
    >  È comunque possibile che si verifichi una contesa di I/O del log se esiste un livello elevato di concorrenza, specialmente se il buffer del log si riempie più velocemente di quanto si scarichi.    
    
 #### <a name="when-to-use-delayed-transaction-durability"></a>Quando utilizzare le transazioni con durabilità ritardata    
    
 Alcuni dei casi in cui è possibile trarre vantaggio dall'utilizzo delle transazioni con durabilità ritardata sono:    
    
 **Possibilità di tollerare un'eventuale perdita di dati.**     
 Se è possibile tollerare un'eventuale perdita di dati, ad esempio la perdita di singoli record non cruciali, purché si disponga della maggior parte dei dati, potrebbe essere opportuno considerare la durabilità ritardata. Se non è possibile tollerare un'eventuale perdita di dati, non utilizzare le transazioni con durabilità ritardata.    
    
 **Collo di bottiglia nella scrittura del log delle transazioni.**     
 Se i problemi di prestazioni sono dovuti alla latenza nella scrittura del log delle transazioni, l'applicazione probabilmente trarrà vantaggio dall'utilizzo delle transazioni con durabilità ritardata.    
    
 **Carichi di lavoro con una frequenza elevata di contesa.**     
 Se nel sistema sono presenti carichi di lavoro con un livello elevato di contesa, si perde molto tempo nell'attesa del rilascio dei blocchi. Le transazioni con durabilità ritardata riducono il tempo di commit rilasciando i blocchi più velocemente con una velocità effettiva più elevata.    
    
 ### <a name="delayed-transaction-durability-guarantees"></a>Garanzie delle transazioni con durabilità ritardata   
    
-   Una volta completato il commit della transazione, le modifiche apportate dalla transazione sono visibili alle altre transazioni nel sistema.    
    
-   La durabilità delle transazioni viene garantita solo in seguito a uno scaricamento su disco del log delle transazioni in memoria. Il log delle transazioni in memoria viene scaricato su disco quando:    
    
    -   Una transazione completamente durevole nello stesso database apporta una modifica nel database e ne viene completato il commit.   
    
    -   L'utente esegue correttamente la stored procedure di sistema `sp_flush_log` .     
    
        Se viene completato il commit di una transazione completamente durevole o di sp_flush_log, si è certi che tutte le transazioni con durabilità ritardata di cui è stato eseguito il commit in precedenza sono state rese durevoli.
        
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prova a scaricare il log su disco sia in base alla generazione dei log che all'intervallo di tempo, anche se tutte le transazioni sono con durabilità ritardata. Questo tentativo in genere riesce se il dispositivo I/O è aggiornato. Tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non fornisce alcuna garanzia effettiva di durabilità oltre alle transazioni durevoli e a sp_flush_log.      
    
  
    
## <a name="how-to-control-transaction-durability"></a>Come controllare la durabilità delle transazioni    
    
###  <a name="bkmk_DbControl"></a> Controllo a livello di database    
 L'amministratore del database può controllare se gli utenti possono utilizzare le transazioni con durabilità ritardata in un database con l'istruzione seguente. È necessario impostare il valore per la durabilità ritardata con ALTER DATABASE.    
    
```sql    
ALTER DATABASE ... SET DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }    
```    
    
 **DISABLED**    
 [impostazione predefinita] Con questa impostazione, tutte le transazioni di cui è stato eseguito il commit nel database sono completamente durevoli, indipendentemente dall'impostazione del livello di commit (DELAYED_DURABILITY=[ON | OFF]). Non è necessaria alcuna modifica e ricompilazione delle stored procedure. In questo modo è possibile garantire che i dati non verranno in alcun modo messi in pericolo dalla durabilità ritardata.    
    
 **ALLOWED**    
 Con questa impostazione, la durabilità di ogni transazione viene determinata a livello di transazione (DELAYED_DURABILITY = { *OFF* | ON }). Per altre informazioni, vedere [Controllo a livello di blocco atomico: stored procedure compilate in modo nativo](../../relational-databases/logs/control-transaction-durability.md#CompiledProcControl) e [Controllo a livello di COMMIT - Transact-SQL](../../relational-databases/logs/control-transaction-durability.md#bkmk_T-SQLControl).    
    
 **FORCED**    
 Con questa impostazione, ogni transazione di cui viene eseguito il commit nel database è con durabilità ritardata. Indipendentemente dal fatto che venga specificata una transazione completamente durevole (DELAYED_DURABILITY = OFF) o non venga specificata alcuna impostazione, la transazione è con durabilità ritardata. Tale impostazione risulta utile quando è necessario specificare le transazioni con durabilità ritardata per un database e non si desidera modificare il codice dell'applicazione.    
    
###  <a name="CompiledProcControl"></a> Controllo a livello di blocco atomico: stored procedure compilate in modo nativo    
 Il codice seguente va inserito nel blocco atomico.    
    
```sql    
DELAYED_DURABILITY = { OFF | ON }    
```    
    
 **OFF**    
 [impostazione predefinita] La transazione è completamente durevole, a meno che non sia attiva l'opzione di database DELAYED_DURABLITY = FORCED, nel qual caso il commit è asincrono e pertanto con durabilità ritardata. Per altre informazioni, vedere [Controllo a livello di database](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) .    
    
 **ON**    
 La transazione è con durabilità ritardata, a meno che non sia attiva l'opzione di database DELAYED_DURABLITY = DISABLED, nel qual caso il commit è sincrono e pertanto completamente durevole.  Per altre informazioni, vedere [Controllo a livello di database](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) .    
    
 **Codice di esempio:**    
    
```sql    
CREATE PROCEDURE <procedureName> ...    
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER    
AS BEGIN ATOMIC WITH     
(    
    DELAYED_DURABILITY = ON,    
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,    
    LANGUAGE = N'English'    
    ...    
)    
END    
```    
    
### <a name="table-1-durability-in-atomic-blocks"></a>Tabella 1: durabilità nei blocchi ATOMIC    
    
|Opzione di durabilità nei blocchi atomici|Nessuna transazione esistente|Transazione in corso (completamente durevole o con durabilità ritardata)|    
|------------------------------------|-----------------------------|---------------------------------------------------------|    
|**DELAYED_DURABILITY = OFF**|Il blocco atomico avvia una nuova transazione completamente durevole.|Il blocco atomico crea un punto di salvataggio nella transazione esistente, quindi avvia una nuova transazione.|    
|**DELAYED_DURABILITY = ON**|Il blocco atomico avvia una nuova transazione con durabilità ritardata.|Il blocco atomico crea un punto di salvataggio nella transazione esistente, quindi avvia una nuova transazione.|    
    
###  <a name="bkmk_T-SQLControl"></a> Controllo a livello di COMMIT -[!INCLUDE[tsql](../../includes/tsql-md.md)]    
 La sintassi di COMMIT viene estesa in modo da poter forzare le transazioni con durabilità ritardata. Se DELAYED_DURABILITY è DISABLED o FORCED a livello di database (vedere sopra) questa opzione di COMMIT viene ignorata.    
    
```sql    
COMMIT [ { TRAN | TRANSACTION } ] [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]    
    
```    
    
 **OFF**    
 [impostazione predefinita] Il COMMIT della transazione è completamente durevole, a meno che non sia attiva l'opzione di database DELAYED_DURABLITY = FORCED, nel qual caso il COMMIT è asincrono e pertanto con durabilità ritardata. Per altre informazioni, vedere [Controllo a livello di database](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) .    
    
 **ON**    
 Il COMMIT della transazione è con durabilità ritardata, a meno che non sia attiva l'opzione di database DELAYED_DURABLITY = DISABLED, nel qual caso il COMMIT è sincrono e pertanto completamente durevole. Per altre informazioni, vedere [Controllo a livello di database](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) .    
    
### <a name="summary-of-options-and-their-interactions"></a>Riepilogo delle opzioni e relative interazioni    
 Nella tabella seguente vengono riepilogate le interazioni tra le impostazioni di durabilità ritardata a livello di database e le impostazioni a livello di commit. Le impostazioni a livello di database hanno sempre la precedenza sulle impostazioni a livello di commit.    
    
|Impostazione di COMMIT/Impostazione di database|DELAYED_DURABILITY = DISABLED|DELAYED_DURABILITY = ALLOWED|DELAYED_DURABILITY = FORCED|    
|--------------------------------------|-------------------------------------|------------------------------------|-----------------------------------|    
|**DELAYED_DURABILITY = OFF** Transazioni a livello di database.|La transazione è completamente durevole.|La transazione è completamente durevole.|La transazione è con durabilità ritardata.|    
|**DELAYED_DURABILITY = ON** Transazioni a livello di database.|La transazione è completamente durevole.|La transazione è con durabilità ritardata.|La transazione è con durabilità ritardata.|    
|**DELAYED_DURABILITY = OFF** Transazione distribuita o tra database.|La transazione è completamente durevole.|La transazione è completamente durevole.|La transazione è completamente durevole.|    
|**DELAYED_DURABILITY = ON** Transazione distribuita o tra database.|La transazione è completamente durevole.|La transazione è completamente durevole.|La transazione è completamente durevole.|    
    
## <a name="how-to-force-a-transaction-log-flush"></a>Come forzare lo scaricamento di un log delle transazioni    
 Sono disponibili due metodi per forzare lo scaricamento del log delle transazioni su disco.    
    
-   Eseguire una transazione completamente durevole che modifica lo stesso database. In questo modo viene forzato lo scaricamento su disco dei record del log di tutte transazioni con durabilità ritardata di cui è stato eseguito il commit in precedenza.    
    
-   Eseguire la stored procedure di sistema `sp_flush_log`. In questo modo viene forzato lo scaricamento su disco dei record del log di tutte transazioni con durabilità ritardata di cui è stato eseguito il commit in precedenza. Per altre informazioni, vedere [sys.sp_flush_log &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-flush-log-transact-sql.md).    
    
##  <a name="bkmk_OtherSQLFeatures"></a>Durabilità ritardata e altre funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]    
 **Rilevamento delle modifiche e Change Data Capture**    
 Tutte le transazioni con rilevamento delle modifiche sono completamente durevoli. Una transazione dispone della proprietà di rilevamento delle modifiche se esegue operazioni di scrittura in tabelle abilitate per il rilevamento delle modifiche. L'uso di durabilità posticipata non è supportato per i database che usano Change Data Capture (CDC).    
    
 **Recupero a seguito dell'arresto anomalo del sistema**    
 La coerenza è garantita, ma alcune modifiche delle transazioni con durabilità ritardata di cui è stato eseguito il commit possono andare perse.    
    
 **Transazione distribuita o tra database**    
 Se una transazione è distribuita o tra database, è completamente durevole, indipendentemente da qualsiasi impostazione del commit della transazione o del database.    
    
 **Gruppi di disponibilità AlwaysOn e mirroring**    
 Le transazioni con durabilità ritardata non garantiscono alcuna durabilità nel database primario né in quelli secondari. Inoltre, non garantiscono informazioni sulla transazione nel database secondario. Dopo il commit, il controllo viene restituito al client prima che venga ricevuto un acknowledgement da un database secondario sincrono. La replica in repliche secondarie continua a verificarsi come scaricamento su disco per la replica primaria.   
    
 **Clustering di failover**    
 Alcune scritture delle transazioni con durabilità ritardata potrebbero andare perse.    
    
 **Replica transazionale**    
 La replica transazionale non supporta le transazioni con durabilità ritardata.    
    
 **Log shipping**    
 Solo le transazioni che sono diventate durevoli vengono incluse nel log shipping.    
    
 **Backup del log**    
 Solo le transazioni che sono diventate durevoli vengono incluse nel backup.    
    
##  <a name="bkmk_DataLoss"></a> Quando può verificarsi una perdita di dati?    
 Se si implementa la durabilità ritardata in una delle tabelle, è importante comprendere che in determinate circostanze può verificarsi una perdita di dati. Se non è possibile tollerare un'eventuale perdita di dati, è consigliabile non usare la durabilità ritardata nelle tabelle.    
    
### <a name="catastrophic-events"></a>Eventi irreversibili    
 Nel caso di un evento irreversibile, come ad esempio un arresto anomalo del server, si verificherà una perdita di dati per tutte le transazioni di cui è stato eseguito il commit che non sono state salvate su disco. Le transazioni con durabilità ritardata vengono salvate su disco ogni volta che in una tabella del database (durevole ottimizzata per la memoria o basata su disco) viene eseguita una transazione completamente durevole o viene chiamato `sp_flush_log`. Se si usano le transazioni con durabilità ritardata, è possibile creare una tabella di piccole dimensioni nel database da aggiornare periodicamente oppure è possibile chiamare periodicamente `sp_flush_log` per salvare tutte le transazioni in sospeso di cui è stato eseguito il commit. Inoltre, il log delle transazioni viene scaricato ogni volta che diventa pieno, condizione che però è difficile da prevedere e impossibile da controllare.    
    
### <a name="includessnoversionincludesssnoversion-mdmd-shutdown-and-restart"></a>Arresto e riavvio di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]    
 Per la durabilità ritardata non esiste alcuna differenza tra un arresto imprevisto e un arresto/riavvio previsto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Analogamente agli eventi irreversibili, occorre prevedere la possibilità di una perdita di dati. In un arresto/riavvio pianificato alcune transazioni che non sono state scritte su dico possono essere prima salvate su disco ma non è una condizione che è possibile pianificare. Considerare un arresto/riavvio, indipendentemente che sia pianificato o meno, allo stesso modo di un evento irreversibile in cui può verificarsi una perdita di dati.    
    
## <a name="see-also"></a>Vedere anche    
 [Transactions with Memory-Optimized Tables](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)    
    
  
