---
title: Configurare la sincronizzazione Web | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- SQL10.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
helpviewer_keywords:
- Web synchronization, security best practices
- Web synchronization, configuring
ms.assetid: 21f8e4d4-cd07-4856-98f0-9c9890ebbc82
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b987fef5bfb36fc84f55f5058f956a691f446a2c
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710314"
---
# <a name="configure-web-synchronization"></a>Configurazione della sincronizzazione Web
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  L'opzione di sincronizzazione Web per la replica di tipo merge di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente la replica dei dati tramite il protocollo HTTPS su Internet. Per utilizzare la sincronizzazione Web, è innanzitutto necessario eseguire le azioni di configurazione riportate di seguito:  
  
1.  Creare nuovi account di dominio ed eseguire il mapping degli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Configurare il computer che esegue [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) per la sincronizzazione delle sottoscrizioni.  
  
3.  Configurare una pubblicazione di tipo merge per consentire la sincronizzazione Web.  
  
4.  Configurare una o più sottoscrizioni per l'utilizzo della sincronizzazione Web.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

> [!NOTE]  
>  Se si intende replicare volumi elevati di dati o utilizzare tipi di dati di grandi dimensioni, ad esempio **varchar(max)** , leggere la sezione "Replica di volumi elevati di dati" in questo argomento.  
  
 Per configurare correttamente la sincronizzazione Web, è necessario decidere come verrà configurata la sicurezza per soddisfare requisiti e criteri specifici. È preferibile prendere queste decisioni e creare gli account necessari prima di configurare IIS, la pubblicazione e le sottoscrizioni.  
  
 Nelle procedure riportate di seguito viene descritta una configurazione della sicurezza semplificata in cui vengono utilizzati account locali, per motivi di brevità. Questa configurazione semplificata è adatta per installazioni in cui sia IIS sia il server di pubblicazione e il server di distribuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono eseguiti nello stesso computer, anche se è più probabile (e consigliabile) utilizzare una topologia a più server per un'installazione di produzione. È possibile sostituire gli account locali indicati nelle procedure con account di dominio.  
  
## <a name="creating-new-accounts-and-mapping-sql-server-logins"></a>Creazione di nuovi account e mapping di account di accesso di SQL Server  
 Il listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (replisapi.dll) si connette al server di pubblicazione rappresentando l'account specificato per il pool di applicazioni associato al sito Web di replica.  
  
 L'account utilizzato per il listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve disporre di autorizzazioni come descritto in [Merge Agent Security](../../relational-databases/replication/merge-agent-security.md), nella sezione relativa alla connessione al server di pubblicazione o al server di distribuzione". In breve è necessario che l'account:  
  
-   sia membro dell'elenco di accesso alla pubblicazione;  
  
-   sia sottoposto a mapping a un account di accesso associato a un utente nel database di pubblicazione;  
  
-   sia sottoposto a mapping a un account di accesso associato a un utente nel database di distribuzione;  
  
-   disponga delle autorizzazioni di lettura per la condivisione snapshot.  
  
 Se si utilizza la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la prima volta è inoltre necessario creare account e account di accesso per gli agenti di replica. Per ulteriori informazioni, vedere le sezioni "Configurazione della pubblicazione" e "Configurazione della sottoscrizione" in questo argomento.  
  
 Prima di configurare la sincronizzazione Web, vedere la sezione "Procedure consigliate per la sicurezza nella sincronizzazione Web" in questo argomento. Per ulteriori informazioni sulla sicurezza della sincronizzazione Web, vedere [Security Architecture for Web Synchronization](../../relational-databases/replication/security/security-architecture-for-web-synchronization.md).  
  
## <a name="configuring-the-computer-that-is-running-iis"></a>Configurazione del computer che esegue IIS  
 La sincronizzazione Web richiede l'installazione e la configurazione di IIS. Prima di poter configurare una pubblicazione per l'utilizzo della sincronizzazione Web, è necessario l'URL del sito Web di replica.  
  
 La sincronizzazione Web è supportata in IIS a partire dalla versione 5.0. La Configurazione guidata sincronizzazione Web non è supportata in IIS versione 7.0. A partire da SQL Server 2012, per usare il componente di sincronizzazione Web nel server IIS, è consigliabile installare SQL Server con la replica. Ad esempio, è possibile installare l'edizione gratuita SQL Server Express.  
  
 Per la sincronizzazione Web è richiesto SSL. È necessario un certificato di sicurezza rilasciato da un'autorità di certificazione. Solo ai fini del test, è possibile utilizzare un certificato di sicurezza autocertificato.  
   
  
 **Per configurare IIS per la sincronizzazione Web**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configurare IIS per la sincronizzazione Web](../../relational-databases/replication/configure-iis-for-web-synchronization.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configurare IIS 7 per la sincronizzazione Web](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md)  
  
## <a name="creating-a-web-garden"></a>Creazione di un Web garden  
 Il listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta due operazioni di sincronizzazione simultanee per thread. Il superamento di questo limite potrebbe causare interruzioni nella risposta del listener. Il numero di thread allocato a replisapi.dll è determinato dalla proprietà Numero massimo di processi di lavoro del pool di applicazioni. Il valore predefinito della proprietà è 1.  
  
 È possibile supportare un numero maggiore di operazioni di sincronizzazione simultanee per CPU aumentando il valore della proprietà Numero massimo di processi di lavoro. L'operazione di scalabilità orizzontale applicata attraverso l'aumento del numero di processi di lavoro per CPU è nota come creazione di un Web garden.  
  
 Il Web garden consente la sincronizzazione di più di due sottoscrittori contemporaneamente. Aumenterà inoltre l'utilizzo della CPU da parte di replisapi.dll, con un potenziale impatto negativo sulle prestazioni complessive del server. È importante valutare queste considerazioni quando si sceglie un valore per la proprietà Numero massimo di processi di lavoro.  
  
#### <a name="to-increase-maximum-worker-processes-in-iis-7"></a>Per aumentare il valore di Numero massimo di processi di lavoro in IIS 7  
  
1.  In **Gestione Internet Information Services (IIS)** espandere il nodo del server locale, quindi fare clic sul nodo **Pool di applicazioni** .  
  
2.  Selezionare il pool di applicazioni associato al sito di sincronizzazione Web, quindi fare clic su **Impostazioni avanzate** nel riquadro **Azioni** .  
  
3.  Nella finestra di dialogo Impostazioni avanzate, sotto l'intestazione **Elabora modello** , fare clic sulla riga **Numero massimo di processi di lavoro**. Modificare il valore della proprietà, quindi fare clic su **OK**.  
  
## <a name="configuring-the-publication"></a>Configurazione della pubblicazione  
 Per utilizzare la sincronizzazione Web, creare una pubblicazione con le stesse modalità utilizzate per una topologia di merge standard. Per altre informazioni, vedere [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 Dopo la creazione della pubblicazione, abilitare l'opzione che consente la sincronizzazione Web utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o gli oggetti RMO (Replication Management Objects). Per abilitare la sincronizzazione Web, è necessario fornire l'indirizzo del server Web per le connessioni del sottoscrittore.  
  
 Se si utilizza un server di pubblicazione per la prima volta, è necessario configurare un server di distribuzione e una condivisione snapshot. L'agente di merge in ogni sottoscrittore deve disporre delle autorizzazioni di lettura per la condivisione snapshot. Per altre informazioni, vedere [Configurare la distribuzione](../../relational-databases/replication/configure-distribution.md) e [Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
 **gen** è una parola riservata nei file XML websync. Non tentare di pubblicare tabelle contenenti colonne denominate **gen**.  
  
## <a name="configuring-the-subscription"></a>Configurazione della sottoscrizione  
 Dopo avere abilitato una pubblicazione e configurato IIS, creare una sottoscrizione pull e specificare che deve essere sincronizzata utilizzando IIS. La sincronizzazione Web è supportata solo per le sottoscrizioni pull.  
  
## <a name="upgrading-from-an-earlier-version-of-sql-server"></a>Aggiornamento da una versione precedente di SQL Server  
 Se una topologia di sincronizzazione Web è presente e configurata e si aggiorna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario assicurarsi che la versione più recente di Replisapi.dll venga copiata nella directory virtuale utilizzata dalla sincronizzazione Web. Per impostazione predefinita, la versione più recente di Replisapi.dll si trova in C:\Programmi\ Microsoft SQL Server\\<nnn\>\COM.  
  
## <a name="replicating-large-volumes-of-data"></a>Replica di volumi elevati di dati  
 Per evitare potenziali problemi di memoria nei computer sottoscrittori, nella sincronizzazione Web si utilizza una dimensione massima predefinita di 100 MB per il file XML utilizzato per trasferire le modifiche. Il limite può essere aumentato impostando la chiave del Registro di sistema seguente:  
  
 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\Replication**  
  
 **WebSyncMaxXmlSize DWORD 2000000**  
  
 L'intervallo di valori accettabili per questa chiave è compreso tra 100 MB e 4 GB. Il valore è espresso in KB. L'impostazione di questo parametro su un valore elevato non garantisce che sia possibile sincronizzare tale quantità di dati. Il limite effettivo è vincolato dalla quantità di memoria contigua disponibile nel computer del Sottoscrittore. Se è necessario impostare un valore maggiore di 100 MB, si consiglia di aumentare il valore in modo incrementale e testare l'utilizzo della memoria con un carico di lavoro tipico nel Sottoscrittore.  
  
 La dimensione massima per il file XML è 4 GB, ma la replica sincronizza le modifiche di quel file in batch. La dimensione massima dei batch di dati e metadati è di 25 MB. È necessario assicurarsi che i dati di ciascun batch non superino approssimativamente i 20 MB di dimensioni, per tenere conto dell'overhead dei metadati e di altro tipo. Questo limite presenta le implicazioni seguenti:  
  
-   Non è possibile replicare colonne che causano il superamento del limite di 25 MB per dati e metadati. Questo potrebbe essere un problema quando si replicano righe contenenti tipi di dati di grandi dimensioni, ad esempio **varchar(max)** .  
  
-   Se si replicano volumi elevati di dati, può essere necessario regolare la dimensione dei batch dell'agente di merge.  
  
 La dimensione dei batch per la replica di tipo merge è misurata in *generazioni*, ovvero raccolte di modifiche per ogni articolo. Per specificare il numero di generazioni in un batch, si usano i parametri -**DownloadGenerationsPerBatch** e -**UploadGenerationsPerBatch** dell'agente di merge. Per altre informazioni, vedere [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
 Per volumi elevati di dati, specificare un numero basso per ognuno dei parametri di batch. Si consiglia di iniziare con il valore 10, quindi regolarlo in base alle esigenze e alle prestazioni dell'applicazione. In genere, questi parametri sono specificati in un profilo dell'agente. Per ulteriori informazioni sui profili, vedere [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
## <a name="security-best-practices-for-web-synchronization"></a>Procedure consigliate per la sicurezza nella sincronizzazione Web  
 Sono disponibili numerose impostazioni relative alla sicurezza nella sincronizzazione Web. È consigliabile adottare l'approccio seguente:  
  
-   Il server di distribuzione e il server di pubblicazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono trovarsi nello stesso computer. Si tratta della configurazione tipica nella replica di tipo merge. È tuttavia necessario che IIS sia installato in un computer separato.  
  
-   Utilizzare SSL (Secure Sockets Layer) per la crittografia della connessione tra il sottoscrittore e il computer che esegue IIS. Questa operazione è necessaria per la sincronizzazione Web.  
  
-   Utilizzare l'autenticazione di base per le connessioni dal sottoscrittore a IIS. Con l'autenticazione di base, IIS è in grado di eseguire connessioni al server di pubblicazione/distribuzione per conto del Sottoscrittore senza alcuna delega. La delega è necessaria se si utilizza l'autenticazione integrata.  
  
    > [!NOTE]  
    >  L'autenticazione di base è il metodo mediante il quale vengono passate le credenziali a IIS. L'autenticazione di base non impedisce di specificare account di dominio di Windows per le connessioni a IIS.  
  
-   Specificare che l'agente snapshot deve essere eseguito con un account di dominio di Windows e che deve utilizzare tale account per le connessioni. Si tratta della configurazione predefinita. Specificare che ogni agente di merge deve essere eseguito con l'account di dominio dell'utente che utilizza il computer Sottoscrittore e che deve utilizzare tale account per le connessioni.  
  
     Per ulteriori informazioni sulle autorizzazioni richieste dagli agenti, vedere [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Specificare lo stesso account di dominio usato dall'agente di merge quando si specifica un account e una password nella pagina **Informazioni sul server Web** della Creazione guidata nuova sottoscrizione o quando si specificano i valori per i parametri `@internet_url` e `@internet_login` di [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Questo account deve disporre delle autorizzazioni di lettura per la condivisione snapshot.  
  
-   Ogni pubblicazione deve utilizzare una directory virtuale separata per IIS.  
  
-   L'account con cui viene eseguito il listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Replisapi.dll) è anche l'account utilizzato per la connessione al server di pubblicazione e al server di distribuzione durante la sincronizzazione. Deve essere eseguito il mapping di questo account a un account di accesso di SQL nel server di pubblicazione e nel server di distribuzione. Per altre informazioni, vedere la sezione "Impostazione delle autorizzazioni per Listener per la replica di SQL Server" in [Configurare IIS per la sincronizzazione Web](../../relational-databases/replication/configure-iis-for-web-synchronization.md).  
  
-   È possibile utilizzare la connessione FTP per trasferire lo snapshot dal server di pubblicazione al computer che esegue IIS. Lo snapshot viene sempre trasferito dal computer che esegue IIS al Sottoscrittore tramite HTTPS. Per altre informazioni, vedere [Trasferire snapshot tramite FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
-   Se i server nella topologia di replica sono protetti da un firewall, potrebbe essere necessario aprire porte nel firewall per consentire la sincronizzazione Web.  
  
    -   Il computer sottoscrittore si connette al computer che esegue IIS tramite HTTPS utilizzando SSL. In questo caso è in genere configurato l'utilizzo della porta 443. I Sottoscrittori di[!INCLUDE[ssEW](../../includes/ssew-md.md)] possono inoltre connettersi tramite HTTP, in genere configurato per l'utilizzo della porta 80.  
  
    -   Il computer che esegue IIS si connette in genere al server di pubblicazione o al server di distribuzione mediante la porta 1433 (istanza predefinita). Quando il server di pubblicazione o di distribuzione corrisponde a un'istanza denominata in un server con un'altra istanza predefinita, per la connessione all'istanza denominata viene in genere utilizzata la porta 1500.  
  
    -   Se il computer che esegue IIS e il server di distribuzione sono separati da un firewall e per il recapito di snapshot viene utilizzata una condivisione FTP, è necessario aprire le porte utilizzate per FTP. Per altre informazioni, vedere [Trasferire snapshot tramite FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).  
  
> [!IMPORTANT]  
>  L'apertura di porte nel firewall potrebbe esporre il server ad attacchi dannosi. Prima di aprire una porta, verificare di comprenderne le implicazioni per un sistema firewall. Per altre informazioni, vedere [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Sincronizzazione Web per la replica di tipo merge](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
