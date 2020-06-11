---
title: Raccolta dati di utilizzo di PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9057cb89-fb17-466e-a1ce-192c8ca20692
author: minewiskan
ms.author: owend
ms.openlocfilehash: c5d28ef26a24f65be180b73620cf3f665db24d3c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547813"
---
# <a name="powerpivot-usage-data-collection"></a>Raccolta dati di utilizzo di PowerPivot
  La raccolta dati di utilizzo è una funzionalità di SharePoint a livello di farm. In PowerPivot per SharePoint questo sistema viene utilizzato ed esteso per fornire i report nel dashboard di gestione PowerPivot in cui viene mostrato l'utilizzo dei servizi e dei dati PowerPivot. A seconda dell'installazione di SharePoint, la raccolta dati di utilizzo potrebbe essere disabilitata per la farm. È necessario che un amministratore della farm abiliti la registrazione dell'utilizzo per creare i dati di utilizzo che vengono visualizzati nel dashboard di gestione PowerPivot. Per ulteriori informazioni su come abilitare e configurare la raccolta dati di utilizzo per gli eventi PowerPivot, vedere [configurare la raccolta dati di utilizzo per &#40;PowerPivot per SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 Per informazioni sui dati di utilizzo nel dashboard di gestione PowerPivot, vedere [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
 **Contenuto dell'argomento:**  
  
 [Raccolta dei dati di utilizzo e architettura dei report](#usagearch)  
  
 [Origini dei dati di utilizzo](#sources)  
  
 [Servizi e processi timer](#servicesjobs)  
  
 [Creazione di report sui dati di utilizzo](#reporting)  
  
##  <a name="usage-data-collection-and-reporting-architecture"></a><a name="usagearch"></a> Raccolta dati di utilizzo e architettura dei report  
 I dati sull'utilizzo di PowerPivot vengono raccolti, archiviati e gestiti attraverso una combinazione di funzionalità dell'infrastruttura di SharePoint e dei componenti server di PowerPivot. L'infrastruttura di SharePoint fornisce un servizio sull'utilizzo centralizzato e processi timer predefiniti. PowerPivot per SharePoint offre un'archiviazione a lungo termine dei dati di utilizzo di PowerPivot e report visualizzabili in Amministrazione centrale.  
  
 Nel sistema di raccolta dati sull'utilizzo, le informazioni sugli eventi accedono al sistema di raccolta dati sull'utilizzo nel server applicazioni o nel computer front-end Web. I dati sull'utilizzo vengono spostati nel sistema in risposta a processi timer che causano lo spostamento dei dati da file di dati temporanei nel server fisico all'archiviazione persistente in un server di database. Nel diagramma seguente vengono illustrati i componenti e i processi che causano lo spostamento dei dati sull'utilizzo attraverso il sistema di raccolta dati e di creazione report.  
  
 **Nota:** verificare che la raccolta dati di utilizzo sia abilitata. A tal fine, passare a **Monitoraggio** in Amministrazione centrale SharePoint. Per altre informazioni, vedere [configurare la raccolta dati di utilizzo per &#40;PowerPivot per SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 ![Componenti e processi di raccolta dei dati di utilizzo](../media/gmni-usagedata.gif "Componenti e processi di raccolta dei dati di utilizzo")  
  
|Fase|Descrizione|  
|-----------|-----------------|  
|1|La raccolta dati di utilizzo viene attivata dagli eventi generati dai componenti di PowerPivot e dai provider di dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in distribuzioni di SharePoint. Gli eventi configurabili che è possibile abilitare o disabilitare includono richieste di connessione, richieste di caricamento e scaricamento ed eventi relativi ai tempi di risposta alle query monitorati dal servizio PowerPivot nel server applicazioni. Altri eventi gestiti unicamente dal server e che non è possibile disabilitare. Sono inclusi gli eventi relativi all'integrità del server e all'aggiornamento dati.<br /><br /> Inizialmente, i dati di utilizzo vengono raccolti e archiviati in file di log locali mediante le funzionalità di raccolta dati del sistema SharePoint. Questi file e i relativi percorsi fanno parte del sistema di raccolta dati di utilizzo standard in SharePoint. Il percorso dei file è lo stesso in ogni server nella farm. Per visualizzare o modificare il percorso della directory di registrazione, passare a **Monitoraggio** in Amministrazione centrale SharePoint, quindi fare clic su **Configura raccolta dati di utilizzo e integrità**.|  
|2|A intervalli pianificati, ogni ora per impostazione predefinita, tramite il processo timer Importazione dati di utilizzo di Microsoft SharePoint Foundation i dati di utilizzo vengono spostati dai file locali al database dell'applicazione di servizio PowerPivot. Se in una farm sono presenti più applicazioni del servizio PowerPivot, ciascuna disporrà di un proprio database. Negli eventi sono incluse informazioni interne mediante le quali viene identificata l'applicazione di servizio PowerPivot tramite cui è stato generato l'evento. Gli identificatori dell'applicazione garantiscono che i dati di utilizzo vengano associati all'applicazione che li ha creati.|  
|3|I dati vengono copiati in un database di report interno disponibile per il dashboard di gestione di PowerPivot in Amministrazione centrale.|  
|4|L'origine dati è una cartella di lavoro di PowerPivot a cui è possibile accedere per creare report personalizzati in Excel. È disponibile un'unica istanza della cartella di lavoro di origine. I report localizzati sono tutti basati sulla stessa cartella di lavoro di origine.|  
|5|I dati di utilizzo vengono presentati in report per applicazioni di servizio PowerPivot per amministratori che gestiscono la disponibilità e le prestazioni del server. Le istanze localizzate delle cartelle di lavoro vengono create per le lingue di SharePoint supportate.<br /><br /> Per ulteriori informazioni, vedere [Report relativi ai dati di utilizzo](#reporting) in questo argomento.|  
  
##  <a name="sources-of-usage-data"></a><a name="sources"></a> Origini dei dati sull'utilizzo  
 Quando la raccolta dati di utilizzo viene abilitata, i dati vengono generati per gli eventi server seguenti.  
  
|Event|Descrizione|Configurabile|  
|-----------|-----------------|------------------|  
|Connessioni|Connessioni server effettuate per conto di un utente che esegue query sui dati PowerPivot in una cartella di lavoro di Excel. Gli eventi connessione identificano l'utente che ha aperto una connessione a una cartella di lavoro di PowerPivot. Nei report, queste informazioni vengono utilizzate per identificare gli utenti più frequenti, le origini dati PowerPivot a cui gli stessi utenti hanno effettuato l'accesso e le tendenze delle connessioni nel tempo.|È possibile abilitare e disabilitare [la configurazione della raccolta dati di utilizzo per &#40;PowerPivot per SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Tempi di risposta alle query|Statistiche di risposta alle query che consentono di suddividere le query in base al tempo necessario per il loro completamento. Le statistiche di risposta alle query indicano il tempo impiegato dal server per rispondere alle richieste di query.|È possibile abilitare e disabilitare [la configurazione della raccolta dati di utilizzo per &#40;PowerPivot per SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Caricamento dati|Operazioni di caricamento dati eseguite dal [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. Gli eventi di caricamento dati consentono di identificare le origini dati utilizzate con maggiore frequenza.|È possibile abilitare e disabilitare [la configurazione della raccolta dati di utilizzo per &#40;PowerPivot per SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Scaricamento dati|Operazioni di scaricamento dati eseguite dalle applicazioni del servizio PowerPivot. Un [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] consente di scaricare le origini dati PowerPivot inattive se non vengono utilizzate o quando la quantità di memoria del server è insufficiente per eseguire i processi di aggiornamento dati.|È possibile abilitare e disabilitare [la configurazione della raccolta dati di utilizzo per &#40;PowerPivot per SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md).|  
|Stato di integrità del server|Operazioni server che consentono di indicare l'integrità del server, misurata in utilizzo della memoria e della CPU. Questi dati sono cronologici. Non forniscono informazioni in tempo reale sul carico di elaborazione corrente nel server.|No. I dati di utilizzo vengono sempre raccolti per questo evento.|  
|Aggiornamento dati|Operazioni di aggiornamento dati avviate dal servizio PowerPivot per gli aggiornamenti dati pianificati. I dati cronologici sull'utilizzo per l'aggiornamento dati vengono raccolti a livello dell'applicazione per i report operativi e vengono riflessi nelle pagine Gestisci aggiornamento dati per le singole cartelle di lavoro.<br /><br /> **Nota:** per distribuzioni di [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] e SharePoint 2013, l'aggiornamento dati è gestito da Excel Services e non dal server Analysis Services.|No. I dati di utilizzo relativi all'aggiornamento dati vengono sempre raccolti se l'aggiornamento dati per l'applicazione del servizio PowerPivot è abilitato.|  
  
##  <a name="services-and-timer-jobs"></a><a name="servicesjobs"></a> Processi timer e servizi  
 Nella tabella seguente vengono descritti gli archivi di raccolta dati e servizi nel sistema di raccolta dati di utilizzo. Per istruzioni su come eseguire l'override delle pianificazioni del processo timer per forzare un aggiornamento dati dello stato di integrità del server e dei dati di utilizzo nei report del dashboard di gestione PowerPivot, vedere [aggiornamento dati PowerPivot con SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md). È possibile visualizzare i processi timer in Amministrazione centrale SharePoint. Passare a **Monitoraggio**, quindi fare clic su **Controlla stato processo**. Fare clic su **Rivedi definizioni processi**.  
  
|Componente|Pianificazione predefinita|Descrizione|  
|---------------|----------------------|-----------------|  
|Servizio Timer di SharePoint (SPTimerV4)||Questo servizio di Windows viene eseguito in modalità locale in ogni computer membro della farm ed elabora tutti i processi timer definiti a livello di farm.|  
|Importazione dati di utilizzo di Microsoft SharePoint Foundation|Ogni 30 minuti in SharePoint 2010. Ogni 5 minuti in SharePoint 2013.|Questo processo timer viene configurato globalmente a livello di farm. I dati di utilizzo vengono spostati dai file di log locali al database di raccolta dati di utilizzo centrale. È possibile eseguire manualmente questo processo timer per forzare un'operazione di importazione dati.|  
|Processo timer di Elaborazione dati di utilizzo di Microsoft SharePoint Foundation|Giornalmente alle 3.00|**( \* )** A partire da SQL Server 2012 PowerPivot per SharePoint, questo processo temporale è supportato per scenari di migrazione o di aggiornamento in cui è ancora possibile includere dati di utilizzo più vecchi nei database di utilizzo di SharePoint. A partire da SQL Server 2012 PowerPivot per SharePoint, il database di utilizzo di SharePoint non viene utilizzato per il flusso di lavoro del dashboard di gestione e la raccolta utilizzo di PowerPivot. Il processo timer può essere eseguito manualmente per spostare tutti i dati correlati a PowerPivot rimanenti nel database di utilizzo di SharePoint nei database dell'applicazione di servizio PowerPivot.<br /><br /> Questo processo timer viene configurato globalmente a livello di farm. Consente di verificare la presenza di dati di utilizzo scaduti nel database di raccolta dati di utilizzo centrale (cioè i record risalenti a più di 30 giorni prima). Per i server PowerPivot della farm, questo processo timer esegue un controllo aggiuntivo per i dati sull'utilizzo di PowerPivot. Quando vengono rilevati dati sull'utilizzo di PowerPivot, il processo timer sposta i dati in un database dell'applicazione di servizio utilizzando un identificatore dell'applicazione per trovare il database corretto.<br /><br /> È possibile eseguire manualmente questo processo timer per forzare un controllo sui dati scaduti o un'importazione dei dati di utilizzo PowerPivot in un database dell'applicazione di servizio PowerPivot.|  
|Processo timer di elaborazione dashboard di gestione PowerPivot|Giornalmente alle 3.00|Questo processo timer aggiorna la cartella di lavoro di PowerPivot interna che fornisce i dati amministrativi al dashboard di gestione PowerPivot. Ottiene le informazioni aggiornate gestite da SharePoint, inclusi i nomi dei server, i nomi utente, i nomi delle applicazioni e i nomi dei file visualizzati nei report del dashboard o nelle web part.|  
  
##  <a name="reporting-on-usage-data"></a><a name="reporting"></a> Report relativi ai dati di utilizzo  
 Per visualizzare i dati di utilizzo nei dati PowerPivot, è possibile visualizzare report predefiniti nel dashboard di gestione PowerPivot. I report predefiniti consolidano i dati di utilizzo recuperati dalle strutture di dati di report nel database dell'applicazione del servizio. Poiché i dati di report sottostanti vengono aggiornati ogni giorno, i report sull'utilizzo predefiniti conterranno le informazioni aggiornate solo dopo che il processo timer di Elaborazione dati di utilizzo di Microsoft SharePoint Foundation copia i dati in un database dell'applicazione del servizio PowerPivot. Tale operazione si verifica una volta al giorno per impostazione predefinita.  
  
 Per ulteriori informazioni su come visualizzare i report, vedere [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Dati di utilizzo e dashboard di gestione PowerPivot](power-pivot-management-dashboard-and-usage-data.md)   
 [Informazioni di riferimento sulle impostazioni di configurazione &#40;PowerPivot per SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Configurare la raccolta dati di utilizzo per &#40;PowerPivot per SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
