---
title: Confronto delle stime per i modelli di previsione (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ead8a1fe-60d8-4017-8fb8-6fe32168e46d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 26cc445d3bad5c628628353d5c0c84ffa4755e97
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63066336"
---
# <a name="comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial"></a>Confronto delle stime per i modelli di previsione (Esercitazione intermedia sul data mining)
  Nei passaggi precedenti di questa esercitazione sono stati creati più modelli Time Series:  
  
-   Stime per ogni combinazione di area e modello, basate solo sui dati per il singolo modello e l'area.  
  
-   Stime per ogni area, basate sui dati aggiornati.  
  
-   Stime per tutti i modelli su scala mondiale, basate sui dati aggregati.  
  
-   Stime per il modello M200 nell'area dell'America del nord, basate sul modello aggregato.  
  
 Per riepilogare le funzionalità per le stime basate su serie temporali, si rivedranno le modifiche per verificare in che modo l'utilizzo delle opzioni per estendere o sostituire dati hanno influito sui risultati della previsione.  
  
 [EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
##  <a name="comparing-the-original-results-with-results-after-adding-data"></a><a name="bkmk_EXTEND"></a>Confronto dei risultati originali con i risultati dopo l'aggiunta di dati  
 Esaminiamo i dati solo per la linea di prodotti M200 nell'area del Pacifico, per vedere in che modo l'aggiornamento del modello con i nuovi dati influiscono sui risultati. Si tenga presente che le serie dei dati originali terminano a giugno 2004 e sono stati ottenuti nuovi dati per i mesi di luglio, agosto e settembre.  
  
-   Nella prima colonna sono riportati i nuovi dati aggiunti.  
  
-   Nella seconda colonna è riportata la previsione per luglio e i mesi successivi in base alla serie di dati originali.  
  
-   Nella terza colonna è riportata la previsione basata sui dati estesi.  
  
|**M200 Pacific**|Dati di vendita reali aggiornati|Previsione prima dell'aggiunta di dati|Stima estesa|  
|----------------------|-----------------------------|------------------------------------|-------------------------|  
|7-25-2008|**65**|32|**65**|  
|8-25-2008|**54**|37|**54**|  
|9-25-2008|**61**|32|**61**|  
|10-25-2008|Nessun dato|36|32|  
|11-25-2008|Nessun dato|31|41|  
|12-25-2008|Nessun dato|34|32|  
  
 Si noterà che le previsioni che utilizzando i dati estesi, visualizzati in grassetto, ripetono esattamente i punti dati reali. La ripetizione avviene per motivi strutturali. Finché sono presenti punti dati reali da utilizzare, la query di stima restituirà i valori effettivi e genererà nuovi valori di stima solo dopo avere utilizzato i nuovi punti dati effettivi.  
  
 In generale l'algoritmo pondera le modifiche nei nuovi dati in modo più attendibile rispetto ai dati dall'inizio dei dati del modello. In questo caso, tuttavia, le nuove cifre di vendita rappresentano un aumento solo del 20-30% rispetto al periodo precedente, pertanto l'impatto sulle vendite stimate risulta minimo, dopo di che le proiezioni di vendita diminuiscono di nuovo, maggiormente in linea con la tendenza nei mesi prima dei nuovi dati.  
  
##  <a name="comparing-the-original-and-cross-prediction-results"></a><a name="bkmk_REPLACE"></a>Confronto tra risultati di stima originali e incrociati  
 Si tenga presente che il modello di data mining originale ha rivelato notevoli differenze tra le aree e tra le linee di prodotti. Ad esempio, le vendite per il modello M200 sono state particolarmente elevate, mentre quelle per il modello T1000 sono state piuttosto basse in tutte le aree. Inoltre, alcune serie non hanno molti dati. Le serie erano incomplete, ovvero non hanno lo stesso punto di partenza.  
  
 ![Serie per la stima delle quantità M200 e T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "Serie per la stima delle quantità M200 e T1000")  
  
 È quindi opportuno verificare in che modo vengono modificate le stime quando si eseguono in base al modello generale, che era basato sulle vendite mondiali, piuttosto che sui set di dati originali. Per assicurarsi di non aver perso alcuna informazione o distorto le stime, è possibile salvare i risultati in una tabella, unire in join la tabella delle stime alla tabella dei dati cronologici, quindi tracciare i due set di dati cronologici e stime.  
  
 Il diagramma seguente è basato su una sola linea di prodotti, M200. Nel grafico vengono confrontate le stime dal modello di data mining iniziale rispetto alle stime tramite il modello di data mining aggregato.  
  
 ![Grafico di Excel che confronta stime](../../2014/tutorials/media/m200-predictions-compared.gif "Grafico di Excel che confronta stime")  
  
 Da questo grafico è possibile osservare che il modello di data mining aggregato mantiene complessivamente l'intervallo e le tendenze dei valori riducendo però al minimo le fluttuazioni nella singola serie di dati.  
  
## <a name="conclusion"></a>Conclusioni  
 È stato descritto come creare e personalizzare un modello Time Series che può essere utilizzato per la stima.  
  
 Si è appreso come aggiornare i modelli Time Series senza doverli rielaborare, aggiungendo nuovi dati e creando stime con il parametro EXTEND_MODEL_CASES.  
  
 È stato descritto come creare modelli che possono essere utilizzati per stima incrociata tramite il parametro REPLACE_MODEL_CASES e applicando il modello a una serie di dati diversa.  
  
## <a name="see-also"></a>Vedi anche  
 [Esercitazione intermedia sul data mining &#40;Analysis Services-&#41;di data mining](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Time Series Model Query Examples](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
