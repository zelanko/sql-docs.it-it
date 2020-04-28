---
title: Informazioni sui requisiti per un modello Time Series (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1ce2b3e3-108a-4f7e-985f-a20b816d0da7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8e46d7fc8a0c214501841de448a94d1211b95fa1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892965"
---
# <a name="understanding-the-requirements-for-a-time-series-model-intermediate-data-mining-tutorial"></a>Informazioni sui requisiti per un modello Time Series (Esercitazione intermedia sul data mining)
  Quando si preparano i dati per l'utilizzo in un modello di previsione, è necessario assicurarsi che i dati contengano una colonna che possa essere utilizzata per identificare i passaggi nella serie temporale. Tale colonna sarà designata come colonna `Key Time`. Essendo una chiave, nella colonna devono essere contenuti valori univoci.  
  
 La scelta dell'unità corretta per la colonna `Key Time` è una parte importante dell'analisi. Si supponga ad esempio che i dati di vendita vengano aggiornati una volta al minuto. Non è necessario utilizzare minuti come unità per la serie temporale. Potrebbe invece risultare più significativo eseguire il rollup dei dati di vendita per giorno, settimana o persino per mese. Se non si è certi di quale unità di tempo utilizzare, è possibile creare una nuova vista origine dati per ogni aggregazione e compilare i modelli correlati per verificare se emergono tendenze diverse a ogni livello di aggregazione.  
  
 Per questa esercitazione, i dati di vendita vengono raccolti su base giornaliera nel database transazionale delle vendite, ma ai fini del data mining i dati sono stati preaggregati per mese utilizzando una vista.  
  
 È inoltre auspicabile che nei dati utilizzati per l'analisi sia presente il minor numero di gap possibile. Se si prevede di analizzare più serie di dati, è preferibile che tutte le serie inizino e terminino nella stessa data. Se nei dati sono presenti gap, ma questi non si trovano all'inizio o alla fine di una serie, è possibile utilizzare il parametro MISSING_VALUE_SUBSTITUTION per riempire la serie. In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sono inoltre disponibili diverse opzioni per sostituire i dati mancanti con valori, ad esempio utilizzando medie o costanti.  
  
> [!WARNING]  
>  Gli strumenti Grafico pivot e Tabella pivot inclusi nelle versioni precedenti della finestra di progettazione Vista origine dati non vengono più forniti. È consigliabile identificare in anticipo i gap nei dati della serie temporale utilizzando strumenti come Profiler dati incluso in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
### <a name="to-identify-the-time-key-for-the-forecasting-model"></a>Per identificare la chiave temporale per il modello di previsione  
  
1.  Nel riquadro **SalesByRegion. dsv [Progettazione]** fare clic con il pulsante destro del mouse sulla tabella vTimeSeries, quindi scegliere **Esplora dati**.  
  
     Viene visualizzata una nuova scheda denominata **Explore VTimeSeries Table**.  
  
2.  Nella scheda **tabella** esaminare i dati utilizzati nelle colonne TimeIndex e Reporting Date.  
  
     Sono entrambe sequenze con valori univoci ed entrambe possono essere utilizzate come chiave di serie temporale. I tipi di dati delle colonne sono tuttavia diversi. L'algoritmo Microsoft Time Series non richiede un tipo di dati `datetime`, ma solo che i valori siano distinti e ordinati. Pertanto, qualsiasi colonna può essere utilizzata come chiave temporale per il modello di previsione.  
  
3.  Nell'area di progettazione della vista origine dati selezionare la colonna report data e selezionare **Proprietà**. Fare quindi clic sulla colonna TimeIndex e selezionare **Proprietà**.  
  
     Il campo TimeIndex dispone del tipo di dati System. Int32, mentre la data di segnalazione dei campi ha il tipo di dati System. DateTime. Molti data warehouse convertono i valori data/ora in Integer e utilizzano la colonna Integer come chiave, per migliorare le prestazioni di indicizzazione. Se tuttavia si utilizza questa colonna, le stime verranno eseguite dall'algoritmo Microsoft Time Series utilizzando valori futuri, ad esempio 201014, 201014 e così via. Poiché si desidera rappresentare la previsione dei dati sulle vendite tramite date del calendario, sarà possibile utilizzare la colonna Reporting Date come identificatore univoco della serie.  
  
### <a name="to-set-the-key-in-the-data-source-view"></a>Per impostare la chiave nella vista origine dati  
  
1.  Nel riquadro **SalesByRegion. DSV**selezionare la tabella vTimeSeries.  
  
2.  Fare clic con il pulsante destro del mouse sulla colonna Reporting Date, quindi scegliere **Imposta chiave primaria logica**.  
  
## <a name="handling-missing-data-optional"></a>Gestione di dati mancanti (facoltativo)  
 Se in una serie mancano alcuni dati, è possibile che venga visualizzato un errore quando si tenta di elaborare il modello. Esistono diversi modi per risolvere il problema relativo ai dati mancanti:  
  
-   È possibile lasciare che Analysis Services riempia i valori mancanti, calcolando una media o utilizzando un valore precedente. A tale scopo, impostare il parametro MISSING_VALUE_SUBSTITUTION nel modello di data mining. Per ulteriori informazioni su questo parametro, vedere [riferimento tecnico per l'algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md). Per informazioni su come modificare i parametri in un modello di data mining esistente, vedere [visualizzare o modificare i parametri dell'algoritmo](../../2014/analysis-services/data-mining/view-or-change-algorithm-parameters.md).  
  
-   È possibile modificare l'origine dati o filtrare la vista sottostante per eliminare la serie incomplete o sostituire valori. È possibile eseguire questa operazione nell'origine dati relazionale oppure modificare la vista origine dati creando query denominate personalizzate o calcoli denominati. Per altre informazioni, vedere [Viste origine dati in modelli multidimensionali](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models). Un'attività successiva in questa lezione fornisce un esempio di come compilare una query denominata e un calcolo personalizzato.  
  
 Per questo scenario mancano alcuni dati all'inizio di una serie, ovvero non sono presenti dati per la linea di prodotti T1000 fino a luglio 2007. Diversamente tutte le serie terminano nella stessa data e non vi sono valori mancanti.  
  
 Il requisito dell'algoritmo Microsoft Time Series è che le serie incluse in un singolo modello devono avere lo stesso punto **finale** . Poiché il modello di bicicletta T1000 è stato introdotto nel 2007, i dati per questa serie iniziano più tardi rispetto agli altri modelli di bicicletta, ma la serie termina nella stessa data. I dati sono pertanto accettabili.  
  
#### <a name="to-close-the-data-source-view-designer"></a>Per chiudere Progettazione vista origine dati  
  
-   Fare clic con il pulsante destro del mouse sulla scheda, **esplorare la tabella vTimeSeries**e selezionare **Chiudi**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creazione di una struttura e di un modello di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
