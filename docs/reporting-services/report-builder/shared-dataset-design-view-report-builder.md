---
title: Visualizzazione della struttura set di dati condivisi (Generatore report) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 47c502da-d163-45d9-bf04-0849e5ba7929
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b00e626bf9823d45d7437bfa3219fb2b0afa8cc
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287949"
---
# <a name="shared-dataset-design-view-report-builder"></a>Visualizzazione di progettazione set di dati condivisi (Generatore report)
  In un report un set di dati rappresenta i dati del report restituiti dall'esecuzione di una query in un'origine dati esterna. Un set di dati condiviso viene pubblicato in un server di report e può essere usato da più report. È possibile creare set di dati da condividere con altri utenti. Nella finestra di progettazione di set di dati condivisi è possibile selezionare un'origine dati condivisa, specificare proprietà per il set di dati condiviso e creare una query in Progettazione query.  
  
 ![rs_SharedDatasetDesignMode](../../reporting-services/report-builder/media/rs-shareddatasetdesignmode.gif "rs_SharedDatasetDesignMode")  
  
 Per altre informazioni sull'uso di dati in un report, vedere [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md).  
  
##  <a name="Ribbon"></a> Barra multifunzione  
 La barra multifunzione consente la rapida individuazione dei comandi necessari per completare un'attività. I comandi sono organizzati nei gruppi logici seguenti: Connessione, set di dati e Progettazione query.  
  
### <a name="connection"></a>Connessione  
 Usare il pulsante **Seleziona** nel gruppo Connessione per selezionare un'origine dati condivisa o individuare e selezionare l'origine dati condivisa nel server di report.  
  
> [!NOTE]  
>  Un set di dati condiviso deve essere basato su un'origine dati condivisa. Se l'origine dati richiesta non è disponibile, è necessario crearne una nel server di report. Per altre informazioni, vedere [Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
 Per altre informazioni, vedere [Connessioni dati, origini dati e stringhe di connessione](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
### <a name="dataset"></a>Set di dati  
 Usare il pulsante **Opzioni SET** per impostare le proprietà del set di dati condiviso, tra cui:  
  
-   Campi. È possibile aggiungere o modificare un campo nella raccolta di campi.  
  
-   Opzioni dati. È possibile impostare opzioni che influiscono su criteri di corrispondenza e ordinamento, ad esempio distinzione tra maiuscole e minuscole e regole di confronto.  
  
-   Filtri. È possibile definire filtri che limitano i dati contenuti in un report dopo che sono stati recuperati dalla connessione dati.  
  
-   Parametri. È possibile aggiungere un parametro o modificarne le opzioni. Ad esempio, è possibile specificare un valore predefinito per ogni parametro in modo da creare un piano di aggiornamento della cache per questo set di dati condiviso nel server di report.  
  
 I valori impostati diventano parte della definizione del set di dati condiviso nel server di report. Quando l'autore di un report include questo set di dati condiviso in un report, le opzioni specificate vengono applicate a quell'istanza del set di dati.  
  
 Dopo l'aggiunta di un set di dati condiviso a un report, l'autore di un report può eseguire l'override delle opzioni seguenti: regole di confronto, distinzione tra maiuscole e minuscole, distinzione tra caratteri accentati e non accentati, distinzione Kana, distinzione larghezza, subtotali. Può inoltre creare filtri dei set di dati aggiuntivi per limitare i dati nel report.  
  
 Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Per altre informazioni sui piani di aggiornamento della cache, vedere [Memorizzare nella cache set di dati condivisi &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md).  
  
### <a name="query-designer"></a>Progettazione query  
 Utilizzare la barra degli strumenti di Progettazione query per compilare una query che specifichi quali dati recuperare dalla connessione dati. La barra degli strumenti visualizzata dipende dalla finestra Progettazione query associata al tipo di origine dati della connessione dati.  
  
 Per altre informazioni, vedere l'argomento corrispondente al tipo di origine dati in [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md).  
  
  
##  <a name="DesignSurface"></a> Area di progettazione query  
 La finestra Progettazione query consente di compilare una query utilizzando la sintassi richiesta dall'origine dati esterna.  
  
 Per alcuni tipi di origini dati è disponibile una finestra Progettazione query con interfaccia grafica che è possibile utilizzare per esplorare i metadati in un'origine dati esterna. È possibile trascinare nomi in modo interattivo dal riquadro di metadati all'area di progettazione query o selezionare in modo interattivo i nomi da utilizzare.  
  
 Alcuni tipi di origine dati supportano una finestra Progettazione query basata su testo che è possibile usare per incollare query create in altri strumenti, ad esempio [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 A ogni tipo di origine dati sono associati requisiti specifici per la query che funzioneranno con l'origine dati esterna. Per altre informazioni, vedere l'argomento corrispondente al tipo di origine dati in [Aggiungere dati da origini dati esterne &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) e [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
  
##  <a name="Results"></a> Visualizzazione dei risultati di query  
 Nella visualizzazione di progettazione del set di dati condiviso viene compilata una query che recupererà dati dalla connessione dati al momento dell'elaborazione del report.  
  
 Eseguire la query per visualizzare dati di esempio dalla connessione dati, in modo da verificare che la query restituisca il tipo di dati previsto. Le colonne nel set di risultati appartengono ai metadati relativi agli schemi di dati dalla connessione dati. I nomi delle colonne diventano la raccolta di campi del set di dati. I valori dei dati visualizzati nel set di risultati della query rappresentano i dati della fase di progettazione. Dopo aver salvato il set di dati condiviso come definizione del set di dati condiviso nel server di report, verrà salvato solo il testo della query. I dati nel set di risultati della query non verranno salvati.  
  
 Quando l'autore di un report aggiunge questo set di dati condiviso a un report, viene aggiunto un puntatore alla definizione del set di dati presente nel server di report. Nel report la raccolta di campi del set di dati viene visualizzata nel riquadro dei dati del report. Il testo della query non è disponibile.  
  
 Le credenziali utilizzate per eseguire una query sono diverse dalle credenziali utilizzate per visualizzare in anteprima un report o eseguire un report dal server di report. Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
### <a name="running-a-report-with-parameters"></a>Esecuzione di un report con parametri  
 Quando la query include variabili, i parametri del set di dati vengono creati automaticamente. Quando si completa la compilazione della query del set di dati, vengono creati automaticamente i parametri del report impostati sui parametri del set di dati.  
  
 Se un report contiene parametri, prima che il report possa essere eseguito automaticamente, è necessario che per tutti i parametri siano presenti valori predefiniti. Se un parametro non ha un valore predefinito, quando si esegue il report è necessario scegliere un valore per il parametro e quindi fare clic su **Visualizza report** nella scheda **Esegui** .  
  
 Per altre informazioni, vedere [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Save"></a> Salvataggio del set di dati condiviso  
 Per salvare la query generata, sul pulsante **Generatore report** fare clic su **Salva** o su **Salva con nome**. Passare alla cartella appropriata sul server di report e salvare la definizione del set di dati condiviso. Il set di dati condiviso non sarà disponibile ad altri utenti finché non verrà salvato nel server di report.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
