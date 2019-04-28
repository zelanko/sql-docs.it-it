---
title: Elaborare manualmente i dati (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.datarefreshprogressdb.f1
ms.assetid: 0918c04c-c1e6-45b4-acfa-96fa578e684b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6f87cda5fb38fad586e5272d7d7c3ea255a478b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728337"
---
# <a name="manually-process-data-ssas-tabular"></a>Elaborare manualmente i dati (SSAS tabulare)
  In questo argomento viene illustrato come elaborare manualmente i dati dell'area di lavoro in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Quando si crea un modello tabulare in cui vengono utilizzati dati esterni, è possibile aggiornare manualmente i dati tramite il comando Elabora. È possibile elaborare una sola tabella, tutte le tabelle nel modello o una o più partizioni. Ogni volta che si elaborano i dati, potrebbe anche essere necessario ricalcolarli.  Per elaborazione dei dati si intende il recupero dei dati più recenti dalle origini esterne. Con ricalcolo si intende l'aggiornamento del risultato di qualsiasi formula in cui vengono utilizzati i dati.  
  
 Sezioni dell'argomento:  
  
-   [Elaborare manualmente i dati](#bkmk_mahually_process)  
  
-   [Stato elaborazione dati](#bkmk_data_process_progress)  
  
##  <a name="bkmk_mahually_process"></a> Elaborare manualmente i dati  
  
#### <a name="to-process-data-for-a-single-table-or-all-tables-in-a-model"></a>Per elaborare i dati per una sola tabella o tutte le tabelle in un modello  
  
1.  In Progettazione modelli fare clic sulla tabella che si desidera elaborare.  
  
2.  Nel menu **Modello** fare clic su **Elabora**, quindi su **Elabora** o **Elabora tutto**.  
  
#### <a name="to-process-data-for-all-tables-using-the-same-connection"></a>Per elaborare i dati di tutte le tabelle utilizzando la stessa connessione  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]fare clic sul menu **Modello** , quindi scegliere **Connessioni esistenti**.  
  
2.  Nella finestra di dialogo **Connessioni esistenti** selezionare una connessione, quindi fare clic su **Elabora**.  
  
#### <a name="to-process-data-for-one-or-more-partitions"></a>Per elaborare i dati di una o più partizioni  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Elabora** dal menu **Modello**, quindi fare clic su **Elabora partizioni**.  
  
2.  In **Modalità** della finestra di dialogo **Elabora partizioni**selezionare una delle modalità di elaborazione seguenti:  
  
    |Elabora partizioni|Descrizione|  
    |----------|-----------------|  
    |**Elaborazione predefinita**|Rileva lo stato di elaborazione di un oggetto partizione ed esegue l'elaborazione necessaria per recapitare oggetti partizione non elaborati o elaborati parzialmente in uno stato di elaborazione completa. Vengono caricati i dati per le tabelle vuote e le partizioni; vengono compilate o ricompilate le gerarchie, le colonne calcolate e le relazioni.|  
    |**Elaborazione completa**|Elabora un oggetto partizione e tutti gli oggetti in esso contenuti. Quando viene eseguita l'elaborazione completa per un oggetto che è stato già elaborato, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] vengono eliminati tutti i dati dell'oggetto, quindi quest'ultimo viene elaborato. Questo tipo di elaborazione è necessario quando è stata apportata una modifica strutturale a un oggetto.|  
    |**Elaborare dati**|Carica i dati in una partizione o in una tabella senza ricompilare le gerarchie o le relazioni oppure ricalcolare le colonne calcolate e le misure.|  
    |**Elaborazione pulizia**|Rimuove tutti i dati da una partizione.|  
    |**Elaborazione aggiunta**|Aggiornare in modo incrementale la partizione con i nuovi dati.|  
  
3.  Nell'elenco delle partizioni selezionare le partizioni da elaborare, quindi scegliere **OK**.  
  
##  <a name="bkmk_data_process_progress"></a> Stato elaborazione dati  
 La finestra di dialogo **Stato elaborazione dati** consente di monitorare l'elaborazione di dati importati nel modello da un'origine esterna. Per accedere a questa finestra di dialogo, scegliere **Elabora partizioni** , **Elabora tabella**o **Elabora tutto** dal menu **Modello**.  
  
 **Stato**  
 Viene indicato se l'operazione di elaborazione ha avuto esito positivo o negativo.  
  
 **Dettagli**  
 Vengono elencate le tabelle e le visualizzazioni importate, il numero di righe importato e viene fornito un collegamento a un report di qualsiasi problema.  
  
 **Arresta aggiornamento**  
 Fare clic per arrestare l'operazione di elaborazione. Questa opzione è utile se l'operazione è troppo lunga o se si sono verificati troppi errori.  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborare dati &#40;SSAS tabulare&#41;](process-data-ssas-tabular.md)   
 [Risolvere i problemi relativi all'elaborazione dei dati &#40;SSAS tabulare&#41;](troubleshoot-process-data-ssas-tabular.md)  
  
  
