---
title: Esplorazione di un modello Association Rules | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining model, association
- mining models, viewing
- association [data mining]
ms.assetid: faffe208-7a64-4ec6-825f-ecbaa79caff7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30ff9705949be3fb9bf99d985d0db1aa17d93ab1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088466"
---
# <a name="browsing-an-association-rules-model"></a>Esplorazione di un modello Association Rules
  Quando si apre un modello di associazione utilizzando **Sfoglia**, il modello viene visualizzato in un visualizzatore interattivo, simile al visualizzatore Association Rules [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]in.  Il visualizzatore consente di visualizzare immediatamente gli elementi correlati l'uno con l'altro e le regole che è possibile utilizzare per la stima o creare indicazioni.  
  
##  <a name="BKMK_ViewerTabs"></a>Esplorare il modello  
 Quando si apre un modello di data mining creato utilizzando l' [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Association Rules, nella finestra **Sfoglia** sono incluse le visualizzazioni seguenti, ciascuna progettata per consentire l'esplorazione di un aspetto diverso del modello:  
  
-   [Set](#BKMK_Itemsets)  
  
-   [Regole](#BKMK_Rules)  
  
-   [Rete di dipendenze](#BKMK_Dependency)  
  
 Prendere nota dell'opzione in ogni scheda, **Mostra nome lungo** . Selezionando questa opzione, è possibile mostrare o nascondere la tabella di origine del set di elementi e abbreviare o allungare il nome della regola o del set di elementi. Questa opzione risulta particolarmente utile quando i dati dei case e degli attributi derivano da origini dati diverse.  
  
 Per provare un modello di associazione, è possibile utilizzare i dati di esempio nella scheda Associazione della cartella di lavoro dei dati di esempio e compilare un modello di associazione utilizzando tutte le impostazioni predefinite. È inoltre possibile creare un modello di Market Basket Analysis e aprirlo utilizzando **Sfoglia**.  
  
###  <a name="BKMK_Itemsets"></a>Set  
 La scheda **set** di elementi è una posizione ideale per iniziare a esplorare un modello di associazione. In questa scheda viene mostrato un elenco degli elementi spesso trovati insieme dal modello.  
  
 ![Elenco di elementi in un modello di associazione](media/dm13-association-itemsets.gif "Elenco di elementi in un modello di associazione")  
  
 L'esempio più comune di set di elementi è in un modello Market basket, dove un set di elementi rappresenta coppie o set di prodotti che molti clienti acquistano contemporaneamente. Tuttavia, a seconda di come si raggruppano e si ordinano gli elementi, il set di elementi potrebbe contenere una sequenza di filmati che i clienti ordinano in un determinato periodo di tempo, o eventi che tendono a verificarsi in una posizione specifica.  
  
 Un set di *elementi* può contenere un massimo di un elemento a due, tre o, tuttavia, molti è impostato come dimensione massima del set di elementi per il modello. Per ogni set di elementi, nel visualizzatore vengono visualizzati il *supporto*, la *probabilità*e le *dimensioni*del set di elementi. Il supporto e probabilità sono le statistiche principali utilizzate per classificare i set di elementi e le regole generati da un modello di associazione. Questi valori vengono anche utilizzati per calcolare e descrivere la relativa priorità.  
  
 **Supporto tecnico**. Il supporto indica il numero di case o righe di dati di input associati a questo elemento. Se, ad esempio, un set di elementi contiene due elementi trovati in un carrello acquisti, il numero nella colonna **supporto** indica il numero di volte in cui si è verificata la combinazione di elementi nei dati di origine.  
  
 **Dimensioni**. Modificando le dimensioni del set di elementi, è possibile controllare la lunghezza degli elenchi di set di elementi. Se non si desidera visualizzare i singoli prodotti nell'elenco, modificare l'opzione, **dimensioni minime set di elementi**, su 2 o più.  Se si limita l'elenco aumentando la dimensione minima dei set di elementi, è possibile cercare modelli molto specifici. Questo potrebbe essere utile se si utilizza un set di dati di dimensioni molto grandi.  
  
 È possibile filtrare il numero di set di elementi visualizzati nella scheda modificando il **supporto minimo** e i valori **massimi delle righe** . Se si aumenta il valore di **supporto minimo** , nell'elenco verranno visualizzati meno set di elementi, ma i set di elementi saranno quelli più comuni nei dati di input. La scelta comune è la stessa importante è un'altra domanda, che è possibile esplorare usando la scheda **regole** .  
  
 Si noti che la modifica del valore di supporto o di altri controlli nella scheda **set** di elementi modifica solo gli elementi visualizzati e non influisce sul modello sottostante. Se si desidera generare meno o più set di elementi o limitarne le dimensioni, è necessario utilizzare i parametri `MINIMUM_SUPPORT` e `MAXIMUM_SUPPORT`, disponibili nella finestra di dialogo **parametri algoritmo** .  
  
##### <a name="explore-the-itemsets-list"></a>Esplorare l'elenco dei set di elementi  
  
1.  Fare clic sulla colonna **supporto** per eseguire l'ordinamento in base al supporto massimo a quello più basso. In questo modo verrà fornita un'idea dei clienti che fanno acquisti più spesso.  
  
2.  Per concentrarsi su un particolare set di elementi di interesse, da molte migliaia di combinazioni possibili, digitare del testo nella casella **Filtra set di elementi** .  
  
     Qui abbiamo digitato `Gloves`. Quando si applica il filtro, l'elenco viene aggiornato per mostrare solo i set di elementi che contengono guanti. Ciò consente di concentrarsi sulle transazioni in cui i clienti hanno acquistato guanti e qualche altro elemento.  
  
     L'opzione **Filtra set di elementi** consente inoltre di visualizzare un elenco dei filtri utilizzati in precedenza.  
  
3.  Modificare il valore di **dimensioni minime set di elementi** per filtrare i clienti che hanno acquistato solo i guanti e nessun altro elemento.  
  
4.  Fare clic sull'elenco a discesa dell'opzione **Mostra**per controllare la modalità di visualizzazione degli attributi:  
  
    -   **Mostra nome e valore dell'attributo**  
  
    -   **Mostra solo il valore dell'attributo**  
  
    -   **Mostra solo il nome dell'attributo**  
  
     Si noti come il nome cambia. Nel caso di un modello Market Basket, basato sulle tabelle annidate dei prodotti acquistati da più clienti, il nome dell'attributo è in genere il nome del prodotto e la presenza del prodotto nell'elenco viene contrassegnata come `Existing`, a indicare che il cliente ha acquistato l'elemento.  
  
     Il contrario di `Existing` è `Missing`, che può essere un attributo molto utile per eseguire analisi nel data mining. Si supponga, ad esempio, che il set di elementi A + B sia molto popolare per trovare i clienti che hanno acquistato l'elemento A ma non l'elemento B. A tale scopo, è possibile utilizzare una query di stima e recuperare le transazioni con una, ma non l'altra, ed eseguire ulteriori analisi su tali query. Per informazioni su come creare query di stima sui modelli di associazione, vedere [esempi di query sul modello di associazione](data-mining/association-model-query-examples.md) in documentazione online di SQL Server  
  
5.  Per forzare la rivisualizzazione dell'elenco di set di elementi usando i nuovi criteri di filtro, è possibile selezionare o deselezionare la casella di controllo **Mostra nomi lunghi** .  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a>Regole  
 La scheda **regole** combina le informazioni sui set di elementi e il relativo valore.  
  
 ![Elenco di regole create da un modello di associazione](media/dm13-association-rules.gif "Elenco di regole create da un modello di associazione")  
  
 La *probabilità* rappresenta la frazione di case nel set di dati che contengono la combinazione di elementi di destinazione. La probabilità è simile al concetto statistico di *confidenza*e fornisce un'indicazione della probabilità che si verifichi il risultato di una regola. È possibile modificare il valore della **probabilità minima** in questo riquadro per filtrare le regole visualizzate.  
  
 Il valore della **probabilità minima** visualizzata inizialmente è il valore soglia utilizzato dall'algoritmo durante la compilazione del modello. Una volta completato il modello, non è possibile ridurre questo valore, ma è possibile aumentarlo per mostrare solo gli elementi con probabilità più elevata.  
  
 L' *importanza* è progettata per misurare l'utilità di una regola. Una regola che è molto comune potrebbe essere così universale che presenta un valore delle informazioni ridotto. Maggiore è la priorità, più attendibile è la regola per la stima del risultato. In Market [Basket Analysis &#40;Table AnalysisTools per Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md) Tool, l'importanza può essere combinata con il prezzo degli elementi per determinare i bundle potenzialmente più preziosi in termini di vendite.  
  
##### <a name="explore-the-rules-list"></a>Esplorare l'elenco delle regole  
  
1.  Provare a fare clic sulle intestazioni di colonna: **probabilità**, **priorità**e **regola** per vedere come vengono modificati i dati.  
  
2.  Utilizzare l'opzione **filtro regola** per digitare i valori e concentrarsi sulle regole di destinazione.  
  
     Se, ad esempio, si desidera visualizzare tutte le regole per la stima dei clienti che probabilmente acquisteranno insieme ai guanti, digitare "Gloves" nella casella di testo e aggiornare il riquadro.  
  
     L'opzione **Filtra set di elementi** consente inoltre di visualizzare un elenco dei filtri utilizzati in precedenza.  
  
3.  Per forzare la rivisualizzazione dell'elenco di regole utilizzando i criteri di filtro, è possibile selezionare o deselezionare la casella di controllo **Mostra nomi lunghi** .  
  
4.  Usare l'opzione **Mostra** per controllare la modalità di visualizzazione dei nomi delle regole.  
  
5.  Impostare il valore dell'opzione **numero massimo di righe** su 100, quindi fare clic su **copia in Excel**.  
  
     Si noti che la modifica di questo valore non ha alcun effetto sulla quantità di dati nel modello. controlla semplicemente il numero di righe nell'elenco di visualizzazione. Questa opzione può essere utile quando si utilizzano modelli di dimensioni molto grandi.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a>Rete di dipendenze  
 La scheda **rete di dipendenze** è una mappa visiva delle correlazioni tra gli elementi. Ogni ovale nel grafico (denominato *nodo*) rappresenta una coppia attributo-valore, ad esempio "gilet = existing" o "Age = 1-30".  Ogni riga che connette gli ovali (denominata *bordo*) rappresenta un tipo di correlazione.  
  
 ![Grafico della rete di dipendenze per un modello di associazione](media/dm13-association-dependencynetwork.gif "Grafico della rete di dipendenze per un modello di associazione")  
  
##### <a name="explore-the-dependency-network"></a>Esplorare la rete di dipendenze  
  
1.  Fare clic sul pulsante **trova** e utilizzare la finestra di dialogo **Trova nodo** per digitare un elemento di interesse.  
  
     Ad esempio, digitare "Gloves" e quindi ingrandire il grafico nella finestra per poter visualizzare facilmente i risultati.  
  
     Il nodo che contiene l'elemento viene evidenziato, mentre le frecce che puntano al nodo rappresentano una regola che collega gli elementi.  
  
     La direzione della freccia indica la direzione della regola. Se, ad esempio, un utente che acquista guanti è anche in grado di acquistare un giubbotto, la freccia viene avviata dal nodo "guanto" e termina sul nodo "gilet".  
  
     Per ottenere statistiche aggiuntive su questa regola, è possibile fare clic sulla scheda **regole** e cercare una regola con la descrizione "Glove-existing"-> "gilet-existing".  
  
2.  Fare clic e trascinare il dispositivo di scorrimento a sinistra del visualizzatore.  
  
     Il dispositivo di scorrimento funge da filtro in base alla probabilità delle regole. Riducendo l'indicatore di scorrimento, verranno visualizzate solo le regole più attendibili.  
  
3.  Fare clic su **copia in Excel** per copiare uno snapshot della finestra corrente in Excel.  
  
     Non sarà possibile usare il grafico copiato in Excel. Se è necessario un grafico di rete interattivo, utilizzare la [visualizzazione dei modelli di data mining in Visio &#40;componenti aggiuntivi Data mining&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>Ulteriori informazioni sui modelli di associazione  
 È possibile utilizzare la funzionalità **Sfoglia** per aprire ed esplorare qualsiasi modello creato utilizzando l'algoritmo Microsoft Association Rules. Sono inclusi i modelli compilati mediante lo strumento Market [Basket Analysis &#40;Table AnalysisTools per Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md) , nella barra multifunzione strumenti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] **analisi tabelle** o in.  
  
 Se si crea un modello Association Rules utilizzando lo strumento Market basket analysis, molte delle opzioni avanzate vengono configurate automaticamente.  
  
 Se si desidera impostare parametri avanzati o modificare la probabilità minima e il supporto, utilizzare la [procedura guidata associa &#40;client di data mining per&#41;](associate-wizard-data-mining-client-for-excel.md) guidata di Excel oppure creare un modello personalizzato utilizzando l'opzione [Aggiungi modello a struttura &#40;componenti aggiuntivi Data mining per Excel&#41;di](add-model-to-structure-data-mining-add-ins-for-excel.md) modellazione.  
  
-   **Set** di elementi: Quando si crea il modello, è anche possibile controllare il numero di set di elementi generati assegnando un valore al parametro MINIMUM_PROBABILITY. Questo parametro è disponibile nella finestra di dialogo Parametri algoritmo.  
  
-   **Regole:** L' [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Association Rules utilizza i valori di probabilità per limitare il numero di regole generate. È possibile controllare il numero di regole impostando i parametri `MINIMUM_PROBABILITY` o `MINIMUM _IMPORTANCE`.  
  
 Per ulteriori informazioni sulla configurazione di parametri avanzati, vedere [algoritmi di data mining &#40;SQL Server componenti aggiuntivi Data mining&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
