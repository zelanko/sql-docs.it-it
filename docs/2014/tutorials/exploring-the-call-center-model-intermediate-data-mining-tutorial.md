---
title: Esplorazione del modello Call Center (esercitazione intermedia di Data Mining) | Microsoft Docs
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
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56037762"
---
# <a name="exploring-the-call-center-model-intermediate-data-mining-tutorial"></a>Esplorazione del modello Call Center (Esercitazione intermedia sul data mining)
  Dopo aver compilato il modello esplorativo, è possibile utilizzarlo per ottenere ulteriori informazioni sui dati tramite gli strumenti seguenti disponibili in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   [Visualizzatore Microsoft Neural Network](#bkmk_NNviewer) **:** Questo visualizzatore è disponibile nel **visualizzatore modello di Data Mining** scheda Progettazione modelli di Data Mining ed è progettato per consentire di sperimentare le interazioni nei dati.  
  
-   [Microsoft Generic Content Tree Viewer](#bkmk_genviewer) **:** Questo visualizzatore standard fornisce informazioni dettagliate sui modelli e statistiche individuate dall'algoritmo durante la generazione di modelli.  
  
##  <a name="bkmk_NNviewer"></a> Visualizzatore Microsoft Neural Network  
 Il visualizzatore presenta tre riquadri - **Input**, **Output**, e **variabili**.  
  
 Tramite il **Output** riquadro, è possibile selezionare valori diversi per l'attributo stimabile o la variabile dipendente. Se il modello contiene più attributi stimabili, è possibile selezionare l'attributo dal **attributo Output** elenco.  
  
 Il **variabili** riquadro confronta i due risultati scelti per gli attributi o le variabili. Le barre colorate rappresentano visivamente l'impatto della variabile sui risultati di destinazione. È possibile visualizzare anche punteggi di accuratezza per le variabili. I punteggi di accuratezza vengono calcolati in modo diverso a seconda del tipo di modello di data mining utilizzato, ma indica in generale il miglioramento del modello in caso di utilizzo dell'attributo per la stima.  
  
 Il **Input** riquadro consente di aggiungere fattori di influenza al modello per provare vari scenari di simulazione.  
  
### <a name="using-the-output-pane"></a>Utilizzo del riquadro Output  
 In questo modello iniziale interessa vedere come i vari fattori influiscono sul livello del servizio. A tale scopo, è possibile selezionare Service Grade dall'elenco di attributi di output e quindi confrontare i diversi livelli di servizio selezionando intervalli negli elenchi a discesa **valore 1** e **valore 2**.  
  
##### <a name="to-compare-lowest-and-highest-service-grades"></a>Per confrontare i livelli di servizio più basso e più elevato  
  
1.  Per la **valore 1**, selezionare l'intervallo con i valori più bassi. Ad esempio, l'intervallo 0-0-0,7 rappresenta la frequenza di abbandono più bassa e pertanto il migliore livello di servizio.  
  
    > [!NOTE]  
    >  I valori esatti di questo intervallo possono variare a seconda di come è stato configurato il modello.  
  
2.  Per la **valore 2**, selezionare l'intervallo con i valori più alti. Ad esempio, l'intervallo con il valore >= 0,12 rappresenta la frequenza di abbandono più elevata e pertanto il livello di servizio peggiore. In altre parole, il 12% dei clienti che ha telefonato durante questo turno ha riagganciato prima di parlare con un rappresentante.  
  
     Il contenuto del **variabili** riquadro viene aggiornato per confrontare gli attributi che contribuiscono ai valori risultanti. Nella colonna sinistra vengono pertanto elencati gli attributi associati al migliore livello di servizio, mentre nella colonna destra vengono elencati gli attributi associati al peggiore livello di servizio.  
  
### <a name="using-the-variables-pane"></a>Utilizzo del riquadro Variabili  
 In questo modello, perché sembra che `Average Time Per Issue` è un fattore importante. Questa variabile indica il tempo medio necessario per rispondere a una chiamata, indipendentemente dal tipo di chiamata.  
  
##### <a name="to-view-and-copy-probability-and-lift-scores-for-an-attribute"></a>Per visualizzare e copiare i punteggi di probabilità e accuratezza per un attributo  
  
1.  Nel **variabili** riquadro, posizionare il mouse sulla barra colorata nella prima riga.  
  
     Questa barra colorata indica quanto duramente `Average Time Per Issue` contribuisca a livello di servizio. La descrizione comando indica un punteggio complessivo e i punteggi di probabilità e accuratezza per ogni combinazione di una variabile e un risultato di destinazione.  
  
2.  Nel **variabili** riquadro, pulsante destro del mouse, una barra colorata e selezionare **copia**.  
  
3.  In un foglio di lavoro di Excel, fare doppio clic su una cella qualsiasi e scegliere **Incolla**.  
  
     Il report verrà incollato come tabella HTML e includerà solo i punteggi per ogni barra.  
  
4.  In un foglio di lavoro di Excel diverso, fare doppio clic su una cella qualsiasi e scegliere **Incolla speciale**.  
  
     Il report verrà incollato in formato testo e includerà le statistiche correlate descritte nella sezione successiva.  
  
### <a name="using-the-input-pane"></a>Utilizzo del riquadro Input  
 Si supponga di essere interessati all'analisi dell'effetto di un particolare fattore, ad esempio il turno o il numero di operatori. È possibile selezionare una determinata variabile tramite la **Input** riquadro e il **variabili** riquadro viene aggiornato automaticamente per confrontare i due precedentemente selezionati i gruppi di base alla variabile specificata.  
  
##### <a name="to-review-the-effect-on-service-grade-by-changing-input-attributes"></a>Per verificare l'effetto sul livello di servizio modificando gli attributi di input  
  
1.  Nel **Input** riquadro per **attributo**, selezionare Shift.  
  
2.  Per la **valore**, selezionare **AM**.  
  
     Il **variabili** riquadro aggiornamenti per illustrare l'impatto sul modello quando il turno è **AM**. Tutte le altre selezioni rimarranno invariate, si confrontano ancora i livelli di servizio minimo e massimo.  
  
3.  Per la **valore**, selezionare **PM1**.  
  
     Il **variabili** riquadro aggiornamenti per illustrare l'impatto sul modello quando viene modificato il turno.  
  
4.  Nel **Input** riquadro, fare clic sulla riga vuota successiva nella **attributo**e selezionare Calls. Per la **valore**, selezionare l'intervallo che indica il numero massimo di chiamate.  
  
     All'elenco verrà aggiunta una nuova condizione di input. Il **variabili** riquadro aggiornamenti per illustrare l'impatto sul modello per un determinato turno quando il volume di chiamate è massimo.  
  
5.  Continuare a modificare i valori per Shift e Calls per trovare eventuali correlazioni interessanti tra turno, volume di chiamate e livello del servizio.  
  
    > [!NOTE]  
    >  Per cancellare il **Input** riquadro, in modo che è possibile usare attributi diversi, fare clic su **Aggiorna contenuto visualizzatore**.  
  
### <a name="interpreting-the-statistics-provided-in-the-viewer"></a>Interpretazione delle statistiche presenti nel visualizzatore  
 Tempi di attesa più lunghi rappresentano un importante criterio di stima di una frequenza di abbandono elevata, che indica un livello di servizio insufficiente. Sebbene possa sembrare una conclusione ovvia, il modello di data mining fornisce dati statistici aggiuntivi per l'interpretazione di queste tendenze.  
  
-   **Punteggio**: Valore che indica l'importanza complessiva della variabile per l'analisi discriminante tra risultati. Più elevato è il punteggio, maggiore sarà l'effetto della variabile sul risultato.  
  
-   **Probabilità del valore 1**: Percentuale che rappresenta la probabilità che questo valore per questo risultato.  
  
-   **Probabilità di valore 2**: Percentuale che rappresenta la probabilità che questo valore per questo risultato.  
  
-   **Accuratezza per valore 1** e **accuratezza per valore 2**: Punteggi che rappresentano l'impatto dell'uso di questa variabile specifica per la stima dei risultati di valore 1 e valore 2. Più elevato è il punteggio, migliore risulterà la variabile per la stima dei risultati.  
  
 La tabella seguente contiene alcuni valori di esempio per i principali fattori di influenza. Ad esempio, il **probabilità del valore 1** corrisponde a 60,6% e **probabilità di valore 2** corrisponde a 8,30%, vale a dire che, quando Average Time Per Issue era compreso nell'intervallo di 44-70 minuti, 60,6% dei casi sono nel turno con i più elevata dei livelli di servizio (valore 1) e l'8,30% dei casi sono nel turno con i livelli di servizio peggiori (valore 2).  
  
 Da queste informazioni è possibile trarre alcune conclusioni. I tempi di risposta alle chiamate più brevi (intervallo 44-70) influiscono decisamente su un livello di servizio migliore (intervallo 0,00-0,07). Il punteggio (92,35) suggerisce che questa variabile è molto importante.  
  
 Tuttavia, analizzando l'elenco dei fattori di influenza, è possibile notare altri fattori con effetti più complessi e più difficili da interpretare. Ad esempio, il turno sembra influire sul servizio, ma i punteggi di accuratezza e le probabilità relative indicano che il turno non è un fattore principale.  
  
|attribute|Value|Predilige \< 0,07|Predilige >= 0,12|  
|---------------|-----------|--------------------|----------------------|  
|Average Time Per Issue|89.087 - 120.000||Punteggio:  100<br /><br /> Probabilità di Value1: 4.45 %<br /><br /> Probabilità di Value2: 51.94 %<br /><br /> Livello di accuratezza per Value1: 0.19<br /><br /> Livello di accuratezza per Value2: 1.94|  
|Average Time Per Issue|44.000 - 70.597|Punteggio: 92.35<br /><br /> Probabilità di Value1: 60.06 %<br /><br /> Probabilità di Value2: 8.30 %<br /><br /> Livello di accuratezza per Value1: 2.61<br /><br /> Livello di accuratezza per Value2: 0.31||  
  
 [Torna all'inizio](#bkmk_NNviewer)  
  
##  <a name="bkmk_genviewer"></a> Microsoft Generic Content Tree Viewer  
 Questo visualizzatore può essere utilizzato per visualizzare informazioni ancora più dettagliate create dall'algoritmo quando il modello viene elaborato. Il **MicrosoftGeneric Content Tree Viewer** rappresenta il modello di data mining come serie di nodi, in cui ogni nodo rappresenta le informazioni sui dati di training. Questo visualizzatore può essere utilizzato con tutti i modelli, ma il contenuto dei nodi è diverso a seconda del tipo di modello.  
  
 Per i modelli di rete neurale o i modelli di regressione logistica, il `marginal statistics node` può risultare particolarmente utile. Questo nodo contiene statistiche derivate sulla distribuzione di valori nei dati. Queste informazioni possono risultare utili se si desidera ottenere un riepilogo dei dati senza dovere scrivere molte query T-SQL. Il grafico dei valori per la creazione di contenitori nell'argomento precedente deriva dal nodo delle statistiche marginali.  
  
#### <a name="to-obtain-a-summary-of-data-values-from-the-mining-model"></a>Per ottenere un riepilogo dei valori dei dati dal modello di data mining  
  
1.  Progettazione modelli di Data Mining, nelle **visualizzatore modello di Data Mining** scheda, seleziona \<Predict=1=«mining model name >.  
  
2.  Dal **Viewer** elenco, selezionare **Microsoft Generic Content Tree Viewer**.  
  
     La vista del modello di data mining verrà aggiornata per visualizzare una gerarchia di nodi nel riquadro sinistro e una tabella HTML nel riquadro destro.  
  
3.  Nel **didascalia del nodo** riquadro, fare clic sul nodo denominato 10000000000000000.  
  
     Il nodo di livello più alto in qualsiasi modello è sempre il nodo radice del modello. In un modello di rete neurale o di regressione logistica il nodo immediatamente successivo è il nodo delle statistiche marginali.  
  
4.  Nel **dei dettagli del nodo** riquadro, scorrere verso il basso fino a individuare la riga NODE_DISTRIBUTION.  
  
5.  Scorrere la tabella NODE_DISTRIBUTION per visualizzare la distribuzione dei valori calcolati dall'algoritmo Microsoft Neural Network.  
  
 Per utilizzare questi dati in un report, è possibile selezionare e copiare le informazioni per le righe specifiche oppure utilizzare la query DMX (Data Mining Extensions) seguente per estrarre il contenuto completo del nodo.  
  
```  
SELECT *   
FROM [Call Center EQ4].CONTENT  
WHERE NODE_NAME = '10000000000000000'  
```  
  
 È inoltre possibile utilizzare la gerarchia di nodi e i dettagli nella tabella NODE_DISTRIBUTION per attraversare singoli percorsi della rete neurale e visualizzare statistiche del livello nascosto. Per altre informazioni, vedere [Neural Network Model Query Examples](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md).  
  
 [Torna all'inizio](#bkmk_NNviewer)  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Aggiunta di un modello di regressione logistica alla struttura del Call Center &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto dei modelli di data mining per i modelli di rete neurale &#40;Analysis Services - Data mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Esempi di query sul modello di rete neurale](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Microsoft Neural Network Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Modificare la discretizzazione di una colonna in un modello di data mining](../../2014/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)  
  
  
