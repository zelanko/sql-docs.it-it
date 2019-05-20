---
title: Finestra di dialogo Proprietà pubblicazione di replica di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
- sql13.rep.newpubwizard.pubproperties.filterrows.f1
- sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1
- sql13.rep.newpubwizard.pubproperties.general.f1
- sql13.rep.newpubwizard.pubproperties.publicationaccesslist.f1
- sql13.rep.newpubwizard.pubproperties.snapshotformat.f1
helpviewer_keywords:
- Publication Properties dialog box
ms.assetid: 66e845e9-1308-4288-9110-ad2f22f1fc58
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: da86b20dba26536626010d14c1f81a1bbd852156
ms.sourcegitcommit: 553ecea0427e4d2118ea1ee810f4a73275b40741
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65620376"
---
# <a name="sql-server-replication-publication-properties--dialog-box"></a>Finestra di dialogo Proprietà pubblicazione di replica di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa pagina descrive le pagine disponibili nella finestra di dialogo Proprietà pubblicazione. 

## <a name="general"></a>Generale
 La pagina **Generale** della finestra di dialogo **Proprietà pubblicazione** contiene informazioni di base sulla pubblicazione, tra cui il nome, la descrizione e i criteri di scadenza della sottoscrizione.  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Nome del database della pubblicazione (informazione di sola lettura).  
  
 **Database**  
 Nome del database di pubblicazione (informazione di sola lettura).  
  
 **Descrizione**  
 Descrizione della pubblicazione.  
  
 **Tipo**  
 Tipo di pubblicazione (informazione di sola lettura).  
  
 **Scadenza sottoscrizione**  
 Selezionare una delle opzioni per la scadenza della sottoscrizione: **Le sottoscrizioni non hanno scadenza** oppure **Le sottoscrizioni scadono**, con un periodo di tempo esplicito (**Intervallo**).  
  
 Per le pubblicazioni snapshot e transazionali, [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di accettare l'impostazione predefinita **Le sottoscrizioni non hanno scadenza**.  
  
 Per la replica di tipo merge, [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di accettare l'impostazione predefinita **Le sottoscrizioni scadono** e di impostare il valore più basso possibile per **Intervallo**. Più è alto il valore del periodo di tempo di scadenza, maggiore è la quantità di metadati archiviati, con conseguenti possibili effetti negativi sulle prestazioni. Raggiungere un equilibrio tra la necessità di disconnettere i Sottoscrittori o semplicemente di non consentire ai Sottoscrittori di eseguire la sincronizzazione per un periodo di tempo esteso e i potenziali problemi di prestazioni derivanti dall'archiviazione e dall'elaborazione di grandi quantità di metadati.  
  
 Per altre informazioni, vedere [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Livello di compatibilità**  
 Solo per[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive. Solo per le pubblicazioni di tipo merge. Consente di selezionare la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] minima richiesta per i Sottoscrittori che eseguono la sincronizzazione con la pubblicazione. Il livello di compatibilità viene determinato da una serie di regole associate.  

## <a name="filter-rows"></a>Filtra righe
  La pagina **Filtra righe** della finestra di dialogo **Proprietà pubblicazione** consente di aggiungere, modificare o eliminare filtri progettati per eseguire le operazioni seguenti:  
  
-   Applicare filtri di riga statici agli articoli di tabella nelle pubblicazioni snapshot, transazionali e di tipo merge.   
-   Applicare filtri di riga con parametri agli articoli di tabella nelle pubblicazioni di tipo merge.    
-   Utilizzare filtri join per estendere i filtri degli articoli di tabelle di merge agli articoli di tabelle correlate. Per altre informazioni sulle opzioni di filtro, vedere [Filtrare i dati pubblicati](../../relational-databases/replication/publish/filter-published-data.md).  
  
> [!NOTE]  
>  Per aggiungere, modificare o eliminare un filtro sono necessari un nuovo snapshot per la pubblicazione e la reinizializzazione di tutte le sottoscrizioni.  
  
Per ottimizzare le prestazioni dell'applicazione e ridurre la quantità di spazio di archiviazione necessario o per limitare la disponibilità di determinati dati a Sottoscrittori specifici, è consigliabile pubblicare solo i dati necessari. La pubblicazione può includere sia tabelle filtrate che tabelle non filtrate. È possibile ad esempio includere la tabella completa, non filtrata, dei prodotti della società e utilizzare i filtri di riga per generare una tabella filtrata dei clienti di una regione specifica. Tramite l'applicazione di filtri ai dati pubblicati è possibile:  
  
-   Ridurre al minimo la quantità di dati inviati in rete.    
-   Ridurre la quantità di spazio di archiviazione necessaria nel Sottoscrittore.    
-   Personalizzare le pubblicazioni e le applicazioni in base ai requisiti dei singoli Sottoscrittori.    
-   Evitare o limitare i conflitti in caso di aggiornamento dei dati da parte dei Sottoscrittori grazie alla possibilità di inviare partizioni di dati diverse a Sottoscrittori diversi. In due Sottoscrittori pertanto non verranno mai aggiornati gli stessi valori di dati.    
-   Evitare la trasmissione di dati riservati. È possibile utilizzare i filtri di riga e di colonna per limitare l'accesso ai dati da parte dei Sottoscrittori. Nella replica di tipo merge è necessario tenere in considerazione alcuni aspetti relativi alla sicurezza se si utilizza un filtro con parametri che include HOST_NAME(). Per ulteriori informazioni, vedere la sezione relativa all'utilizzo dei filtri con HOST_NAME() in [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
### <a name="options"></a>Opzioni  
 **Tabelle filtrate**  
 Questo riquadro viene popolato di filtri mano a mano che vengono aggiunti agli articoli di tabella nella pubblicazione. Le tabelle con filtri di riga vengono visualizzate nel riquadro come nodi di livello principale. Per le pubblicazioni di tipo merge, le tabelle alle quali sono stati estesi i filtri tramite un filtro di join vengono visualizzate come nodi figlio.  
  
 **Aggiungi**  
 Fare clic su **Aggiungi** per visualizzare una finestra di dialogo che consente di filtrare gli articoli di tabella. Facendo clic su **Aggiungi** per una pubblicazione snapshot o transazionale verrà visualizzata immediatamente una finestra di dialogo. Facendo clic su **Aggiungi** per una pubblicazione di tipo merge verranno visualizzate tre opzioni: **Aggiungi filtro**; **Aggiungi join per estendere il filtro selezionato**; **Genera filtri automaticamente**.  
  
-   Selezionare l'opzione **Aggiungi filtro** per visualizzare la finestra di dialogo **Aggiungi filtro** , che consente di applicare i filtri di riga a un articolo di tabella. Nella finestra di dialogo **Aggiungi filtro** è possibile, ad esempio, specificare che una tabella contenente dati sui clienti possa contenere solo dati sui clienti francesi quando viene replicata nei Sottoscrittori.  
  
-   Selezionare **Aggiungi join per estendere il filtro selezionato** per visualizzare la finestra di dialogo **Aggiungi join** , La finestra di dialogo **Aggiungi join** consente di estendere un filtro di riga in modo che filtri i dati delle tabelle correlate alla tabella con il filtro di riga. Se, ad esempio, una tabella clienti viene filtrata in modo che contenga solo dati relativi ai clienti francesi ed esiste una tabella correlata per gli ordini dei clienti, è possibile definire un join tra le due tabelle in modo che la tabella degli ordini includa solo gli ordini dei clienti francesi.  
  
    > [!NOTE]  
    >  Questa opzione è disponibile solo selezionando prima la tabella di base del join nel riquadro dei filtri.  
  
-   Selezionare **Genera filtri automaticamente** per visualizzare la finestra di dialogo **Genera filtri** , che consente di definire un filtro di riga su una tabella in una pubblicazione di tipo merge che viene automaticamente esteso dalla replica ad altre tabelle correlate tramite relazioni di chiave esterna. Ad esempio, una pubblicazione può includere tre tabelle: una tabella dei clienti, una tabella degli ordini con una chiave esterna alla tabella dei clienti e una tabella dei dettagli degli ordini con una chiave esterna alla tabella degli ordini. Definendo un filtro di riga sulla tabella dei clienti, la replica lo estenderà alle altre tabelle.  
  
    > [!NOTE]  
    >  Se i filtri vengono generati automaticamente dalla replica, qualsiasi filtro esistente per la pubblicazione viene eliminato. Per includere sia i filtri generati automaticamente che i filtri specificati manualmente, generare i filtri prima di specificarne altri. È possibile specificare un solo set di filtri generati automaticamente per ogni pubblicazione.  
  
 **Modifica**  
 Selezionare un filtro di riga o un filtro join nel riquadro dei filtri e fare clic su **Modifica** per visualizzare la finestra di dialogo **Modifica filtro** o **Modifica join** .  
  
 **Elimina**  
 Selezionare un filtro di riga o un filtro join nel riquadro dei filtri e fare clic su **Elimina** per eliminare il filtro.  
  
 **Trova tabella**  
 Solo per le pubblicazioni di tipo merge. Fare clic su **Trova tabella** per trovare una tabella in un'albero di filtro complesso. In un database con relazioni complesse una tabella può essere unita in join a più tabelle e pertanto può apparire in più posizioni all'interno dell'albero di filtro.  
  
 La tabella effettiva appare solo in una posizione all'interno dell'albero, mentre nelle altre posizioni è rappresentata da un collegamento. Un collegamento a una tabella è semplicemente un riferimento alla tabella e non ne visualizza i nodi figlio. Un nodo collegamento è contrassegnato dalla freccia di collegamento ed espandendo tale nodo viene visualizzato il testo **Fare clic su Trova tabella per vedere la tabella per \<NomeTabella>**.  
  
 Selezionare un nodo collegamento nel riquadro e fare clic su **Trova tabella** . Il riquadro verrà espanso e la tabella verrà evidenziata. Se si fa clic su **Trova tabella** senza aver selezionato un nodo collegamento verrà visualizzata la finestra di dialogo **Trova tabella** .  
  
 **Filter**  
 Contiene la definizione [!INCLUDE[tsql](../../includes/tsql-md.md)] del filtro selezionato nel riquadro dei filtri.  

## <a name="publication-access-list"></a>Elenco di accesso alla pubblicazione
  La pagina **Elenco accesso pubblicazione** della finestra di dialogo **Proprietà pubblicazione** consente di aggiungere e rimuovere account di accesso, account e gruppi dall'elenco di accesso alla pubblicazione. L'elenco di accesso alla pubblicazione costituisce il principale sistema di sicurezza del server di pubblicazione. Quando si crea una pubblicazione, la replica crea un elenco di accesso alla pubblicazione per la pubblicazione creata. L'elenco di accesso alla pubblicazione opera in modo analogo all'elenco di controllo di accesso di [!INCLUDE[msCoName](../../includes/msconame-md.md)] e include un elenco di account di accesso, account e gruppi ai quali viene consentito l'accesso alla pubblicazione.  
  
 Quando un Sottoscrittore si connette al server di pubblicazione o al server di distribuzione e richiede l'accesso alla pubblicazione, l'account di accesso del Sottoscrittore viene confrontato con le informazioni di autenticazione contenute nell'elenco di accesso alla pubblicazione. Ciò garantisce un maggior livello di sicurezza del server di pubblicazione, impedendo che gli account di accesso del server di pubblicazione e del server di distribuzione vengano utilizzati da uno strumento client per apportare modifiche direttamente nel server di pubblicazione. Per altre informazioni, vedere [Proteggere il server di pubblicazione](../../relational-databases/replication/security/secure-the-publisher.md).  
  
### <a name="options"></a>Opzioni  
 **Aggiungi**  
 Consente di aggiungere una nuova voce all'elenco. È possibile aggiungere solo gli account di accesso, gli account o i nomi dei gruppi già definiti sia nel server di pubblicazione sia nel server di distribuzione. Tali account di accesso, account e nomi di gruppi vengono definiti in entrambi i server nei casi in cui si utilizzino account di dominio o siano stati creati account locali in entrambi i server.  
  
 **Rimuovi**  
 Consente di rimuovere la voce selezionata dall'elenco.  
  
 **Rimuovi tutto**  
 Consente di rimuovere tutte le voci dall'elenco.  

## <a name="ftp-snapshot-and-internet"></a>Snapshot FTP e Internet

-   Impostare le proprietà per il recapito dello snapshot tramite FTP (File Transfer Protocol). Per altre informazioni, vedere [Recapitare uno snapshot tramite FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md). Per eseguire il recapito di snapshot tramite FTP è necessario configurare un server FTP. Per ulteriori informazioni, vedere la documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
    > [!NOTE]  
    >  Le modifiche apportate a qualsiasi impostazione relativa al protocollo FTP richiedono la generazione di un nuovo snapshot.  
  
-   Impostare le proprietà per la sincronizzazione Web per la replica di tipo merge in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive, in modo da consentire la sincronizzazione delle sottoscrizioni tramite il protocollo HTTPS. Per utilizzare la sincronizzazione Web è necessario configurare un server [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS). Per altre informazioni, vedere [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
### <a name="options"></a>Opzioni  
 **Accedi ai file di snapshot tramite FTP**  
 Selezionare **I Sottoscrittori possono scaricare i file di snapshot utilizzando FTP (File Transfer Protocol)** e specificare **Nome server FTP**, **Numero di porta**, **Percorso dalla cartella radice FTP**, **Account di accesso**e **Password**per consentire ai Sottoscrittori l'utilizzo del protocollo FTP per il recapito di snapshot.  
  
 La selezione di questa opzione consente ai Sottoscrittori di utilizzare il protocollo FTP per recuperare i file di snapshot, senza tuttavia imporne l'obbligo di utilizzo. Se si seleziona questa opzione, l'impostazione predefinita per la Creazione guidata nuova sottoscrizione viene impostata per consentire al Sottoscrittore di recuperare file di snapshot tramite FTP. Per modificare l'impostazione utilizzare la finestra di dialogo **Proprietà sottoscrizione** . Se si consente ai Sottoscrittori l'accesso ai file di snapshot tramite FTP, specificare la cartella FTP come posizione per i file di snapshot nella pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione** . In tal modo l'agente snapshot aggiornerà automaticamente i file nella cartella FTP quando viene generato un nuovo snapshot. Se la posizione non è impostata sulla cartella FTP, sarà necessario aggiornare i file manualmente ogni volta che vengono generati nuovi snapshot. Per altre informazioni, vedere [Recapitare uno snapshot tramite FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
 **Sincronizzazione Web**  
 Solo per la replica di tipo merge. Selezionare **I Sottoscrittori possono eseguire la sincronizzazione tramite connessione a un server Web**e specificare l'indirizzo di un server Web per consentire ai Sottoscrittori della replica di tipo merge di utilizzare la sincronizzazione Web. È necessario che il server Web usi SSL (Secure Sockets Layer) e che l'indirizzo Web sia completo, ad esempio `https://server.domain.com/synchronize`. Per altre informazioni, vedere [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).  


## <a name="agent-security"></a>Sicurezza agente
  La pagina **Sicurezza agente** della finestra di dialogo **Proprietà pubblicazione** consente di accedere alle impostazioni relative agli account nell'ambito dei quali gli agenti seguenti vengono eseguiti e si connettono ai computer inclusi in una topologia di replica.  
  
-   Agente snapshot per tutte le pubblicazioni.  
  
-   Agente di lettura log per tutte le pubblicazioni transazionali. Per ogni database pubblicato per la replica transazionale, esiste un solo agente di lettura log. Le modifiche apportate alle impostazioni dell'agente di lettura log sono valide per tutte le pubblicazioni transazionali in un database.  
  
-   Agente di lettura coda per pubblicazioni transazionali che consentono sottoscrizioni ad aggiornamento in coda. A ogni database di distribuzione è associato un agente di lettura coda. Le modifiche apportate all'agente di lettura coda sono valide per tutte le pubblicazioni transazionali con sottoscrizioni ad aggiornamento in coda che utilizzano il medesimo database di distribuzione. Per altre informazioni sulle impostazioni di sicurezza di Agente di lettura coda, vedere [Visualizzare e modificare le impostazioni di sicurezza della replica](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md).  
  
 Per ulteriori informazioni sulle autorizzazioni e le impostazioni di sicurezza necessarie per ogni agente, vedere [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
### <a name="options"></a>Opzioni  
 **Impostazioni di sicurezza** o **Crea agente**  
 Se è stato creato un processo agente, fare clic su **Impostazioni di sicurezza** per accedere a una finestra di dialogo che consente di modificare le impostazioni di sicurezza relative a un agente. Se non è stato creato alcun processo agente, fare clic su **Crea agente** per crearne uno e specificare le relative impostazioni di sicurezza.  

## <a name="data-partitions"></a>Partizioni dati
Partizioni dati  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]  
  La pagina **Partizioni dati** della finestra di dialogo **Proprietà pubblicazione** consente di definire le partizioni di dati per pubblicazioni di tipo merge che utilizzano filtri con parametri. Dopo aver definito le partizioni è possibile generare gli snapshot per queste partizioni, specificando set di dati iniziali diversi per Sottoscrittori diversi in base alle proprietà della connessione, ovvero nome dell'account di accesso e/o nome del computer, dei Sottoscrittori. È inoltre possibile consentire ai Sottoscrittori di richiedere il recapito e la generazione di snapshot nel caso in cui questi non dispongano di uno snapshot per la propria partizione al momento della prima sincronizzazione. Per altre informazioni, vedere [Creazione di uno snapshot per una pubblicazione di tipo merge con filtri con parametri](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
### <a name="options"></a>Opzioni  
 **Aggiungi**  
 Fare clic su **Aggiungi** per definire una partizione. Nella finestra di dialogo **Aggiungi partizione dati** specificare i valori per **HOST_NAME()** e/o **SUSER_SNAME()** e definire una pianificazione per l'aggiornamento degli snapshot.  
  
 **Modifica**  
 Selezionare una partizione esistente nella griglia e fare clic su **Modifica** per modificarla.  
  
 **Elimina**  
 Selezionare una partizione esistente nella griglia e fare clic su **Elimina** per eliminarla.  
  
 **Genera gli snapshot selezionati adesso**  
 Selezionare una o più partizioni nella griglia e fare clic su **Genera gli snapshot selezionati adesso** per generare gli snapshot per tali partizioni.  
  
 **Elimina gli snapshot esistenti**  
 Selezionare una o più partizioni nella griglia e fare clic su **Elimina gli snapshot esistenti** per eliminare gli snapshot per tali partizioni.  
  
 **Definisci automaticamente una partizione e genera uno snapshot, se necessario, quando un nuovo Sottoscrittore cerca di eseguire la sincronizzazione**  
 Selezionare questa opzione se si desidera consentire ai Sottoscrittori di richiedere la generazione e l'applicazione di snapshot. I Sottoscrittori potrebbero richiedere questa opzione nel caso in cui non dispongano di uno snapshot per la propria partizione al momento della prima sincronizzazione.  

## <a name="snapshot"></a>Snapshot
Snapshot  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]  
  La pagina **Snapshot** della finestra di dialogo **Proprietà pubblicazione** consente di impostare il formato dello snapshot, il percorso dello snapshot e gli script da eseguire prima e dopo l'applicazione dello snapshot. La cartella dello snapshot deve essere designata come condivisione e disporre delle autorizzazioni sufficienti per la lettura e la scrittura dei file nella cartella da parte degli agenti. Per altre informazioni sulle impostazioni di sicurezza appropriate per la cartella, vedere [Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
> [!NOTE]  
>  In caso di modifiche, sarà necessario un nuovo snapshot per la pubblicazione. Per altre informazioni, vedere [Modificare le proprietà di pubblicazioni e articoli](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
### <a name="options"></a>Opzioni  
 **Formato snapshot**  
 Consente di selezionare la modalità nativa o la modalità carattere per il formato dello snapshot.  
  
-   Selezionare **Formato nativo di SQL Server: tutti i Sottoscrittori devono essere server che eseguono SQL Server** se tutti i Sottoscrittori sono istanze di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diverse da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Il formato nativo dello snapshot offre le migliori prestazioni.    
-   Selezionare **Carattere: obbligatorio se in un server di pubblicazione o in un Sottoscrittore non è in esecuzione SQL Server** se uno o più Sottoscrittori eseguono [!INCLUDE[ssEW](../../includes/ssew-md.md)] oppure non sono Sottoscrittori[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .    
 **Percorso dei file di snapshot**  
 Consente di selezionare il percorso per l'archiviazione dei file di snapshot. Questi file possono essere archiviati nel percorso predefinito. È inoltre possibile archiviarli in un percorso alternativo in sostituzione o in aggiunta al percorso predefinito. I file archiviati in un percorso alternativo possono essere archiviati.  
  
-   Selezionare **Inserisci i file nella cartella predefinita** per utilizzare la cartella dello snapshot predefinita per il server di pubblicazione. Il percorso dello snapshot in questa finestra di dialogo è di sola lettura, poiché può essere modificato per il server di pubblicazione solo nella finestra di dialogo **Proprietà server di distribuzione** . Per altre informazioni, vedere [Modificare le opzioni snapshot](../../relational-databases/replication/snapshot-options.md).    
-   Selezionare **Inserisci i file nella cartella seguente** per specificare un percorso alternativo in sostituzione o in aggiunta al percorso predefinito. Immettere un percorso nella casella di testo oppure fare clic su **Sfoglia** per selezionare un percorso. Selezionare **Comprimi i file di snapshot in questa cartella** per comprimere i file nel percorso dello snapshot alternativo. Il percorso alternativo può trovarsi in un altro server, in un'unità di rete oppure in un supporto rimovibile, ad esempio un CD-ROM o un disco rimovibile. Per altre informazioni, vedere [Modificare le opzioni snapshot](../../relational-databases/replication/snapshot-options.md).  
  
 **Script aggiuntivi**  
 Consente di specificare gli script da eseguire prima e dopo l'applicazione dello snapshot nel Sottoscrittore. Non è possibile specificare gli script se l'opzione **Formato snapshot** è impostata su **Carattere**.  
  
 L'utilizzo degli script è facoltativo, tuttavia esso rappresenta un metodo pratico per eseguire comandi e applicare modifiche amministrative nei Sottoscrittori. Per altre informazioni sull'esecuzione di script, vedere [Eseguire gli script prima e dopo l'applicazione dello snapshot](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).  
  
-   Immettere un percorso nella casella di testo **Prima di applicare lo snapshot, esegui lo script seguente** oppure fare clic su **Sfoglia** per selezionare il percorso dello script.    
-   Immettere un percorso nella casella di testo **Dopo l'applicazione dello snapshot, esegui lo script seguente** oppure fare clic su **Sfoglia** per selezionare il percorso dello script. 
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   

  
  
