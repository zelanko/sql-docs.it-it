---
title: Esplorazione di un'associazione di modello delle regole | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: 1259cc627ef53d8f5a201e42772a9dba390824cc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62664405"
---
# <a name="browsing-an-association-rules-model"></a>Esplorazione di un modello Association Rules
  Quando si apre un modello di associazione utilizzando **esplorare**, il modello viene visualizzato in un visualizzatore interattivo, simile al visualizzatore Microsoft Association Rules in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  Il visualizzatore consente di visualizzare immediatamente gli elementi correlati l'uno con l'altro e le regole che è possibile utilizzare per la stima o creare indicazioni.  
  
##  <a name="BKMK_ViewerTabs"></a> Esplorare il modello  
 Quando si apre un modello di data mining che è stato creato utilizzando il [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Microsoft Association Rules, il **Sfoglia** finestra include le viste seguenti, ognuna progettata per consentire l'esplorazione di un aspetto diverso del modello:  
  
-   [Set di elementi](#BKMK_Itemsets)  
  
-   [Regole](#BKMK_Rules)  
  
-   [Rete di dipendenze](#BKMK_Dependency)  
  
 Prendere nota dell'opzione in ogni scheda **Mostra nomi lunghi** . Selezionando questa opzione, è possibile mostrare o nascondere la tabella di origine del set di elementi e abbreviare o allungare il nome della regola o del set di elementi. Questa opzione risulta particolarmente utile quando i dati dei case e degli attributi derivano da origini dati diverse.  
  
 Per provare un modello di associazione, è possibile utilizzare i dati di esempio nella scheda Associazione della cartella di lavoro dei dati di esempio e compilare un modello di associazione utilizzando tutte le impostazioni predefinite. È anche possibile compilare un modello market Basket Analysis e aprirlo utilizzando **esplorare**.  
  
###  <a name="BKMK_Itemsets"></a> Set di elementi  
 Il **set di elementi** scheda è un buon punto di iniziare l'esplorazione di un modello di associazione. In questa scheda viene mostrato un elenco degli elementi spesso trovati insieme dal modello.  
  
 ![Elenco di elementi in un modello di associazione](media/dm13-association-itemsets.gif "elenco di elementi in un modello di associazione")  
  
 L'esempio più comune di set di elementi è in un modello Market basket, dove un set di elementi rappresenta coppie o set di prodotti che molti clienti acquistano contemporaneamente. Tuttavia, a seconda di come si raggruppano e si ordinano gli elementi, il set di elementi potrebbe contenere una sequenza di filmati che i clienti ordinano in un determinato periodo di tempo, o eventi che tendono a verificarsi in una posizione specifica.  
  
 Un' *set di elementi* può contenere da un elemento a due, tre, o, tuttavia, molti viene impostato come le dimensioni del set di elementi massimo per il modello. Per ogni set di elementi nel visualizzatore viene visualizzato il set di elementi *supportano*, *probabilità*, e *dimensioni*. Il supporto e probabilità sono le statistiche principali utilizzate per classificare i set di elementi e le regole generati da un modello di associazione. Questi valori vengono anche utilizzati per calcolare e descrivere la relativa priorità.  
  
 **Supporto**. Il supporto indica il numero di case o righe di dati di input associati a questo elemento. Ad esempio, se un set di elementi contiene due elementi che si trovano in un carrello carrello, il numero dei **supporto** colonna indica il numero di volte che si sono verificati combinazione di elementi nei dati di origine.  
  
 **Dimensioni**. Modificando le dimensioni del set di elementi, è possibile controllare la lunghezza degli elenchi di set di elementi. Se non si desidera visualizzare singoli prodotti nell'elenco, modificare l'opzione **dimensioni minime set di elementi**, a 2 o più.  Se si limita l'elenco aumentando la dimensione minima dei set di elementi, è possibile cercare modelli molto specifici. Questo potrebbe essere utile se si utilizza un set di dati di dimensioni molto grandi.  
  
 È possibile filtrare il numero di set di elementi visualizzati nella scheda modificando la **supporto minimo** e **numero massimo di righe** valori. Se si aumenta il **supporto minimo** valore, l'elenco verrà visualizzato un numero inferiore di set di elementi, ma i set di elementi saranno quelli più comuni nei dati di input. Se comune corrisponde a importante è un'altra questione, che è possibile esplorare utilizzando il **regole** scheda.  
  
 Si noti che la modifica il valore di supporto o altri controlli nel **set di elementi** scheda Modifica solo gli elementi che vengono visualizzati e non influiscono sul modello sottostante. Se si desidera generare meno o più set di elementi o limitarne le dimensioni, è necessario usare i parametri `MINIMUM_SUPPORT` e `MAXIMUM_SUPPORT`, disponibile nel **i parametri dell'algoritmo** nella finestra di dialogo.  
  
##### <a name="explore-the-itemsets-list"></a>Esplorare l'elenco dei set di elementi  
  
1.  Scegliere il **supportano** colonna per ordinare dal più alto al più basso supporto tecnico. In questo modo verrà fornita un'idea dei clienti che fanno acquisti più spesso.  
  
2.  Per concentrare l'attenzione su un particolare set di elementi di interesse, tra le molte migliaia di combinazioni possibile, digitare un testo nel **Filtra set di elementi** casella.  
  
     Qui abbiamo digitato `Gloves`. Quando si applica il filtro, l'elenco viene aggiornato per mostrare solo i set di elementi che contengono guanti. Ciò consente di concentrarsi sulle transazioni in cui i clienti hanno acquistato guanti e qualche altro elemento.  
  
     L'opzione **Filtra set di elementi** consente inoltre di visualizzare un elenco dei filtri utilizzati in precedenza.  
  
3.  Modificare il valore della **dimensioni minime set di elementi** per filtrare i clienti che hanno acquistato solo guanti e non altri elementi.  
  
4.  Fare clic sull'elenco a discesa per l'opzione **mostrare**per controllare la modalità di visualizzazione di attributi:  
  
    -   **Mostra nome e valore dell'attributo**  
  
    -   **Mostra solo il valore dell'attributo**  
  
    -   **Mostra solo il nome dell'attributo**  
  
     Si noti come il nome cambia. Nel caso di un modello Market Basket, basato sulle tabelle annidate dei prodotti acquistati da più clienti, il nome dell'attributo è in genere il nome del prodotto e la presenza del prodotto nell'elenco viene contrassegnata come `Existing`, a indicare che il cliente ha acquistato l'elemento.  
  
     Il contrario di `Existing` è `Missing`, che può essere un attributo molto utile per eseguire analisi nel data mining. Ad esempio, si supponga che il set di elementi A + B è pertanto molto diffuso che si desidera trovare i clienti che hanno acquistato l'elemento A ma non l'elemento B. È possibile eseguire questa operazione usando una query di stima e recuperando le transazioni con una ma non in altra ed effettuare un'ulteriore analisi su quelle. Per informazioni su come creare query di stima nei modelli di associazione, vedere [Association Model Query Examples](data-mining/association-model-query-examples.md) nella documentazione Online di SQL Server  
  
5.  Per forzare l'elenco di set di elementi per visualizzare nuovamente usando i nuovi criteri di filtro, è possibile selezionare o deselezionare i **Mostra nomi lunghi** casella di controllo.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Rules"></a> Regole  
 Il **regole** scheda combina informazioni sui set di elementi e il relativo valore.  
  
 ![Elenco di regole create da un modello di associazione](media/dm13-association-rules.gif "elenco di regole create da un modello di associazione")  
  
 *Probabilità* rappresenta la frazione di case nel set di dati che contengono la combinazione di elementi prevista. È simile al concetto statistico di probabilità *confidenza*e offre un'indicazione del modo in cui probabilmente il risultato di una regola deve verificarsi. È possibile modificare il valore di **probabilità minima** in questo riquadro per filtrare le regole visualizzate.  
  
 Il valore per **probabilità minima** inizialmente visualizzato è il valore di soglia che è stato usato dall'algoritmo quando si compila il modello. Una volta completato il modello, è possibile ridurre questo valore, ma è possibile aumentarlo per mostrare solo gli elementi di probabilità superiore.  
  
 *Importanza* è progettato per misurare l'utilità di una regola. Una regola che è molto comune potrebbe essere così universale che presenta un valore delle informazioni ridotto. Maggiore è la priorità, più attendibile è la regola per la stima del risultato. Nel [market Basket Analysis &#40;strumenti di analisi tabelle per Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) strumento di proprietà può essere combinata con il prezzo degli articoli per determinare i pacchetti che sono potenzialmente più importanti in termini di vendite.  
  
##### <a name="explore-the-rules-list"></a>Esplorare l'elenco delle regole  
  
1.  Provare a fare clic sulla colonna intestazioni - **probabilità**, **importanza**, e **regola** : per vedere come cambiano i dati.  
  
2.  Usare la **regola di filtro** opzione per digitare i valori e concentrarsi sulle regole di destinazione.  
  
     Ad esempio, se si desidera visualizzare tutte le regole che stimano quali clienti probabilmente acquisteranno insieme ai guanti, digitare "guanti" nella casella di testo e aggiornare il riquadro.  
  
     L'opzione **Filtra set di elementi** consente inoltre di visualizzare un elenco dei filtri utilizzati in precedenza.  
  
3.  Per forzare l'elenco di regole per visualizzare nuovamente usando criteri di filtro, è possibile selezionare o deselezionare i **Mostra nomi lunghi** casella di controllo.  
  
4.  Usare l'opzione **mostrare** per controllare il modo in cui visualizzare i nomi delle regole.  
  
5.  Impostare il valore per il **numero massimo di righe** opzione e 100 e quindi fare clic su **copia in Excel**.  
  
     Si noti che se si modifica questo valore non hanno alcun effetto sulla quantità di dati del modello. Controlla semplicemente il numero di righe nell'elenco visualizzato. Questa opzione può essere utile quando si utilizzano modelli di dimensioni molto grandi.  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Dependency"></a> Rete di dipendenze  
 Il **rete di dipendenze** scheda è una mappa visiva delle correlazioni tra gli elementi. Ogni ovale nel grafico (definito come un *nodo*) rappresenta una coppia attributo-valore, ad esempio "Vest = Existing" o "Age = 1-30".  Ogni riga che collega gli ovali (definito come un *edge*) rappresenta un tipo di correlazione.  
  
 ![Grafico della rete di dipendenze per un modello di associazione](media/dm13-association-dependencynetwork.gif "grafico della rete di dipendenze per un modello di associazione")  
  
##### <a name="explore-the-dependency-network"></a>Esplorare la rete di dipendenze  
  
1.  Fare clic sui **trovare** pulsante e utilizzare il **Trova nodo** finestra di dialogo in cui digitare un elemento di interesse.  
  
     Ad esempio, digitare "guanti", quindi ingrandire il grafico nella finestra in modo che è possibile visualizzare facilmente i risultati.  
  
     Il nodo che contiene l'elemento viene evidenziato, mentre le frecce che puntano al nodo rappresentano una regola che collega gli elementi.  
  
     La direzione della freccia indica la direzione della regola. Ad esempio, se persona che acquista guanti è anche probabile che acquisti un gilè, la freccia verrà avviata dal nodo "glove" e terminare nel nodo "vest".  
  
     Per ottenere statistiche aggiuntive su questa regola, è possibile scegliere il **regole** scheda e cercare una regola con la descrizione, "Glove - esistente" -> "Vest - esistente.")  
  
2.  Fare clic e trascinare il dispositivo di scorrimento a sinistra del visualizzatore.  
  
     Il dispositivo di scorrimento funge da filtro in base alla probabilità delle regole. Riducendo l'indicatore di scorrimento, verranno visualizzate solo le regole più attendibili.  
  
3.  Fare clic su **copia in Excel** per copiare uno snapshot della finestra corrente in Excel.  
  
     Sarà possibile utilizzare il grafico che verranno copiati in Excel. Se è necessario un grafico di rete interattivo, usare il [visualizzazione di modelli di Data Mining di Visio &#40;componenti aggiuntivi Data Mining&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md).  
  
 [Torna all'inizio](#BKMK_ViewerTabs)  
  
## <a name="more-about-association-models"></a>Ulteriori informazioni sui modelli di associazione  
 È possibile usare la **esplorare** funzionalità aprire ed esplorare qualsiasi modello creato utilizzando l'algoritmo Microsoft Association Rules. Questo include i modelli compilati utilizzando il [market Basket Analysis &#40;strumenti di analisi tabelle per Excel&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md) strumento il **strumenti di analisi tabelle** sulla barra multifunzione o nel [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Se si crea un modello Association Rules utilizzando lo strumento Market basket analysis, molte delle opzioni avanzate vengono configurate automaticamente.  
  
 Se si desidera impostare parametri avanzati o alter probabilità minima e il supporto, usare il [associare guidata &#40;Client di Data Mining per Excel&#41; ](associate-wizard-data-mining-client-for-excel.md) procedura guidata, o creare il proprio modello utilizzando la [aggiunta modello a Struttura &#40;aggiuntivi di Data Mining per Excel&#41; ](add-model-to-structure-data-mining-add-ins-for-excel.md) opzione di modellazione.  
  
-   **Set di elementi:** Quando si crea il modello, è anche possibile controllare il numero di set di elementi generati tramite l'assegnazione di un valore al parametro MINIMUM_PROBABILITY. Questo parametro è disponibile nella finestra di dialogo parametri algoritmo.  
  
-   **Regole:** Il [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo Microsoft Association Rules utilizza i valori di probabilità per limitare il numero di regole generate. È possibile controllare il numero di regole impostando i parametri `MINIMUM_PROBABILITY` o `MINIMUM _IMPORTANCE`.  
  
 Per altre informazioni sulla configurazione dei parametri avanzati, vedere [algoritmi di Data Mining &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorazione di modelli in Excel &#40;componenti aggiuntivi Data Mining di dati SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
