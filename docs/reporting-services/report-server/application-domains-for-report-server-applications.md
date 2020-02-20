---
title: Domini applicazione per applicazioni del server di report | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- application domains [Reporting Services]
- recycling application domains
ms.assetid: a455e2e6-8764-493d-a1bc-abe80829f543
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d39f1b9b081d50e5d64a6d5f948255f3a4d6e53b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65574801"
---
# <a name="application-domains-for-report-server-applications"></a>Domini applicazione per applicazioni del server di report
  In [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]il server di report viene implementato come un unico servizio che contiene il servizio Web ReportServer, Gestione report e un'applicazione di elaborazione in background. Ogni applicazione viene eseguita nel proprio dominio all'interno del singolo processo del server di report. Nella maggior parte dei casi, i domini applicazione vengono creati, configurati e gestiti internamente. Tuttavia la conoscenza del modo in cui vengono eseguite le operazioni di riciclo per i domini applicazione del server di report può risultare utile per ottenere prestazioni elevate, per ricercare problemi di memoria o per risolvere interruzioni del servizio.  
  
> [!NOTE]  
>  Se si configura l'accesso a Generatore report in un server di report che utilizza l'autenticazione di base, Generatore report verrà eseguito nel proprio dominio applicazione. Questo dominio applicazione è diverso da altri domini applicazione eseguiti nel processo server. Viene gestito dal Controller servizi e non è soggetto a caratteristiche di gestione della memoria che rimodificano l'allocazione della memoria in risposta a richieste di memoria sul server di report.  
  
 Nell'elenco seguente vengono descritti gli eventi che provocano le operazioni di riciclo del dominio applicazione per applicazioni [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Operazioni di riciclo pianificate eseguite a intervalli predefiniti.  
  
-   Modifiche alla configurazione sul server di report.  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] .  
  
-   Errori di allocazione di memoria.  
  
 Nella tabella seguente viene riepilogato il comportamento del riciclo del dominio applicazione in risposta a questi eventi:  
  
|Event|Descrizione evento|Si applica a|Configurabile|Descrizione dell'operazione di riciclo|  
|-----------|-----------------------|----------------|------------------|-----------------------------------|  
|Operazioni di riciclo pianificate eseguite a intervalli predefiniti|Per impostazione predefinita, i domini applicazione vengono riciclati ogni 12 ore.<br /><br /> Le operazioni di riciclo pianificate vengono in genere utilizzate per applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] che agevolano l'integrità complessiva del processo.|Servizio Web ReportServer<br /><br /> Gestione report<br /><br /> Applicazione di elaborazione in background|Sì. L'impostazione di configurazione**RecycleTime** nel file RSReportServer.config determina l'intervallo di riciclo.<br /><br /> **MaxAppDomainUnloadTime** consente di impostare il tempo di attesa durante il quale è possibile completare l'elaborazione in background.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] .<br /><br /> Per l'applicazione di elaborazione in background, il server di report crea un nuovo dominio applicazione per i nuovi processi avviati in base alle pianificazioni. I processi già in corso possono essere completati nel dominio applicazione corrente entro la scadenza del tempo di attesa.|  
|Modifiche alla configurazione sul server di report|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] i domini applicazione verranno riciclati in risposta alle modifiche apportate al file RSReportServer.config.|Servizio Web ReportServer<br /><br /> Gestione report<br /><br /> Applicazione di elaborazione in background|No.|Non è possibile arrestare le operazioni di riciclo. Tuttavia, le operazioni di riciclo eseguite in risposta alle modifiche alla configurazione vengono gestite in modo analogo alle operazioni di riciclo pianificate. Per le nuove richieste vengono creati nuovi domini applicazione, mentre le richieste e i processi in corso vengono completati nel dominio applicazione corrente.|  
|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] Modifiche alla configurazione|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] Se sono presenti modifiche ai file monitorati, ad esempio machine.config, Web.config e i file di programma di [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] , i domini applicazione verranno riciclati.|Servizio Web ReportServer<br /><br /> Gestione report|No.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] .<br /><br /> Le operazioni di riciclo avviate da [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] non influiscono sul dominio applicazione dell'elaborazione in background.|  
|Utilizzo della memoria ed errori di allocazione di memoria|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Servizio Web ReportServer<br /><br /> Gestione report<br /><br /> Applicazione di elaborazione in background|No.|In condizioni di utilizzo alto della memoria, il server di report non accetterà nuove richieste nel dominio applicazione corrente. Durante il periodo in cui il server rifiuta nuove richieste, si verifica l'errore HTTP 503. Non verrà creato alcun nuovo dominio applicazione fino a quando quello obsoleto non viene scaricato. Questo significa che se si apporta una modifica al file di configurazione in condizioni di utilizzo alto della memoria da parte del server, richieste e processi in corso potrebbero non essere avviati o completati.<br /><br /> Nel caso in cui si verifichi un errore di allocazione di memoria, tutti i domini applicazione vengono riavviati immediatamente. I processi e le richieste in corso vengono eliminati ed è necessario riavviarli manualmente.|  
  
## <a name="planned-and-unplanned-recycle-operations"></a>Operazioni di riciclo pianificate e non pianificate  
 Le operazioni di riciclo vengono pianificate o meno in base alle condizioni che determinano l'operazione:  
  
-   Le operazioni di riciclo pianificate vengono eseguite a intervalli regolari definiti nel file RSReportServer.config. Il valore predefinito è ogni 12 ore. Le operazioni di riciclo pianificate vengono in genere utilizzate per applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] che agevolano l'integrità complessiva del processo. Per le operazioni di riciclo pianificate, nel server di report vengono creati domini applicazione aggiuntivi per le nuove richieste. Le richieste già in corso possono essere completate nel dominio applicazione corrente entro la scadenza del tempo di attesa. Le impostazioni di configurazione che controllano le operazioni di riciclo pianificate vengono specificate complessivamente per il server. Non è possibile configurare una pianificazione per il riciclo o una soglia di memoria diversa per ogni applicazione.  
  
-   Le operazioni di riciclo non pianificate vengono eseguite a ore arbitrarie in risposta a modifiche alla configurazione, utilizzo della memoria ed errori di allocazione di memoria:  
  
    -   Nel caso di modifiche alla configurazione, il server di report tenterà di utilizzare un riciclo leggero che reindirizza le nuove richieste a una nuova istanza del dominio applicazione. Se non è possibile eseguire il riciclo leggero in modo corretto, viene avviato un riciclo hardware del dominio applicazione che annulla tutte le richieste in corso, chiude i domini applicazione correnti e successivamente riavvia nuovi domini applicazione.  
  
    -   Gli errori di allocazione di memoria indicano che le risorse di sistema sono insufficienti per la quantità di elaborazione di report eseguita dal server. Se si verifica un errore di allocazione di memoria, viene eseguita un'operazione di riciclo pesante per tutti i domini applicazione. Tutte le code di richieste vengono cancellate. Le richieste annullate non vengono riavviate. Se era in corso la visualizzazione interattiva di un report da parte di un utente, è necessario aggiornare o riaprire il report. L'elaborazione pianificata verrà eseguita all'ora prevista successiva. Se il ritardo non è accettabile, è possibile aggiornare manualmente uno snapshot del report o modificare una pianificazione della sottoscrizione o dello snapshot del report in modo che venga eseguito immediatamente.  
  
 I domini applicazione per il servizio Web ReportServer, Gestione report e l'applicazione di elaborazione in background potrebbero essere riciclati contemporaneamente o individualmente, in base alle circostanze che determinano il verificarsi del riciclo:  
  
-   Le operazioni di riciclo avviate da [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] interessano solo le applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]: servizio Web ReportServer e Gestione Report. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] , i domini applicazione verranno riciclati. Le operazioni di riciclo avviate da [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] sono in genere indipendenti da quelle per l'applicazione di elaborazione in background.  
  
-   Le operazioni di riciclo avviate dal server di report influiscono in genere sul servizio Web ReportServer, su Gestione report e sull'applicazione di elaborazione in background. Le operazioni di riciclo vengono eseguite in risposta alle modifiche alle impostazioni di configurazione e ai riavvii del servizio.  
  
## <a name="rsreportserver-configuration-settings-for-application-domains"></a>Impostazioni di configurazione RSReportServer per i domini applicazione  
 Le impostazioni di configurazione sono specificate nel file [RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md). Nell'esempio seguente vengono illustrate le impostazioni di configurazione predefinite per il riciclo del dominio applicazione pianificato.  
  
 `<RecycleTime>720</RecycleTime>`  
  
 `<MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>`  
  
 Nella tabella seguente vengono descritti questi elementi.  
  
|Elemento|Si applica a|Definizione|  
|-------------|----------------|----------------|  
|**RecycleTime**|Tutti i tre domini applicazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Specifica la frequenza di riciclo dei domini applicazione. La pianificazione predefinita per il riciclo è conforme al modello di 12 ore seguito in genere per il riciclo dei domini applicazione di [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . All'ora pianificata, tutte le nuove richieste vengono inoltrate a una nuova istanza del dominio applicazione. Le richieste attualmente in corso nell'istanza originale possono proseguire fino al loro completamento. Dopo che tutti i processi sono stati completati, l'istanza originale viene eliminata e la nuova istanza diviene l'unica istanza del dominio applicazione attiva.<br /><br /> Il valore predefinito è 720 minuti.|  
|**MaxAppDomainUnloadTime**|Solo dominio applicazione dell'elaborazione in background|Per impostazione predefinita, in un server di report viene allocato un tempo di attesa di 30 minuti durante il quale un dominio applicazione può essere arrestato nel corso di un'operazione di riciclo. Se non è possibile completare i processi attualmente in corso entro il tempo stabilito o se l'esecuzione di un processo richiede più tempo rispetto al tempo di attesa, l'istanza del dominio applicazione viene riavviata immediatamente. Tutti i processi non completati vengono terminati.<br /><br /> Per altre informazioni su come visualizzare lo stato o annullare i processi in esecuzione nel server di report, vedere [Annulla processi server di report &#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md).|  
  
> [!NOTE]  
>  Sebbene il servizio Web ReportServer e Gestione report siano applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] , nessuna applicazione risponde al riciclo del dominio applicazione pianificato che potrebbe essere specificato in machine.config per applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] ospitate in IIS.  
  
## <a name="see-also"></a>Vedere anche  
 [File di configurazione RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurare la memoria disponibile per applicazioni del server di report](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
  
  
