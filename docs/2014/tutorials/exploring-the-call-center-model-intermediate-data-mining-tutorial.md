---
title: Esplorazione del modello di Call Center (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9095212c-9068-4dd8-85ce-17a467adeabb
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a6aa4074aa04af86e478b57b1870fd0dd855bea8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63315074"
---
# <a name="exploring-the-call-center-model-intermediate-data-mining-tutorial"></a>Esplorazione del modello Call Center (Esercitazione intermedia sul data mining)
  Dopo aver compilato il modello esplorativo, è possibile utilizzarlo per ottenere ulteriori informazioni sui dati tramite gli strumenti seguenti disponibili in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   [Visualizzatore Microsoft Neural Network](#bkmk_NNviewer) **:** questo visualizzatore è disponibile nella scheda **Visualizzatore modello** di data mining di progettazione modelli di data mining ed è progettato per consentire di sperimentare le interazioni nei dati.  
  
-   [Microsoft Generic Content Tree Viewer](#bkmk_genviewer) **:** questo visualizzatore standard fornisce informazioni dettagliate sui modelli e le statistiche individuati dall'algoritmo durante la generazione del modello.  
  
##  <a name="bkmk_NNviewer"></a>Visualizzatore Microsoft Neural Network  
 Il visualizzatore include tre riquadri: **input**, **output**e **variabili**.  
  
 Utilizzando il riquadro di **output** , è possibile selezionare valori diversi per l'attributo stimabile o variabile dipendente. Se il modello contiene più attributi stimabili, è possibile selezionare l'attributo dall'elenco degli attributi di **output** .  
  
 Il riquadro **variabili** Confronta i due risultati scelti in termini di aggiunta di attributi o variabili. Le barre colorate rappresentano visivamente l'impatto della variabile sui risultati di destinazione. È possibile visualizzare anche punteggi di accuratezza per le variabili. I punteggi di accuratezza vengono calcolati in modo diverso a seconda del tipo di modello di data mining utilizzato, ma indica in generale il miglioramento del modello in caso di utilizzo dell'attributo per la stima.  
  
 Il riquadro Input consente di aggiungere **fattori** di influenza al modello per provare diversi scenari di simulazione.  
  
### <a name="using-the-output-pane"></a>Utilizzo del riquadro Output  
 In questo modello iniziale interessa vedere come i vari fattori influiscono sul livello del servizio. A tale scopo, è possibile selezionare il livello di servizio dall'elenco degli attributi di output, quindi confrontare diversi livelli di servizio selezionando intervalli dagli elenchi a discesa per **valore 1** e **valore 2**.  
  
##### <a name="to-compare-lowest-and-highest-service-grades"></a>Per confrontare i livelli di servizio più basso e più elevato  
  
1.  Per **valore 1**selezionare l'intervallo con i valori più bassi. Ad esempio, l'intervallo 0-0-0,7 rappresenta la frequenza di abbandono più bassa e pertanto il migliore livello di servizio.  
  
    > [!NOTE]  
    >  I valori esatti di questo intervallo possono variare a seconda di come è stato configurato il modello.  
  
2.  Per **valore 2**selezionare l'intervallo con i valori più alti. Ad esempio, l'intervallo con il valore >= 0,12 rappresenta la frequenza di abbandono più elevata e pertanto il livello di servizio peggiore. In altre parole, il 12% dei clienti che ha telefonato durante questo turno ha riagganciato prima di parlare con un rappresentante.  
  
     Il contenuto del riquadro **variabili** viene aggiornato per confrontare gli attributi che contribuiscono ai valori di risultato. Nella colonna sinistra vengono pertanto elencati gli attributi associati al migliore livello di servizio, mentre nella colonna destra vengono elencati gli attributi associati al peggiore livello di servizio.  
  
### <a name="using-the-variables-pane"></a>Utilizzo del riquadro Variabili  
 In questo modello viene visualizzato `Average Time Per Issue` un fattore importante. Questa variabile indica il tempo medio necessario per rispondere a una chiamata, indipendentemente dal tipo di chiamata.  
  
##### <a name="to-view-and-copy-probability-and-lift-scores-for-an-attribute"></a>Per visualizzare e copiare i punteggi di probabilità e accuratezza per un attributo  
  
1.  Nel riquadro **variabili** , posizionare il mouse sulla barra colorata nella prima riga.  
  
     Questa barra colorata Mostra come contribuisce fortemente `Average Time Per Issue` al livello del servizio. La descrizione comando indica un punteggio complessivo e i punteggi di probabilità e accuratezza per ogni combinazione di una variabile e un risultato di destinazione.  
  
2.  Nel riquadro **variabili** fare clic con il pulsante destro del mouse su una barra colorata e scegliere **copia**.  
  
3.  In un foglio di lavoro di Excel fare clic con il pulsante destro del mouse su una cella e scegliere **Incolla**.  
  
     Il report verrà incollato come tabella HTML e includerà solo i punteggi per ogni barra.  
  
4.  In un foglio di lavoro di Excel diverso, fare clic con il pulsante destro del mouse su una cella e scegliere **Incolla speciale**  
  
     Il report verrà incollato in formato testo e includerà le statistiche correlate descritte nella sezione successiva.  
  
### <a name="using-the-input-pane"></a>Utilizzo del riquadro Input  
 Si supponga di essere interessati all'analisi dell'effetto di un particolare fattore, ad esempio il turno o il numero di operatori. È possibile selezionare una determinata variabile utilizzando il riquadro **input** e il riquadro **variabili** viene aggiornato automaticamente per confrontare i due gruppi selezionati in precedenza in base alla variabile specificata.  
  
##### <a name="to-review-the-effect-on-service-grade-by-changing-input-attributes"></a>Per verificare l'effetto sul livello di servizio modificando gli attributi di input  
  
1.  Nel riquadro **input** selezionare MAIUSC per **attributo**.  
  
2.  Per **valore**selezionare **am**.  
  
     Il riquadro **variabili** viene aggiornato per mostrare l'effetto sul modello quando il turno è **am**. Tutte le altre selezioni rimangono invariate. si sta ancora confrontando i livelli di servizio più bassi e massimi.  
  
3.  Per **valore**selezionare **PM1**.  
  
     Il riquadro **variabili** viene aggiornato per mostrare l'effetto sul modello quando lo spostamento cambia.  
  
4.  Nel riquadro **input** fare clic sulla riga vuota successiva sotto **attributo**e selezionare chiamate. Per **valore**selezionare l'intervallo che indica il maggior numero di chiamate.  
  
     All'elenco verrà aggiunta una nuova condizione di input. Il riquadro **variabili** viene aggiornato per mostrare l'effetto sul modello per un determinato turno quando il volume di chiamate è più alto.  
  
5.  Continuare a modificare i valori per Shift e Calls per trovare eventuali correlazioni interessanti tra turno, volume di chiamate e livello del servizio.  
  
    > [!NOTE]  
    >  Per cancellare il contenuto del riquadro **input** in modo che sia possibile utilizzare attributi diversi, fare clic su **Aggiorna contenuto Visualizzatore**.  
  
### <a name="interpreting-the-statistics-provided-in-the-viewer"></a>Interpretazione delle statistiche presenti nel visualizzatore  
 Tempi di attesa più lunghi rappresentano un importante criterio di stima di una frequenza di abbandono elevata, che indica un livello di servizio insufficiente. Sebbene possa sembrare una conclusione ovvia, il modello di data mining fornisce dati statistici aggiuntivi per l'interpretazione di queste tendenze.  
  
-   **Score**: valore che indica l'importanza complessiva della variabile per la discriminazione tra i risultati. Più elevato è il punteggio, maggiore sarà l'effetto della variabile sul risultato.  
  
-   **Probabilità del valore 1**: percentuale che rappresenta la probabilità di questo valore per il risultato.  
  
-   **Probabilità di valore 2**: percentuale che rappresenta la probabilità di questo valore per il risultato.  
  
-   **Accuratezza per valore 1** e **accuratezza per valore 2**: punteggi che rappresenta l'effetto dell'utilizzo di questa particolare variabile per la stima dei risultati di valore 1 e valore 2. Più elevato è il punteggio, migliore risulterà la variabile per la stima dei risultati.  
  
 La tabella seguente contiene alcuni valori di esempio per i principali fattori di influenza. Ad esempio, la **probabilità di valore 1** è 60,6% e la **probabilità di valore 2** è 8,30%, ovvero quando il tempo medio per il problema è compreso nell'intervallo di 44-70 minuti, il 60,6% dei case è stato spostato con i livelli di servizio più elevati (valore 1) e il 8,30% dei case è stato spostato con i livelli di servizio peggiori (valore 2).  
  
 Da queste informazioni è possibile trarre alcune conclusioni. I tempi di risposta alle chiamate più brevi (intervallo 44-70) influiscono decisamente su un livello di servizio migliore (intervallo 0,00-0,07). Il punteggio (92,35) suggerisce che questa variabile è molto importante.  
  
 Tuttavia, analizzando l'elenco dei fattori di influenza, è possibile notare altri fattori con effetti più complessi e più difficili da interpretare. Ad esempio, il turno sembra influire sul servizio, ma i punteggi di accuratezza e le probabilità relative indicano che il turno non è un fattore principale.  
  
|Attributo|valore|Predilige \< 0,07|Predilige >= 0,12|  
|---------------|-----------|--------------------|----------------------|  
|Average Time Per Issue|89,087-120,000||Punteggio: 100<br /><br /> Probabilità di value1:4,45%<br /><br /> Probabilità di value2:51,94%<br /><br /> Accuratezza per value1:0,19<br /><br /> Accuratezza per value2:1,94|  
|Average Time Per Issue|44,000-70,597|Punteggio: 92,35<br /><br /> Probabilità di Valore 1: 60,06%<br /><br /> Probabilità di Valore 2: 8,30%<br /><br /> Accuratezza per Valore 1: 2,61<br /><br /> Accuratezza per Valore 2: 0,31||  
  
 [Torna all'inizio](#bkmk_NNviewer)  
  
##  <a name="bkmk_genviewer"></a>Microsoft Generic Content Tree Viewer  
 Questo visualizzatore può essere utilizzato per visualizzare informazioni ancora più dettagliate create dall'algoritmo quando il modello viene elaborato. **MicrosoftGeneric Content Tree Viewer** rappresenta il modello di data mining come una serie di nodi, in cui ogni nodo rappresenta le conoscenze acquisite sui dati di training. Questo visualizzatore può essere utilizzato con tutti i modelli, ma il contenuto dei nodi è diverso a seconda del tipo di modello.  
  
 Per i modelli di rete neurale o i modelli di regressione logistica, il `marginal statistics node` può risultare particolarmente utile. Questo nodo contiene statistiche derivate sulla distribuzione di valori nei dati. Queste informazioni possono risultare utili se si desidera ottenere un riepilogo dei dati senza dovere scrivere molte query T-SQL. Il grafico dei valori per la creazione di contenitori nell'argomento precedente deriva dal nodo delle statistiche marginali.  
  
#### <a name="to-obtain-a-summary-of-data-values-from-the-mining-model"></a>Per ottenere un riepilogo dei valori dei dati dal modello di data mining  
  
1.  Nella scheda **Visualizzatore modello** di data mining di progettazione modelli di data mining \<Selezionare Nome modello di data mining>.  
  
2.  Dall'elenco **Visualizzatore** selezionare **Microsoft Generic Content Tree Viewer**.  
  
     La vista del modello di data mining verrà aggiornata per visualizzare una gerarchia di nodi nel riquadro sinistro e una tabella HTML nel riquadro destro.  
  
3.  Nel riquadro **Didascalia nodo** fare clic sul nodo con il nome 10000000000000000.  
  
     Il nodo di livello più alto in qualsiasi modello è sempre il nodo radice del modello. In un modello di rete neurale o di regressione logistica il nodo immediatamente successivo è il nodo delle statistiche marginali.  
  
4.  Nel riquadro dei **Dettagli del nodo** scorrere verso il basso fino a individuare la riga NODE_DISTRIBUTION.  
  
5.  Scorrere la tabella NODE_DISTRIBUTION per visualizzare la distribuzione dei valori calcolati dall'algoritmo Microsoft Neural Network.  
  
 Per utilizzare questi dati in un report, è possibile selezionare e copiare le informazioni per le righe specifiche oppure utilizzare la query DMX (Data Mining Extensions) seguente per estrarre il contenuto completo del nodo.  
  
```  
SELECT *   
FROM [Call Center EQ4].CONTENT  
WHERE NODE_NAME = '10000000000000000'  
```  
  
 È inoltre possibile utilizzare la gerarchia di nodi e i dettagli nella tabella NODE_DISTRIBUTION per attraversare singoli percorsi della rete neurale e visualizzare statistiche del livello nascosto. Per ulteriori informazioni, vedere [esempi di query sul modello di rete neurale](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md).  
  
 [Torna all'inizio](#bkmk_NNviewer)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Aggiunta di un modello di regressione logistica alla struttura del Call Center &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto del modello di data mining per i modelli di rete neurale &#40;Analysis Services-Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Esempi di query sul modello di rete neurale](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Riferimento tecnico per l'algoritmo Microsoft Neural Network](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Modificare la discretizzazione di una colonna in un modello di data mining](../../2014/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)  
  
  
