---
title: Gestione configurazione SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server], managing
- network protocols [SQL Server], managing
- Client Network Utility
- accounts [SQL Server]
- SQL Server Configuration Manager
- Server Network Utility
- accounts [SQL Server], services
- services [SQL Server], managing
- tools [SQL Server], SQL Server Configuration Manager
- configuration manager [SQL Server]
ms.assetid: e6beaea4-164c-4078-95ae-b9e28b0aefe8
author: rothja
ms.author: jroth
ms.openlocfilehash: a2ec44d192f688e25f2c9a12452de141eca7ca22
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068372"
---
# <a name="sql-server-configuration-manager"></a>Gestione configurazione SQL Server
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è uno strumento che consente di gestire i servizi associati a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], di configurare i protocolli di rete utilizzati da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e di gestire la configurazione della connettività di rete da computer client [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Gestione configurazione è uno snap-in di [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console disponibile tramite il menu Start o che può essere aggiunto a qualsiasi altra visualizzazione di [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console. [!INCLUDE[msCoName](../includes/msconame-md.md)]La console di gestione (mmc.exe) usa il file SQLServerManager10. msc nella cartella system32 di Windows per aprire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Gestione configurazione e SQL Server Management Studio usano Strumentazione gestione Windows (WMI) per la visualizzazione e la modifica di alcune impostazioni server. WMI offre una modalità unificata di interfacciamento con le chiamate API che gestiscono le operazioni del Registro di sistema richieste dagli strumenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e per fornire un controllo e una manipolazione avanzati dei servizi SQL selezionati del componente snap-in Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per informazioni sulla configurazione delle autorizzazioni relative a WMI, vedere [Configurazione di WMI per mostrare lo stato del server in Strumenti SQL Server](../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md).  
  
> [!NOTE]
>  Poiché Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è uno snap-in per il programma [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console e non un programma autonomo, Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non viene visualizzato come applicazione nelle versioni più recenti di Windows.  
> 
>  -   **Windows 10**:  
>          Per aprire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, nella **pagina iniziale**digitare SQLServerManager12. msc (per [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] ). Per le versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , sostituire 12 con un numero inferiore. Se si fa clic su SQLServerManager12.msc, viene aperto Gestione configurazione. Per aggiungere la Configuration Manager alla pagina iniziale o alla barra delle applicazioni, fare clic con il pulsante destro del mouse su SQLServerManager12. msc, quindi scegliere **Apri percorso file**. In Esplora file di Windows fare clic con il pulsante destro del mouse su SQLServerManager12. msc, quindi scegliere **Aggiungi a Start** o **Aggiungi alla barra delle applicazioni**.  
> -   **Windows 8**.  
>          Per aprire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager, nell'accesso alla **ricerca** , in **app**digitare **SQLServerManager \<version> . msc** , ad esempio `SQLServerManager12.msc` , quindi premere **invio**.  
  
 Per avviare, arrestare, sospendere, riprendere o configurare i servizi in un altro computer tramite Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Connessione a un altro computer &#40;Gestione configurazione SQL Server&#41;](../database-engine/configure-windows/scm-services-connect-to-another-computer.md).  
  
## <a name="managing-services"></a>Gestione di servizi  
 Utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per avviare, sospendere, riprendere o arrestare i servizi oppure per visualizzarne o modificarne le proprietà.  
  
 Utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per avviare i parametri di avvio del [!INCLUDE[ssDE](../includes/ssde-md.md)].  Per altre informazioni, vedere [Configurazione delle opzioni di avvio del server &#40;Gestione configurazione SQL Server&#41;](../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
## <a name="changing-the-accounts-used-by-the-services"></a>Modifica degli account utilizzati dai servizi  
 Gestire i servizi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzando Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Usare sempre strumenti [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , ad esempio Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , per modificare l'account usato dai servizi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent oppure per modificare la password per l'account. Oltre alla modifica del nome dell'account, Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] consente di eseguire altre configurazioni, ad esempio l'impostazione delle autorizzazioni nel Registro di sistema di Windows in modo che il nuovo account possa leggere le impostazioni [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Altri strumenti, ad esempio Gestione controllo servizi di Windows, consentono di modificare il nome dell'account ma non le impostazioni ad esso associate. Se non riesce ad accedere alla parte [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] del Registro di sistema, il servizio potrebbe non avviarsi correttamente.  
  
 Un ulteriore vantaggio è che le password modificate tramite Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , SMO o WMI diventano subito operative senza che sia necessario riavviare il servizio.  
  
## <a name="manage-server--client-network-protocols"></a>Gestione dei protocolli di rete server e client  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] consente di configurare i protocolli di rete server e client e le opzioni di connessione. Dopo aver attivato i protocolli corretti, non è in genere necessario modificare le connessioni di rete server. È tuttavia possibile utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per riconfigurare le connessioni al server affinché [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esegua l'ascolto su una porta, una pipe o un protocollo di rete specifici. Per altre informazioni sull'attivazione di protocolli, vedere [Abilitare o disabilitare un protocollo di rete del server](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md). Per informazioni sull'attivazione dell'accesso ai protocolli tramite un firewall, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Gestione configurazione consente di gestire i protocolli di rete server e client, imporre la crittografia dei protocolli, visualizzare le proprietà con alias o attivare/disabilitare un protocollo.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] consente di creare o rimuovere un alias, modificare l'ordine di utilizzo dei protocolli o visualizzare le proprietà per un alias server, compresi:  
  
-   Alias server: l'alias server usato per il computer a cui si sta connettendo il client.  
  
-   Protocollo: il protocollo di rete usato per la voce di configurazione.  
  
-   Parametri per la connessione: i parametri associati all'indirizzo di connessione per la configurazione del protocollo di rete.  
  
 Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] consente inoltre di visualizzare le informazioni sulle istanze cluster di failover, sebbene per alcune azioni, ad esempio l'avvio e l'arresto di servizi, sia necessario utilizzare Amministrazione cluster.  
  
### <a name="available-network-protocols"></a>Protocolli di rete disponibili  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta protocolli Shared Memory, TCP/IP e Named Pipes. Per ulteriori informazioni sulla scelta dei protocolli di rete, vedere [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md). [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non supporta i protocolli di rete VIA, Banyan VINES Sequenced Packet Protocol (SPP), Multiprotocol, AppleTalk o NWLink IPX/SPX. Per i client che in precedenza eseguivano la connessione con questi protocolli, è necessario selezionare un protocollo diverso per la connessione a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Non è possibile utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per configurare il proxy WinSock. Per configurare il proxy WinSock, vedere la documentazione su ISA Server.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Procedure per la gestione dei servizi &#40;Gestione configurazione SQL Server&#41;](../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
 [Avviare, arrestare, sospendere, riprendere, riavviare il motore di database, SQL Server Agent o SQL Server Browser](../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
 [Start, Stop, or Pause the SQL Server Agent Service](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
 [Impostare un'istanza di SQL Server per l'avvio automatico &#40;Gestione configurazione SQL Server&#41;](../database-engine/configure-windows/scm-services-set-an-instance-to-start-automatically.md)  
  
 [Impedire l'avvio automatico di un'istanza di SQL Server &#40;Gestione configurazione SQL Server&#41;](../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)  
  
  
