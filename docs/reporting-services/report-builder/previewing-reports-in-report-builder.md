---
title: Anteprima di report in Generatore report | Microsoft Docs
ms.date: 01/09/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: ba6b5bdd-d8c6-4aa8-ba32-3a10b11969d4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6fe16659ce288a664d684eced0de22ce4382f3a7
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288289"
---
# <a name="previewing-reports-in-report-builder"></a>Anteprima di report in Generatore report
  Durante la creazione di un report impaginato di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , è utile visualizzarne spesso l'anteprima per verificare che il contenuto visualizzato corrisponda a quanto desiderato. Per visualizzare l'anteprima del report, fare clic su **Esegui**. Il report viene visualizzato nella modalità di anteprima.  
  
 Generatore report consente di migliorare l'anteprima tramite sessioni di modifica se connesso a un server di report. La sessione di modifica crea una cache di dati e rende disponibili i set di dati della cache per anteprime ripetute del report. Una sessione di modifica non è una caratteristica con cui si interagisce direttamente, tuttavia sapendo il momento in cui il set di dati memorizzato nella cache viene aggiornato sarà possibile migliorare le prestazioni quando si visualizza in anteprima un report e capire il motivo per cui il report viene visualizzato più rapidamente o più lentamente.  
  
 Un altro vantaggio delle sessioni di modifica è la possibilità di modificare report che utilizzano origini dati incorporate o elementi di riferimento, ad esempio immagini o sottoreport archiviati nel server di report.  
  
> [!NOTE]  
> Esistono alcune differenze tra l'anteprima in Generatore Report e la visualizzazione in un browser. Ad esempio, un controllo di calendario, che viene aggiunto a un report quando si specifica un parametro di tipo Data/ora, è diverso in Generatore Report e in un browser. 
  
## <a name="improving-preview-performance"></a>Miglioramento delle prestazioni di anteprima  
 La modalità di creazione e aggiornamento dei report influisce sulla velocità di visualizzazione dell'anteprima dei report. Alla prima visualizzazione dell'anteprima di un report che si basa su un riferimento al server, viene creata una sessione di modifica e i dati utilizzati durante l'esecuzione del report vengono aggiunti a una cache di dati archiviata sul server di report. Quando si apportano modifiche al report che non influisce sui dati, la copia memorizzata nella cache dei dati viene utilizzata dal report. In questo modo non saranno mostrate le modifiche apportate ai dati ogni volta che si visualizza in anteprima il report. Se si desiderano nuovi dati, fare clic sul pulsante **Aggiorna** sulla barra multifunzione.  
  
 Le azioni seguenti comportano l'aggiornamento della cache e rallentano la successiva visualizzazione in anteprima del report:  
  
-   Aggiunta, modifica o eliminazione di un set di dati. Il set di dati memorizzato nella cache contiene tutti i set di dati utilizzati da un report e qualsiasi modifica ai set di dati invalida il set di dati memorizzato nella cache. È inclusa la modifica del nome, della query o dei campi nel set di dati.  
  
    > [!NOTE]  
    >  Se il set di dati dispone di un gran numero di campi che non si intende utilizzare, è necessario aggiornare il set di dati per omettere tali campi. Sebbene questa scelta crei una nuova sessione di modifica che rende più lenta la prima anteprima del report, un set di dati memorizzato nella cache più piccolo rappresenta un vantaggio generale per le prestazioni del server di report.  
  
-   Aggiunta, modifica o eliminazione di un'origine dati. È inclusa la modifica del nome o delle proprietà dell'origine dati, dell'estensione dei dati della relativa origine o delle proprietà della connessione all'origine dati.  
  
-   Modifica dell'origine dati condivisa utilizzata dal report in un'origine dati diversa.  
  
-   Modifica della lingua del report.  
  
-   Modifica degli assembly o del codice personalizzato utilizzato dal report.  
  
-   Aggiunta, modifica o eliminazione dei parametri delle query del report o dei valori dei parametri.  
  
 Le modifiche apportate al layout del report e alla formattazione dei dati non influiscono sul set di dati memorizzato nella cache. Le azioni seguenti possono essere eseguite senza aggiornare il set di dati memorizzato nella cache:  
  
-   Aggiunta o rimozione di aree dati, ad esempio tabelle, matrici o grafici.  
  
-   Aggiunta o eliminazione di colonne dal report. Tutti i campi del set di dati possono essere utilizzati nel report. L'aggiunta o la rimozione di campi nel report non ha effetto sul set di dati.  
  
-   Modifica dell'ordine dei campi nelle tabelle e matrici.  
  
-   Aggiunta, modifica o eliminazione dei gruppi di righe e colonne.  
  
-   Aggiunta, modifica o eliminazione della formattazione dei valori dei dati nei campi.  
  
-   Aggiunta, modifica o eliminazione di immagini, linee o caselle di testo.  
  
-   Modifica di interruzioni di pagina.  
  
 La sessione di modifica viene creata alla prima visualizzazione in anteprima di un report. Per impostazione predefinita, una sessione di modifica dura 7200 secondi (2 ore). La sessione viene reimpostata su due ore ogni volta che si esegue il report. Quando la sessione di modifica scade, la cache di dati viene eliminata. Se la sessione di modifica scade, ne viene creata automaticamente un'altra alla successiva visualizzazione in anteprima del report. La data di scadenza per le sessioni di modifica è configurabile. Se si ritiene che due ore sia un tempo troppo lungo o troppo corto, contattare l'amministratore del server di report.  
  
 Per impostazione predefinita, la cache di dati può contenere fino a cinque set di dati. Se si utilizzano molte combinazioni diverse di valori del parametro, il report potrebbe aver bisogno di più dati. Questa condizione richiede che la cache venga aggiornata e il report sia visualizzato più lentamente alla successiva anteprima. Il numero di voci nella cache può essere configurato dall'amministratore del server di report.  
  
## <a name="concurrency-of-report-updates"></a>Concorrenza di aggiornamenti del report  
 Di solito, la visualizzazione in anteprima di un report rappresenta un passaggio dell'aggiornamento e del conseguente salvataggio di un report in un relativo server. Quando si aggiorna un report, è possibile che un altro utente lo stia aggiornando e salvando nello stesso momento. Il report salvato per ultimo è la versione di report che è disponibile per la visualizzazione e l'aggiornamento futuri. Questo significa che la versione del report visualizzata in anteprima potrebbe non essere la versione che si riapre. È possibile salvare il report con un nome nuovo tramite l'opzione **Salva con nome** presente nel menu Generatore report.  
  
## <a name="external-report-items"></a>Elementi del report esterni  
 Il report potrebbe includere elementi quali origini dati condivise, immagini esterne e sottoreport archiviati separatamente dal report. Poiché gli elementi vengono archiviati separatamente, è possibile che possano essere spostati in una posizione diversa sul server di report o possano essere eliminati. In tal caso, potrebbe essere impossibile visualizzare in anteprima il report. È possibile aggiornare il report per indicare la posizione aggiornata dell'elemento oppure se l'elemento è stato eliminato, sostituirlo con un elemento esistente o rimuovere il riferimento all'elemento dal report.  
  
 Se un sottoreport utilizzato dal report viene modificato dopo la creazione della sessione di modifica, non sarà possibile visualizzare in anteprima il report. Per visualizzare correttamente in anteprima il report, è necessario salvare il report o fare clic su **Aggiorna** per ottenere dati aggiornati.  
  
## <a name="see-also"></a>Vedere anche  
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Formattazione degli elementi del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Salvataggio di report &#40;Generatore report&#41;](../../reporting-services/report-builder/saving-reports-report-builder.md)  
  
  
