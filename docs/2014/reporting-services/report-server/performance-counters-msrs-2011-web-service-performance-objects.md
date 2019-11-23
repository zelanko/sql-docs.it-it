---
title: Contatori delle prestazioni per gli oggetti prestazioni MSRS 2014 Web Service e MSRS 2014 Windows Service (modalità nativa) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- Report Server Web service, performance counters
- Reporting Services performance object
- RS Web Service performance object
- counters [Reporting Services]
- performance [Reporting Services]
ms.assetid: c642fc4f-8734-4626-a194-42ac9cd8e2ef
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e3acf02dff2d0d699a6d4dfe271d0aed8419683a
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782814"
---
# <a name="performance-counters-for-the-msrs-2014-web-service-and-msrs-2014-windows-service-performance-objects-native-mode"></a>Contatori delle prestazioni per gli oggetti prestazioni MSRS 2014 Web Service e MSRS 2014 Windows Service (modalità nativa)
  In questo argomento sono descritti i contatori delle prestazioni per gli oggetti prestazioni `MSRS 2014 Web Service` e `MSRS 2014 Windows Service`.  
  
> [!NOTE]  
>  Tramite questi oggetti prestazioni vengono monitorati gli eventi nel server di report locale. Se si esegue un server di report in una distribuzione con scalabilità orizzontale, i conteggi si applicano al server corrente e non alla distribuzione con scalabilità orizzontale.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]  
  
 Gli oggetti prestazioni sono disponibili nel monitor di prestazioni di Windows (**Perfmon.exe**). Per altre informazioni, vedere la documentazione di Windows, [Profilatura di runtime](https://msdn.microsoft.com/library/w4bz2147.aspx) (https://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 Per informazioni correlate ai contatori delle prestazioni in modalità SharePoint, vedere [contatori delle prestazioni per gli oggetti &#40;&#41;prestazioni MSRS 2014 Web service SharePoint Mode e MSRS 2014 Windows Service SharePoint Mode](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md)SharePoint Mode.  
  
 **Contenuto dell'argomento:**  
  
-   [Contatori delle prestazioni del servizio Web MSRS 2014](#bkmk_webservice)  
  
-   [Contatori delle prestazioni del servizio Windows MSRS 2014](#bkmk_windowsservice)  
  
-   [Utilizzare i cmdlet di PowerShell per restituire gli elenchi](#bkmk_powershell)  
  
##  <a name="bkmk_webservice"></a>Contatori delle prestazioni del servizio Web MSRS 2014  
 Tramite l'oggetto prestazioni `MSRS 2014 Web Service` vengono monitorate le prestazioni del server di report. Questo oggetto prestazione include una raccolta di contatori che consentono di tenere traccia delle elaborazioni nel server di report avviate in genere da operazioni di visualizzazione dei report interattive. Quando si configura questo contatore, è possibile applicarlo a tutte le istanze di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] oppure è possibile selezionare istanze specifiche. I contatori vengono reimpostati ogni volta che il servizio Web ReportServer viene arrestato da [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] .  
  
 Nella tabella seguente sono elencati i contatori inclusi con l'oggetto prestazioni `MSRS 2014 Web Service`.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|`Active Sessions`|Numero di sessioni attive. Tramite questo contatore viene restituito un conteggio cumulativo di tutte le sessioni del browser generate dalle esecuzioni dei report, indipendentemente dal fatto che siano ancora attive o meno.<br /><br /> Quando i record di sessione vengono rimossi, il contatore viene diminuito. Per impostazione predefinita, le sessioni vengono rimosse dopo dieci minuti di inattività.|  
|`Cache Hits/Sec`|Numero di richieste al secondo di report memorizzati nella cache. Si tratta di richieste relative a report di nuovo visualizzabili, non delle richieste relative a report elaborati direttamente dalla cache. Vedere `Total Cache Hits` più avanti in questo argomento.|  
|`Cache Hits/Sec (Semantic Models)`|Numero di richieste al secondo per il modello memorizzato nella cache. Si tratta di richieste relative a report di nuovo visualizzabili, non delle richieste relative a report elaborati direttamente dalla cache.|  
|`Cache Misses/Sec`|Numero di richieste al secondo che non hanno restituito un report dalla cache. Consente di stabilire se le risorse utilizzate per la memorizzazione nella cache, su disco o in memoria, siano sufficienti.|  
|`Cache Misses/Sec (Semantic Models)`|Numero di richieste al secondo tramite cui non è stato restituito alcun modello dalla cache. Consente di stabilire se le risorse utilizzate per la memorizzazione nella cache, su disco o in memoria, siano sufficienti.|  
|`First Session Requests/Sec`|Numero di nuove sessioni utente avviate al secondo dalla cache del server di report.|  
|`Memory Cache Hits/Sec`|Numero di volte al secondo in cui è stato possibile recuperare i report dalla cache in memoria. La*cache in memoria* è una parte della cache che archivia i report nella memoria della CPU. Quando viene usata la cache in memoria, il server di report non esegue query su [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per individuare il contenuto memorizzato nella cache.|  
|`Memory Cache Misses/Sec`|Numero di volte al secondo in cui non è stato possibile recuperare i report dalla cache in memoria.|  
|`Next Session Requests/Sec`|Numero di richieste al secondo di report aperti in una sessione esistente, ovvero i report di cui è stato eseguito il rendering da una sessione di snapshot.|  
|`Report Requests`|Numero di report attualmente attivi e gestiti dal server di report.|  
|`Reports Executed/Sec`|Numero di report eseguiti al secondo. Fornisce informazioni statistiche sul volume dei report. Utilizzare questo contatore con `Request/Sec` per confrontare il numero di report eseguiti con il numero di richieste di report restituibili dalla cache.|  
|`Requests/Sec`|Numero di richieste al secondo inviate al server di report. Tramite questo contatore si tiene traccia di tutti i tipi di richieste gestite dal server di report.|  
|`Total Cache Hits`|Numero totale di richieste di report alla cache dall'avvio del servizio. Il contatore viene reimpostato ogni volta che il servizio Web ReportServer viene arrestato da [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] .|  
|`Total Cache Hits (Semantic Models)`|Numero totale di richieste per il modello dalla cache dopo l'avvio del servizio. Il contatore viene reimpostato ogni volta che il servizio Web ReportServer viene arrestato da ASP.NET.|  
|`Total Cache Misses`|Numero totale di volte in cui non è stato possibile recuperare un report dalla cache dall'avvio del servizio. Il contatore viene reimpostato ogni volta che il servizio Web ReportServer viene arrestato da [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] . Utilizzare questo contatore per stabilire se lo spazio su disco e la memoria siano sufficienti.|  
|`Total Cache Misses (Semantic Models)`|Numero totale di volte in cui non è stato possibile restituire un modello dalla cache dopo l'avvio del servizio. Il contatore viene reimpostato ogni volta che il servizio Web ReportServer viene arrestato da ASP.NET. Utilizzare questo contatore per stabilire se lo spazio su disco e la memoria siano sufficienti.|  
|`Total Memory Cache Hits`|Numero totale di report memorizzati nella cache restituiti dalla cache in memoria dall'avvio del servizio. Il contatore viene reimpostato ogni volta che il servizio Web ReportServer viene arrestato da [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] . La*cache in memoria* è una parte della cache che archivia i report nella memoria della CPU. Quando viene usata la cache in memoria, il server di report non esegue query su [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per individuare il contenuto memorizzato nella cache.|  
|`Total Memory Cache Misses`|Numero totale di accessi alla cache in memoria non riusciti dall'avvio del servizio. Il contatore viene reimpostato ogni volta che il servizio Web ReportServer viene arrestato da [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] .|  
|`Total Processing Failures`|Numero di errori di elaborazione delle richieste per il servizio Web ReportServer.|  
|`Total Rejected Threads`|Numero totale di thread rifiutati per l'elaborazione asincrona e gestiti in un secondo momento come processi sincroni nello stesso thread. Ogni origine dei dati viene elaborata in un thread. Se il volume dei thread supera la capacità, i thread non verranno sottoposti all'elaborazione asincrona e verranno elaborati in modo seriale.|  
|`Total Reports Executed`|Numero totale di report eseguiti dall'avvio del servizio. Il contatore viene reimpostato ogni volta che il servizio Web ReportServer viene arrestato da [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] .|  
|`Total Requests`|Numero totale di richieste inviate al server di report dall'avvio del servizio. Il contatore viene reimpostato ogni volta che il servizio Web ReportServer viene arrestato da [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] .|  
  
##  <a name="bkmk_windowsservice"></a>Contatori delle prestazioni del servizio Windows MSRS 2014  
 Tramite l'oggetto prestazione `MSRS 2014 Windows Service` viene monitorato il servizio Windows ReportServer. Questo oggetto prestazione include una raccolta di contatori che consentono di tenere traccia delle elaborazioni di report avviate tramite operazioni pianificate, quali sottoscrizioni e recapiti, snapshot delle esecuzioni dei report e cronologie dei report. Quando si configura questo contatore, è possibile applicarlo a tutte le istanze di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] oppure è possibile selezionare istanze specifiche.  
  
 Nella tabella seguente sono elencati i contatori inclusi nell'oggetto prestazioni `MSRS 2014 Windows Service`.  
  
|Contatore|Descrizione|  
|-------------|-----------------|  
|`Active Sessions`|Numero di sessioni attive archiviate nel database del server di report. Questo contatore restituisce un conteggio cumulativo di tutte le sessioni utilizzabili del browser generate dalle sottoscrizioni del report, indipendentemente dal fatto che siano attive o meno.|  
|`Cache Flushes/Sec`|Numero di scaricamenti della cache al secondo.|  
|`Cache Hits/Sec`|Numero di richieste al secondo di report memorizzati nella cache. Si tratta di richieste relative a report di nuovo visualizzabili, non delle richieste relative a report elaborati direttamente dalla cache. Vedere `Total Cache Hits` più avanti in questo argomento.|  
|`Cache Hits/Sec (Semantic Models)`|Numero di richieste al secondo per i modelli memorizzati nella cache.|  
|`Cache Misses/Sec`|Numero di richieste al secondo che non hanno restituito un report dalla cache. Consente di stabilire se le risorse utilizzate per la memorizzazione nella cache, su disco o in memoria, siano sufficienti.|  
|`Cache Misses/Sec (Semantic Models)`|Numero di richieste al secondo tramite cui non è stato restituito alcun modello dalla cache. Consente di stabilire se le risorse utilizzate per la memorizzazione nella cache, su disco o in memoria, siano sufficienti.|  
|`Delivers/Sec`|Numero di recapiti di report al secondo, da parte di tutte le estensioni per il recapito.|  
|`Events/Sec`|Numero di eventi elaborati al secondo. Tra gli eventi monitorati sono inclusi `SnapshotUpdated` e `TimedSubscription`.|  
|`First Session Requests/Sec`|Numero di nuove sessioni di esecuzione del report create al secondo.|  
|`Memory Cache Hits/Sec`|Numero di volte al secondo in cui è stato possibile recuperare i report dalla cache in memoria. La*cache in memoria* è una parte della cache che archivia i report nella memoria della CPU. Quando viene usata la cache in memoria, il server di report non esegue query su [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per individuare il contenuto memorizzato nella cache.|  
|`Memory Cache Misses/Sec`|Numero di volte al secondo in cui non è stato possibile recuperare i report dalla cache in memoria.|  
|`Next Session Requests/Sec`|Numero di richieste al secondo di report aperti in una sessione esistente, ovvero i report di cui è stato eseguito il rendering da una sessione di snapshot.|  
|`Report Requests`|Numero di report attualmente attivi e gestiti dal server di report. Utilizzare questo contatore per valutare la strategia utilizzata per la memorizzazione nella cache. Potrebbero essere presenti più richieste rispetto ai report generati.|  
|`Reports Executed/Sec`|Numero di report generati al secondo.|  
|`Requests/Sec`|Numero totale di richieste elaborate correttamente al secondo da parte del servizio ReportServer.|  
|`Snapshot Updates/Sec`|Numero totale di aggiornamenti di snapshot dell'esecuzione dei report al secondo.|  
|`Total App Domain Recycles`|Numero totale di cicli del dominio applicazione dopo l'avvio del servizio Windows ReportServer.|  
|**Totale scaricamenti cache**|Numero totale di aggiornamenti della cache del server di report dall'avvio del servizio. Il contatore viene reimpostato dopo il riciclo del dominio applicazione. Vedere `Cache Flushes/Sec`.|  
|`Total Cache Hits`|Numero totale di richieste di report elaborate direttamente dalla cache dall'avvio del servizio Windows ReportServer. Il contatore viene reimpostato dopo il riciclo del dominio applicazione. Vedere `Cache Hits/Sec`.|  
|`Total Cache Hits (Semantic Models)`|Numero totale di richieste per i modelli elaborate direttamente dalla cache dopo l'avvio del servizio Windows ReportServer. Il contatore viene reimpostato dopo il riciclo del dominio applicazione. Vedere `Cache Hits/Sec`.|  
|`Total Cache Misses`|Numero totale di volte in cui non è stato possibile recuperare un report dalla cache dopo l'avvio del servizio Windows ReportServer. Il contatore viene reimpostato dopo il riciclo del dominio applicazione. Vedere `Cache Misses/Sec`.|  
|`Total Cache Misses (Semantic Models)`|Numero totale di volte in cui non è stato possibile restituire un modello dalla cache dopo l'avvio del servizio Windows ReportServer. Il contatore viene reimpostato dopo il riciclo del dominio applicazione.|  
|`Total Deliveries`|Numero totale di report recapitati tramite Elaborazione pianificazione e recapito, per tutte le estensioni per il recapito. Il contatore viene reimpostato dopo il riciclo del dominio applicazione.|  
|`Total Events`|Numero totale di eventi dopo l'avvio del servizio Windows ReportServer. Il contatore viene reimpostato dopo il riciclo del dominio applicazione.|  
|`Total Memory Cache Hits`|Numero totale di report memorizzati nella cache restituiti dalla cache in memoria dopo l'avvio del servizio Windows ReportServer. Il contatore viene reimpostato dopo il riciclo del dominio applicazione.|  
|`Total Memory Cache Misses`|Numero totale di accessi alla cache in memoria non riusciti dall'avvio del servizio. Il contatore viene reimpostato dopo il riciclo del dominio applicazione.|  
|`Total Processing Failures`|Numero di errori di elaborazione delle richieste nel servizio Windows ReportServer.|  
|`Total Rejected Threads`|Numero totale di thread rifiutati per l'elaborazione asincrona e gestiti in un secondo momento come processo sincrono nello stesso thread. In presenza di un carico moderato o elevato, questo contatore viene incrementato costantemente.|  
|`Total Reports Executed`|Numero totale di report eseguiti.|  
|`Total Requests`|Numero totale di report eseguiti dall'avvio del servizio. Il contatore viene reimpostato dopo il riciclo del dominio applicazione.|  
|`Total Snapshot Updates`|Numero totale di aggiornamenti per gli snapshot dell'esecuzione dei report.|  
  
##  <a name="bkmk_powershell"></a> Utilizzare i cmdlet di PowerShell per restituire gli elenchi  
 ![Contenuto correlato di PowerShell](../media/rs-powershellicon.jpg "Contenuto correlato di PowerShell") Tramite il seguente script di Windows PowerShell vengono restituiti i set di contatori in cui CounterSetName inizia con "MSR":  
  
```powershell
Get-Counter -ListSet msr*  
```  
  
 Tramite il seguente script di Windows PowerShell viene restituito l'elenco di contatori delle prestazioni per CounterSetName.  
  
```powershell
(Get-Counter -ListSet "MSRS 2014 Windows Service").Paths  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio delle prestazioni del server di report](monitoring-report-server-performance.md)   
 [Contatori delle prestazioni per gli oggetti &#40;prestazioni MSRS 2014 Web Service SharePoint Mode e MSRS 2014 Windows Service SharePoint Mode in&#41; modalità SharePoint](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md)   
 [Contatori delle prestazioni per gli oggetti prestazioni di ReportServer:Service e ReportServerSharePoint:Service](performance-counters-reportserver-service-performance-objects.md)  
