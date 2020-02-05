---
title: Filtri di riga con parametri | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], dynamic filters
- merge replication [SQL Server replication], dynamic filters
- parameterized filters [SQL Server replication]
- filters [SQL Server replication], dynamic
- merge replication parameterized filters [SQL Server replication]
- publications [SQL Server replication], parameterized filters
- parameterized filters [SQL Server replication], about parameterized filters
- filters [SQL Server replication], parameterized
- dynamic filters [SQL Server replication]
ms.assetid: b48a6825-068f-47c8-afdc-c83540da4639
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3dee5b4c6522afd93591d1e8aa0c94052d41d9bd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71711060"
---
# <a name="parameterized-filters---parameterized-row-filters"></a>Filtri con parametri - Filtri di riga con parametri
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  I filtri di riga con parametri consentono l'invio di partizioni di dati diverse a Sottoscrittori diversi senza che sia necessario creare più pubblicazioni. Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], i filtri con parametri vengono definiti filtri dinamici. Una partizione è un subset delle righe di una tabella. In base alle impostazioni scelte durante la creazione di un filtro di riga con parametri, ogni riga di una tabella pubblicata può appartenere a un'unica partizione, con la conseguente produzione di partizioni non sovrapposte, o a due o più partizioni, con la conseguente produzione di partizioni sovrapposte.  
  
 È possibile condividere le partizioni non sovrapposte tra sottoscrizioni oppure limitarle in modo che solo una sottoscrizione riceva una determinata partizione. Le impostazioni che controllano il comportamento delle partizioni vengono descritte nella sezione "Utilizzo delle opzioni di filtro appropriate" di seguito in questo argomento. L'utilizzo di tali impostazioni consente di personalizzare il filtro con parametri in base ai requisiti dell'applicazione e delle prestazioni. In generale, le partizioni sovrapposte offrono maggiore flessibilità, mentre le partizioni non sovrapposte replicate in una singola sottoscrizione garantiscono prestazioni superiori.  
  
 I filtri con parametri vengono utilizzati in una tabella singola e vengono in genere uniti ai filtri join per estendere il filtro alle tabelle correlate. Per altre informazioni, vedere [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
 Per definire o modificare un filtro di riga con parametri, vedere [Definizione e modifica di un filtro di riga con parametri per un articolo di merge](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
## <a name="how-parameterized-filters-work"></a>Modalità di funzionamento dei filtri con parametri  
 Un filtro di riga con parametri utilizza una clausola WHERE per selezionare i dati appropriati da pubblicare. Anziché specificare un valore letterale nella clausola, come avviene con il filtro di riga statico, si specificano una o entrambe le funzioni di sistema seguenti: SUSER_SNAME() e HOST_NAME(). È anche possibile utilizzare funzioni definite dall'utente, ma è necessario che le funzioni di sistema SUSER_SNAME() o HOST_NAME() siano incluse nel corpo della funzione oppure vengano valutate, ad esempio `MyUDF(SUSER_SNAME()`. Se una funzione definita dall'utente include SUSER_SNAME() o HOST_NAME() nel corpo della funzione, non è possibile passare parametri alla funzione.  
  
 Le funzioni di sistema SUSER_SNAME() e HOST_NAME() non sono specifiche della replica di tipo merge, ma vengono utilizzate da questo tipo di replica per il filtro con parametri:  
  
-   SUSER_SNAME() restituisce informazioni di accesso per le connessioni stabilite a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Quando viene impiegata in un filtro con parametri, restituisce le informazioni di accesso utilizzate dall'agente di merge per connettersi al server di pubblicazione. Le informazioni di accesso vengono specificate quando si crea una sottoscrizione.  
  
-   HOST_NAME() restituisce il nome del computer che sta effettuando la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Quando viene impiegata in un filtro con parametri, per impostazione predefinita restituisce il nome del computer in cui è in esecuzione l'agente di merge. Per le sottoscrizioni pull è il nome del Sottoscrittore, mentre per le sottoscrizioni push è il nome del server di distribuzione.  
  
     È inoltre possibile sostituire questa funzione con un valore diverso dal nome del Sottoscrittore o del server di distribuzione. In genere il valore di questa funzione viene sostituito con valori più significativi, ad esempio il nome o l'ID del venditore. Per ulteriori informazioni, vedere la sezione relativa alla sostituzione del valore di HOST_NAME() in questo argomento.  
  
 Il valore restituito dalla funzione di sistema viene confrontato con una colonna specificata nella tabella in cui viene applicato il filtro e i dati appropriati vengono scaricati nel Sottoscrittore. Il confronto viene effettuato quando la sottoscrizione è inizializzata, in modo che solo i dati appropriati siano contenuti nello snapshot iniziale, e ogni volta che la sottoscrizione viene sincronizzata. Per impostazione predefinita, se una modifica nel server di pubblicazione ha come conseguenza la rimozione di una riga da una partizione, la riga viene eliminata nel Sottoscrittore. Questo comportamento viene controllato tramite il parametro `@allow_partition_realignment` di [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
> [!NOTE]  
>  Quando i confronti vengono effettuati per i filtri con parametri, vengono sempre utilizzate le regole di confronto del database. Se, ad esempio, nelle regole di confronto del database non viene fatta distinzione tra maiuscole e minuscole, mentre in quelle della colonna o della tabella sì, durante il confronto non viene fatta tale distinzione.  
  
### <a name="filtering-with-suser_sname"></a>Applicazione del filtro con SUSER_SNAME()  
 Si consideri la tabella **Employee Table** nel database di esempio [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] . In questa tabella è inclusa la colonna **LoginID**, contenente l'account di accesso per ogni dipendente nel formato*dominio\account accesso*. Per filtrare questa tabella in modo che i dipendenti ricevano solo i dati pertinenti, specificare una clausola di filtro:  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 Il valore per uno dei dipendenti è, ad esempio, "adventure-works\john5". Quando l'agente di merge si connette al server di pubblicazione, utilizza l'account di accesso specificato durante la creazione della sottoscrizione, in questo caso "adventure-works\john5". L'agente di merge confronta quindi il valore restituito da SUSER_SNAME() con i valori nella tabella e scarica solo la riga che contiene un valore di "adventure-works\john5" nella colonna **LoginID** .  
  
### <a name="filtering-with-host_name"></a>Applicazione del filtro con HOST_NAME()  
 Si consideri la tabella **HumanResources.Employee** . Si supponga che in questa tabella sia inclusa una colonna **ComputerName** con il nome del computer di ogni dipendente nel formato*nome_tipo di computer*. Per filtrare questa tabella in modo che i dipendenti ricevano solo i dati pertinenti, specificare una clausola di filtro:  
  
```  
ComputerName = HOST_NAME()  
```  
  
 Il valore per uno dei dipendenti potrebbe ad esempio essere "john5_laptop". Quando l'agente di merge si connette al server di pubblicazione, confronta il valore restituito da HOST_NAME() con i valori nella tabella e scarica solo la riga che contiene un valore di "john5_laptop" nella colonna **ComputerName** .  
  
 Le funzioni possono inoltre essere combinate in un filtro. Per essere certi che un dipendente riceva i dati solo nel caso utilizzi il proprio account di accesso nel computer, ad esempio, la clausola di filtro sarà:  
  
```  
LoginID = SUSER_SNAME() AND ComputerName = HOST_NAME()  
```  
  
 A meno che non si sostituisca il valore di HOST_NAME(), il filtro con HOST_NAME() viene in genere utilizzato solo con le sottoscrizioni pull. Il valore restituito dalla funzione è il nome del computer in cui è in esecuzione l'agente di merge. Per quanto riguarda le sottoscrizioni pull, il valore è diverso per ogni sottoscrizione, mentre per quanto riguarda le sottoscrizioni push il valore è identico. Per le sottoscrizioni push tutti gli agenti di merge vengono eseguiti nel server di distribuzione.  
  
> [!IMPORTANT]  
>  Poiché è possibile sostituire il valore della funzione HOST_NAME(), per controllare l'accesso a partizioni di dati non è possibile utilizzare filtri che includano HOST_NAME(). Per controllare l'accesso a partizioni di dati, utilizzare SUSER_SNAME(), SUSER_SNAME() in combinazione con HOST_NAME() oppure filtri di riga statici.  
  
#### <a name="overriding-the-host_name-value"></a>Sostituzione del valore di HOST_NAME()  
 Come già evidenziato, per impostazione predefinita HOST_NAME() restituisce il nome del computer che sta effettuando la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Quando vengono utilizzati filtri con parametri, è normale sostituire questo valore fornendo un valore durante la creazione di una sottoscrizione. La funzione HOST_NAME() restituisce quindi il valore specificato anziché il nome del computer.  
  
> [!NOTE]  
>  Se si sostituisce il valore HOST_NAME(), tutte le chiamate alla funzione HOST_NAME() restituiranno il valore specificato dall'utente. Verificare che il funzionamento di altre applicazioni non dipenda dal fatto che HOST_NAME() restituisca il nome del computer.  
  
 Si consideri la tabella **HumanResources.Employee** . In questa tabella è inclusa la colonna **EmployeeID**. Per filtrare questa tabella in modo che ogni dipendente riceva solo i dati di pertinenza, specificare una clausola di filtro:  
  
 `EmployeeID = CONVERT(int,HOST_NAME())`  
  
 Alla dipendente Pamela Ansman-Wolfe, ad esempio, è stato associato l'ID 280. Specificare il valore dell'ID del dipendente (280 nell'esempio) come valore di HOST_NAME() durante la creazione di una sottoscrizione per questo dipendente. Quando l'agente di merge si connette al server di pubblicazione, confronta il valore restituito da HOST_NAME() con i valori nella tabella e scarica solo la riga che contiene un valore di 280 nella colonna **EmployeeID** .  
  
> [!IMPORTANT]
>  La funzione HOST_NAME() restituisce un valore **nchar** . Se la colonna nella clausola di filtro è di un tipo di dati numerico, come nell'esempio sopra riportato, è pertanto necessario utilizzare CONVERT. Per motivi relativi alle prestazioni, è consigliabile non applicare funzioni ai nomi di colonna nelle clausole di filtro di riga con parametri, come `CONVERT(nchar,EmployeeID) = HOST_NAME()`. È consigliabile invece utilizzare l'approccio indicato nell'esempio: `EmployeeID = CONVERT(int,HOST_NAME())`. Questa clausola può essere usata per il parametro `@subset_filterclause` di [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), ma in genere non può essere adottata nella Creazione guidata nuova pubblicazione. La procedura guidata esegue la clausola di filtro per la relativa convalida, ma tale operazione ha esito negativo poiché il nome del computer non può essere convertito in un tipo di dati **int**. Se si utilizza la Creazione guidata nuova pubblicazione, è consigliabile specificare `CONVERT(nchar,EmployeeID) = HOST_NAME()` nella procedura guidata e quindi utilizzare [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) per modificare la clausola in `EmployeeID = CONVERT(int,HOST_NAME())` prima della creazione di uno snapshot per la pubblicazione.  
  
 **Per sostituire il valore di HOST_NAME()**  
  
 Utilizzare uno dei metodi seguenti per sostituire il valore di HOST_NAME():  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: specificare un valore nella pagina **Valori HOST\_NAME\(\)** della Creazione guidata nuova sottoscrizione. Per altre informazioni sulla creazione di sottoscrizioni, vedere [Sottoscrivere le pubblicazioni](../../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Programmazione [!INCLUDE[tsql](../../../includes/tsql-md.md)] della replica: specificare un valore per il parametro `@hostname` di [sp_addmergesubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) (per le sottoscrizioni push) o [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) (per le sottoscrizioni pull).  
  
-   Agente di merge: specificare un valore per il parametro **-Hostname** nella riga di comando o tramite un profilo agente. Per ulteriori informazioni sull'agente di merge, vedere [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md). Per ulteriori informazioni sui profili agenti, vedere [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="initializing-a-subscription-to-a-publication-with-parameterized-filters"></a>Inizializzazione di una sottoscrizione di una pubblicazione con filtri con parametri  
 Quando si utilizzano filtri di riga con parametri nelle pubblicazioni di tipo merge, ogni sottoscrizione con uno snapshot in due parti viene inizializzata dalla replica. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## <a name="using-the-appropriate-filtering-options"></a>Utilizzo delle opzioni di filtro appropriate  
 Quando si utilizzano filtri con parametri, è possibile avere il controllo su due aree principali:  
  
-   La modalità di elaborazione dei filtri da parte della replica di tipo merge, operazione che viene controllata da una delle due impostazioni di pubblicazione: **use partition groups** e **keep partition changes**.  
  
-   La modalità di condivisione dei dati tra i Sottoscrittori, che deve essere riflessa dall'impostazione dell'articolo **partition options**.  
  
 Per impostare le opzioni di filtro, vedere [Optimize Parameterized Row Filters](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md).  
  
### <a name="setting-use-partition-groups-and-keep-partition-changes"></a>Impostazione di "use partition groups" e "keep partition changes"  
 Entrambe le opzioni **use partition groups** e **keep partition changes** consentono di migliorare le prestazioni di sincronizzazione delle pubblicazioni con gli articoli filtrati tramite l'archiviazione di metadati aggiuntivi nel database di pubblicazione. L'opzione **use partition groups** offre prestazioni superiori tramite l'utilizzo della funzionalità delle partizioni pre-calcolate. Questa opzione viene impostata su **true** per impostazione predefinita, se gli articoli nella pubblicazione sono conformi a un set di requisiti. Per altre informazioni su questi requisiti, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md). Se gli articoli non soddisfano i requisiti per l'utilizzo delle partizioni pre-calcolate, l'opzione **keep partition changes** verrà impostata su **true**.  
  
### <a name="setting-partition-options"></a>Impostazione di "partition options"  
 Durante la creazione di un articolo, si specifica un valore per la proprietà **partition options** in base al modo in cui i dati nella tabella filtrata verranno condivisi dai Sottoscrittori. È possibile impostare la proprietà su uno di quattro valori utilizzando [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)e la finestra di dialogo **Proprietà articolo** . La proprietà può essere impostata su uno dei due valori utilizzando la finestra di dialogo **Aggiungi filtro** o **Modifica filtro** , disponibile nella Creazione guidata nuova pubblicazione, e nella finestra di dialogo **Proprietà pubblicazione** . Nella tabella seguente vengono descritti i valori disponibili.  
  
|Descrizione|Valore in Aggiungi filtro e Modifica filtro|Valore in Proprietà articolo|Valore nelle stored procedure|  
|-----------------|-----------------------------------------|---------------------------------|--------------------------------|  
|I dati nelle partizioni sono sovrapposti e il Sottoscrittore può aggiornare le colonne a cui si fa riferimento in un filtro con parametri.|**Una riga di questa tabella verrà inviata a più sottoscrizioni**|**Sovrapposte**|**0**|  
|I dati nelle partizioni sono sovrapposti e il Sottoscrittore non può aggiornare le colonne a cui si fa riferimento in un filtro con parametri.|N/D*|**Sovrapposte, non ammesse modifiche dei dati fuori partizione**|**1**|  
|I dati nelle partizioni non sono sovrapposti e vengono condivisi dalle sottoscrizioni. Il Sottoscrittore non può aggiornare le colonne a cui si fa riferimento in un filtro con parametri.|N/D*|**Non sovrapposte, condivise dalle sottoscrizioni**|**2**|  
|I dati nelle partizioni non sono sovrapposti ed esiste un'unica sottoscrizione per partizione. Il Sottoscrittore non può aggiornare le colonne a cui si fa riferimento in un filtro con parametri.**|**Una riga di questa tabella verrà inviata a una sola sottoscrizione**|**Non sovrapposte, sottoscrizione unica**|**3**|  
  
 \*Se l'opzione di filtro sottostante è impostata su **0**, **1** o **2**, nelle finestre di dialogo **Aggiungi filtro** e **Modifica filtro** verrà visualizzata l'opzione **Una riga di questa tabella verrà inviata a più sottoscrizioni**.  
  
 **Se si specifica questa opzione, per ogni partizione dei dati dell'articolo può esistere una sola sottoscrizione. Se si crea una seconda sottoscrizione nella quale il criterio di filtro porta alla restituzione della stessa partizione della sottoscrizione esistente, quest'ultima viene eliminata.  
  
> [!IMPORTANT]  
>  È necessario che il valore di **partition options** venga impostato in base alla modalità con cui i dati vengono condivisi dai Sottoscrittori. Se, ad esempio, si specifica che una partizione non sia sovrapposta, con una sola sottoscrizione per partizione, ma successivamente i dati vengono aggiornati in un altro Sottoscrittore, è possibile che si verifichi un errore nell'agente di merge durante la sincronizzazione e che quindi i dati non siano convergenti.  
  
#### <a name="selecting-the-appropriate-partition-option"></a>Selezione dell'opzione di partizione appropriata  
 Le partizioni non sovrapposte vengono utilizzate insieme alle partizioni pre-calcolate per migliorare le prestazioni in situazioni in cui alcuni limiti funzionali sono accettabili. Le partizioni pre-calcolate consentono di velocizzare i download nei Sottoscrittori, ma rallentano le operazioni di caricamento. Le partizioni non sovrapposte riducono al minimo il costo di caricamento associato alle partizioni pre-calcolate. Il vantaggio a livello di prestazioni delle partizioni non sovrapposte è più evidente quando i filtri con parametri e i filtri join utilizzati sono più complessi.  
  
 Quando si scelgono le opzioni di partizione da utilizzare in una pubblicazione, considerare gli scenari seguenti.  
  
-   [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] dispone di una forza vendite mobile in cui ogni venditore è responsabile dei clienti appartenenti a un determinato codice postale. L'applicazione richiede l'aggiornamento del codice postale nel caso un cliente passi da un territorio di vendita a un altro, affinché il cliente venga assegnato a un altro venditore. Il filtro con parametri è basato sul codice postale del cliente e l'aggiornamento determina la rimozione del codice postale dalla partizione di un venditore e il relativo inserimento nella partizione di un altro venditore. A tale scopo, sono necessarie partizioni sovrapposte che consentano di aggiornare le colonne a cui si fa riferimento in un filtro con parametri. Questa opzione ottimizza la flessibilità, ma il funzionamento potrebbe non essere ottimale come quello delle partizioni non sovrapposte.  
  
-   Un'agenzia di collocamento dispone di dati che vengono inviati alle filiali di ogni regione dello stato. I dati non si sovrappongono e ogni riga della tabella nella sede centrale dell'agenzia è inclusa in un'unica partizione, ma tale partizione viene inviata a più uffici della stessa regione. L'opzione che prevede partizioni non sovrapposte con partizioni condivise dalle sottoscrizioni è appropriata, poiché garantisce prestazioni migliori rispetto alle partizioni sovrapposte soddisfacendo al tempo stesso i requisiti dell'applicazione.  
  
-   Se si dispone di partizioni non sovrapposte e una sola sottoscrizione riceve e aggiorna i dati in una partizione, sarà possibile ottenere ulteriori vantaggi a livello di prestazioni. Questo scenario è tipico dei sistemi POS e delle applicazioni relative al personale esterno in cui i dati vengono raccolti principalmente nel Sottoscrittore e caricati nel server di pubblicazione. Si consideri una tabella **Package** in un'applicazione di recapito: quando ogni pacco viene caricato su un furgone, lo stato del pacco viene modificato nella tabella **Package** e la modifica viene replicata nella sede centrale. Gli autisti non aggiornerebbero lo stato dello stesso pacco su due furgoni diversi, quindi per la tabella **Package** è ideale ricorrere a una partizione non sovrapposta con una sola sottoscrizione per partizione.  
  
#### <a name="considerations-for-nonoverlapping-partitions"></a>Considerazioni sulle partizioni non sovrapposte  
 Quando si utilizzano le partizioni non sovrapposte, tenere presenti le considerazioni seguenti:  
  
##### <a name="general-considerations"></a>Considerazioni generali  
  
-   È necessario che nella pubblicazione vengano utilizzate partizioni pre-calcolate.  
  
-   È necessario che una riga appartenga a una sola partizione.  
  
-   Gli articoli non possono fare parte di un record logico.  
  
-   I partner di sincronizzazione alternativi non sono supportati. Questa funzionalità è deprecata.  
  
-   Il Sottoscrittore non può aggiornare le colonne a cui si fa riferimento in un filtro con parametri.  
  
-   Se un'operazione di inserimento nel Sottoscrittore non appartiene alla partizione, non viene eliminata. Tuttavia, non verrà replicata in altri Sottoscrittori.  
  
-   In alcuni casi con le partizioni sovrapposte, gli intervalli di valori Identity vengono modificati quando vengono inseriti dati tramite l'agente di merge. Con le partizioni non sovrapposte, gli intervalli possono essere modificati solo durante le operazioni di inserimento di un utente che dispone dell'autorizzazione necessaria per modificare gli intervalli di valori Identity nel database di sottoscrizione. L'utente deve essere il proprietario della tabella oppure un membro del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** o **db_ddladmin** .  
  
##### <a name="additional-considerations-for-nonoverlapping-partitions-with-a-single-subscription-per-partition"></a>Considerazioni aggiuntive sulle partizioni non sovrapposte con una sola sottoscrizione per partizione  
  
-   Gli articoli possono esistere in una sola pubblicazione e non possono essere ripubblicati.  
  
-   La pubblicazione deve consentire ai Sottoscrittori di avviare l'elaborazione degli snapshot. Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
##### <a name="additional-considerations-for-join-filters"></a>Considerazione aggiuntive sui filtri join  
  
-   In una gerarchia di filtri join un articolo con una partizione sovrapposta non può trovarsi sopra un articolo con una partizione non sovrapposta. In altre parole, un articolo padre deve utilizzare partizioni non sovrapposte se queste sono utilizzate dall'articolo figlio. Per informazioni sui filtri join, vedere [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   È necessario che in un filtro join in cui la partizione non sovrapposta è un elemento figlio, la proprietà **join unique key** sia impostata su 1. Per altre informazioni, vedere [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   È necessario che l'articolo abbia un solo filtro con parametri o un solo filtro join. L'articolo può avere un filtro con parametri ed essere l'elemento padre in un filtro join. Non può invece avere un filtro con parametri ed essere l'elemento figlio in un filtro join. Non può inoltre avere più di un filtro join.  
  
-   Se due tabelle nel server di pubblicazione hanno una relazione tra filtri join e la tabella figlio contiene righe che non hanno una riga corrispondente nella tabella padre, un'operazione di inserimento della riga padre mancante non avrà come conseguenza il download delle righe correlate nel Sottoscrittore. Le righe verrebbero invece scaricate con partizioni sovrapposte. Se ad esempio la tabella **SalesOrderDetail** contiene righe che non dispongono di alcuna riga corrispondente nella tabella **SalesOrderHeader** e si inserisce la riga mancante in **SalesOrderHeader**, tale riga viene scaricata nel Sottoscrittore, mentre non vengono scaricate le righe corrispondenti presenti in **SalesOrderDetail** .  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure consigliate per i filtri di riga basati sul tempo](../../../relational-databases/replication/merge/best-practices-for-time-based-row-filters.md)   
 [Filtrare i dati pubblicati](../../../relational-databases/replication/publish/filter-published-data.md)   
 [Filtrare i dati pubblicati per la replica di tipo merge](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)  
  
  
