---
title: Pianificazioni | Microsoft Docs
ms.date: 07/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- schedules [Reporting Services]
- schedules [Reporting Services], about schedules
- published reports [Reporting Services], schedules
- reports [Reporting Services], scheduling
- subscriptions [Reporting Services], scheduling
- automatic report processing
ms.assetid: ecccd16b-eba9-4e95-b55d-f15c621e003f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e73ce189b38f3610468993999df172d778f30026
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578101"
---
# <a name="schedules"></a>Pianificazioni
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] offre **pianificazioni condivise** e **pianificazioni in base al report** che consentono di controllare l'elaborazione e la distribuzione di report. La differenza tra i due tipi di pianificazione consiste nella modalità con cui vengono definite, archiviate e gestite. La costruzione interna dei due tipi di pianificazione è identica. Tutte le pianificazioni specificano un tipo di occorrenza: mensile, settimanale o giornaliera. All'interno del tipo di occorrenza, è possibile impostare gli intervalli relativi alla frequenza con cui un evento deve verificarsi. Il tipo di criterio di occorrenza e il modo in cui tali criteri vengono specificati sono identici sia che venga creata una pianificazione condivisa o una pianificazione in base al report.
  
  -   Le pianificazioni condivise vengono create come elementi distinti. Dopo che sono state create, è possibile farvi riferimento nel contesto della definizione di una sottoscrizione o di un'altra operazione pianificata.  
  
-   Le pianificazioni in base al report vengono create quando si definisce una sottoscrizione o si impostano le proprietà di esecuzione dei report. L'impostazione delle informazioni di pianificazione fa parte del processo di definizione di una sottoscrizione o di impostazione di proprietà. Per definire una pianificazione in base al report, è necessario aprire il report o la sottoscrizione che la utilizzerà.  
  
 In una pianificazione condivisa sono contenute le informazioni sulla pianificazione e sull'occorrenza che possono essere utilizzate da qualsiasi numero di sottoscrizioni e report pubblicati in esecuzione in un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se il numero di report e sottoscrizioni in esecuzione contemporaneamente è elevato, è possibile creare una pianificazione condivisa per tali processi. Se si desidera modificare successivamente il criterio di occorrenza o la data di fine, è possibile apportare la modifica in un unico punto.  
  
 Le pianificazioni condivise sono più semplici da gestire e consentono una maggiore flessibilità nella gestione di operazioni pianificate. È possibile ad esempio sospendere e quindi riprendere una pianificazione condivisa. Inoltre, se si rileva che sono in esecuzione contemporaneamente troppe operazioni pianificate, sarà possibile creare più pianificazioni condivise per eseguirle in orari diversi, quindi modificare le informazioni sulla pianificazione fino a quando il carico di elaborazione non risulterà distribuito in modo equo nel server di report.  
  
  
##  <a name="bkmk_whatyoucando"></a> Operazioni possibili con le pianificazioni  
 È possibile usare il portale Web di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] nelle pagine della modalità nativa e di amministrazione del sito SharePoint in modalità SharePoint per creare e gestire le pianificazioni. È possibile effettuare le operazioni seguenti:  
  
-   Pianificare il recapito di un report in una sottoscrizione standard o guidata dai dati.  
  
-   Pianificare la cronologia dei report in modo che vengano aggiunti nuovi snapshot alla cronologia dei report a intervalli regolari.  
  
-   Pianificare le operazioni di aggiornamento dei dati di uno snapshot di un report.  
  
-   Pianificare le operazioni di aggiornamento dei dati di un set di dati condiviso  
  
-   Pianificare un orario per la scadenza di un set di dati condiviso o di un report memorizzato nella cache, in modo che possa essere successivamente aggiornato.  
  
 Se si desidera utilizzare le stesse informazioni di pianificazione per più report o sottoscrizioni, è possibile creare una pianificazione condivisa. Le pianificazioni condivise vengono definite separatamente e quindi vi viene fatto riferimento nei report, nei set di dati condivisi e nelle sottoscrizioni per i quali sono necessarie informazioni di pianificazione.  
  
 Quando si crea una pianificazione, le informazioni della pianificazione vengono salvate dal report nel database del server di report oppure, per la modalità SharePoint, nel database dell'applicazione di servizio. Il server di report crea inoltre un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent che verrà utilizzato per avviare la pianificazione. L'elaborazione della pianificazione è basata sull'ora locale del server di report contenente la pianificazione. Il formato dell'ora dipende dal sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Per informazioni dettagliate sulla creazione e gestione delle pianificazioni, vedere [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md).  
  
> [!NOTE]  
>  Le operazioni sulle pianificazioni sono disponibili solo in alcune edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Edizioni e funzionalità supportate di SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md).  
  
##  <a name="bkmk_compare"></a> Pianificazioni condivise e pianificazioni in base al report  
 Dai due tipi di pianificazioni viene generato lo stesso output:  
  
-   Le**pianificazioni condivise** sono elementi portabili e multifunzione in cui sono contenute informazioni di pianificazione pronte per l'utilizzo. Dato che le pianificazioni condivise sono elementi a livello di sistema, per crearle sono necessarie autorizzazioni a livello di sistema. Per questo motivo, le pianificazioni condivise disponibili nel server di report vengono in genere create da un amministratore del server di report o da un utente con ruolo Gestione contenuto. Le pianificazioni condivise vengono archiviate e gestite nel server di report tramite le impostazioni del portale Web o del sito di SharePoint.  
  
     A differenza delle pianificazioni specifiche che vengono definite tramite le proprietà del report, del set di dati o delle sottoscrizioni, le pianificazioni condivise sono più semplici da gestire e mantenere per i motivi seguenti:  
  
    -   Le pianificazioni condivise possono essere gestite da una posizione centrale, semplificando il confronto delle proprietà della pianificazione e regolando frequenza e criteri di occorrenza se le operazioni pianificate vengono eseguiti in tempi troppo vicini o in conflitto con altri processi nel server.  
  
    -   Si adattano rapidamente alle modifiche nell'ambiente del calcolo. Si supponga ad esempio di disporre di un set di report in esecuzione alle 4.00. dopo che un data warehouse è stato aggiornato. Se l'operazione di aggiornamento dei dati viene ripianificata o posticipata, è possibile adattarsi a tale modifica aggiornando le informazioni sulla pianificazione in un'unica pianificazione condivisa.  
  
    -   Se si utilizzano solo pianificazioni condivise, il momento in cui vengono le operazioni pianificate vengono eseguite è noto con precisione. In questo modo è più semplice anticipare e adattare carichi del server prima si verifichino problemi di prestazioni. Se ad esempio si decide di pianificare operazioni di backup del computer a un'ora specifica, è possibile impostare l'esecuzione delle pianificazioni condivise in ore diverse.  
  
-   Le**pianificazioni specifiche dei report** sono definite nel contesto di un singolo report, una sottoscrizione o un'operazione di esecuzione di un report per determinare la scadenza della cache o gli aggiornamenti degli snapshot. Queste pianificazioni vengono create direttamente durante la definizione di una sottoscrizione o l'impostazione delle proprietà di esecuzione di un report. È possibile creare una pianificazione in base al report se nessuna pianificazione condivisa offre la frequenza o il criterio di occorrenza desiderato. Per evitare l'esecuzione di un report, è necessario modificare manualmente una pianificazione in base al report. Le pianificazioni in base al report possono essere create dai singoli utenti.  
  
##  <a name="bkmk_configuredatasources"></a> Configurare le origini dati  
 Prima di poter pianificare l'elaborazione dei dati o delle sottoscrizioni per un report, è necessario configurare l'origine dati del report in modo da utilizzare le credenziali archiviate o l'account per l'elaborazione automatica dei report. Se si utilizzano credenziali archiviate, sarà possibile archiviare un unico set di credenziali, che verrà utilizzato da tutti gli utenti che eseguono il report. Tali credenziali possono essere costituite da un account utente di Windows o da un account utente del database.  
  
 L'account per l'elaborazione automatica dei report è uno speciale account configurato sul server di report, che viene utilizzato dal server di report per la connessione ai computer remoti quando un'operazione pianificata richiede il recupero o l'elaborazione di un file esterno. Se configurato, tale account può essere utilizzato per la connessione a origini dati esterne che forniscono dati a un report.  
  
 Per specificare credenziali archiviate o l'account per l'elaborazione automatica dei report, modificare le proprietà del report relative alle origini dati. Se invece nel report viene utilizzata un'origine dati condivisa, modificare quest'ultima.  
  
##  <a name="bkmk_credentials"></a> Archiviare le credenziali e gli account di elaborazione  
 Il tipo di operazioni di gestione delle pianificazioni consentite a un determinato utente dipende dalle attività che fanno parte dell'assegnazione di ruolo di tale utente. Se si utilizzano ruoli predefiniti, gli utenti con ruolo Gestione contenuto e gli amministratori di sistema possono creare e gestire qualsiasi pianificazione. Se si utilizzano assegnazioni di ruolo personalizzate, tali assegnazioni devono includere attività che supportano le operazioni pianificate.  
  
|Per|Includere questa attività|Ruoli predefiniti della modalità nativa|Gruppi della modalità SharePoint|  
|----------------|-----------------------|----------------------------------|----------------------------|  
|Creare, modificare o eliminare pianificazioni condivise|Gestione di pianificazioni condivise|Amministratore sistema|Proprietari|  
|Selezionare pianificazioni condivise|Visualizzazione di pianificazioni condivise|Utente sistema|Membri|  
|Creare, modificare o eliminare pianificazioni in base al report in una sottoscrizione definita dall'utente|Gestione di sottoscrizioni individuali|Browser, Generatore report, Report personali, Gestione contenuto|Visitatori, Membri|  
|Creare, modificare o eliminare pianificazioni in base al report per tutte le altre operazioni pianificate|Gestione della cronologia dei report, Gestione di tutte le sottoscrizioni e Gestione di report|Gestione contenuto|Proprietari|  
  
 Per altre informazioni sulla sicurezza in modalità nativa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Ruoli predefiniti](../../reporting-services/security/role-definitions-predefined-roles.md), [Concessione di autorizzazioni in un server di report in modalità nativa](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md) e [Attività e autorizzazioni](../../reporting-services/security/tasks-and-permissions.md). Per la modalità SharePoint, vedere [Confrontare ruoli e attività di Reporting Services con autorizzazioni e gruppi di SharePoint](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
  
##  <a name="bkmk_how_scheduling_works"></a> Funzionamento di Elaborazione pianificazione e recapito  
 Elaborazione pianificazione e recapito offre le funzionalità seguenti:  
  
-   Gestisce una coda di eventi e notifiche nel database del server di report. In una distribuzione con scalabilità orizzontale la coda viene condivisa tra tutti i server di report che appartengono alla distribuzione.  
  
-   Chiama Elaborazione report per eseguire report, elaborare sottoscrizioni o cancellare un report memorizzato nella cache. Tutta l'elaborazione di report che si verifica come conseguenza di un evento pianificato viene eseguita come processo in background. Nella modalità SharePoint i processi timer vengono utilizzati per.  
  
-   Chiama l'estensione per il recapito specificata in una sottoscrizione in modo da consentire il recapito del report.  
  
 Altri aspetti di un'operazione di pianificazione e recapito vengono gestiti da altri componenti e servizi compatibili con Elaborazione pianificazione e recapito. In particolare, Elaborazione pianificazione e recapito viene eseguito nel servizio del server di report e utilizza SQL Server Agent come timer per generare eventi pianificati. Nella descrizione dettagliata seguente viene illustrato il funzionamento delle operazioni pianificate in una distribuzione di Reporting Services:  
  
1.  Un'operazione pianificata viene definita quando un utente crea una pianificazione. Con la pianificazione vengono definite una data e un'ora che verranno utilizzate per l'attivazione di una sottoscrizione per il recapito di report, l'aggiornamento di uno snapshot o la scadenza di una cache.  
  
2.  Il server di report salva le informazioni relative alla pianificazione nel database del server di report.  
  
3.  Il server di report crea un processo corrispondente in SQL Server Agent che include le informazioni di pianificazione specificate. I processi vengono creati tramite una stored procedure utilizzando la connessione aperta esistente al database del server di report.  
  
4.  SQL Server Agent esegue il processo nella data e all'ora specificate nella pianificazione. Il processo crea un evento che viene aggiunto a una coda gestita da Reporting Services.  
  
5.  Tale evento causa l'esecuzione di un processo di report o sottoscrizione. Gli eventi vengono elaborati quando vengono rilevati nella coda e il report viene elaborato o recapitato di conseguenza.  
  
     Prima dell'elaborazione degli eventi, Elaborazione pianificazione e recapito esegue un passaggio di autenticazione per verificare che il proprietario della sottoscrizione disponga delle autorizzazioni per visualizzare il report.  
  
 Reporting Services gestisce una coda degli eventi per tutte le operazioni pianificate ed esegue il polling della coda a intervalli regolari per verificare la disponibilità di nuovi eventi. Per impostazione predefinita, l'analisi della coda viene eseguita a intervalli di 10 secondi. Per cambiare l'intervallo, è possibile modificare le impostazioni di configurazione **PollingInterval**, **IsNotificationService**e **IsEventService** nel file RSReportServer.config. In modalità SharePoint viene utilizzato anche RSreporserver.config per queste impostazioni e i valori vengono applicati a tutte le applicazioni di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [File di configurazione RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
##  <a name="bkmk_serverdependencies"></a> Dipendenze del server  
 Per il funzionamento di Elaborazione pianificazione e recapito è necessario che vengano avviati il servizio del server di report e SQL Server Agent. La funzionalità Elaborazione pianificazione e recapito deve essere abilitata mediante la proprietà **ScheduleEventsAndReportDeliveryEnabled** del facet **Configurazione superficie di attacco per Reporting Services** della gestione basata su criteri. Affinché vengano eseguite le operazioni pianificate, è necessario che SQL Server Agent e il servizio del server di report siano in esecuzione.  
  
> [!NOTE]  
>  È possibile utilizzare il facet **Configurazione superficie di attacco per Reporting Services** per arrestare le operazioni pianificate temporaneamente o definitivamente. Anche se è possibile creare e distribuire estensioni personalizzate per il recapito, Elaborazione pianificazione e recapito non è estendibile né è possibile modificare il modo in cui gestisce eventi e notifiche. Per altre informazioni sulla disabilitazione delle funzionalità, vedere la sezione relativa al **recapito e agli eventi pianificati** di [Turn Reporting Services Features On or Off](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md).  
  
###  <a name="bkmk_stoppingagent"></a> Effetti dell'arresto di SQL Server Agent  
 Per l'elaborazione pianificata di report viene utilizzato SQL Server Agent per impostazione predefinita. Se si arresta il servizio, non verranno aggiunte nuove richieste di elaborazione alla coda a meno di aggiungerle a livello di programmazione usando il metodo <xref:ReportService2010.ReportingService2010.FireEvent%2A> . Quando si riavvia il servizio, i processi che creano le richieste di elaborazione di report vengono ripresi. Il server di report non tenterà di ricreare i processi di elaborazione di report riferiti al periodo in cui SQL Server Agent era offline. Se si arresta SQL Server Agent per una settimana, tutte le operazioni pianificate per quella settimana andranno perse.  
  
> [!NOTE]  
>  La funzionalità assicurata da SQL Server Agent a Reporting Services può essere sostituita da codice personalizzato che usa il metodo <xref:ReportService2010.ReportingService2010.FireEvent%2A> per aggiungere eventi pianificati alla coda.  
  
###  <a name="bkmk_stoppingservice"></a> Effetti dell'arresto del servizio del server di report  
 Se si arresta il servizio del server di report, SQL Server Agent continuerà ad aggiungere richieste di elaborazione di report alla coda. Le informazioni sullo stato di SQL Server Agent indicano che il processo è stato completato, ma poiché il servizio del server di report è arrestato, non viene effettivamente eseguita alcuna operazione di elaborazione di report. Le richieste continueranno ad accumularsi nella coda finché il servizio non verrà riavviato. Dopo il riavvio del servizio del server di report tutte le richieste di elaborazione di report presenti nella coda verranno elaborate nell'ordine in cui sono state inserite.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare, modificare ed eliminare snapshot nella cronologia dei report](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [Memorizzazione dei report nella cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)   
 [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)  
  
  
