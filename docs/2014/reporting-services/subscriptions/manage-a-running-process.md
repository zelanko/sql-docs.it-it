---
title: Gestire un processo in esecuzione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report processing [Reporting Services], status information
- jobs [Reporting Services]
- viewing jobs
- canceling jobs
- user jobs [Reporting Services]
- system jobs [Reporting Services]
- report processing [Reporting Services], managing running processes
- processes [Reporting Services]
- scanning processes [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services]
- canceling subscriptions
- report servers [Reporting Services], jobs
- data-driven subscriptions
- displaying jobs
- subscriptions [Reporting Services], running processes
ms.assetid: 473e574e-f1ff-4ef9-bda6-7028b357ac42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f0c465a50547d8ca45947dc5db5c56221a8a4538
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100814"
---
# <a name="manage-a-running-process"></a>Manage a Running Process
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consente di monitorare lo stato dei processi in esecuzione nel server di report. Tramite il server di report viene effettuata un'analisi a intervalli regolari dei processi in corso e vengono scritte informazioni sullo stato nel database del server di report o nei database dell'applicazione di servizio per la modalità SharePoint. Un processo è considerato in corso se è in esecuzione una delle operazioni seguenti, ovvero esecuzione di query su un server di database locale o remoto, elaborazione di report e rendering di report.  
  
 È possibile gestire sia i *processi utente* sia i *processi di sistema*.  
  
-   I processi utente vengono avviati da un singolo utente o da una sottoscrizione. Includono l'esecuzione di un report su richiesta, la richiesta di uno snapshot della cronologia del report, la creazione manuale di uno snapshot del report e l'elaborazione di una sottoscrizione standard.  
  
-   I processi di sistema vengono avviati dal server di report. Includono snapshot dell'esecuzione di report pianificati, snapshot della cronologia dei report pianificati e sottoscrizioni guidate dai dati.  
  
 L'utilizzo delle risorse e il tempo di elaborazione del report variano significativamente a seconda del report, della complessità della query, della quantità di dati e del formato di rendering specificato per il report. I report con query semplici su un'origine dei dati locale vengono spesso completati in millisecondi e non richiedono mai operazioni di gestione o di ottimizzazione. Un report di grandi dimensioni per il quale viene eseguito il rendering nel formato PDF o Excel può richiedere, al contrario, un tempo di elaborazione elevato a seconda delle risorse hardware, delle opzioni di recapito e dall'eventuale esecuzione di altri processi simultaneamente. Su un server di report la maggior parte dei processi con esecuzione prolungata riguarda le operazioni di rendering dei report e i processi in attesa di conclusione dell'elaborazione di query. Può talvolta essere necessario annullare l'elaborazione di un report per mettere un computer in modalità offline o per arrestare un processo in esecuzione il cui completamento richiede troppo tempo.  
  
 È possibile annullare i processi seguenti:  
  
-   Elaborazione di report su richiesta.  
  
-   Elaborazione di report pianificati.  
  
-   Sottoscrizioni standard appartenenti a utenti singoli.  
  
 L'annullamento di un processo comporta l'annullamento solo dei processi in esecuzione nel server di report. Poiché il server di report non gestisce elaborazione di dati su altri computer, è necessario annullare manualmente i processi di query che rimangono di conseguenza isolati su altri sistemi. Per chiudere automaticamente le query con esecuzione eccessivamente prolungata, è possibile specificare valori di timeout delle query. Per altre informazioni, vedere [Impostazione dei valori di timeout per l'elaborazione di report e di set di dati condivisi &#40;SSRS&#41;](../report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md). Per ulteriori informazioni sulla sospensione temporanea di un report, vedere [sospendere l'elaborazione di report e sottoscrizioni](disable-or-pause-report-and-subscription-processing.md).  
  
> [!NOTE]  
>  Per annullare un processo, in rare circostanze potrebbe essere necessario riavviare il server. Per la modalità SharePoint, potrebbe essere necessario riavviare il pool di applicazioni in cui viene ospitata l'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Avviare e arrestare il servizio del server di report](../report-server/start-and-stop-the-report-server-service.md).  
  
 Contenuto dell'argomento:  
  
-   [Visualizzare e annullare i processi (modalità nativa)](#bkmk_native)  
  
-   [Visualizzare e annullare i processi (modalità SharePoint)](#bkmk_sharepoint)  
  
-   [Gestione di processi a livello di programmazione](#bkmk_programmatically)  
  
##  <a name="view-and-cancel-jobs-native-mode"></a><a name="bkmk_native"></a> Visualizzare e annullare i processi (modalità nativa)  
 È possibile usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per visualizzare o annullare un processo in esecuzione nel server di report. È necessario aggiornare la pagina per recuperare un elenco di processi attualmente in esecuzione oppure per ottenere stato del processo aggiornato dal database del server di report. Quando si esegue la connessione a un server di report in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], è possibile aprire una cartella Processi per visualizzare un elenco di report che attualmente in esecuzione nel computer server di report. Le informazioni sullo stato per ogni processo vengono visualizzate nella pagina Proprietà processo. Per visualizzare informazioni sullo stato di tutti i processi, aprire la finestra di dialogo Annulla processi server di report.  
  
 È possibile usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per visualizzare o annullare un processo in esecuzione nel server di report. È necessario aggiornare la pagina per recuperare un elenco di processi attualmente in esecuzione oppure per ottenere stato del processo aggiornato dal database del server di report. Quando si esegue la connessione a un server di report in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], è possibile aprire una cartella Processi per visualizzare un elenco di report che attualmente in esecuzione nel computer server di report. Le informazioni sullo stato per ogni processo vengono visualizzate nella pagina Proprietà processo. Per visualizzare informazioni sullo stato di tutti i processi, aprire la finestra di dialogo Annulla processi server di report.  
  
 Non è possibile usare [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] per elencare o annullare la generazione o l'elaborazione di modelli o sottoscrizioni guidate dai dati. In Reporting Services non è possibile annullare la generazione o l'elaborazione di modelli. Per annullare sottoscrizioni guidate dai dati, è possibile tuttavia utilizzare le istruzioni fornite in questo argomento.  
  
### <a name="how-to-cancel-report-processing-or-subscription"></a>Annullamento di un'elaborazione del report o di una sottoscrizione  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]connettersi al server di report. Per istruzioni, vedere [Eseguire la connessione a un server di report in Management Studio](../tools/connect-to-a-report-server-in-management-studio.md).  
  
2.  Aprire la cartella **Processi** .  
  
3.  Fare clic con il pulsante destro del mouse sul report, quindi scegliere **Annulla processi**.  
  
### <a name="how-to-cancel-a-data-driven-subscription"></a>Annullamento di una sottoscrizione guidata dai dati  
  
1.  Aprire il file RSReportServer.config in un editor di testo.  
  
2.  Individuare `IsNotificationService`.  
  
3.  Impostarlo su `False`.  
  
4.  Salvare il file.  
  
5.  In Gestione report eliminare la sottoscrizione guidata dai dati dalla scheda Sottoscrizioni del report o da **Sottoscrizioni personali**.  
  
6.  Dopo avere eliminato la sottoscrizione, nel file RSReportServer.config individuare `IsNotificationService` e impostarlo su `True`.  
  
7.  Salvare il file.  
  
### <a name="configuring-frequency-settings-for-retrieving-job-status"></a>Configurazione delle impostazioni di frequenza per il recupero dello stato di un processo  
 Un processo in esecuzione viene archiviato nel database temporaneo del server di report. Per controllare la frequenza con la quale il server di report esegue l'analisi dei processi in corso e l'intervallo trascorso il quale lo stato di un processo cambia da nuovo a in esecuzione, è possibile modificare le impostazioni di configurazione nel file RSReportServer.config. L'impostazione `RunningRequestsDbCycle` consente di specificare la frequenza con la quale il server di report esegue l'analisi dei processi in esecuzione. Per impostazione predefinita, le informazioni sullo stato vengono registrate ogni 60 secondi. L'impostazione `RunningRequestsAge` consente di specificare l'intervallo dopo il quale un processo passa da nuovo a in esecuzione.  
  
##  <a name="view-and-cancel-jobs-sharepoint-mode"></a><a name="bkmk_sharepoint"></a> Visualizzare e annullare i processi (modalità SharePoint)  
 La gestione di processi in una distribuzione della modalità SharePoint viene completata utilizzando Amministrazione centrale SharePoint, per ogni applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
#### <a name="to-manage-jobs-in-sharepoint-mode"></a>Per gestire i processi in modalità SharePoint  
  
1.  In Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Trovare e fare clic sul nome dell'applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per aprire la pagina di gestione dell'applicazione.  
  
3.  Fare clic su **Gestione di processi**.  
  
4.  Fare clic su **ID processo** per visualizzare i dettagli del processo.  
  
5.  In alternativa, fare clic sulla casella per il processo e scegliere **Elimina** per annullare il processo. L'eliminazione del processo non comporta l'eliminazione della sottoscrizione.  
  
##  <a name="managing-jobs-programmatically"></a><a name="bkmk_programmatically"></a> Gestione di processi a livello di programmazione  
 I processi possono essere gestiti a livello di programmazione o mediante l'utilizzo di uno script. Per altre informazioni, vedere <xref:ReportService2010.ReportingService2010.ListJobs%2A>e <xref:ReportService2010.ReportingService2010.CancelJob%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [Annulla processi server di report &#40;Management Studio&#41;](../tools/cancel-report-server-jobs-management-studio.md)   
 [Proprietà processo &#40;Management Studio&#41;](../tools/job-properties-management-studio.md)   
 [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [File di configurazione RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Monitoraggio delle prestazioni del server di report](../report-server/monitoring-report-server-performance.md)  
  
  
