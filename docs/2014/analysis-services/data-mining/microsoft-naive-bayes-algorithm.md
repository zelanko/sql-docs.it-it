---
title: Algoritmo Microsoft Naive Bayes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Bayesian classifiers
- algorithms [data mining]
- predictive modeling [Analysis Services]
- classification algorithms [Analysis Services]
- naive bayes algorithms [Analysis Services]
ms.assetid: 3b53e011-3b1a-4cd1-bdc2-456768ba31b5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b1290e92ecd49a95f250574fb8778a8aa27eb2e2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083882"
---
# <a name="microsoft-naive-bayes-algorithm"></a>Algoritmo Microsoft Naive Bayes
  Il [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes è un algoritmo di classificazione basato su teoremi di Bayes e fornito da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per la modellazione predittiva. La parola naive nel nome Naive Bayes deriva dal fatto che nell'algoritmo vengono utilizzate tecniche di Bayes, ma non vengono considerate le dipendenze eventualmente presenti.  
  
 Questo algoritmo include funzionalità di calcolo più semplici di quelle di altri algoritmi [!INCLUDE[msCoName](../../includes/msconame-md.md)] ed è utile pertanto per generare rapidamente i modelli di data mining al fine di individuare le relazioni tra colonne di input e colonne stimabili. È possibile utilizzare questo algoritmo per eseguire l'esplorazione iniziale dei dati e applicare successivamente i risultati ottenuti per creare modelli di data mining aggiuntivi con altri algoritmi dotati di funzionalità di calcolo più avanzate e accurate.  
  
## <a name="example"></a>Esempio  
 Come strategia promozionale continuativa, il reparto marketing dell'azienda Adventure Works Cycle ha deciso di inviare volantini ai potenziali clienti mediante mailing diretto. Per ridurre i costi, i volantini verranno inviati solo ai clienti che probabilmente risponderanno. L'azienda archivia in un database le informazioni demografiche e relative alla risposta dei clienti a un mailing precedente. L'obiettivo è analizzare tali dati per scoprire in che modo è possibile utilizzare informazioni demografiche come l'età e il luogo di residenza per eseguire la stima relativa alla risposta a una promozione, confrontando i potenziali clienti con quelli che presentano caratteristiche analoghe e in passato hanno acquistato prodotti dell'azienda. In particolare, si intende esaminare le differenze tra i clienti che hanno acquistato una bicicletta e quelli che non l'hanno acquistata.  
  
 Tramite l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes, il reparto marketing può eseguire rapidamente la stima relativa al profilo di un cliente specifico e determinare quindi i clienti che, con maggiore probabilità, risponderanno ai volantini. Mediante il Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes disponibile in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], il reparto può inoltre individuare visivamente in modo specifico le colonne di input che contribuiscono alle risposte positive ai volantini.  
  
## <a name="how-the-algorithm-works"></a>Funzionamento dell'algoritmo  
 L'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes consente di calcolare la probabilità di ogni stato per ogni colonna di input, considerando ogni stato possibile della colonna stimabile.  
  
 Per comprendere questo funzionamento, utilizzare il Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] (come mostrato nel grafico seguente) per esplorare in modo visivo la distribuzione degli stati eseguita dall'algoritmo.  
  
 ![Naive bayes distribuzione degli stati](../media/naive-bayes.gif "Naive bayes distribuzione degli Stati")  
  
 Nel Visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes viene elencata ogni colonna di input nel set di dati e viene mostrata la distribuzione degli stati corrispondenti, considerando ogni stato della colonna stimabile.  
  
 Questa vista del modello consente di identificare le colonne di input significative ai fini della differenziazione degli stati della colonna stimabile.  
  
 Ad esempio, nella riga per Distanza dal lavoro qui indicata, la distribuzione dei valori di input è visibilmente diversa per gli acquirenti rispetto ai non acquirenti. Questo indica che l'input, Distanza dal lavoro = 0-1 chilometri, è un potenziale criterio di stima.  
  
 Il visualizzatore fornisce inoltre valori per le distribuzioni, pertanto è possibile visualizzare che, per i clienti che risiedono a una distanza dal posto di lavoro compresa tra uno e due chilometri, la probabilità che acquistino una bicicletta è pari a 0,387, mentre la probabilità che non effettuino tale acquisto è pari a 0,287. In questo esempio nell'algoritmo vengono utilizzate le informazioni numeriche derivate da caratteristiche del cliente, ad esempio la distanza dal posto di lavoro, per stimare se il cliente acquisterà una bicicletta.  
  
 Per altre informazioni sull'uso del visualizzatore [!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes, vedere [Visualizzare un modello utilizzando il Visualizzatore Microsoft Naive Bayes](browse-a-model-using-the-microsoft-naive-bayes-viewer.md).  
  
## <a name="data-required-for-naive-bayes-models"></a>Dati necessari per i modelli Naive Bayes  
 Quando si preparano i dati da utilizzare per il training di un modello Naive Bayes, verificare che siano chiari i requisiti dell'algoritmo, tra cui la quantità di dati necessari e la modalità di utilizzo dei dati.  
  
 I requisiti di un modello Naive Bayes sono i seguenti:  
  
-   **Una colonna a chiave singola** Ogni modello deve contenere una colonna numerica o di testo che identifichi in modo univoco ogni record. Le chiavi composte non sono consentite.  
  
-   **Colonne di input** In un modello Naive Bayes, tutte le colonne devono essere discrete o discretizzate colonne. Per informazioni sulla discretizzazione delle colonne, vedere [metodi di discretizzazione &#40;Data Mining&#41;](discretization-methods-data-mining.md).  
  
     Per un modello Naive Bayes, è importante verificare inoltre che gli attributi di input siano indipendenti uno dall'altro. Questo aspetto è particolarmente importante quando si utilizza il modello per la stima.  
  
     Il motivo è dovuto al fatto che l'utilizzo di due colonne di dati già strettamente correlati comporterebbe un'influenza ancora maggiore di tali colonne e verrebbero pertanto messi in secondo piano gli altri fattori che influiscono sul risultato.  
  
     Viceversa, la possibilità dell'algoritmo di identificare le correlazioni fra variabili è utile quando si esplora un modello o un set di dati, per identificare le relazioni fra input.  
  
-   **Almeno una colonna stimabile** Nell'attributo stimabile devono essere contenuti valori discreti o discretizzati.  
  
     I valori della colonna stimabile possono essere utilizzati come input. Ciò può essere utile quando si esplora un nuovo set di dati, per trovare le relazioni fra le colonne.  
  
## <a name="viewing-the-model"></a>Visualizzazione del modello  
 Per esplorare il modello, è possibile usare il **Visualizzatore Microsoft Naive Bayes**. Nel visualizzatore viene illustrato il modo in cui gli attributi di input sono correlati all'attributo stimabile. Nel visualizzatore viene inoltre fornito un profilo dettagliato di ogni cluster, un elenco degli attributi che consentono di distinguere ogni cluster dagli altri e le caratteristiche dell'intero set di dati di training. Per altre informazioni, vedere [Visualizzare un modello utilizzando il Visualizzatore Microsoft Naive Bayes](browse-a-model-using-the-microsoft-naive-bayes-viewer.md).  
  
 Per maggiori dettagli, è possibile esplorare il modello in [Microsoft Generic Content Tree Viewer &#40;Data Mining&#41;](../microsoft-generic-content-tree-viewer-data-mining.md). Per altre informazioni sul tipo di informazioni archiviate nel modello, vedere [Contenuto dei modelli di data mining per i modelli Naive Bayes &#40;Analysis Services - Data mining&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md).  
  
## <a name="making-predictions"></a>Esecuzione di stime  
 In seguito al training del modello, i risultati vengono archiviati come set di modelli, esplorabili o utilizzabili per eseguire stime.  
  
 È possibile creare query per restituire stime sul modo in cui i nuovi dati sono correlati all'attributo stimabile oppure recuperare statistiche che descrivono le correlazioni rilevate dal modello.  
  
 Per informazioni sulla creazione di query in base a un modello di data mining, vedere [Query di data mining](data-mining-queries.md). Per esempi di come usare le query con un modello Naive Bayes, vedere [Esempi di query sul modello Naive Bayes](naive-bayes-model-query-examples.md).  
  
## <a name="remarks"></a>Note  
  
-   Supporta l'utilizzo del linguaggio PMML (Predictive Model Markup Language) per la creazione di modelli di data mining.  
  
-   Supporta il drill-through.  
  
-   Non supporta la creazione di dimensioni di data mining.  
  
-   Supporta l'utilizzo di modelli di data mining OLAP.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Selezione delle caratteristica &#40;Data mining&#41;](feature-selection-data-mining.md)   
 [Esempi di query sul modello Naive Bayes](naive-bayes-model-query-examples.md)   
 [Contenuto dei modelli di data mining per i modelli Naive Bayes &#40;Analysis Services - Data mining&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Naive Bayes](microsoft-naive-bayes-algorithm-technical-reference.md)  
  
  
