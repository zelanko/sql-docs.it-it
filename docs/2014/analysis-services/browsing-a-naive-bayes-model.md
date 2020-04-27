---
title: Esplorazione di un modello Naive Bayes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f9160b48-3beb-439c-9694-f084e1afa625
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65b8bb26a72903644b5985d69efc8adb362fe412
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088475"
---
# <a name="browsing-a-naive-bayes-model"></a>Esplorazione di un modello Naïve Bayes
  Quando si apre un modello Naive Bayes utilizzando **Sfoglia**, il modello viene visualizzato in un visualizzatore interattivo con quattro riquadri diversi. Il visualizzatore consente di esplorare le correlazioni e ottenere informazioni sul modello e sui dati sottostanti.  
  
-   [Rete di dipendenze](#bkmk_DepNet)  
  
-   [Profili attributo](#bkmk_AttProf)  
  
-   [Caratteristiche attributo](#bkmk_AttChar)  
  
-   [Analisi discriminante attributi](#bkmk_AttDisc)  
  
##  <a name="explore-the-model"></a><a name="BKMK_Tabs"></a>Esplorare il modello  
 Lo scopo del visualizzatore è consentire di esplorare l'interazione tra gli attributi di input e output (input e variabili dipendenti) che sono stati individuati dal modello [!INCLUDE[msCoName](../includes/msconame-md.md)] Naïve Bayes.  
  
 Se si desidera provare il Visualizzatore Naive Bayes, utilizzare la [procedura guidata classificazione &#40;componenti aggiuntivi Data mining per&#41;](classify-wizard-data-mining-add-ins-for-excel.md) guidata di Excel sulla barra multifunzione data mining, fare clic sull'opzione **Avanzate** e modificare l'algoritmo in modo da utilizzare l'algoritmo Naive Bayes.  
  
 Per questi esempi, sono stati usati i dati di origine nella cartella di lavoro di esempio e la colonna **Yearly Income**è stata raggruppata in cinque gruppi di reddito, da **molto bassa** a **molto alta**. Nel modello Naïve Bayes sono stati quindi analizzati i fattori correlati a ogni categoria di reddito.  
  
###  <a name="dependency-network"></a><a name="bkmk_DepNet"></a>Rete di dipendenze  
 La prima finestra che verrà usata è la **rete di dipendenze**. Vengono visualizzati immediatamente gli input strettamente correlati al risultato selezionato.  
  
 ![Rete di dipendenze in Visualizzatore Naive Bayes](media/dm13-nb.gif "Rete di dipendenze in Visualizzatore Naive Bayes")  
  
##### <a name="explore-the-dependency-network"></a>Esplorare la rete di dipendenze  
  
1.  Innanzitutto, fare clic sul risultato di destinazione, **yearly**Income, che è rappresentato come un nodo nel grafico.  
  
     I nodi evidenziati che circondano la variabile di destinazione sono quelli correlati statisticamente con questo risultato. Utilizzare la legenda nella parte inferiore del visualizzatore per comprendere la natura della relazione.  
  
2.  Fare clic sul dispositivo di scorrimento a sinistra del visualizzatore e trascinarlo verso il basso.  
  
     Questo controllo consente di filtrare le variabili indipendenti, in base ai livelli di attendibilità delle dipendenze. Quando si trascina il dispositivo di scorrimento verso il basso, nel grafico restano solo i collegamenti più attendibili.  
  
3.  Dopo aver filtrato il grafico, fare clic sul pulsante **copia la visualizzazione del grafico**. Selezionare quindi un foglio di lavoro in Excel e premere CTRL+V.  
  
     Questa opzione consente di copiare la vista selezionata, inclusi i filtri e l'evidenziazione.  
  
 [Torna all'inizio](#BKMK_Tabs)  
  
###  <a name="attribute-profiles"></a><a name="bkmk_AttProf"></a> Profili attributo  
 Le finestre **Profili attributo** offrono un'indicazione visiva del modo in cui tutte le altre variabili sono correlate ai singoli risultati.  
  
##### <a name="explore-the-profiles"></a>Esplorazione del profili  
  
1.  Per nascondere alcuni valori in modo da poter confrontare più facilmente i risultati, fare clic sull'intestazione di colonna e trascinarla sotto un'altra colonna.  
  
     ![Profili attributi in Visualizzatore Naive Bayes](media/dm13-nb-attprof.gif "Profili attributi in Visualizzatore Naive Bayes")  
  
2.  Fare clic su una cella per visualizzare la distribuzione dei valori in **Legenda data mining**.  
  
     Poiché gli attributi associati ai differenti risultati vengono rappresentati visivamente, è facile individuare correlazioni interessanti, ad esempio i redditi sono distribuiti per area.  
  
3.  Per ottenere i dati sottostanti a questa visualizzazione, fare clic su **copia in Excel**. Viene generata una tabella in un nuovo foglio di lavoro in cui vengono visualizzate le correlazioni tra singoli attributi e risultati. In questa tabella di Excel è possibile nascondere o filtrare facilmente le colonne.  
  
 [Torna all'inizio](#BKMK_Tabs)  
  
###  <a name="attribute-characteristics"></a><a name="bkmk_AttChar"></a>Caratteristiche degli attributi  
 La vista **Caratteristiche attributo** è utile per l'analisi approfondita di una determinata variabile di risultato e dei fattori che contribuiscono.  
  
 ![Caratteristiche attributi in Visualizzatore Naive Bayes](media/dm13-nb-viewer.gif "Caratteristiche attributi in Visualizzatore Naive Bayes")  
  
##### <a name="explore-the-attribute-characteristics"></a>Esplorazione delle caratteristiche degli attributi  
  
1.  Fare clic su **valore** e selezionare un elemento del **valore**.  
  
     Quando si seleziona un risultato di destinazione, il grafico viene aggiornato per visualizzare i fattori associati in modo più sicuro al risultato, ordinati in base alla priorità.  
  
     Si noti che se si crea un modello utilizzando l'opzione [Analizza fattori di influenza chiave &#40;strumenti di analisi tabelle per Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md) , è possibile creare modelli con più di un attributo stimabile. Tuttavia, tutte le altre procedure guidate nei componenti aggiuntivi Data mining limitano l'utente a un attributo stimabile.  
  
2.  Fare clic su **copia in Excel** per creare una tabella in un nuovo foglio di lavoro, elencando i punteggi per tutti gli attributi correlati al risultato di destinazione selezionato.  
  
 [Torna all'inizio](#BKMK_Tabs)  
  
###  <a name="attribute-discrimination"></a><a name="bkmk_AttDisc"></a>Discriminazione degli attributi  
 La visualizzazione analisi **discriminante attributi** consente di confrontare due risultati o un risultato rispetto a tutti gli altri risultati.  
  
 ![Discriminante attributi in Visualizzatore Naive Bayes](media/dm13-nb-attdisc.gif "Discriminante attributi in Visualizzatore Naive Bayes")  
  
##### <a name="explore-attribute-discrimination"></a>Esplorazione dell'analisi discriminante attributi  
  
1.  Utilizzare i controlli, **valore 1** e **valore 2**, per selezionare i risultati che si desidera confrontare.  
  
     Ad esempio, in questo modello sono presenti alcuni attributi interessanti nel gruppo low income, quindi è stato scelto il gruppo di reddito più basso nel primo elenco a discesa e sono **stati scelti tutti gli altri Stati** nel secondo elenco a discesa.  
  
     Gli attributi vengono ordinati in ordine di importanza (calcolata in base ai dati di training). Pertanto, occupazione è il fattore più strettamente correlato al reddito (almeno per questo gruppo di destinazione).  
  
     Per visualizzare le cifre esatte, fare clic sulla barra colorata e visualizzare **Legenda data mining**.  
  
2.  Si noti che anche i redditi inferiori sono correlati con l'area Europa.  
  
     Il modello Naïve Bayes non supporta il drill-down; tuttavia, se si desidera esaminare i case associati a questo gruppo di risultati, è possibile utilizzare una query. Per informazioni sulle query su questo tipo di modello, vedere [esempi di query sul modello Naive Bayes](data-mining/naive-bayes-model-query-examples.md).  
  
 [Torna all'inizio](#BKMK_Tabs)  
  
## <a name="see-also"></a>Vedi anche  
 [Esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
