---
title: Informazioni sull'accesso alla connessione client per le repliche di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 29027e46-43e4-4b45-b650-c4cdeacdf552
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 13a863603353ee47639cd327c8c5eebd6df8e12a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62789843"
---
# <a name="about-client-connection-access-to-availability-replicas-sql-server"></a>Informazioni sull'accesso alla connessione client per le repliche di disponibilità (SQL Server)
  In un gruppo di disponibilità AlwaysOn è possibile configurare una o più repliche di disponibilità per consentire connessioni di sola lettura quando in esecuzione nel ruolo secondario, cioè quando in esecuzione come replica secondaria. È inoltre possibile configurare ogni replica di disponibilità per consentire o escludere le connessioni di sola lettura quando l'esecuzione avviene nel ruolo primario, ossia come replica primaria.  
  
 Per facilitare l'accesso client ai database primari o secondari di un determinato gruppo di disponibilità, è necessario definire un listener del gruppo di disponibilità. Per impostazione predefinita, il listener del gruppo di disponibilità instrada le connessioni in ingresso alla replica primaria. Tuttavia, è possibile configurare un gruppo di disponibilità per supportare il routing di sola lettura che consente al listener del gruppo di disponibilità di reinstradare le richieste di connessione di applicazioni con finalità di lettura a una replica secondaria leggibile. Per altre informazioni, vedere [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md).  
  
 Durante un failover, una replica secondaria assume il ruolo primario e la replica primaria precedente passa al ruolo secondario. Durante il processo di failover, tutte le connessioni client sia alla replica primaria sia alle repliche secondarie vengono terminate. Dopo il failover, quando un client si riconnette al listener del gruppo di disponibilità, il listener riconnette il client alla nuova replica primaria, ad eccezione di una richiesta di connessione con finalità di lettura. Se il routing di sola lettura viene configurato sul client e sulle istanze del server che ospitano la nuova replica primaria e su almeno un replica secondaria leggibile, le richieste di connessione con finalità di lettura vengono indirizzate nuovamente a una replica secondaria che supporta il tipo di accesso alla connessione richiesto dal client. Per garantire un'esperienza client senza problemi dopo un failover, è importante per configurare l'accesso alla connessione sia per i ruoli secondari, sia per quelli primari di ogni replica di disponibilità.  
  
> [!NOTE]  
>  Per informazioni sul listener del gruppo di disponibilità che gestisce le richieste di connessione del client, vedere [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
 **Contenuto dell'argomento:**  
  
-   [Tipi di accesso alla connessione supportati dal ruolo secondario](#ConnectAccessForSecondary)  
  
-   [Tipi di accesso alla connessione supportati dal ruolo primario](#ConnectAccessForPrimary)  
  
-   [Effetti della configurazione dell'accesso alla connessione sulla connettività client](#HowConnectionAccessAffectsConnectivity)  
  
-   [Attività correlate](#RelatedTasks)  
  
-   [Contenuto correlato](#RelatedContent)  
  
##  <a name="ConnectAccessForSecondary"></a> Tipi di accesso alla connessione supportati dal ruolo secondario  
 Il ruolo secondario supporta tre alternative per le connessioni client, indicate di seguito:  
  
 Nessuna connessione  
 Non sono consentite connessioni utente. I database secondari non sono disponibili per l'accesso in lettura. Si tratta del comportamento predefinito nel ruolo secondario.  
  
 Solo connessioni con finalità di lettura  
 I database secondari sono disponibili solo per le connessioni per il quale il `Application Intent` proprietà di connessione è impostata su `ReadOnly` (*connessioni con finalità di lettura*).  
  
 Per informazioni su questa proprietà di connessione, vedere [Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
 Consentire qualsiasi connessione di sola lettura  
 I database secondari sono tutti disponibili per le connessioni con accesso in lettura. Questa opzione consente la connessione di client di versioni precedenti.  
  
 Per altre informazioni, vedere [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
##  <a name="ConnectAccessForPrimary"></a> Tipi di accesso alla connessione supportati dal ruolo primario  
 Il ruolo primario supporta due alternative per le connessioni client, indicate di seguito:  
  
 Tutte le connessioni sono consentite  
 Sono consentite sia le connessioni di lettura e scrittura sia le connessioni in sola lettura ai database primari. Si tratta del comportamento predefinito per il ruolo primario.  
  
 Consentire solo le connessioni in lettura/scrittura  
 Quando la `Application Intent` proprietà di connessione è impostata su **ReadWrite** o non è impostata, la connessione è consentita. Le connessioni per cui il `Application Intent` parola chiave di stringa di connessione è impostata su `ReadOnly` non sono consentiti. Se si consentono solo le connessioni in lettura/scrittura, è possibile impedire la connessione, per errore, di un carico di lavoro con finalità di lettura alla replica primaria da parte dei clienti.  
  
 Per informazioni su questa proprietà di connessione, vedere [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Per altre informazioni, vedere [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md).  
  
##  <a name="HowConnectionAccessAffectsConnectivity"></a> Effetti della configurazione dell'accesso alla connessione sulla connettività client  
 Le impostazioni dell'accesso alla connessione di una replica determinano l'esito positivo o negativo di un tentativo di connessione. Nella tabella seguente viene riepilogato l'esito positivo o negativo di un tentativo di connessione per ciascuna impostazione di accesso alla connessione.  
  
|Ruolo di replica|Accesso alla connessione supportato sulla replica|Finalità di connessione|Risultato tentativo di connessione|  
|------------------|--------------------------------------------|-----------------------|--------------------------------|  
|Secondari|All|Finalità di lettura, lettura e scrittura o nessuna finalità di connessione specificata|Riuscito|  
|Secondari|Nessuno (comportamento predefinito nel ruolo secondario).|Finalità di lettura, lettura e scrittura o nessuna finalità di connessione specificata|Failure|  
|Secondari|Solo finalità di lettura|Con finalità di lettura|Riuscito|  
|Secondari|Solo finalità di lettura|Finalità di lettura e scrittura o nessuna finalità di connessione specificata|Failure|  
|Primario|Tutto (comportamento predefinito del ruolo primario).|Sola lettura, lettura e scrittura o nessuna finalità di connessione specificata|Riuscito|  
|Primario|Lettura/scrittura|Solo finalità di lettura|Failure|  
|Primario|Lettura/scrittura|Finalità di lettura e scrittura o nessuna finalità di connessione specificata|Riuscito|  
  
 Per informazioni sulla configurazione di un gruppo di disponibilità in modo che accetti le connessioni dei client alle proprie repliche, vedere [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
### <a name="example-connection-access-configuration"></a>Esempio di configurazione dell'accesso alla connessione  
 A seconda della modalità di configurazione delle diverse repliche di disponibilità per l'accesso alla connessione, è possibile che il supporto per le connessioni client cambi dopo il failover di un gruppo di disponibilità. Ad esempio, si consideri un gruppo di disponibilità per il quale la creazione di report viene eseguita nelle repliche secondarie con commit asincrono remote. Per tutte le applicazioni di sola lettura per i database in questo gruppo di disponibilità la proprietà di connessione `Application Intent` è impostata su `ReadOnly`, in modo che tutte le connessioni in sola lettura abbiano finalità di lettura.  
  
 Questo gruppo di disponibilità di esempio dispone di due repliche con commit sincrono al centro del calcolo principale e due repliche con commit asincrono a un sito satellite. Per il ruolo primario, tutte le repliche vengono configurate per l'accesso di lettura/scrittura che impedisce le connessioni con finalità di lettura alla replica primaria in tutte le situazioni. Nel ruolo secondario con commit sincrono viene utilizzata la configurazione dell'accesso alla connessione predefinita ("nessuno") tramite cui vengono impedite tutte le connessioni client nel ruolo secondario.  Al contrario, le repliche con commit asincrono sono configurate per consentire le connessioni con finalità di lettura nel ruolo secondario. Nella tabella seguente viene riepilogata questa configurazione di esempio:  
  
|Replica|Modalità di commit|Ruolo iniziale|Accesso alla connessione per il ruolo secondario|Accesso alla connessione per il ruolo primario|  
|-------------|-----------------|------------------|------------------------------------------|----------------------------------------|  
|Replica1|Sincrona|Primario|None|Lettura/scrittura|  
|Replica2|Sincrona|Secondari|None|Lettura/scrittura|  
|Replica3|Asincrona|Secondari|Solo con finalità di lettura|Lettura/scrittura|  
|Replica4|Asincrono|Secondari|Solo finalità di lettura|Lettura/scrittura|  
  
 In genere, in questo scenario di esempio, i failover si verificano solo tra le repliche con commit sincrono e immediatamente dopo il failover, le applicazioni con finalità di lettura sono in grado di riconnettersi a una delle repliche secondarie con commit asincrono. Tuttavia, in caso di emergenza nel centro di elaborazione principale vengono perse entrambe le repliche con commit sincrono. L'amministratore del database del sito satellite esegue un failover manuale forzato a una replica secondaria con commit asincrono. I database secondari nella replica secondaria rimanente vengono sospesi dal failover forzato e diventano pertanto non disponibili per i carichi di lavoro di sola lettura. La nuova replica primaria, configurata per le connessioni in lettura/scrittura, evita che il carico di lavoro con finalità di lettura entri in competizione con il carico di lavoro di lettura/scrittura. Ciò significa che finché l'amministratore del database non riprende i database secondari nella replica del secondaria rimanente con commit asincrono, i client con finalità di lettura non saranno in grado di connettersi ad alcuna replica di disponibilità.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Monitorare Gruppi di disponibilità &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
-   [Visualizzazione delle proprietà della replica di disponibilità &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [Utilizzare la finestra di dialogo Nuovo gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [Microsoft SQL Server AlwaysOn Solutions Guide for High Availability and Disaster Recovery](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server AlwaysOn Team Blog: Il Team Blog ufficiale di SQL Server AlwaysOn](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)   
 [Statistiche](../../../relational-databases/statistics/statistics.md)  
  
  
