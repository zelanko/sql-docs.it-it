---
title: Impostazione dei valori di timeout per l'elaborazione di report e di set di dati condivisi (SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- time-outs [Reporting Services]
- query time-outs [Reporting Services]
- report processing [Reporting Services], time-outs
- report execution time-outs [Reporting Services]
ms.assetid: 0f9dc61d-d03c-4bbf-8090-7a53844350f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8a0a28974b50d5230c962a19bc19630a55dbef48
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65580953"
---
# <a name="setting-time-out-values-for-report-and-shared-dataset-processing-ssrs"></a>Impostazione dei valori di timeout per l'elaborazione di report e di set di dati condivisi (SSRS)
  È possibile fare in modo che [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] specifichi valori di timeout per limitare l'uso delle risorse del sistema. Il server di report supporta due valori di timeout:  
  
-   Il valore di timeout per le query del set di dati incorporato, ovvero il numero di secondi per cui il server di report rimane in attesa di una risposta dal database. Questo valore viene definito in un report.  
  
-   Il valore di timeout per le query del set di dati condiviso, ovvero il numero di secondi per cui il server di report rimane in attesa di una risposta dal database. Questo valore è parte della definizione del set di dati condiviso e può essere modificato quando si gestisce tale set sul server di report.  
  
-   Il valore del timeout di esecuzione di un report è il numero massimo di secondi disponibile per l'elaborazione del report, dopo il quale l'esecuzione viene arrestata. Questo valore viene definito a livello di sistema. È possibile modificare questa impostazione per singoli report.  
  
 La maggior parte degli errori di timeout si verifica durante l'elaborazione di query. Se si verificano spesso errori di timeout, provare ad aumentare il valore di timeout della query. Verificare che il valore del timeout di esecuzione del report sia impostato su un valore maggiore del valore del timeout per le query. È necessario impostare un periodo di tempo sufficiente per completare sia l'elaborazione delle query che quella del report.  
  
## <a name="setting-a-query-time-out-for-an-embedded-dataset-in-a-report"></a>Impostazione di un timeout per la query per un set di dati incorporato in un report  
 I valori di timeout della query vengono specificati durante la creazione del report al momento della definizione di un set di dati incorporato. Il valore di timeout viene archiviato con il report nell'elemento **Timeout** della definizione del report. Per impostazione predefinita, questo valore è impostato su 30 secondi. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Gli utenti che dispongono di autorizzazioni per la modifica delle proprietà di un report pubblicato possono reimpostare questo valore modificando il file di definizione del report.  
  
 È inoltre possibile specificare un valore di timeout della query per le sottoscrizioni guidate dai dati. Il valore di timeout della query viene specificato nelle pagine Sottoscrizione guidata dai dati. Il valore specificato dall'utente determina la durata dell'attesa del server di report per il completamento dell'elaborazione della query quando si esegue il recupero dei dati dall'origine dati del sottoscrittore.  
  
## <a name="setting-a-query-time-out-for-a-shared-dataset"></a>Impostazione del timeout per la query per un set di dati condiviso  
 I valori di timeout per la query vengono specificati in secondi sul server di report quando si crea o si gestisce un set di dati condiviso. Per impostazione predefinita, questo valore viene impostato su 0 secondi che indica l'assenza del valore di timeout. Per altre informazioni, vedere [Gestire set di dati condivisi](../../reporting-services/report-data/manage-shared-datasets.md).  
  
## <a name="setting-a-report-execution-time-out"></a>Impostazione del timeout dell'esecuzione del report  
 È possibile impostare il valore di timeout dell'esecuzione del report in modo da limitare la quantità di tempo utilizzata da un server di report per elaborare un report. I valori di timeout dell'esecuzione del report possono essere impostati in Gestione report. È possibile impostare un valore predefinito per tutti i report nella pagina Impostazioni sito e quindi modificare tale valore per un determinato report nella pagina per impostare le proprietà di esecuzione. Per impostazione predefinita, il valore è impostato su 1800 secondi. Per altre informazioni, vedere [Impostare proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md).  
  
## <a name="how-report-execution-time-out-values-are-evaluated"></a>Valutazione dei valori di timeout per l'esecuzione dei report  
 Il server di report valuta i processi in esecuzione a intervalli di 60 secondi. Ogni 60 secondi, il server di report confronta il tempo di elaborazione effettivo con il valore di timeout per l'esecuzione del report. Se il tempo di elaborazione di un report supera il valore di timeout previsto, l'elaborazione del report viene arrestata.  
  
 Si noti che se si specifica un valore di timeout minore di 60 secondi, il report può venire eseguito completamente se l'elaborazione ha inizio e termina durante la parte di attesa del ciclo, ossia quando il server di report non valuta i processi in esecuzione. Se, ad esempio, si imposta un valore di timeout di 10 secondi per un report la cui esecuzione richiede 20 secondi, il report viene elaborato completamente se l'esecuzione inizia all'inizio del ciclo di 60 secondi.  
  
> [!NOTE]  
>  È possibile definire l'impostazione **RunningRequestsDbCycle** nel file RSReportServer.config per modificare la frequenza di valutazione dei processi in esecuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare le opzioni di elaborazione &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Server di report di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Manage a Running Process](../../reporting-services/subscriptions/manage-a-running-process.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
