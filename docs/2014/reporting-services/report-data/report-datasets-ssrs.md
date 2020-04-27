---
title: Aggiungere dati a un report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f2e42303-e355-4c1f-bb3b-3338fbdd230d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 019ca09c83b0b3011e9940d9a4c988ce223e192f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107116"
---
# <a name="add-data-to-a-report-report-builder-and-ssrs"></a>Aggiungere dati a un report (Generatore report e SSRS)
  Per aggiungere dati a un rapporto, è necessario creare set di dati. Ogni set di dati rappresenta il set di risultati dall'esecuzione di un comando di query su un'origine dati. Le colonne del set di risultati sono la raccolta di campi. Le righe del set di risultati sono i dati. Un set di dati non contiene i dati effettivi. Un set di dati contiene le informazioni necessarie per recuperare un set di dati specifico da un'origine dati.  
  
 Esistono due tipi di set di dati: incorporato e condiviso. Un set di dati incorporato viene definito in un report e viene usato solo dal report specifico. Un set di dati condiviso viene definito sul server di report o un sito di SharePoint e può essere usato da più report. In Generatore report è possibile creare set di dati condivisi in modalità Set di dati condiviso oppure set di dati incorporati in modalità Progettazione report. In Progettazione report in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]è possibile creare set di dati condivisi come parte di un progetto oppure set di dati incorporati come parte di un report.  
  
-   **Set di dati incorporati.** A differenza di applicazioni quali [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel dove si lavora con i dati direttamente in un foglio di lavoro, in Generatore report o Progettazione report si lavora con metadati che rappresentano i dati che verranno recuperati durante l'elaborazione del report. Per creare un set di dati incorporato, selezionare l'origine dati condivisa e specificare una query. Dopo avere creato un set di dati, usare il riquadro dei dati del report per visualizzare la raccolta di campi. È possibile visualizzare i dati di un set di dati in un'area dati quale una tabella o un grafico. In ogni area dati è possibile raggruppare, filtrare e ordinare i dati per organizzarli. Dopo avere progettato il layout del report, eseguire il report per visualizzare i dati effettivi.  
  
     Nel riquadro dei dati del report riportato nella figura seguente vengono visualizzati un'origine dati denominata [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)], un set di dati denominato DataSet1 e cinque campi nella raccolta di campi del set di dati. Nel riquadro Layout viene visualizzata una tabella con la riga superiore di intestazioni di colonna e la riga inferiore con celle della tabella contenenti testo. Il testo segnaposto [Name] indica i metadati per il campo Nome. Durante l'esecuzione del report, il testo segnaposto viene sostituito dai valori dei dati effettivi. La tabella può essere espansa in base alle esigenze per visualizzare tutti i dati.  
  
     ![rs_DataDesignandPreview](../media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  
  
-   **Set di dati condivisi.** Creare un set di dati condiviso quando si vuole usare un set di dati in più report. Per creare un set di dati condiviso e salvarlo in un server di report o in un sito di SharePoint, usare Generatore report in una visualizzazione di progettazione del set di dati condiviso. Per creare un set di dati condiviso come parte di un progetto che può essere distribuito su un server o su un sito, usare Progettazione report.  
  
     Nella figura seguente è illustrata una visualizzazione di progettazione set di dati condiviso in Generatore report. È possibile selezionare o modificare la connessione dati, le proprietà del set di dati, la query, i filtri, e facoltativamente contrassegnare i filtri come parametri, nonché visualizzare i risultati della query. Le modifiche vengono quindi salvate nel server o nel sito.  
  
     ![rs_SharedDatasetDesignMode](../media/rs-shareddatasetdesignmode.gif "rs_SharedDatasetDesignMode")  
  
 Per altre informazioni, vedere [Set di dati condivisi e incorporati &#40;Generatore report e SSRS&#41;](embedded-and-shared-datasets-report-builder-and-ssrs.md) e [Connessioni dati o origini dati condivise e incorporate &#40;Generatore report 3.0 e SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md).  
  
 È inoltre possibile aggiungere set di dati a un report aggiungendo parti del report che includono i set di dati da cui dipendono. [!INCLUDE[ssRBrptparts](../../../includes/ssrbrptparts-md.md)]  
  
 Per informazioni su come creare un report in cui sono visualizzati i dati di un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Esercitazione: Creazione di un report tabella semplice &#40;Generatore report&#41;](../tutorial-creating-a-basic-table-report-report-builder.md). Per creare un report comprendente i propri dati, vedere [Esercitazione: Creare un report grafico rapido offline &#40;Generatore report&#41;](../report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="adding-report-data"></a><a name="Methods"></a> Aggiunta di dati del report  
 In Generatore report è possibile aggiungere dati del report nei modi seguenti.  
  
-   Aggiungendo parti di report da un server di report al report. Ogni parte di report è autonoma e consente di includere set di dati dipendenti. I set di dati sono predefiniti.  
  
-   Utilizzando le procedure guidate per la creazione di tabelle, matrici, grafici e mappe. Dalle procedure guidate è possibile selezionare origini dati condivise e set di dati condivisi o creare nuovi set di dati continuando la progettazione del report.  
  
-   Aggiungendo set di dati condivisi da un server di report. I set di dati condivisi sono predefiniti e consentono di specificare quali dati usare da un'origine dati predefinita. Quando si aggiunge un set di dati condiviso al report in uso, viene aggiunto un riferimento del set di dati che punta alla definizione del set di dati condiviso.  
  
 In Generatore report o Progettazione report è possibile aggiungere dati del report nei modi seguenti.  
  
-   Aggiungendo set di dati incorporati basati su origini dati condivise.  
  
-   Aggiungendo set di dati incorporati basati su origini dati incorporate.  
  
> [!NOTE]  
>  In un server di report, gli elementi condivisi sono protetti singolarmente o ereditando autorizzazioni dalla cartella in cui sono pubblicati. Per consentire ad altri utenti di avere accesso ai set di dati condivisi che sono stati salvati, è necessario comprendere il modo in cui vengono concesse le autorizzazioni. Per altre informazioni, vedere [Sicurezza &#40;Generatore report&#41;](../report-builder/security-report-builder.md) o [Proteggere gli elementi del set di dati condiviso](../security/secure-shared-dataset-items.md).  
  
 Dopo avere aggiunto dati a un report, è possibile organizzare i dati nella pagina del report con le aree dati, modificare le parti di report, condividendo tali modifiche con altri utenti, e consentire agli utenti di limitare od ordinare i dati che visualizzano nel report. Per altre informazioni, vedere i seguenti argomenti correlati:  
  
-   [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
-   [Grafici &#40;Generatore report e SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
-   [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
-   [Indicatori &#40;Generatore report e SSRS&#41;](../report-design/indicators-report-builder-and-ssrs.md)  
  
-   [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [Parti del report &#40;Generatore report e SSRS&#41;](../report-parts-report-builder-and-ssrs.md)  
  
-   [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  

##  <a name="adding-data-with-report-parts"></a><a name="QuickStart"></a> Aggiunta di dati con parti di report  
 Nelle parti di report sono contenuti i set di dati dai quali dipendono. Questi set di dati vengono creati in base alle origini dati condivise disponibili nel server di report. In Generatore report, quando si aggiunge una parte di report al report in uso, i set di dati dipendenti vengono aggiunti al report come se fossero stati aggiunti manualmente. Ad esempio, in un grafico predefinito è contenuto un set di dati. Per vedere i dati, visualizzare l'anteprima del report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBrptparts](../../../includes/ssrbrptparts-md.md)]  
  
 Le parti del report, le origini dati condivise e i set di dati condivisi sono definiti in precedenza e salvati in un server di report. Per accedere ad essi, è necessario aprire Generatore report in modalità server connettendosi al server di report. Tutti questi elementi possono essere usati per creare nuove versioni personalizzate, se si dispone di autorizzazioni di scrittura per il server di report.  
  
-   Per altre informazioni, vedere [Parti del report &#40;Generatore report e SSRS&#41;](../report-parts-report-builder-and-ssrs.md) e [Parti del report in Progettazione report &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).  

##  <a name="queries-and-query-designers"></a><a name="Queries"></a> Query e Progettazione query  
 Per specificare i dati desiderati da un'origine dati, è necessario compilare un comando di query. Per ciascun tipo di origine dati, è disponibile una finestra *Progettazione query* correlata che consente di compilare la query. che può essere basata sull'interfaccia grafica o su testo. In una finestra Progettazione query con interfaccia grafica, vengono visualizzati i metadati che rappresentano i dati nell'origine dati esterna ed è possibile compilare in modo interattivo una query trascinando campi o entità nell'area di progettazione della query. In una Progettazione query basata su testo, si scrivono o importano query nella sintassi della query supportata dall'origine dati esterna.  
  
 Nella Progettazione query, è possibile eseguire la query per visualizzare i dati di esempio e convalidare la sintassi del comando di query. I nomi di colonna nel set di risultati diventano i nomi campo visualizzati nel riquadro dei dati del report. Il set di risultati deve essere un singolo set di righe e colonne in cui esiste lo stesso numero di valori per ogni riga di dati. Non sono supportati più set di risultati di una singola query. Non sono supportate le gerarchie incomplete che non dispongono di un numero costante di colonne e che possono produrre un numero diverso di valori dei dati per ogni riga.  
  
 Per eseguire una query, è necessario disporre di credenziali per la fase di progettazione. Per ulteriori informazioni, vedere [specificare le credenziali in Generatore report](../specify-credentials-in-report-builder.md) e [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Le comunicazioni tra un'estensione per i dati e l'origine dati esterna sono gestite dai provider di dati. Il supporto per la sintassi del comando di query, per i parametri query e per i tipi di dati per i valori nel set di risultati è determinato da ogni provider di dati. Per altre informazioni, vedere l'argomento relativo al tipo specifico di estensione per dati e [Finestre di progettazione query &#40;Generatore report&#41;](../query-designers-report-builder.md).  

##  <a name="how-to-topics"></a><a name="HowTo"></a> Procedure  
 [Aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Aggiunta, modifica e aggiornamento di campi nel riquadro dei dati del report &#40;Generatore report e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
 [Compilare una query in Progettazione query relazionale &#40;Generatore report e SSRS&#41;](build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)  
  
 [Visualizzare set di dati nascosti per i valori dei parametri di dati multidimensionali &#40;Generatore report e SSRS&#41;](show-hidden-datasets-for-parameter-values-multidimensional-data.md)  
  
 [Aggiungere un filtro a un set di dati &#40;Generatore report e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 [Impostare una proprietà NoDataMessage per un'area dati &#40;Generatore report e SSRS&#41;](set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [Associazione di un parametro di query a un parametro di report &#40;Generatore report e SSRS&#41;](associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md)  
  
 [Definizione dei parametri in Progettazione query MDX per Analysis Services &#40;Generatore report e SSRS&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md)  

##  <a name="in-this-section"></a><a name="Section"></a> Contenuto della sezione  
 [Parti del report e set di dati in Generatore report](report-parts-and-datasets-in-report-builder.md)  
  
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
 [Specifica di credenziali in Generatore report](../specify-credentials-in-report-builder.md)  
  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  

## <a name="see-also"></a>Vedere anche  
 [Visualizzazione di progettazione report &#40;Generatore report&#41;](../report-builder/report-design-view-report-builder.md)   
 [Concetti relativi alla creazione di report &#40;Generatore report e SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
