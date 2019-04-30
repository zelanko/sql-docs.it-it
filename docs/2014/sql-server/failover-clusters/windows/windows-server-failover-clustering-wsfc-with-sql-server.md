---
title: WSFC (Windows Server Failover Clustering) con SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- Windows Server Failover Clustering (WSFC), with SQL Server
- WSFC, with SQL Server
- quorum [SQL Server]
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: 79d2ea5a-edd8-4b3b-9502-96202057b01a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f39911901b6ab729382c2e08b34c3452d4ec65cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63246025"
---
# <a name="windows-server-failover-clustering-wsfc-with-sql-server"></a>WSFC (Windows Server Failover Clustering) con SQL Server
  Un cluster *Windows Server Failover Clustering (WSFC)* è un gruppo di server indipendenti usati congiuntamente per aumentare la disponibilità di applicazioni e servizi. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] vengono utilizzate le funzionalità e i servizi di WSFC per supportare le istanze del cluster di failover di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 
  
##  <a name="TermsAndDefs"></a> Termini e definizioni  
 Cluster WSFC  
 Un cluster Windows Server Failover Clustering (WSFC) è un gruppo di server indipendenti utilizzati congiuntamente per aumentare la disponibilità di applicazioni e servizi.  
  
 Istanza del cluster di failover  
 Istanza di un servizio Windows tramite cui è possibile gestire una risorsa dell'indirizzo IP, una risorsa del nome di rete e le risorse aggiuntive necessarie per eseguire uno o più servizi o applicazioni. Il nome di rete può essere utilizzato dai client per accedere alle risorse nel gruppo, in modo analogo all'utilizzo del nome di un computer per accedere ai servizi in un server fisico. Tuttavia, poiché un'istanza del cluster di failover è un gruppo, non è possibile eseguirne il failover in un altro nodo senza influire sul nome o l'indirizzo sottostante.  
  
 Node  
 Un sistema Microsoft Windows membro attivo o inattivo di un cluster di server.  
  
 Risorsa cluster  
 Entità fisica o logica che può essere di proprietà di un nodo e che è possibile portare online e offline, spostare tra nodi e gestire come oggetto cluster. Una risorsa cluster può essere solo di proprietà di un nodo singolo in qualsiasi punto nel tempo.  
  
 Gruppo di risorse  
 Raccolta di risorse cluster gestita come un solo oggetto cluster. In genere, un gruppo di risorse contiene tutte le risorse cluster richieste per eseguire un'applicazione o un servizio specifico. Failover e failback vengono sempre eseguiti su gruppi di risorse.  
  
 Dipendenza dalla risorsa  
 Risorsa da cui dipende un'altra risorsa. Se la risorsa A dipende dalla risorsa B, B è una dipendenza di A.  
  
 Risorsa nome di rete  
 Nome di server logico gestito come risorsa cluster. Una risorsa nome di rete deve essere utilizzata con una risorsa indirizzo IP.  
  
 Proprietario preferito  
 Nodo in cui si preferisce eseguire un gruppo di risorse. Ogni gruppo di risorse è associato a un elenco di proprietari preferiti ordinato in base alla preferenza. Durante il failover automatico, il gruppo di risorse viene spostato al nodo preferito successivo nell'elenco di proprietari preferiti.  
  
 Possibile proprietario  
 Nodo secondario in cui è possibile eseguire una risorsa. Ogni gruppo di risorse è associato a un elenco di possibili proprietari. È possibile eseguire il failover dei gruppi di risorse solo ai nodi elencati come possibili proprietari.  
  
 Modalità quorum  
 Configurazione del quorum in un cluster di failover che determina il numero di errori di nodo supportati dal cluster.  
  
 Quorum forzato  
 Processo di avvio del cluster anche nel caso in cui sia in comunicazione solo una minoranza degli elementi richiesti per il quorum.  
  
 Per altre informazioni, vedere: [Glossario del Cluster di failover](/previous-versions/windows/desktop/MsCS/server-cluster-glossary)  
  
##  <a name="Overview"></a> Panoramica di Windows Server Failover Clustering  
 In Windows Server Failover Clustering sono disponibili funzionalità di infrastruttura che supportano gli scenari di disponibilità elevata e ripristino di emergenza delle applicazioni server ospitate quali Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e Microsoft Exchange. Se si verifica un errore in un nodo o servizio cluster, i servizi ospitati su tale nodo possono essere trasferiti automaticamente o manualmente a un altro nodo disponibile in un processo noto come *failover*.  
  
 I nodi del cluster WSFC operano insieme per fornire collettivamente questi tipi di funzionalità:  
  
-   **Notifiche e metadati distribuiti.** I metadati del servizio WSFC e delle applicazioni ospitate vengono gestiti in ogni nodo del cluster. I metadati includono la configurazione e lo stato di WSFC oltre alle impostazioni delle applicazioni ospitate. Le modifiche apportate ai metadati o allo stato di un nodo vengono automaticamente propagate agli altri nodi del cluster.  
  
-   **Gestione delle risorse.** I singoli nodi del cluster possono fornire risorse fisiche, ad esempio archiviazione a collegamento diretto, interfacce di rete e accesso all'archiviazione su dischi condivisi. Le applicazioni ospitate effettuano la registrazione come risorse cluster e possono configurare dipendenze di avvio e integrità su altre risorse.  
  
-   **Monitoraggio dello stato.** Il rilevamento dello stato del nodo primario e tra nodi viene effettuato tramite una combinazione di comunicazioni di rete di tipo heartbeat e di monitoraggio delle risorse. Lo stato complessivo del cluster è determinato dai voti di un quorum di nodi nel cluster.  
  
-   **Coordinamento del failover.** Ogni risorsa è configurata per essere ospitata su un nodo primario e può essere trasferita automaticamente o manualmente a uno o più nodi secondari. I criteri di failover basati sull'integrità controllano il trasferimento automatico della proprietà della risorsa tra i nodi. Quando si verifica il failover, viene inviata una notifica ai nodi e alle applicazioni ospitate affinché siano in grado di reagire nel modo appropriato.  
  
 Per altre informazioni, vedere: [Cluster di failover in Windows Server 2008 R2](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
##  <a name="AlwaysOnWsfcTech"></a> Cluster WSFC e le tecnologie SQL Server AlwaysOn  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] *AlwaysOn* è una nuova elevata disponibilità e ripristino di emergenza soluzione di ripristino che si avvale del cluster WSFC. AlwaysOn è una soluzione integrata e flessibile che aumenta la disponibilità delle applicazioni, garantisce un migliore utile sugli investimenti in componenti hardware e semplifica la distribuzione e la gestione della disponibilità elevata.  
  
 Per le istanze del cluster di failover [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e AlwaysOn viene utilizzata la tecnologia della piattaforma WSFC che prevede la registrazione dei componenti come risorse cluster WSFC.  Le risorse correlate vengono combinate in un *gruppo di risorse*che può essere reso dipendente dalle altre risorse del cluster WSFC. Il servizio cluster WSFC può quindi rilevare e segnalare la necessità di riavviare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o eseguirne automaticamente il failover a un altro nodo server nel cluster WSFC.  
  
> [!IMPORTANT]  
>  Per sfruttare al meglio i vantaggi delle tecnologie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn, è necessario applicare diversi prerequisiti correlati a WSFC.  
>   
>  Per altre informazioni, vedere: [Prerequisiti, restrizioni e consigli per gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
### <a name="instance-level-high-availability-with-alwayson-failover-cluster-instances"></a>Disponibilità elevata a livello di istanza con istanze del cluster di failover AlwaysOn  
 Un' *istanza del cluster di failover* AlwaysOn è un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] installata nei nodi di un cluster WSFC. Questo tipo di istanza dispone di dipendenze dalle risorse sull'archiviazione su disco condivisa (tramite Fibre Channel o SAN iSCSI) e su un nome di rete virtuale. Il nome di rete virtuale presenta una dipendenza dalle risorse su uno o più indirizzi IP virtuali, ciascuno in una subnet diversa. Il servizio SQL Server e il servizio SQL Server Agent vengono registrati come risorse ed entrambi vengono resi dipendenti dalla risorsa del nome di rete virtuale.  
  
 In caso di failover, la proprietà delle risorse di un'istanza viene trasferita dal servizio WSFC a un nodo di failover definito. L'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene quindi riavviata sul nodo di failover e i database vengono recuperati nel modo consueto. In un qualsiasi momento specifico, solo un nodo singolo nel cluster può ospitare l'istanza del cluster di failover e le risorse sottostanti.  
  
> [!NOTE]  
>  Un'istanza del cluster di failover AlwaysOn richiede l'archiviazione su disco condiviso simmetrica, ad esempio una rete di archiviazione SAN o una condivisione file SMB.  I volumi dell'archiviazione su disco condiviso devono essere disponibili a tutti i nodi di failover potenziali nel cluster WSFC.  
  
 Per altre informazioni, vedere: [Istanze del Cluster di Failover AlwaysOn](always-on-failover-cluster-instances-sql-server.md)  
  
### <a name="database-level-high-availability-with-includesshadrincludessshadr-mdmd"></a>Disponibilità elevata a livello di database con [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]  
 Un *gruppo di disponibilità* è un set di database utente il cui failover viene eseguito contemporaneamente. Un gruppo di disponibilità è costituito da una *replica di disponibilità primaria* e da una a quattro repliche secondarie gestite tramite lo spostamento dati basato su log di SQL Server per la protezione dei dati senza la necessità di archiviazione condivisa. Ogni replica è ospitata da un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] su un nodo diverso del cluster WSFC. Il gruppo di disponibilità e un nome di rete virtuale corrispondente sono registrati come risorse nel cluster WSFC.  
  
 Tramite un *listener del gruppo di disponibilità* sul nodo della replica primaria si risponde alle richieste client in ingresso per connettersi al nome di rete virtuale e, in base agli attributi nella stringa di connessione, si indirizza ogni richiesta all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] appropriata.  
  
 In caso di failover, anziché trasferire la proprietà delle risorse fisiche condivise a un altro nodo si utilizza WSFC per riconfigurare una replica secondaria su un'altra istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come replica primaria del gruppo di disponibilità. La risorsa del nome di rete virtuale del gruppo di disponibilità viene quindi trasferita a tale istanza.  
  
 In un qualsiasi momento specifico, solo una singola istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può ospitare la replica primaria dei database di un gruppo di disponibilità; tutte le repliche secondarie associate devono trovarsi ciascuna in un'istanza separata e ogni istanza deve risiedere su nodi fisici separati.  
  
> [!NOTE]  
>  Per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] non è necessario distribuire un'istanza del cluster di failover né utilizzare l'archiviazione condivisa simmetrica (SAN o SMB).  
>   
>  È possibile utilizzare un'istanza del cluster di failover con un gruppo di disponibilità per migliorare la disponibilità di una replica di disponibilità. Per evitare potenziali race condition nel cluster WSFC, tuttavia, non è consentito eseguire il failover automatico del gruppo di disponibilità a o da una replica di disponibilità ospitata in un'istanza del cluster di failover.  
  
 Per altre informazioni, vedere: [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
##  <a name="AlwaysOnWsfcHealth"></a> Monitoraggio dello stato e failover di WSFC  
 La disponibilità elevata per una soluzione AlwaysOn viene realizzata attraverso il monitoraggio dello stato proattivo di risorse cluster WSFC fisiche e logiche, insieme al failover automatico e alla riconfigurazione dell'hardware ridondante.  Un amministratore di sistema può inoltre iniziare un *failover manuale* di un gruppo di disponibilità o un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da un nodo a un altro.  
  
### <a name="failover-policies-for-nodes-failover-cluster-instances-and-availability-groups"></a>Criteri di failover per nodi, istanze del cluster di failover e gruppi di disponibilità  
 I *criteri di failover* vengono configurati a livello di nodo del cluster WSFC, di istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e di gruppo di disponibilità.  Tali criteri, basati sulla gravità, la durata e la frequenza degli stati non integri delle risorse cluster e sulla velocità di risposta del nodo, possono attivare un riavvio del servizio o un *failover automatico* delle risorse cluster da un nodo a un altro oppure attivare lo spostamento di una replica primaria del gruppo di disponibilità da un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un'altra.  
  
 Il failover di una replica del gruppo di disponibilità non ha effetti sull'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sottostante.  Con il failover di un'istanza del cluster di failover le repliche del gruppo di disponibilità ospitate vengono spostate con l'istanza.  
  
 Per altre informazioni, vedere: [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md)  
  
### <a name="wsfc-resource-health-detection"></a>Rilevamento dell'integrità delle risorse WSFC  
 Ogni risorsa in un nodo del cluster WSFC può segnalare il proprio stato e la propria integrità, periodicamente o su richiesta. Un'ampia gamma di circostanze potrebbe indicare un errore della risorsa; ad esempio, interruzione dell'alimentazione, errori di disco o memoria, errori nella comunicazione di rete o servizi che non rispondono.  
  
 È possibile rendere dipendenti l'una dall'altra risorse cluster WSFC quali reti, archiviazione o servizi. L'integrità cumulativa di una risorsa è determinata dal rollup successivo dell'integrità e con l'integrità di ognuna delle dipendenze della risorsa.  
  
### <a name="wsfc-inter-node-health-detection-and-quorum-voting"></a>Rilevamento dell'integrità tra nodi WSFC e voto del quorum  
 Ogni nodo in un cluster WSFC partecipa alla comunicazione heartbeat periodica per condividere il proprio stato di integrità con gli altri nodi. I nodi che non rispondono sono considerati in stato di errore.  
  
 Un set di nodi *quorum* rappresenta una maggioranza dei nodi votanti e degli elementi di controllo nel cluster WSFC. L'integrità e lo stato complessivi di un cluster WSFC sono determinati da un *voto quorum*periodico. La presenza di un quorum indica che il cluster è integro e in grado di fornire tolleranza di errore a livello di nodo.  
  
 Una *modalità quorum* è configurata a livello del cluster WSFC che determina la metodologia utilizzata per il voto del quorum, nonché quando eseguire un failover automatico o portare il cluster offline.  
  
> [!TIP]  
>  La procedura consigliata prevede di disporre sempre di un numero dispari di voti del quorum in un cluster WSFC.  Ai fini del voto del quorum, non è necessario che [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sia installato in tutti i nodi nel cluster. Un server aggiuntivo può fungere da membro del quorum o è possibile configurare il modello del quorum WSFC per utilizzare una condivisione file remota come elemento per la risoluzione dei conflitti.  
>   
>  Per altre informazioni, vedere: [Modalità quorum WSFC e configurazione del voto &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)  
  
### <a name="disaster-recovery-through-forced-quorum"></a>Ripristino di emergenza tramite quorum forzato  
 A seconda delle procedure operative e della configurazione del cluster WSFC, è possibile generare failover sia automatici sia manuali pur mantenendo una soluzione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn affidabile e a tolleranza d'errore. Se tuttavia un quorum di nodi votanti idonei nel cluster WSFC non è in grado di comunicare reciprocamente o se la convalida dell'integrità del cluster WSFC ha esito negativo, è possibile che il cluster WSFC passi alla modalità offline.  
  
 Se il cluster WSFC passa alla modalità offline a causa di un'emergenza non pianificata o di un errore persistente a livello di hardware o di comunicazione, è necessario un intervento amministrativo manuale per *forzare un quorum* e riportare online i nodi del cluster ancora esistenti in una configurazione non a tolleranza d'errore.  
  
 Successivamente, sarà inoltre necessario effettuare una serie di passaggi per riconfigurare il cluster WSFC, recuperare le repliche di database interessate e ristabilire un nuovo quorum.  
  
 Per altre informazioni, vedere: [Ripristino di emergenza WSFC tramite quorum forzato &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
##  <a name="AlwaysOnWsfcRelationship"></a> Relazione dei componenti AlwaysOn di SQL Server con WSFC  
 Sono presenti diversi livelli di relazione tra le funzionalità e i componenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn e WSFC.  
  
 I gruppi di disponibilità AlwaysOn sono ospitati nelle istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
 Una richiesta client tramite cui viene specificato un nome di rete del listener del gruppo di disponibilità logico per connettersi a un database primario o secondario viene reindirizzato al nome di rete dell'istanza appropriata di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sottostante o all'istanza del cluster di failover (FCI) di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Le istanze di SQL Server sono ospitate attivamente in un solo nodo.  
 Se presente, un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] autonoma risiede sempre in un solo nodo con un nome di rete dell'istanza statico.  Se presente, un'istanza FCI di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è attiva su uno di due o più nodi di failover possibili con un solo nome di rete dell'istanza virtuale.  
  
 I nodi sono membri di un cluster WSFC.  
 I metadati e lo stato della configurazione WSFC per tutti i nodi sono archiviati in ciascun nodo. In ciascun server possono essere disponibili volumi di archiviazione o archiviazione condivisa (SAN) asimmetrica per i database utente o di sistema. Ogni server dispone almeno di un'interfaccia di rete fisica su una o più subnet IP.  
  
 Tramite il servizio WSFC viene monitorato lo stato e viene gestita la configurazione per un gruppo di server.  
 Tramite il servizio Windows Server Failover Clustering (WSCF) le modifiche vengono propagate ai metadati e allo stato della Configurazione WSFC in tutti i nodi del cluster. È possibile che stato e metadati parziali vengano archiviati in una condivisione di file remota del server di controllo quorum WSFC. Due o più nodi attivi o server di controllo costituiscono un quorum per il voto relativo all'integrità del cluster WSFC.  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] sono sottochiavi del cluster WSFC.  
 Se si elimina e si ricrea un cluster WSFC, è necessario disabilitare e riabilitare la funzionalità [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in ogni istanza del server abilitata per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] nel cluster WSFC originale. Per altre informazioni, vedere [Abilitare e disabilitare la funzionalità Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
 ![Diagramma del contesto del componente SQL Server AlwaysOn](../../../database-engine/media/alwaysoncomponentcontextdiagram.gif "Diagramma del contesto del componente SQL Server AlwaysOn")  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Visualizzare le impostazioni NodeWeight per il quorum del cluster](view-cluster-quorum-nodeweight-settings.md)  
  
-   [Configurare le impostazioni NodeWeight per il quorum del cluster](configure-cluster-quorum-nodeweight-settings.md)  
  
-   [Forzare l'avvio di un cluster WSFC senza un quorum](force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [Tecnologie di Windows Server:  cluster di failover](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)  
  
-   [Cluster di failover in Windows Server 2008 R2](https://technet.microsoft.com/library/ff182338\(WS.10\).aspx)  
  
-   [Visualizzare eventi e registri per un cluster di failover](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Pagina relativa al cluster di failover Get-ClusterLog](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Vedere anche  
 [Istanze del Cluster di Failover AlwaysOn (SQL Server)](always-on-failover-cluster-instances-sql-server.md)   
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Modalità quorum WSFC e configurazione del voto &#40;SQL Server&#41;](wsfc-quorum-modes-and-voting-configuration-sql-server.md)   
 [Criteri di failover per istanze del cluster di failover](failover-policy-for-failover-cluster-instances.md)   
 [Ripristino di emergenza WSFC tramite quorum forzato &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
  
