---
title: Prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], WSFC clusters
- Availability Groups [SQL Server], about
- Availability Groups [SQL Server], prerequisites and restrictions
- Availability Groups [SQL Server], Failover Cluster Instances
- Availability Groups [SQL Server], databases
- Availability Groups [SQL Server]
ms.assetid: edbab896-42bb-4d17-8d75-e92ca11f7abb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b12b9030d27e371e0299e06917464b1467b9b10e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782955"
---
# <a name="prerequisites-restrictions-and-recommendations-for-alwayson-availability-groups-sql-server"></a>Prerequisiti, restrizioni e consigli per i gruppi di disponibilità AlwaysOn (SQL Server)
  In questo argomento si illustrano le considerazioni sulla distribuzione di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], inclusi prerequisiti, restrizioni e indicazioni su computer host, cluster WSCF (Windows Server Failover Clustering), istanze del server e gruppi di disponibilità. Per ognuno di questi componenti sono indicate le eventuali considerazioni sulla sicurezza e le autorizzazioni richieste.  
  
> [!IMPORTANT]  
>  Prima di distribuire [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], si consiglia di leggere tutte le sezioni presenti in questo argomento.  
  
 
  
##  <a name="DotNetHotfixes"></a>Hotfix di .NET che supportano Gruppi di disponibilità AlwaysOn  
 A seconda dei componenti e delle funzionalità di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] che verranno utilizzati con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], potrebbe essere necessario aggiungere hotfix di .Net aggiuntivi identificati nella seguente tabella. Gli hotfix possono essere installati in qualsiasi ordine.  
  
||Funzionalità dipendente|Hotfix|Collegamento|  
|------|-----------------------|------------|----------|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|L'hotfix per .Net 3.5 SP1 aggiunge il supporto a SQL Client per le funzionalità Read-intent, readonly e multisubnetfailover di AlwaysOn. L'hotfix deve essere installato in ogni server di report di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .|KB 2654347: articolo relativo all' [hotfix per .Net 3.5 SP1 per aggiungere supporto alle funzionalità AlwaysOn](https://go.microsoft.com/fwlink/?LinkId=242896)|  
  
##  <a name="SystemReqsForAOAG"></a>Suggerimenti e requisiti di sistema di Windows  
  
  
###  <a name="SystemRequirements"></a> Elenco di controllo: requisiti (sistema Windows)  
 Per supportare la funzionalità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , assicurarsi che ogni computer che fa parte di uno o più gruppi di disponibilità soddisfi i requisiti essenziali seguenti:  
  
||Requisito|Collegamento|  
|------|-----------------|----------|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Assicurarsi che il sistema non sia un controller di dominio.|I gruppi di disponibilità non sono supportati nei controller di dominio.|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Assicurarsi che in ogni computer sia eseguita la versione x86 (non WOW64) o x64 di Windows Server 2008 o successive.|WOW64 (Windows a 32 bit in Windows a 64 bit) non supporta [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Assicurarsi che ogni computer sia un nodo in un cluster WSCF (Windows Server Failover Clustering).|[Windows Server Failover Clustering &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Assicurarsi che nel cluster WSFC siano contenuti nodi sufficienti per supportare le configurazioni dei gruppi di disponibilità.|Un nodo WSFC può ospitare solo una replica di disponibilità per un gruppo di disponibilità specifico. In un nodo WSFC specificato possono essere ospitate repliche di disponibilità per numerosi gruppi di disponibilità da parte di una o più istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Chiedere agli amministratori del database il numero di nodi WSFC necessario per supportare le repliche di disponibilità dei gruppi di disponibilità pianificati.<br /><br /> [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Assicurarsi che tutti gli hotfix di Windows applicabili siano stati installati in ogni nodo nel cluster WSFC.|** \* Importante \* \* ** Sono richiesti o consigliati numerosi hotfix per i nodi di un cluster WSFC in cui [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] viene distribuito. Per altre informazioni, vedere [Hotfix di Windows che supportano i gruppi di disponibilità AlwaysOn (sistema Windows)](#WinHotfixes), più avanti in questa sezione.|  
  
> [!IMPORTANT]  
>  Inoltre, assicurarsi che l'ambiente sia configurato correttamente per la connessione a un gruppo di disponibilità. Per ulteriori informazioni, vedere [connettività client AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md).  
  
####  <a name="WinHotfixes"></a>Hotfix di Windows che supportano Gruppi di disponibilità AlwaysOn (sistema Windows)  
 A seconda della topologia cluster, è possibile che siano applicabili per il supporto di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] diversi hotfix di Windows Server 2008 Service Pack 2 (SP2) o Windows Server 2008 R2 aggiuntivi. Nella tabella seguente vengono identificati questi hotfix. Gli hotfix possono essere installati in qualsiasi ordine.  
  
||Si applica a Windows 2008 SP2|Si applica a Windows 2008 R2 SP1|Incluso in Windows 2012|Per supportare...|Hotfix|Collegamento|  
|------|---------------------------------|------------------------------------|------------------------------|-----------------|------------|----------|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Sì|Sì|Sì|**Configurazione del quorum WSFC ottimale**|In ogni nodo WSFC assicurarsi che sia installato l'hotfix descritto nell'articolo della Knowledge Base 2494036.<br /><br /> Questo hotfix supporta la configurazione del quorum ottimale con le destinazioni di failover non automatico. Questa funzionalità consente di migliorare i cluster multisito permettendo di selezionare a quali nodi è associata la possibilità di votare.|KB 2494036: articolo relativo alla  [disponibilità di un hotfix per configurare un nodo del cluster che non presenta voti quorum in Windows Server 2008 e Windows Server 2008 R2](https://support.microsoft.com/kb/2494036)<br /><br /> Per informazioni sui voti del quorum, vedere [Modalità quorum WSFC e configurazione del voto &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Sì|Sì|Sì|**Utilizzo più efficiente della larghezza di banda della rete**|In ogni nodo WSFC assicurarsi che sia installato l'hotfix descritto nell'articolo della Knowledge Base 2616514.<br /><br /> Senza questo hotfix, il servizio Cluster invia notifiche del Registro di sistema non necessarie tra nodi del cluster. Questo comportamento limita la larghezza di banda della rete, causando seri problemi ad [!INCLUDE[ssHADRc](../../../includes/sshadrc-md.md)].|KB 2616514: articolo della Knowledge Base relativo al  [servizio cluster tramite cui si inviano notifiche di modifiche alla chiave del Registro di sistema non necessarie tra nodi del cluster in Windows Server 2008 o in Windows Server 2008 R2](https://support.microsoft.com/kb/2616514)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")||Sì|Non applicabile|**Test di archiviazione VPD su dischi non disponibili per tutti i nodi WSFC**|Se in un nodo WSFC è in esecuzione Windows Server 2008 R2 Service Pack 1 (SP1) e si verifica un errore del test di archiviazione Convalida VPD (Vital Product Data) dispositivi SCSI dopo un'esecuzione non corretta nei dischi che sono online e non disponibili a tutti i nodi nel cluster WSFC, installare l'hotfix descritto nell'articolo della Knowledge Base 2531907.<br /><br /> Con questo hotfix è possibile evitare avvisi o errori non corretti nel report di convalida quando i dischi sono online.|KB 2531907: articolo relativo all'[errore del test Convalida VPD (Vital Product Data) dispositivi SCSI dopo l'installazione di Windows Server 2008 R2 SP1](https://support.microsoft.com/kb/2531907)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")||Sì|Sì|**Failover più veloce nelle repliche locali**|Se in un nodo WSFC è in esecuzione Windows Server 2008 R2 Service Pack 1 (SP1), assicurarsi che sia installato l'hotfix descritto nell'articolo della Knowledge Base 2687741.<br /><br /> Con questo hotfix è possibile migliorare le prestazioni del failover di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] nelle repliche locali.|KB 2687741: articolo relativo alla  [disponibilità di un hotfix che consente di migliorare le prestazioni della funzionalità "Gruppo di disponibilità AlwaysOn" in SQL Server 2012 per Windows Server 2008 R2](https://support.microsoft.com/KB/2687741)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Sì|Sì|Sì|**Archiviazione asimmetrica per le istanze del cluster di failover (failover)**|Se una qualsiasi istanza del cluster di failover sarà abilitata per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], installare l'hotfix 976097 di Windows Server 2008.<br /><br /> Questo hotfix consente allo snap-in Gestione cluster di failover di Microsoft Management Console (MMC) di supportare i dischi condivisi di archiviazione asimmetrica disponibili solo in alcuni dei nodi WSFC.|KB 976097: articolo relativo all'[hotfix per aggiungere supporto per archiviazioni asimmetriche allo snap-in MMC di Gestione del cluster di failover per un cluster di failover in cui è in esecuzione Windows Server 2008 o Windows Server 2008 R2](https://support.microsoft.com/kb/976097)<br /><br /> [Pagina relativa alla guida all'architettura di AlwaysOn in cui viene illustrata la compilazione di una soluzione a disponibilità elevata e di ripristino di emergenza utilizzando istanze del cluster di failover e gruppi di disponibilità](https://technet.microsoft.com/library/jj215886.aspx)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Sì|Sì|Non applicabile|**IPsec (Internet Protocol Security)**|Se nell'ambiente si utilizzano connessioni IPSec, è possibile che si verifichi un ritardo prolungato (circa due o tre minuti) quando viene ristabilita la connessione IPSec da un computer client a un nome di rete virtuale (in questo contesto, per connettersi al listener del gruppo di disponibilità). Se si utilizzano le connessioni IPSec, è consigliabile rivedere gli scenari specifici descritti in dettaglio nell'articolo della Knowledge Base 980915:|KB 980915: articolo della Knowledge Base relativo al  [ritardo prolungato quando si riconnette una connessione IPSec da un computer in cui è in esecuzione Windows Server 2003, Windows Vista, Windows Server 2008, Windows 7 o Windows Server 2008 R2](https://support.microsoft.com/kb/980915)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Sì|Sì|Sì|**IPv6**|Se si utilizza IPv6, è consigliabile rivedere gli scenari specifici descritti in dettaglio nell'articolo della Knowledge Base 2578103 o 2578113, a seconda del sistema operativo Windows Server:<br /><br /> Se nella topologia Windows Server si utilizza IP versione 6 (IPv6), per il servizio cluster WSFC sono necessari circa 30 secondi per l'esecuzione del failover dell'indirizzo IP IPv6. Di conseguenza i client attenderanno circa 30 secondi per la riconnessione all'indirizzo IP IPv6.|KB 2578103 (Windows Server 2008): articolo relativo al [servizio cluster che richiede circa 30 secondi per eseguire il failover degli indirizzi IP IPv6 in Windows Server 2008](https://support.microsoft.com/kb/2578103)<br /><br /> KB 2578113 (Windows Server 2008 R2): articolo relativo a **Windows Server 2008 R2 sul ** [servizio cluster che richiede circa 30 secondi per eseguire il failover degli indirizzi IP IPv6 in Windows Server 2008 R2](https://support.microsoft.com/kb/2578113)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Sì|Sì|Sì|**Nessun router tra il cluster e il server applicazioni**|Se non esiste alcun router tra il cluster di failover e il server applicazioni, il failover del servizio cluster sulle risorse correlate alla rete avviene lentamente. In questo modo, le connessioni client vengono ritardate dopo il failover di un gruppo di disponibilità. In assenza di un router, è consigliabile rivedere gli scenari specifici descritti in dettaglio nell'articolo della Knowledge Base 2582281 e installare l'hotfix, se applicabile per l'ambiente.|KB 2582281: articolo della Knowledge Base relativo al  [failover lento se non esiste alcun router tra il cluster e un server applicazioni](https://support.microsoft.com/kb/2582281)|  
  
###  <a name="ComputerRecommendations"></a> Indicazioni per computer in cui sono ospitate repliche di disponibilità (sistema Windows)  
  
-   **Sistemi simili:**  Per un determinato gruppo di disponibilità, tutte le repliche di disponibilità devono essere in sistemi simili, in grado di gestire carichi di lavoro identici.  
  
-   **Schede di rete dedicate:**  Per ottenere prestazioni ottimali, usare una scheda di rete dedicata (scheda di interfaccia di rete) per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
-   **Spazio su disco sufficiente:**  Ogni computer in cui un'istanza del server ospita una replica di disponibilità deve disporre di spazio su disco sufficiente per tutti i database nel gruppo di disponibilità. Tenere presente che, con l'aumentare delle dimensioni dei database primari, i database secondari corrispondenti aumentano di conseguenza.  
  
###  <a name="PermissionsWindows"></a> Autorizzazioni (sistema Windows)  
 Per amministrare un cluster WSFC, l'utente deve essere un amministratore di sistema in ogni nodo del cluster.  
  
 Per altre informazioni sull'account per l'amministrazione del cluster, vedere [Appendice A: Requisiti di un cluster di failover](https://technet.microsoft.com/library/dd197454\(WS.10\).aspx).  
  
###  <a name="RelatedTasksWindows"></a> Attività correlate (sistema Windows)  
  
|Attività|Collegamento|  
|----------|----------|  
|Impostare il valore HostRecordTTL.|[Modificare HostRecordTTL (tramite Windows PowerShell)](#ChangeHostRecordTTLps)|  
  
####  <a name="ChangeHostRecordTTLps"></a> Modificare HostRecordTTL (tramite Windows PowerShell)  
  
1.  Aprire la finestra di PowerShell con **Esegui come amministratore**.  
  
2.  Importare il modulo FailoverClusters.  
  
3.  Utilizzare li cmdlet `Get-ClusterResource` per cercare la risorsa nome di rete, quindi utilizzare il cmdlet `Set-ClusterParameter` per impostare il valore `HostRecordTTL`, come segue:  
  
     Get-ClusterResource "*\<NetworkResourceName>*" | Set-ClusterParameter HostRecordTTL *\<TimeInSeconds>*  
  
     Nell'esempio di PowerShell seguente impostare HostRecordTTL su 300 secondi per una risorsa nome di rete denominata "`SQL Network Name (SQL35)`".  
  
    ```powershell
    Import-Module FailoverClusters  
  
    $nameResource = "SQL Network Name (SQL35)"  
    Get-ClusterResource $nameResource | Set-ClusterParameter ClusterParameter HostRecordTTL 300  
    ```  
  
    > [!TIP]  
    >  Ogni volta che viene aperta una nuova finestra di PowerShell, è necessario importare il modulo `FailoverClusters`.  
  
##### <a name="related-content-powershell"></a>Contenuto correlato (PowerShell)  
  
-   [Clustering and High-Availability](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (Failover Clustering and Network Load Balancing Team Blog) (Clustering e disponibilità elevata - Blog del team di clustering di failover e bilanciamento del carico di rete)  
  
-   [Introduzione a Windows PowerShell in un cluster di failover](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [Comandi di risorse cluster e cmdlet di Windows PowerShell equivalenti](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
###  <a name="RelatedContentWS"></a> Contenuto correlato (sistema Windows)  
  
-   [Pagina relativa alla configurazione delle impostazioni DNS in un cluster di failover multisito](https://technet.microsoft.com/library/dd197562\(WS.10\).aspx)  
  
-   [Post sulla registrazione DNS con la risorsa del nome di rete](https://blogs.msdn.com/b/clustering/archive/2009/07/17/9836756.aspx)  
  
-   [Clustering di failover multisito di Windows 2008 R2](https://kiruba4u.blogspot.com/2012/03/failover-clustering-in-windows-server.html)  
  
##  <a name="ServerInstance"></a> Prerequisiti e restrizioni dell'istanza di SQL Server  
 Per ogni gruppo di disponibilità è richiesto un set di partner di failover, noti come *repliche di disponibilità*, ospitati da istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Un'istanza del server specifica può essere un'*istanza autonoma* o un'*istanza del cluster di failover* (FCI) di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 
  
###  <a name="PrerequisitesSI"></a> Elenco di controllo: prerequisiti (istanza del server)  
  
||Prerequisito|Collegamenti|  
|-|------------------|-----------|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Il computer host deve essere un nodo WSFC (Windows Server Failover Clustering). Le istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui sono ospitate le repliche di disponibilità di uno specifico gruppo di disponibilità devono risiedere in nodi diversi di un singolo cluster WSFC. L'unica eccezione è che quando viene eseguita la migrazione a un altro cluster WSFC, un gruppo di disponibilità può risiedere temporaneamente in due cluster.|[Windows Server Failover Clustering &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)<br /><br /> [Clustering di failover e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Se si desidera che in un gruppo di disponibilità venga utilizzato Kerberos:<br /><br /> In tutte le istanze del server in cui è ospitata una replica di disponibilità per il gruppo di disponibilità deve essere utilizzato lo stesso account del servizio SQL Server.<br /><br /> L'amministratore di dominio deve registrare manualmente un nome dell'entità servizio (SPN, Service Principal Name) con Active Directory nell'account del servizio SQL Server per il nome di rete virtuale del listener del gruppo di disponibilità. Se il nome SPN è registrato in un account diverso da quello del servizio SQL Server, l'autenticazione non verrà completata.<br /><br /> **\*\* Importante \*\*** Se si modifica l'account del servizio SQL Server, l'amministratore di dominio dovrà registrare di nuovo manualmente il nome SPN.|[Registrazione di un nome dell'entità servizio per le connessioni Kerberos](../../configure-windows/register-a-service-principal-name-for-kerberos-connections.md)<br /><br /> **Breve spiegazione:**<br /><br /> A Kerberos e ai nomi SPN viene applicata l'autenticazione reciproca. Tramite il nome SPN viene eseguito il mapping all'account di Windows mediante il quale vengono avviati i servizi SQL Server. Se la registrazione del nome SPN non viene eseguita correttamente o presenta un errore, tramite il livello di sicurezza di Windows non è possibile determinare l'account associato al nome SPN e l'autenticazione Kerberos non può essere utilizzata.<br /><br /> Nota: NTLM non presenta questo requisito.|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Se si intende utilizzare un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per ospitare una replica di disponibilità, assicurarsi di aver compreso le restrizioni su questo tipo di istanza e che vengano soddisfatti i relativi requisiti.|[Prerequisiti e requisiti sull'utilizzo di un'istanza del cluster di failover di SQL Server per ospitare una replica di disponibilità](#FciArLimitations) (più avanti in questo argomento)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|In ogni istanza del server deve essere in esecuzione la versione Enterprise Edition di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].|[Funzionalità supportate dalle edizioni di SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|In tutte le istanze del server in cui sono ospitate repliche di disponibilità per un gruppo di disponibilità devono essere utilizzate le stesse regole di confronto di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Impostazione o modifica di regole di confronto del server](../../../relational-databases/collations/set-or-change-the-server-collation.md)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Abilitare la funzionalità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in ogni istanza del server in cui sarà ospitata una replica di disponibilità per qualsiasi gruppo di disponibilità. In un computer specificato è possibile abilitare tante istanze del server per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] quante sono quelle supportate dall'installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Abilitare e disabilitare la funzionalità Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)<br /><br /> ** \* Importante \* \* ** Se si elimina e si ricrea un cluster WSFC, è necessario disabilitare e riabilitare la [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] funzionalità in ogni istanza del server abilitata per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] nel cluster WSFC originale.|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Per ogni istanza del server è necessario un endpoint del mirroring del database. Si noti che questo endpoint è condiviso da tutte le repliche di disponibilità, dai partner di mirroring di database, nonché dai server di controllo nell'istanza del server.<br /><br /> Se un'istanza del server selezionata come host per una replica di disponibilità è in esecuzione in un account utente di dominio e non dispone ancora di un endpoint del mirroring del database, tramite la [Creazione guidata Gruppo di disponibilità](use-the-availability-group-wizard-sql-server-management-studio.md) (o [Procedura guidata Aggiungi replica a gruppo di disponibilità](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)) è possibile creare l'endpoint e concedere l'autorizzazione CONNECT all'account del servizio dell'istanza del server. Se, tuttavia, il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene eseguito come account predefinito, ad esempio Sistema locale, Servizio locale o Servizio di rete, oppure come account non di dominio, è necessario usare certificati per l'autenticazione dell'endpoint e non sarà possibile creare un endpoint del mirroring del database nell'istanza del server tramite la procedura guidata. In tal caso, è consigliabile creare manualmente gli endpoint del mirroring del database prima di avviare la procedura guidata.<br /><br /> **\*\* Nota di sicurezza \*\*** La sicurezza del trasporto per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] corrisponde a quella per il mirroring del database.|[Endpoint del mirroring del database &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)<br /><br /> [Sicurezza del trasporto per il mirroring del database e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-mirroring/transport-security-database-mirroring-always-on-availability.md)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Se tutti i database in cui è utilizzato FILESTREAM saranno aggiunti a un gruppo di disponibilità, verificare che FILESTREAM sia abilitato in ogni istanza del server in cui sarà ospitata una replica di disponibilità per il gruppo di disponibilità.|[Abilitare e configurare FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Se tutti i database indipendenti saranno aggiunti a un gruppo di disponibilità, verificare che l'opzione del server `contained database authentication` sia impostata su `1` in ogni istanza del server in cui sarà ospitata una replica di disponibilità per il gruppo di disponibilità.|[Opzione di configurazione del server contained database authentication](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Opzioni di configurazione del server &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
###  <a name="ThreadUsage"></a> Utilizzo del thread da parte dei gruppi di disponibilità  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] devono essere soddisfatti i requisiti seguenti:  
  
-   In caso di istanza inattiva di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], in [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] non viene utilizzato alcun thread.  
  
-   Il numero massimo di thread utilizzato dai gruppi di disponibilità è dato dall'impostazione configurata per il numero massimo di thread del server ("`max worker threads`") meno 40.  
  
-   Nelle repliche di disponibilità ospitate in un'istanza del server specificata viene condiviso un singolo pool di thread.  
  
     I thread vengono condivisi su richiesta, come riportato di seguito:  
  
    -   In genere, sono presenti 3-10 thread condivisi, tuttavia questo numero può aumentare a seconda del carico di lavoro della replica primaria.  
  
    -   Se un thread specificato è inattivo per un certo periodo di tempo, viene rilasciato nuovamente nel pool di thread generale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . In genere, un thread inattivo viene rilasciato dopo ~15 secondi di inattività. Tuttavia, a seconda dell'ultima attività, un thread inattivo potrebbe essere mantenuto più a lungo.  
  
-   Inoltre, nei gruppi di disponibilità vengono utilizzati thread non condivisi, come riportato di seguito:  
  
    -   In ogni replica primaria viene utilizzato 1 thread di acquisizione del log per ogni database primario. Inoltre, viene utilizzato 1 thread di invio del log per ogni database secondario. I thread di invio del log vengono rilasciati dopo ~15 secondi di inattività.  
  
    -   In ogni replica secondaria viene utilizzato 1 thread della fase di rollforward per ogni database secondario. I thread della fase di rollforward vengono rilasciati dopo ~15 secondi di inattività.  
  
    -   Tramite un backup di una replica secondaria un thread viene mantenuto nella replica primaria per la durata dell'operazione di backup.  
  
 Per altre informazioni, vedere la pagina relativa alla [serie di informazioni su HADRON riguardanti l'uso del pool di lavoro per database abilitati HADRON in AlwaysOn](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx) (blog del Servizio Supporto Tecnico Clienti per gli ingegneri di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]).  
  
###  <a name="PermissionsSI"></a> Autorizzazioni (istanza del server)  
  
|Attività|Autorizzazioni necessarie|  
|----------|--------------------------|  
|Creazione dell'endpoint del mirroring del database|È richiesta l'autorizzazione CREATE ENDPOINT o l'appartenenza al ruolo predefinito del server **sysadmin** .  È richiesta inoltre l'autorizzazione CONTROL ON ENDPOINT. Per altre informazioni, vedere [GRANT - autorizzazioni per endpoint &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql).|  
|Abilitazione di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]|È richiesta l'appartenenza al gruppo degli **amministratori** nel computer locale, nonché il controllo totale nel cluster WSCF.|  
  
###  <a name="RelatedTasksSI"></a> Attività correlate (istanza del server)  
  
|Attività|Argomento|  
|----------|-----------|  
|Determinazione della presenza di un endpoint del mirroring del database|[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)|  
|Creazione dell'endpoint del mirroring del database (se non ancora disponibile)|[Creare un endpoint del mirroring del database per l'autenticazione Windows &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)<br /><br /> [Utilizzare certificati per un endpoint del mirroring del database &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)<br /><br /> [Creazione di un endpoint del mirroring del database per Gruppi di disponibilità AlwaysOn &#40;SQL Server PowerShell&#41;](database-mirroring-always-on-availability-groups-powershell.md)|  
|Abilitazione di Gruppi di disponibilità AlwaysOn|[Abilitare e disabilitare la funzionalità Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)|  
  
###  <a name="RelatedContentSI"></a> Contenuto correlato (istanza del server)  
  
-   [Pagina relativa alla serie di informazioni su HADRON riguardanti l'utilizzo del pool di lavoro per database abilitati HADRON in AlwaysOn](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
##  <a name="NetworkConnect"></a> Consigli sulla connettività di rete  
 Si consiglia di utilizzare gli stessi collegamenti di rete per le comunicazioni tra membri del cluster WSFC e le comunicazioni tra repliche di disponibilità.  L'utilizzo di collegamenti di rete separati può provocare comportamenti imprevisti in caso di errore di alcuni collegamenti (anche in modo intermittente).  
  
 Ad esempio, affinché un gruppo di disponibilità supporti il failover automatico, lo stato della replica secondaria che è partner di failover automatico deve essere SYNCHRONIZED. In caso di errore di collegamento di rete a questa replica secondaria (anche in modo intermittente), lo stato della replica diventa UNSYNCHRONIZED e non sarà possibile cominciare la risincronizzazione fino a quando non viene ripristinato il collegamento. Se per il cluster WSFC è richiesto un failover automatico mentre la replica secondaria non è sincronizzata, il failover automatico non si verificherà.  
  
##  <a name="ClientConnSupport"></a> Supporto della connettività client  
 Per informazioni sul [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] supporto per la connettività client, vedere [connettività client AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md).  
  
##  <a name="FciArLimitations"></a> Prerequisiti e restrizioni per l'utilizzo di un'istanza del cluster di failover di SQL Server per ospitare una replica di disponibilità  
 
  
###  <a name="RestrictionsFCI"></a> Restrizioni (istanze del cluster di failover)  
  
> [!NOTE]  
>  A partire da [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], le istanze del cluster di failover AlwaysOn supportano i volumi condivisi cluster sia in [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] sia in [!INCLUDE[win8srv](../../../includes/win8srv-md.md)]. Per ulteriori informazioni sui volumi condivisi cluster, vedere [Informazioni sui volumi condivisi del cluster in un cluster di failover](https://technet.microsoft.com/library/dd759255.aspx).  
  
-   **I nodi del cluster di un'istanza FCI possono ospitare solo una replica per un determinato gruppo di disponibilità:**  Se si aggiunge una replica di disponibilità in un'istanza FCI, i nodi del cluster WSFC che sono possibili proprietari dell'istanza del cluster di failover non possono ospitare un'altra replica per lo stesso gruppo di disponibilità.  
  
     Inoltre, tutte le altre repliche devono essere ospitate da un'istanza di SQL Server 2012 che risiede in un nodo WSFC diverso nello stesso cluster WSFC. L'unica eccezione è che quando viene eseguita la migrazione a un altro cluster WSFC, un gruppo di disponibilità può risiedere temporaneamente in due cluster.  
  
-   **Le istanze del cluster di failover non supportano il failover automatico da parte di gruppi di disponibilità:**  le istanze del cluster di failover non supportano il failover automatico da gruppi di disponibilità, quindi le repliche di disponibilità ospitate da un'istanza del cluster di failover possono essere configurate solo per il failover manuale.  
  
-   **Modifica del nome di rete di un'istanza del cluster di failover:**  se è necessario modificare il nome di rete di un'istanza del cluster di failover che ospita una replica di disponibilità, è necessario rimuovere la replica dal relativo gruppo di disponibilità e riaggiungerla successivamente a questo gruppo. Non è possibile rimuovere la replica primaria, pertanto se si rinomina un'istanza del cluster di failover in cui è ospitata la replica primaria, è consigliabile eseguire il failover in una replica secondaria e successivamente rimuovere e poi riaggiungere la prima replica primaria. Si noti che la ridenominazione di un'istanza del cluster di failover può comportare la modifica dell'URL del relativo endpoint del mirroring del database. Quando si aggiunge la replica assicurarsi di specificare l'URL dell'endpoint corrente.  
  
###  <a name="PrerequisitesFCI"></a> Elenco di controllo: prerequisiti (istanze del cluster di failover)  
  
||Prerequisito|Collegamento|  
|-|------------------|----------|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Prima di utilizzare un'istanza del cluster di failover per ospitare una replica di disponibilità, assicurarsi che l'amministratore di sistema abbia installato l'hotfix per Windows Server 2008 descritto nell'articolo della Knowledge Base KB 976097. Questo hotfix consente allo snap-in Gestione cluster di failover di Microsoft Management Console (MMC) di supportare i dischi condivisi di archiviazione asimmetrica disponibili solo in alcuni dei nodi WSFC.|KB 976097: articolo relativo all'[hotfix per aggiungere supporto per archiviazioni asimmetriche allo snap-in MMC di Gestione del cluster di failover per un cluster di failover in cui è in esecuzione Windows Server 2008 o Windows Server 2008 R2](https://support.microsoft.com/kb/976097)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Assicurarsi che in ogni istanza del cluster di failover di SQL Server sia disponibile l'archiviazione condivisa necessaria in base all'installazione dell'istanza del cluster di failover di SQL Server standard.||  
  
###  <a name="RelatedTasksFCIs"></a> Attività correlate (istanze del cluster di failover)  
  
|Attività|Argomento|  
|----------|-----------|  
|Installazione di un cluster di failover di SQL Server|[Creare un nuovo cluster di failover di SQL Server &#40;programma di installazione&#41;](../../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Aggiornamento sul posto del cluster di failover di SQL Server esistente|[Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server &#40;installazione&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)|  
|Gestione del cluster di failover di SQL Server esistente|[Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
  
###  <a name="RelatedContentFCIs"></a> Contenuto correlato (istanze del cluster di failover)  
  
-   [Clustering di failover e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)  
  
-   [Pagina relativa alla guida all'architettura di AlwaysOn in cui viene illustrata la compilazione di una soluzione a disponibilità elevata e di ripristino di emergenza utilizzando istanze del cluster di failover e gruppi di disponibilità](https://technet.microsoft.com/library/jj215886.aspx)  
  
##  <a name="PrerequisitesForAGs"></a> Prerequisiti e restrizioni dei gruppi di disponibilità  

  
###  <a name="RestrictionsAG"></a> Restrizioni (gruppi di disponibilità)  
  
-   **Le repliche di disponibilità devono essere ospitate da nodi diversi di un cluster WSFC:**  Per un determinato gruppo di disponibilità, le repliche di disponibilità devono essere ospitate da istanze del server in esecuzione in nodi diversi dello stesso cluster WSFC. L'unica eccezione è che quando viene eseguita la migrazione a un altro cluster WSFC, un gruppo di disponibilità può risiedere temporaneamente in due cluster.  
  
    > [!NOTE]  
    >  In ogni macchina virtuale presente nello stesso computer fisico può essere ospitata una replica di disponibilità per lo stesso gruppo di disponibilità, in quanto ogni macchina virtuale costituisce un computer distinto.  
  
-   **Nome univoco del gruppo di disponibilità:**  Ogni nome di gruppo di disponibilità deve essere univoco nel cluster WSFC. La lunghezza massima consentita per il nome del gruppo di disponibilità è 128 caratteri.  
  
-   **Repliche di disponibilità:**  Ogni gruppo di disponibilità supporta una replica primaria e fino a otto repliche secondarie. È possibile eseguire tutte le repliche in modalità con commit asincrono oppure fino a un massimo di tre in modalità con commit sincrono (una replica primaria con due repliche secondarie sincrone).  
  
-   **Numero massimo di gruppi di disponibilità e database di disponibilità per computer:** il numero effettivo di database e gruppi di disponibilità che è possibile creare in un computer (macchina virtuale o computer fisico) dipende dall'hardware e dal carico di lavoro, tuttavia non esiste un limite imposto. Microsoft ha eseguito test estensivi con 10 gruppi di disponibilità e 100 database per computer fisico. I segnali di sistemi di overload possono includere, a titolo esemplificativo, l'esaurimento del thread di lavoro, tempi di risposta lenti per visualizzazioni di sistema AlwaysOn e DMV e/o dump del sistema dispatcher bloccati. Assicurarsi di testare completamente l'ambiente con un carico di lavoro simile a quello di produzione per assicurare che possa gestire capacità di carico di lavoro di picco all'interno del contratto sul livello di servizio dell'applicazione. Per i contratti sul livello di servizio occorre considerare il carico in condizioni di errore e i tempi di risposta previsti.  
  
-   **Non usare il Gestione cluster di failover per modificare i gruppi di disponibilità:**  
  
     Ad esempio:  
  
    -   Non modificare le proprietà del gruppo di disponibilità, ad esempio i possibili proprietari.  
  
    -   Non utilizzare Gestione cluster di failover per eseguire il failover dei gruppi di disponibilità. È necessario utilizzare [!INCLUDE[tsql](../../../includes/tsql-md.md)] o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="RequirementsAG"></a> Prerequisiti (gruppi di disponibilità)  
 Quando si crea o riconfigura una configurazione del gruppo di disponibilità, assicurarsi che si soddisfino i requisiti seguenti.  
  
||Prerequisito|Descrizione|  
|-|------------------|-----------------|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Se si intende utilizzare un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per ospitare una replica di disponibilità, assicurarsi di aver compreso le restrizioni su questo tipo di istanza e che vengano soddisfatti i relativi requisiti.|[Prerequisiti e restrizioni per l'utilizzo di un'istanza del cluster di failover di SQL Server (FCI) per ospitare una replica di disponibilità](#FciArLimitations) (più indietro in questo argomento)|  
  
###  <a name="SecurityAG"></a> Sicurezza (gruppi di disponibilità)  
  
-   La sicurezza viene ereditata dal cluster WSCF (Windows Server Failover Clustering). WSFC fornisce due livelli di sicurezza utente con granularità di API del cluster WSFC intere:  
  
    -   Accesso di sola lettura  
  
    -   Controllo completo  
  
         
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] necessita di un controllo completo. Se si abilita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene fornito a quest'ultima il controllo completo del cluster WSFC, tramite il SID del servizio.  
  
         Non è possibile aggiungere o rimuovere direttamente la sicurezza per un'istanza del server in Gestione cluster di failover di WSFC. Per gestire sessioni di sicurezza di WSFC, utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o l'equivalente WMI da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve disporre delle autorizzazioni per l'accesso al Registro di sistema, al cluster e così via.  
  
-   È consigliabile utilizzare la crittografia per le connessioni tra istanze del server in cui si ospitano repliche di disponibilità di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
#### <a name="permissions-availability-groups"></a>Autorizzazioni (gruppi di disponibilità)  
  
|Attività|Autorizzazioni necessarie|  
|----------|--------------------------|  
|Creazione di un gruppo di disponibilità|Sono necessarie l'appartenenza al ruolo predefinito del server **sysadmin** e l'autorizzazione server CREATE AVAILABILITY GROUP oppure l'autorizzazione ALTER ANY AVAILABILITY GROUP o CONTROL SERVER.|  
|Modifica di un gruppo di disponibilità|È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.<br /><br /> Inoltre, per la creazione di un join di un database a un gruppo di disponibilità è richiesta l'appartenenza al ruolo predefinito del database **db_owner** .|  
|Rimozione/eliminazione di un gruppo di disponibilità|È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER. Per rimuovere un gruppo di disponibilità non ospitato nel percorso della replica locale, è necessaria l'autorizzazione CONTROL SERVER o CONTROL per questo gruppo di disponibilità.|  
  
###  <a name="RelatedTasksAGs"></a> Attività correlate (gruppi di disponibilità)  
  
|Attività|Argomento|  
|----------|-----------|  
|Creazione di un gruppo di disponibilità|[Utilizzare il gruppo di disponibilità (Creazione guidata Gruppo di disponibilità)](use-the-availability-group-wizard-sql-server-management-studio.md)<br /><br /> [Creare un gruppo di disponibilità (Transact-SQL)](create-an-availability-group-transact-sql.md)<br /><br /> [Creare un gruppo di disponibilità (SQL Server PowerShell)](../../../powershell/sql-server-powershell.md)<br /><br /> [Specifica dell'URL dell'endpoint quando si aggiunge o si modifica una replica di disponibilità &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)|  
|Modifica del numero di repliche di disponibilità|[Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Creare un join di una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)<br /><br /> [Rimuovere una replica secondaria da un gruppo di disponibilità &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
|Creazione di un listener del gruppo di disponibilità|[Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
|Rimozione di un gruppo di disponibilità|[Rimuovere un gruppo di disponibilità &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)|  
  
##  <a name="PrerequisitesForDbs"></a> Prerequisiti e restrizioni dei database di disponibilità  
 Per essere idoneo a essere aggiunto a un gruppo di disponibilità, un database deve soddisfare i prerequisiti e le restrizioni riportate di seguito.  
  
 
  
###  <a name="RequirementsDb"></a> Elenco di controllo: requisiti (database di disponibilità)  
 Per essere idoneo a essere aggiunto a un gruppo di disponibilità, un database deve soddisfare i requisiti seguenti:  
  
||Requisiti|Collegamento|  
|-|------------------|----------|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Deve trattarsi di un database utente. I database di sistema non possono appartenere a un gruppo di disponibilità.||  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Deve trovarsi nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui si crea il gruppo di disponibilità e deve essere accessibile all'istanza del server.||  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Deve trattarsi di un database di lettura/scrittura. I database di sola lettura non possono essere aggiunti a un gruppo di disponibilità.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_read_only** = 0)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Deve trattarsi di un database multiutente.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**user_access** = 0)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Non deve essere utilizzato AUTO_CLOSE.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**is_auto_close_on** = 0)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Utilizzare il modello di recupero con registrazione completa (noto anche come modalità di recupero con registrazione completa).|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**recovery_model** = 1)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Deve disporre di almeno un backup completo del database.<br /><br /> Nota: Dopo aver impostato un database sulla modalità di recupero con registrazione completa, è necessario un backup completo per iniziare la catena di log del recupero con registrazione completa.|[Creazione di un backup completo del database &#40;SQL Server&#41;](../../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Non deve appartenere ad alcun gruppo di disponibilità esistente.|[sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) (**group_database_id** = NULL)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Non deve essere configurato per il mirroring del database.|[sys.database_mirroring](/sql/relational-databases/system-catalog-views/sys-database-mirroring-transact-sql) Se il database non fa parte del mirroring, tutte le colonne con prefisso "mirroring_" sono NULL.|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Prima di aggiungere un database in cui è utilizzato FILESTREAM a un gruppo di disponibilità, verificare che FILESTREAM sia abilitato in ogni istanza del server in cui è o sarà ospitata una replica di disponibilità per il gruppo di disponibilità.|[Abilitare e configurare FILESTREAM](../../../relational-databases/blob/enable-and-configure-filestream.md)|  
|![Casella di controllo](../../media/checkboxemptycenterxtraspacetopandright.gif "Casella di controllo")|Prima di aggiungere un database indipendente a un gruppo di disponibilità, verificare che l'opzione del server `contained database authentication` sia impostata su `1` in ogni istanza del server in cui è o sarà ospitata una replica di disponibilità per il gruppo di disponibilità.|[Opzione di configurazione del server contained database authentication](../../configure-windows/contained-database-authentication-server-configuration-option.md)<br /><br /> [Opzioni di configurazione del server &#40;SQL Server&#41;](../../configure-windows/server-configuration-options-sql-server.md)|  
  
> [!NOTE]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] funziona con qualsiasi livello di compatibilità del database supportato.  
  
###  <a name="RestrictionsDb"></a> Restrizioni (database di disponibilità)  
  
-   Se il percorso del file, inclusa la lettera di unità, di un database secondario differisce da quello del database primario corrispondente, si applicano le restrizioni seguenti:  
  
    -   **[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]/[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]:**  l'opzione **Completo** nella pagina [Seleziona sincronizzazione dati iniziale](select-initial-data-synchronization-page-always-on-availability-group-wizards.md) non è supportata.  
  
    -   **RESTORE WITH MOVE:**  per creare i database secondari, i file di database devono essere sottoposti a RESTORE WITH MOVE in ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui è ospitata una replica secondaria.  
  
    -   **Impatto sulle operazioni di aggiunta di file:**  un'operazione di aggiunta file successiva nella replica primaria potrebbe non riuscire nei database secondari. Questo errore può causare la sospensione dei database secondari. Questa situazione, a sua volta, può causare l'attivazione dello stato NON IN SINCRONIZZAZIONE delle repliche secondarie.  
  
        > [!NOTE]  
        >  Per informazioni sulla risposta a un'operazione di aggiunta di file non riuscita, vedere [Risolvere i problemi relativi a una operazione di aggiunta file non riuscita &#40;Gruppi di disponibilità AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md).  
  
-   Non è possibile eliminare un database che attualmente appartiene a un gruppo di disponibilità.  
  
###  <a name="TDEdbs"></a> Completamento per database protetti tramite crittografia TDE  
 Se si utilizza TDE (Transparent Data Encryption), la chiave asimmetrica o il certificato per la creazione e la decrittografia di altre chiavi deve essere identico in ogni istanza del server in cui viene ospitata una replica di disponibilità per il gruppo di disponibilità. Per altre informazioni, vedere [Spostare un database protetto da TDE in un'altra istanza di SQL Server](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
###  <a name="PermissionsDbs"></a> Autorizzazioni (database di disponibilità)  
 È richiesta l'autorizzazione ALTER per il database.  
  
###  <a name="RelatedTasksADb"></a> Attività correlate (database di disponibilità)  
  
|Attività|Argomento|  
|----------|-----------|  
|Preparazione di un database secondario (manuale)|[Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)|  
|Creazione di un join di un database secondario a un gruppo di disponibilità (manuale)|[Creare un join di un database secondario a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)|  
|Modifica del numero di database di disponibilità|[Aggiungere un database a un gruppo di disponibilità &#40;SQL Server&#41;](availability-group-add-a-database.md)<br /><br /> [Rimuovere un database secondario da un gruppo di disponibilità &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)<br /><br /> [Rimuovere un database primario da un gruppo di disponibilità &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)|  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [Pagina relativa alla guida alle soluzioni AlwaysOn di Microsoft SQL Server per la disponibilità elevata e il ripristino di emergenza](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Blog del team di SQL Server AlwaysOn: Blog del team ufficiale di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
-   [Pagina relativa alla serie di informazioni su HADRON riguardanti l'utilizzo del pool di lavoro per database abilitati HADRON in AlwaysOn](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Clustering di failover e Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](failover-clustering-and-always-on-availability-groups-sql-server.md)   
 [Connettività client AlwaysOn (SQL Server)](always-on-client-connectivity-sql-server.md)  
  
  
