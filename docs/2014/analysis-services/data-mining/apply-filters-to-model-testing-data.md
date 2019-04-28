---
title: Applicare filtri ai dati di Testing del modello | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input row filtering [SQL Server]
- filtering input rows [Analysis Services]
- Mining Accuracy Chart [Analysis Services], filtering input rows
ms.assetid: 9ccc9a23-5597-4b35-a05f-2fc8eb885147
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 967de27eb9bc1f191b138e8b5962b04c145fe191
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689361"
---
# <a name="apply-filters-to-model-testing-data"></a>Applicare filtri ai dati di test del modello
  Quando si specifica un'origine dati esterna da usare per il test di un modello, è possibile applicare un filtro per limitare i dati di input. È ad esempio possibile testare il modello in modo specifico per le stime sui clienti in una determinata fascia di reddito.  
  
 Nello scenario mailing diretto di AdventureWorks mirato, ad esempio, è possibile creare un'espressione di filtro come quello seguente in ProspectiveBuyer, ovvero la tabella che contiene i dati di test, e limitare i test case per fascia di reddito:  
  
 `[YearlyIncome] = '50000'`  
  
 Il comportamento dei filtri cambia a seconda che i filtri vengano applicati ai dati di training del modello o al set di dati di test:  
  
-   Quando si definisce un filtro su un set di dati di test, si crea una clausola WHERE sui dati in ingresso. Se si applica un filtro su un set di dati di input utilizzato per la valutazione di un modello, l'espressione di filtro viene convertita in un'istruzione Transact-SQL e applicata alla tabella di input durante la creazione del grafico. Di conseguenza, il numero di test case può essere sostanzialmente ridotto.  
  
-   Quando si applica un filtro su un modello di data mining, l'espressione di filtro creata viene convertita in un'istruzione DMX (Data Mining Extensions) e applicata al singolo modello. Di conseguenza, quando si applica un filtro a un modello, solo un subset dei dati originali viene utilizzato per il training del modello. Questo può essere causa di problemi se il modello di training viene filtrato con un set di criteri in modo che il modello venga ottimizzato in base a un determinato set di dati, e quindi testato con un altro set di criteri.  
  
-   Se durante la creazione della struttura è stato definito un set di dati di test, i case del modello usati per il training includono solo quelli presenti nel set di training della struttura di data mining **e** che soddisfano le condizioni del filtro. Pertanto, quando si testa un modello e si seleziona l'opzione **Usa test case del modello di data mining**i test case includono solo i case presenti nel set di test della struttura di data mining che soddisfano le condizioni del filtro. Se, tuttavia, non è stato definito un set di dati di controllo, i case del modello utilizzati per il test includono tutti i case presenti nel set di dati che soddisfano le condizioni del filtro.  
  
-   Le condizioni del filtro che si applicano a un modello influiscono anche sulle query drill-through sui case del modello.  
  
 In breve, quando si testano più modelli, anche se tutti i modelli sono basati sulla stessa struttura di data mining, è necessario tenere presente che i modelli utilizzano potenzialmente subset diversi di dati per il training e il test. Questo può produrre gli effetti seguenti sui grafici di accuratezza:  
  
-   Il numero totale di casi nei set di test può variare tra i modelli testati.  
  
-   Le percentuali per ogni modello potrebbero non allinearsi nel grafico se i modelli utilizzano subset diversi di dati di training o dati di test.  
  
 Per determinare se un modello contiene un filtro predefinito che potrebbe influire sui risultati, è possibile cercare la proprietà **Filtro** nel riquadro **Proprietà** oppure eseguire una query sul modello tramite i set di righe dello schema di data mining. La query seguente, ad esempio, restituisce il testo del filtro per il modello specificato:  
  
 `SELECT [FILTER] FROM $system.DMSCHEMA_MINING_MODELS WHERE MODEL_NAME = 'name of model'`  
  
> [!WARNING]  
>  Se si desidera rimuovere il filtro da un modello di data mining esistente o modificare le condizioni del filtro, è necessario rielaborare il modello di data mining.  
  
 Per altre informazioni sui tipi di filtri che è possibile applicare e sulle modalità di valutazione delle espressioni di filtro, vedere [Sintassi ed esempi di filtri dei modelli &#40;Analysis Services – Data mining&#41;](model-filter-syntax-and-examples-analysis-services-data-mining.md).  
  
### <a name="create-a-filter-on-external-testing-data"></a>Creare un filtro sui dati di test esterni  
  
1.  Fare doppio clic sulla struttura di data mining che contiene il modello che si desidera testare per aprire Progettazione modelli di data mining.  
  
2.  Selezionare la scheda **Grafico di accuratezza modello di data mining** , quindi selezionare la scheda **Selezione input** .  
  
3.  Nell'area **Seleziona set di dati da usare per il grafico di accuratezza** della scheda **Selezione input**selezionare l'opzione **Specifica un set di dati diverso**.  
  
4.  Fare clic sul pulsante **(...)**  per aprire una finestra di dialogo e scegliere il set di dati esterno.  
  
5.  Scegliere la tabella del case e aggiungere, se necessario, una tabella nidificata. Se necessario, eseguire il mapping delle colonne del modello alle colonne del set di dati esterno. Chiudere la finestra di dialogo **Specifica mapping colonne** per salvare la definizione della tabella di origine.  
  
6.  Fare clic su **Apri editor filtri** per definire un filtro per il set di dati.  
  
     Verrà visualizzata la finestra di dialogo **Filtro dei set di dati** . Se la struttura contiene una tabella nidificata, è possibile creare un filtro in due parti. Per prima cosa, impostare le condizioni sulla tabella del case usando la finestra di dialogo **Filtro dei set di dati** , quindi impostare le condizioni sulle righe annidate usando la finestra di dialogo **Filtro** .  
  
7.  Nella finestra di dialogo **Filtro dei set di dati** fare clic sulla riga superiore della griglia, in **Colonna struttura di data mining**, quindi selezionare una tabella o una colonna dall'elenco.  
  
     Se la vista origine dati contiene più tabelle o una tabella nidificata, è necessario selezionare prima il nome della tabella. In caso contrario, è possibile selezionare le colonne direttamente dalla tabella del case.  
  
     Aggiungere una nuova riga per ogni colonna che si desidera filtrare.  
  
8.  Usare le colonne **Operator**e **Value** per definire il modo in cui la colonna viene filtrata.  
  
     **Note** Digitare i valori senza usare le virgolette.  
  
9. Fare clic sulla casella di testo **And/Or** e selezionare un operatore logico per definire la modalità di combinazione di più condizioni.  
  
10. Facoltativamente, fare clic sul pulsante Sfoglia **(...)**  a destra della **valore** casella di testo per aprire la **filtro** dialogo casella e impostare le condizioni sulla tabella nidificata o nelle colonne della tabella del case singolo.  
  
11. Verificare la correttezza delle condizioni di filtro completate visualizzando il testo nel riquadro **Espressione** .  
  
12. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     La condizione di filtro viene applicata all'origine dati quando si crea il grafico di accuratezza.  
  
## <a name="see-also"></a>Vedere anche  
 [Scegliere ed eseguire il mapping dei dati di test del modello](choose-and-map-model-testing-data.md)   
 [Utilizzo di dati di tabelle nidificate come input per un grafico di accuratezza](using-nested-table-data-as-an-input-for-an-accuracy-chart.md)   
 [Scegliere un tipo di grafico di accuratezza e impostare le opzioni del grafico](choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
