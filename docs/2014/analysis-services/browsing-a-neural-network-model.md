---
title: Esplorazione di un modello di rete neurale | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- mining model, neural network
- neural networks
- dependency network
ms.assetid: e4224cb7-115b-4889-ac07-03f096fb55fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b32db07a67e309d304aeb145be59fd79c0af5f49
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78174230"
---
# <a name="browsing-a-neural-network-model"></a>Esplorazione di un modello di rete neurale
  Quando si apre un modello di regressione logistica o di rete neurale utilizzando **Sfoglia**, il modello viene visualizzato in un visualizzatore interattivo, simile al visualizzatore del modello di rete neurale in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Il visualizzatore consente di esplorare le correlazioni e ottenere informazioni sugli schemi del modello e sui dati sottostanti.

##  <a name="BKMK_Tabs"></a>Esplorare il modello
 I modelli basati sugli algoritmi di [!INCLUDE[msCoName](../includes/msconame-md.md)] Neural Network o Logistic Regression sono simili nel senso che analizzano i dati come set di connessioni tra gli input e gli output noti. Il visualizzatore **Sfoglia** consente di esplorare tali connessioni tramite i controlli seguenti:

-   [Variabili](#BKMK_Variables)

-   [Input](#BKMK_Inputs)

-   [Output](#BKMK_Outputs)

 Per provare questo visualizzatore, è possibile creare un modello tramite [Procedura guidata Classificazione &#40;componenti aggiuntivi Data Mining per Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md) e usare l'opzione **Avanzate** per modificare l'algoritmo in Microsoft Logistic Regression nella finestra di dialogo **Parametri algoritmo**.

###  <a name="BKMK_Variables"></a>Variabili
 Nel riquadro **Variabili** viene visualizzato un elenco di variabili di input nell'ordine del relativo effetto sul modello. Usare i controlli **Output** e **Input** per filtrare il modello, influendo sulle variabili visualizzate e sul relativo ordine.

 Utilizzando questo visualizzatore, è possibile esplorare i fattori che sono più importanti per determinare se è più probabile che un cliente appartenga alla categoria di acquirenti di biciclette o alla categoria di non acquirenti.

 ![Effetto dei test sui risultati degli attributi selezionati](media/dm13-neuralnet-agebuyer1.gif "Effetto dei test sui risultati degli attributi selezionati")

##### <a name="explore-variables"></a>Esplorazione delle variabili

1.  Inizialmente, il riquadro **Variabili** viene ordinato in base agli attributi più importanti, dati i filtri correnti. La lunghezza della barra indica l'attendibilità del fattore.

     Nell'esempio, è possibile osservare che il reddito è il fattore più influente, seguito dall'area. D'altra parte, è altamente improbabile che i clienti con molte automobili e molti figli acquisteranno una bicicletta.

2.  Nel riquadro **Variabili** fare clic sull'intestazione di colonna **Attributo**.

     Eseguendo l'ordinamento in base all'attributo, è possibile visualizzare i contenitori creati per ciascuna delle colonne di input. Le colonne con valori discreti, ad esempio occupation, sono *suddivise* dai valori letterali.

3.  Si notino gli intervalli di valori trovati per **Age** e **Income**.

     Se una qualsiasi delle colonne di input è in numeri, ossia l'intera colonna di dati è un tipo di dati numerici continui, i numeri sono inseriti in bucket, o suddivisi, in intervalli discreti.

     Per Income, la colonna è stata suddivisa in raggruppamenti, ad esempio 78.4-154.06 (per l'intervallo di reddito superiore).

     ![Ordinamento per visualizzare la modalità di suddivisione delle variabili](media/dm13-nn-bucketing-variables.gif "Ordinamento per visualizzare la modalità di suddivisione delle variabili")

     Se si desiderano raggruppamenti differenti, è necessario usare lo strumento [Modifica etichette &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](relabel-sql-server-data-mining-add-ins.md) o le funzioni di Excel per creare nuove categorie di reddito prima di compilare il modello.

4.  Fare clic su **Predilige Sì** per ripristinare la vista predefinita del grafico.

     Per impostazione predefinita, la vista viene ordinata in base al valore di **Predilige** per il primo valore del risultato. È possibile modificare i risultati assegnati alla prima e alla seconda colonna scegliendo un nuovo valore per **Valore 1** e **Valore 2** in **Output**.

5.  Posizionare il mouse sulla barra colorata superiore del grafico.

     Viene visualizzata una descrizione comando che include un punteggio della *priorità*, una coppia di punteggi di *probabilità* e una coppia di valori di *accuratezza*.

    -   L' **importanza** viene calcolata nell'intero set di dati e identifica l'attributo che, dati tutti gli input, è più correlato al risultato di destinazione. Nel visualizzatore vengono ordinati i valori nel grafico in base ai punteggi di priorità.

    -   La **probabilità** viene calcolata per ogni set di coppie attributo-valore, per i risultati di destinazione, nell'intero set di dati.

    -   **Lift** indica quanto è utile questa particolare coppia attributo-valore per la promozione di un risultato o di un altro.

     Nota: nella descrizione comando sono contenute le stesse informazioni indipendentemente dal fatto che si posizioni il mouse su una colonna o sull'altra.

 [Torna all'inizio](#BKMK_Tabs)

###  <a name="BKMK_Inputs"></a>Input
 Il riquadro **Input** consente di scegliere un set di input e applicarlo come filtro al modello. In questo modo è possibile vedere l'influenza di tali scelte sul risultato, in base ai dati di training

##### <a name="explore-inputs"></a>Esplorazione degli input

1.  Si supponga di voler fare riferimento a un gruppo specifico e visualizzare i fattori che hanno influito maggiormente sugli acquisti in tale gruppo.

     Nel riquadro **input** fare clic sulla ** \<cella all>** in **attributo**e selezionare **Age**.

     Per **Valore** selezionare la categoria di età più giovane.

2.  Si noti che anche quando si filtra una fascia di età specifica, l'area Pacifico viene inclusa nella parte superiore dell'elenco. Questo avviene perché i clienti nell'area Pacifico hanno maggiore probabilità di acquistare una bicicletta rispetto ai clienti in altre aree.

     Poiché l'area non è un fattore che è possibile influenzare, per non prendere in considerazione questa variabile e visualizzare altri fattori, è possibile modificare di nuovo gli input.

     Nel riquadro **Input** fare clic sulla cella vuota sotto **Age** e selezionare **Region**.

     Per **Valore** selezionare **Europe**.

3.  Continuare ad aggiungere i filtri di input per concentrarsi su un gruppo di particolare interesse.

     Ad esempio, per l'attributo di input, aggiungere **Gender** e selezionare **Female** come valore.

     ![Effetto dei test sui risultati degli attributi selezionati](media/dm13-neuralnet-agebuyer2.gif "Effetto dei test sui risultati degli attributi selezionati")

     Si noti come l'elenco di variabili cambia. Ora **Income** è la variabile più importante nella stima del risultato di destinazione.

     L'ordine in cui si applicano i filtri di input non influisce sui risultati.

 [Torna all'inizio](#BKMK_Tabs)

###  <a name="BKMK_Outputs"></a>Uscite
 Nel riquadro **Output** è possibile scegliere il risultato a cui si è interessati. Le reti neurali consentono di specificare il numero di colonne di risultati desiderato, sebbene l'aggiunta di più output aumenti la complessità del modello e possa richiedere un tempo di elaborazione più lungo.

 Per confrontare due output, essi devono essere stati definiti come colonne **Stima** o **Solo stima**.

##### <a name="explore-outputs"></a>Esplorazione degli output

1.  Per selezionare un attributo, usare l'elenco **Attributo output**.

2.  Selezionare due risultati dagli elenchi Valore 1 e Valore 2. Questi due stati dell'attributo di output verranno confrontati nel riquadro **Variabili** .

 [Torna all'inizio](#BKMK_Tabs)

## <a name="more-about-neural-network-models"></a>Ulteriori informazioni sui modelli di rete neurale
 Le informazioni nel visualizzatore vengono recuperate dal server utilizzando una stored procedure specifica di questo tipo di modello: System.Microsoft.AnalysisServices.System.DataMining.NeuralNet.GetAttributeScores.

 Se si desidera creare un modello con più attributi stimabili tramite i componenti aggiuntivi, usare le opzioni di modellazione **Avanzate**.

 Per altre informazioni, vedere [Crea struttura di data mining &#40;componenti aggiuntivi Data Mining di SQL Server&#41;](create-mining-structure-sql-server-data-mining-add-ins.md) e [Aggiunta modello a struttura &#40;componenti aggiuntivi Data Mining per Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md).

## <a name="see-also"></a>Vedere anche
 [Esplorazione di modelli in Excel &#40;SQL Server componenti aggiuntivi Data mining&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)


