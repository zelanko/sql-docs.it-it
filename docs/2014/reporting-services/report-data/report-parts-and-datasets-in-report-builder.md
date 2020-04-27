---
title: Parti del report e set di dati in Generatore report | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1fe86481-9c41-4535-a4b7-c7c4d780cab6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e5f77df0a2e5322687f5724e7921932a551d07ed
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107165"
---
# <a name="report-parts-and-datasets-in-report-builder"></a>Parti del report e set di dati in Generatore report
  In Generatore report il modo più semplice per includere dati in un report consiste nell'aggiungere parti del report esistenti dalla Raccolta parti del report. Nelle parti del report sono contenuti i set di dati dai quali dipendono, chiamati *set di dati dipendenti*. I set di dati dipendenti sono basati sulle origini dati condivise e possono essere set di dati incorporati o condivisi.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 Un altro modo semplice per includere dati in un report è utilizzare un set di dati condiviso. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="adding-a-report-part-with-dependent-datasets-to-your-report"></a><a name="Adding"></a>Aggiunta di una parte di report con set di impostazioni dipendenti al report  
 Quando si aggiunge una parte di report al report, anche i set di dati dipendenti contenuti nella parte di report vengono aggiunti al report. Poiché in una parte di report potrebbe essere incluso un rettangolo contenente molti altri elementi del report, è possibile aggiungere più set di dati dipendenti al report in uso. Ogni set di dati condiviso è un riferimento indipendente; l'origine dati condivisa dalla quale dipende non viene aggiunta al report. A ogni set di dati incorporato viene aggiunta anche l'origine dati incorporata o condivisa dalla quale dipende.  
  
 Le credenziali per un'origine dati incorporata non sono salvate come parte della parte del report. Se un'origine dati incorporata viene aggiunta al report, verranno richieste le credenziali quando si esegue il report. Per evitare questa richiesta, utilizzare le parti di report basate sulle origini dati condivise con le credenziali archiviate.  
  
 Una volta aggiunta una parte di report al report in uso, i set di dati aggiunti non presentano alcuna differenza con i set di dati incorporati o condivisi che sono stati creati. È possibile visualizzare i set di dati aggiuntivi nel riquadro dei dati del report. I set di dati incorporati vengono visualizzati nell'origine dati condivisa corrispondente mentre i set di dati condivisi nella cartella Set di dati condivisi.  
  
  
##  <a name="customizing-dependent-datasets"></a><a name="Customizing"></a>Personalizzazione di set di impostazioni dipendenti  
 Dopo avere aggiunto parti del report al report, è possibile visualizzarlo in anteprima e decidere di apportare alcune modifiche ai dati. Gli elementi modificabili dipendono dal tipo di set di dati che si sta utilizzando.  
  
 Per modificare i dati e le opzioni dati di un set di dati incorporato, è possibile modificare le proprietà del set di dati, inclusa la query, come se si creasse il set di dati personalmente.  
  
 Per modificare i dati e le opzioni dati per un set di dati condiviso, è possibile modificare la definizione del set di dati condiviso sul server di report solo se si dispone di autorizzazioni sufficienti. È possibile personalizzare anche l'istanza del set di dati condiviso nel report aggiungendo filtri, campi calcolati e modificando le opzioni dati, ad esempio per la distinzione maiuscole/minuscole. Per altre informazioni, vedere [Set di dati condivisi e incorporati &#40;Generatore report e SSRS&#41;](embedded-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Per altre informazioni sulla modifica della definizione di un set di dati condiviso o su come mostrare le ultime modifiche dei dati per un set di dati condiviso nel report, vedere [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md) e [Aggiunta, modifica e aggiornamento di campi nel riquadro dei dati del report &#40;Generatore report e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
  
##  <a name="publishing-dependent-datasets-as-shared-datasets"></a><a name="Publishing"></a>Pubblicazione di DataSet dipendenti come set di impostazioni  
 Quando si pubblica un elemento del report che dispone di set di dati dipendenti, è possibile utilizzare l'opzione per pubblicare ogni set di dati come set di dati condiviso o come set di dati incorporato che rimane tale nell'elemento del report.  
  
 Quando si seleziona l'opzione del set di dati condiviso, il set di dati viene salvato nel server di report come definizione del set di dati condiviso. Nel report, ogni elemento del report in cui viene utilizzato il set di dati è aggiornato per puntare al set di dati condiviso che si trova ora sul server di report. Di conseguenza si verificano le seguenti due situazioni:  
  
1.  Nella finestra di dialogo Pubblica ogni set di dati condiviso che è stato pubblicato viene rimosso dall'elenco di elementi disponibili per la pubblicazione.  
  
2.  Quando si esce da Generatore report o si avvia un nuovo report, viene richiesto di salvare il report. Se non si effettua questa operazione, alla successiva apertura del report e pubblicazione degli elementi del report, si potrebbero pubblicare nuove copie degli stessi set di dati. Per impedire il salvataggio di più copie di set di dati condivisi nel server di report, si consiglia di salvare il report.  
  
> [!IMPORTANT]  
>  Per assicurarsi di poter utilizzare i dati di un set di dati condiviso, è necessario comprendere i principi che regolano la protezione degli elementi del report. Per ulteriori informazioni, vedere [Proteggere gli elementi del set di dati condiviso](../security/secure-shared-dataset-items.md).  
  
  
## <a name="see-also"></a>Vedi anche  
 [Visualizzazione di progettazione report &#40;Generatore report&#41;](../report-builder/report-design-view-report-builder.md)   
 [&#40;di sicurezza Generatore report&#41;](../report-builder/security-report-builder.md)   
 [Parti del report &#40;Generatore report e SSRS&#41;](../report-parts-report-builder-and-ssrs.md)   
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
  
