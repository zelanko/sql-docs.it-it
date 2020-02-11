---
title: Creazione guidata cluster (componenti aggiuntivi Data mining per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [data mining]
ms.assetid: 85b25625-a7ab-4960-9f9c-df22e8ecae37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d93f676aec67b5d791924cbbda8f71a966d5bbc2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087806"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>Procedura guidata Cluster (componenti aggiuntivi Data mining per Excel)
  ![Procedura guidata Cluster sulla barra multifunzione Data mining](media/dmc-cluster.gif "Procedura guidata Cluster sulla barra multifunzione Data mining")  
  
 La procedura guidata Cluster consente di compilare un modello che rileva le righe che condividono gruppi e caratteristiche simili per ottimizzare la distanza tra i gruppi. Questa procedura guidata è utile per trovare i modelli in qualsiasi tipo di dati.  
  
 La procedura guidata Cluster utilizza l'algoritmo Microsoft Clustering e può essere ampiamente personalizzata. Utilizza i dati esistenti di una tabella di Excel, un intervallo di Excel o una query di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Funzionalità simili sono fornite dallo strumento [Rileva categorie](detect-categories-table-analysis-tools-for-excel.md) , disponibile in strumenti di analisi tabelle per Excel. Tuttavia, lo strumento Rileva categorie non può essere personalizzato e deve utilizzare i dati nelle tabelle di Excel.  
  
## <a name="using-the-cluster-wizard"></a>Utilizzo della procedura guidata Cluster  
  
1.  Sulla barra multifunzione data mining fare clic su **cluster**, quindi su **Avanti**.  
  
2.  Nella pagina **selezione dati di origine** selezionare una tabella o un intervallo di Excel. Oppure specificare un'origine dati esterna.  
  
     Se si utilizza un'origine dati esterna, è possibile creare viste personalizzate o incollarle nel testo della query personalizzata e salvare il set di dati come origine dati di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Nella pagina **clustering** è possibile personalizzare la modalità di compilazione del modello.  
  
    -   Per **numero di segmenti**, è possibile indicare alla procedura guidata di creare un numero fisso di categorie o lasciare che venga rilevato automaticamente il numero ottimale di raggruppamenti.  
  
    -   Esaminare l'elenco delle colonne nell'elenco **colonne di input** e deselezionare le colonne che non sono utili per la creazione di modelli. Le colonne che è necessario escludere includono numeri ID, nomi di clienti e così via.  
  
4.  Facoltativamente, fare clic su **parametri** per modificare i parametri dell'algoritmo e personalizzare il comportamento del modello di clustering.  
  
5.  Nella pagina **suddivisione dei dati in set di training e di testing** specificare la quantità di dati da mantenere per il test. Il resto viene sempre utilizzato per il training del modello.  
  
     L'impostazione predefinita è il 30% dei dati di testing e il 70% dei dati di training.  
  
6.  Nella pagina **fine** specificare un nome descrittivo per il set di dati e il modello, quindi impostare le opzioni seguenti che consentono di controllare la modalità di utilizzo del modello finito:  
  
    -   **Esplora modello**. Quando questa opzione è selezionata, non appena viene completata l'elaborazione del modello da parte della procedura guidata, viene aperta una finestra **Esplora** che consente di esplorare i risultati. Il contenuto del visualizzatore dipende dal tipo di modello compilato. Per ulteriori informazioni, vedere [esplorazione di un modello di clustering](browsing-a-clustering-model.md).  
  
    -   **Abilitare il drill-through**. Selezionare questa opzione per visualizzare i dati sottostanti dal modello finito. Questa opzione è disponibile solo se si compila un modello Decision Trees.  
  
    -   **Usa modello temporaneo**. Se si seleziona questa opzione, il modello non verrà salvato nel server. I modelli temporanei vengono eliminati quando si chiude Excel.  
  
## <a name="more-about-clustering-models"></a>Ulteriori informazioni sui modelli di clustering  
 È possibile modificare l'algoritmo di clustering utilizzato da questa procedura guidata facendo clic su **Avanzate** e utilizzando la finestra di dialogo **parametri algoritmo** .  
  
 L'algoritmo Microsoft Clustering fornisce i metodi di clustering seguenti:  
  
-   K-medie, scalabile o non scalabile.  
  
-   Expectation Maximization (EM), scalabile o non scalabile.  
  
 È anche possibile utilizzare il parametro CLUSTER_SEED per controllare il valore iniziale e assicurarsi che i modelli ripetuti che utilizzano lo stesso set di dati producano gli stessi risultati.  
  
### <a name="requirements"></a>Requisiti  
 Per utilizzare la procedura guidata Cluster, è necessario essere connessi a un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per ulteriori informazioni, vedere [connettersi ai dati di origine &#40;client di data mining per&#41;Excel ](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un modello di data mining](creating-a-data-mining-model.md)   
 [Rilevare le categorie &#40;strumenti di analisi tabelle per Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
