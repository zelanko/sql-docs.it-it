---
title: Browser (Progettazione cubi) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.view.f1
ms.assetid: efb5ee1c-de50-4bfc-83ff-08a4f03c3ece
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 902d35dfc20973dbbad5e6608d5934b31245d9d2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174300"
---
# <a name="browser-cube-designer-analysis-services---multidimensional-data"></a>Esplorazione (Progettazione cubi) (Analysis Services - Dati multidimensionali)
  La scheda **Esplorazione** di Progettazione cubi consente di esplorare dimensioni, misure e indicatori KPI in un cubo. In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]il Visualizzatore cubi di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è stato integrato con Progettazione query MDX e fornisce interfacce utente grafiche per creare query MDX, filtrare e sezionare cubi ed eseguire il drill-down nelle gerarchie.

 Nella scheda **Esplorazione** sono disponibili due modalità, ovvero **Modalità progettazione** e **Modalità query**. In entrambe le modalità è possibile usare gli oggetti disponibili nel riquadro **Metadati** per esplorare il cubo oppure trascinare membri dal riquadro **Metadati** nell'area della query per compilare una query MDX per il recupero dei dati che si desidera usare.

 **Esplorazione e query tramite la modalità di progettazione grafica**

 Nella figura seguente viene illustrata l'interfaccia **Esplorazione** in **Modalità progettazione**di tipo grafico.

 ![Progettazione query MDX di Analysis Services, visualizzazione progettazione](media/rsqd-dsawas-mdx-designmode.gif "Progettazione query MDX di Analysis Services, visualizzazione progettazione")

 Quando si utilizza la modalità di progettazione grafica, se l'interruttore **esecuzione** automatica (![esecuzione automatica della query](media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")) sulla barra degli strumenti è selezionato, il **browser** esegue una query ogni volta che si rilascia un oggetto metadati nel riquadro dati. È anche possibile eseguire manualmente la query usando il pulsante **Esegui query** (![Esegui query](media/rsqdicon-run.gif "Eseguire la query")) sulla barra degli strumenti.

 Per modificare la finestra Progettazione query con interfaccia grafica attivando la modalità **Query** e usare il testo delle istruzioni MDX, fare clic sul pulsante **Modalità progettazione** sulla barra degli strumenti.

 **Esplorazione e query tramite la modalità testo MDX**

 Mentre è attiva la modalità di progettazione testo MDX, è possibile utilizzare direttamente MDX. Il riquadro **Metadati** è ancora disponibile, quindi è possibile aggiungere oggetti all'area di progettazione della query e trascinare funzioni e operatori MDX dall'elenco nel riquadro **Funzioni** .

 Nella figura seguente viene illustrata l'interfaccia **Esplorazione** per la Modalità query.

 ![Progettazione query MDX di Analysis Services, visualizzazione query](media/rsqd-dsawas-mdx-querymode.gif "Progettazione query MDX di Analysis Services, visualizzazione query")

 È possibile iniziare a utilizzare la modalità di progettazione grafica, aggiungere gli eventuali oggetti richiesti, aggiungere filtri per sezionare il cubo, quindi passare alla modalità testo per estendere la query MDX predefinita generata e includere proprietà del membro e proprietà di cella aggiuntive.

 Nel riquadro **Metadati** vengono visualizzate le schede relative a **Metadati** e **Funzioni**. Dalla scheda **Metadati** è possibile trascinare dimensioni, gerarchie, indicatori KPI e misure nell'area di progettazione della query. È possibile trascinare funzioni dalla scheda **Funzioni** nell'area di progettazione della query. Quando si esegue la query, nell'area di progettazione della query vengono visualizzati i risultati per la query MDX. È possibile anche fare clic su **Analizza in Excel** nella **barra degli strumenti** per esportare i dati in Microsoft Office Excel e visualizzare i risultati in una Tabella pivot come farebbero gli utenti in un PivotTable. Le sezioni seguenti descrivono più dettagliatamente la barra degli strumenti e tutti i riquadri per ogni modalità disponibile in **Esplorazione** .

 Si noti che, mentre si lavora in modalità testo, l'interruttore **esecuzione** automatica (![esecuzione automatica della query](media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")) sulla barra degli strumenti non è disponibile. È tuttavia possibile eseguire manualmente le query usando il pulsante **Esegui query** (![Esegui query](media/rsqdicon-run.gif "Eseguire la query")) sulla barra degli strumenti.

## <a name="sections"></a>Sezioni
 **Barra degli strumenti** La barra degli strumenti contiene lo strumento che può essere utilizzato nella visualizzazione progettazione o nella visualizzazione query. Per altre informazioni sulla barra degli strumenti e su come usare queste funzionalità, vedere [Barra degli strumenti &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services – Dati multidimensionali&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md).

 **Analizza in Excel** Utilizzare la funzionalità **analizza in Excel** per inviare la selezione corrente di dati del cubo a Excel, in modo che sia possibile visualizzare l'anteprima dei dati in una tabella pivot. La selezione di dati corrente è basata sugli elementi aggiunti dal riquadro **Metadati** e sugli eventuali filtri che possono essere stati definito tramite le funzioni di filtro e compilazione di query. Per altre informazioni, vedere [Analizza in Excel &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services - Dati multidimensionali&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md).

 **Metadati** di Utilizzare il riquadro **metadati** per visualizzare gli oggetti contenuti nel cubo, eseguire il drill-down nelle gerarchie ed esplorare e utilizzare le misure. Dopo avere effettuato la selezione, è possibile visualizzare i dati associati nel riquadro **Report**. Per altre informazioni su questo riquadro, vedere [Metadati &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services - Dati multidimensionali&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md).

 **Filtrare ed eseguire query** Utilizzare questa area dell'area di progettazione per compilare query MDX, trascinando e rilasciando oggetti dal riquadro **metadati** e specificando criteri di filtro per il cubo o la dimensione di origine. Per altre informazioni, vedere [Query e filtro &#40;scheda Esplorazione, Progettazione cubi&#41; &#40;Analysis Services - Dati multidimensionali&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md).

## <a name="see-also"></a>Vedi anche
 [Oggetti Cube &#40;Analysis Services-Dati multidimensionali&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md) [cubi in Progettazione cubi modelli multidimensionali](multidimensional-models/cubes-in-multidimensional-models.md) [&#40;Analysis Services-Dati multidimensionali&#41;](cube-designer-analysis-services-multidimensional-data.md)


