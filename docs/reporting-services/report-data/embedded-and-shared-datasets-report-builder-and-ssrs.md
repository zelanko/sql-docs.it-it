---
title: Set di dati condivisi e incorporati (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: adc95cc0-d15a-413d-bc5a-302eab37a069
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f1d665699dc2051745b08a56796588dab51e3bcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77077630"
---
# <a name="embedded-and-shared-datasets-report-builder-and-ssrs"></a>Set di dati condivisi e incorporati (Generatore report e SSRS)
  In un report un set di dati rappresenta i dati del report restituiti dall'esecuzione di una query in un'origine dati esterna. Il set di dati dipende dalla connessione dati contenente le informazioni sull'origine dati esterna. I dati stessi non sono inclusi nella definizione del report. Nel set di dati sono contenuti un comando di query, una raccolta campi, parametri, filtri e opzioni dei dati in cui sono incluse la distinzione tra maiuscole e minuscole e le regole di confronto. Esistono due tipi di set di dati:  
  
-   **Set di dati condivisi.** Un set di dati condiviso viene pubblicato in un server di report e può essere utilizzato da più report. Un set di dati condiviso deve essere basato su un'origine dati condivisa. Può essere memorizzato nella cache ed essere pianificato creando un piano di aggiornamento della cache.  
  
-   **Set di dati incorporati.** I set di dati incorporati vengono definiti e utilizzati in un singolo report.  
  
 La differenza tra i due tipi dipende dalle diverse modalità di creazione, archiviazione e gestione.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="shared-datasets"></a>Set di dati condivisi  
 Utilizzare un set di dati condiviso per fornire una query che può essere utilizzata da più report. I set di dati condivisi vengono archiviati nel server di report e possono essere gestiti separatamente dai report o dalle origini dati condivise. Ad esempio, un amministratore del server di report potrebbe aggiornare la query per sfruttare l'indicizzazione avanzata o un'altra ottimizzazione delle prestazioni di esecuzione delle query.  
  
 Si consiglia di utilizzare sempre i set di dati condivisi quando possibile. È possibile ottimizzare una query o memorizzare nella cache i risultati della query per sfruttare le prestazioni del report. I set di dati condivisi rendono l'accesso ai dati più facile da gestire e offrono una maggiore protezione dei report e dei set di dati a cui hanno accesso, garantendo così migliori prestazioni.  
  
 In Progettazione report è possibile creare set di dati condivisi come parte di un progetto report e controllare se distribuirli a un server di report. Non è possibile accedere a un server di report e selezionare un set di dati condiviso da aggiungere al report in uso.  
  
 In Generatore report è possibile eseguire le operazioni seguenti:  
  
1.  Per creare un set di dati condiviso, utilizzare visualizzazione di progettazione del set di dati condiviso. È possibile salvarlo in un server di report o in un sito di SharePoint per condividere con altri report. È inoltre possibile accedere al server di report e modificare il set di dati condiviso esistente. In questa visualizzazione è possibile compilare una query e impostare tutte le opzioni del set di dati. Per altre informazioni, vedere [Visualizzazione di progettazione set di dati condivisi &#40;Generatore report&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md).  
  
2.  Per aggiungere un set di dati condiviso al report, aprire Generatore report in visualizzazione di progettazione report. Nella procedura guidata o nel riquadro dei dati del report individuare il server di report e selezionare il set di dati condiviso da aggiungere al report. In questa visualizzazione non è possibile modificare la query eccetto per aggiungere campi. È possibile eseguire l'override di altre opzioni dei dati e aggiungere filtri. Non è possibile rimuovere filtri.  
  
3.  Nella tabella seguente vengono confrontate le proprietà configurabili per la definizione del set di dati condiviso nel server di report e quelle configurabili per l'istanza del set di dati condiviso nella definizione del report.  
  
    |Proprietà|Note sulla configurazione per la definizione|Note sulla configurazione per l'istanza|  
    |--------------|--------------------------------------------|------------------------------------------|  
    |Testo della query|Configurare la query, anche definendola come espressione.|Impossibile modificare la query.|  
    |Parametri di query|Non può fare riferimento ai parametri del report<br /><br /> Include valori predefiniti<br /><br /> Include un flag di sola lettura|Configurare parametri non contrassegnati come di sola lettura nella definizione|  
    |Filtri|Definire filtri|Impossibile visualizzare o modificare i filtri del set di dati che fanno parte della definizione<br /><br /> Può creare filtri aggiuntivi|  
    |origine dati|Deve essere un'origine dati condivisa|Impossibile modificare l'origine dati condivisa|  
    |Campi|Campi dal comando di query<br /><br /> I campi calcolati non fanno parte della definizione del set di dati|Visualizzare campi, ma non modificarli<br /><br /> La raccolta di campi è statica basata sulla query al momento dell'aggiunta del set di dati condiviso al report. Per aggiornare, fare clic su **Aggiorna campi** nella finestra di dialogo **Proprietà set di dati** . La raccolta di campi effettivi è qualsiasi risultato restituito dalla query corrente nella definizione.<br /><br /> Aggiungere campi calcolati|  
    |Set di dati|Opzioni dei dati quale la distinzione tra maiuscole e minuscole|Eseguire l'override di opzioni dei dati nell'istanza|  
  
## <a name="embedded-datasets"></a>Set di dati incorporati  
 Utilizzare un set di dati incorporato quando si desidera ottenere dati da un'origine dati esterna da utilizzare solo in un unico report. I set di dati incorporati risultano utili quando si desidera creare una query senza altre dipendenze che non sia necessario utilizzare per più report.  
  
 Per creare o modificare un set di dati incorporato, utilizzare il riquadro dei dati del report. Dopo aver creato un set di dati, è possibile configurare le proprietà nella finestra di dialogo **Proprietà set di dati** .  
  
## <a name="see-also"></a>Vedere anche  
 [Confrontare origini dati incorporate e condivise - Generatore report e SSRS](compare-shared-embedded-data-sources-report-builder-ssrs.md) [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
