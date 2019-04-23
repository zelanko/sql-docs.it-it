---
title: Monitoraggio delle prestazioni del server di report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- report servers [Reporting Services], performance
- counters [Reporting Services]
- monitoring performance [Reporting Services]
- SQL Server Reporting Services, performance
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: c1bc13d4-8297-4daf-bb19-4c1e5ba292a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a296af6a8bcb6f168d5461a6d0f36df1f6ce2339
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59968133"
---
# <a name="monitoring-report-server-performance"></a>Monitoraggio delle prestazioni del server di report
  Con gli strumenti di monitoraggio delle prestazioni è possibile valutare l'attività del server di report, osservare le tendenze, diagnosticare i colli di bottiglia a livello di sistema e raccogliere dati che consentono di determinare più facilmente se la configurazione del sistema corrente è sufficiente. Per ottimizzare le prestazioni del server, è possibile specificare la frequenza di riciclo del dominio dell'applicazione del server di report. Per altre informazioni, vedere [Configurare la memoria disponibile per applicazioni del server di report](../report-server/configure-available-memory-for-report-server-applications.md).  
  
## <a name="sources-of-performance-data"></a>Origini dei dati sulle prestazioni  
 Per raccogliere informazioni complete sulle prestazioni del sistema, è possibile utilizzare una combinazione di tecnologie e strumenti. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Nei sistemi operativi Windows Server le informazioni sulle prestazioni vengono fornite tramite gli strumenti seguenti:  
  
-   Gestione attività  
  
-   Visualizzatore eventi  
  
-   Console Performance  
  
 In Gestione attività sono disponibili informazioni sui programmi e sui processi in esecuzione nel computer. È possibile utilizzare Gestione attività per monitorare i principali indicatori delle prestazioni del server di report nonché per valutare l'attività dei processi in esecuzione e visualizzare grafici e dati sull'utilizzo della CPU e della memoria. Per informazioni sull'utilizzo di Gestione attività, vedere la documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 È possibile utilizzare la console Performance e il Visualizzatore eventi per creare avvisi e log relativi all'elaborazione dei report e all'utilizzo di risorse. Per informazioni su eventi di Windows generati da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Registro applicazioni di Windows](windows-application-log.md). Per informazioni sulla console Performance, vedere "Contatori delle prestazioni di Windows" più avanti in questo argomento.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - Le utilità forniscono anche informazioni sul database del server di report e sui database temporanei usati per la gestione della memorizzazione nella cache e delle sessioni.  
  
## <a name="windows-performance-counters"></a>Contatori delle prestazioni di Windows  
 Il monitoraggio di contatori delle prestazioni specifici consente di:  
  
-   Stimare i requisiti di sistema necessari per supportare un carico di lavoro previsto.  
  
-   Creare un riferimento per le prestazioni che consenta di misurare l'effetto delle modifiche alla configurazione o degli aggiornamenti applicativi.  
  
-   Monitorare le prestazioni dell'applicazione in presenza di determinati carichi, sia reali sia generati artificialmente.  
  
-   Verificare che gli aggiornamenti hardware abbiano l'effetto desiderato sulle prestazioni.  
  
-   Convalidare le modifiche apportate alla configurazione del sistema per verificare che abbiano l'effetto desiderato sulle prestazioni.  
  
## <a name="reporting-services-performance-objects"></a>Oggetti prestazione di Reporting Services  
 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] include gli oggetti prestazione seguenti:  
  
-   **MSRS 2011 Web Service** e `MSRS 2011 SharePoint Mode Web Service` per monitorare le prestazioni del server di report. In questi oggetti prestazione è inclusa una raccolta di contatori che consentono di tenere traccia delle elaborazioni nel server di report avviate in genere da operazioni di visualizzazione dei report interattive. I contatori vengono reimpostati ogni volta che il servizio Web ReportServer viene arrestato da [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] .  
  
-   `MSRS 2011 Windows Service` e `MSRS 2011 Windows Service SharePoint Mode` per monitorare le operazioni pianificate e il recapito dei report. In questi oggetti prestazione è inclusa una raccolta di contatori che consentono di tenere traccia delle elaborazioni di report avviate tramite operazioni pianificate, nelle quali sono incluse sottoscrizioni e recapiti, snapshot delle esecuzioni dei report e cronologie dei report.  
  
-   `ReportServer:Service` e `ReportServerSharePoint:Service` per monitorare gli eventi correlati ad HTTP e la gestione della memoria. Tali contatori sono specifici di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]e consentono di tenere traccia degli eventi correlati ad HTTP per il server di report, ad esempio richieste, connessioni e tentativi di accesso. Questo oggetto prestazione, inoltre, include contatori correlati alla gestione della memoria.  
  
 Se sono presenti più istanze del server di report in uno stesso computer, è possibile scegliere se monitorare le istanze insieme o separatamente. Scegliere quali istanze includere quando si aggiunge un contatore. Per altre informazioni sull'uso della console Performance (perfmon.msc) e sull'aggiunta di contatori, vedere la documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## <a name="other-performance-counters"></a>Altri contatori delle prestazioni  
 Alcuni contatori delle prestazioni personalizzati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono disponibili solo per `MSRS 2008 Web Service`, `MSRS 2008 Windows Service` e `ReportServer:Service`. Gli oggetti prestazione seguenti forniscono dati di monitoraggio delle prestazioni aggiuntivi per il server di report.  
  
|Oggetto prestazione|Note|  
|------------------------|-----------|  
|`.NET CLR Data` e `.NET CLR Memory`|In Gestione report vengono utilizzati i contatori delle prestazioni di [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . Per ulteriori informazioni, vedere "Miglioramento delle prestazioni e della scalabilità di applicazioni .NET" su MSDN.|  
|`Process`|Aggiungere i contatori delle prestazioni `Elapsed Time` e `ID Process` affinché un'istanza ReportingServicesService registri il tempo di attività del processo in base all'ID processo.|  
  
## <a name="sharepoint-events"></a>Eventi di SharePoint  
 Oltre agli oggetti relativi alle prestazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] può essere necessario configurare eventi di SharePoint se si esegue un server di report in modalità integrata SharePoint e l'ambiente di report è stato configurato per l'uso di un prodotto SharePoint. In questa sezione utilizzare Eventi per un server di report in modalità integrata SharePoint per esaminare gli eventi di diagnostica che potrebbero fornire informazioni utili se l'ambiente di report è integrato con SharePoint.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Contatori delle prestazioni per il MSRS 2014 Web Service e MSRS 2014 Windows Service prestazioni oggetti &#40;modalità nativa&#41;](performance-counters-msrs-2011-web-service-performance-objects.md)  
 Descrive i contatori delle prestazioni utilizzati dal servizio Web ReportServer.  
  
 [Contatori delle prestazioni per il MSRS 2014 Web Service SharePoint Mode e oggetti prestazioni MSRS 2014 Windows Service SharePoint in modalità &#40;modalità SharePoint&#41;](performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
 Descrive i contatori delle prestazioni utilizzati dal servizio Windows ReportServer.  
  
 [Contatori delle prestazioni per gli oggetti prestazioni di ReportServer:Service e ReportServerSharePoint:Service](performance-counters-reportserver-service-performance-objects.md)  
 Vengono descritti i contatori delle prestazioni correlati ad HTTP e alla memoria in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Eventi per un server di report in modalità integrata SharePoint  
 Vengono descritti gli eventi di diagnostica che è utile registrare quando si esegue un ambiente di report un prodotto SharePoint.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare la memoria disponibile per applicazioni del server di report](../report-server/configure-available-memory-for-report-server-applications.md)   
 [Reporting Services Report Server &#40;Native Mode&#41;](reporting-services-report-server-native-mode.md)   
 [Strumenti di Reporting Services](../tools/reporting-services-tools.md)  
  
  
