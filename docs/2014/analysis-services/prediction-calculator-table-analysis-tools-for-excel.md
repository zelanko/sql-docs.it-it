---
title: Calcolo stime (strumenti di analisi tabelle per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining model, regression
- Table Analysis tools
- scorecard
- logistic regression
- prediction calculator
ms.assetid: 8bb8c318-e85f-4fd6-b32b-4cdfb13ca1b5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e57aee7142da5c256a213ddd2eb0390a0f3b042a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070855"
---
# <a name="prediction-calculator-table-analysis-tools-for-excel"></a>Calcolo stime (Strumenti di analisi tabelle per Excel)
  ![Strumento Calcolo stime](media/tat-predcal.gif "Strumento Calcolo stime")  
  
 Lo strumento **Calcolo stime** consente di creare una scorecard che può essere usata per analizzare i nuovi dati e valutare le opzioni o i rischi. Se, ad esempio, si dispone di dati cronologici e demografici sui clienti, lo strumento **Calcolo stime** può essere utile per due attività principali:  
  
-   Generazione di un'analisi sottostante dei dati demografici, del comportamento di acquisto e di diversi altri fattori.  
  
-   Creazione di una scorecard di lavoro che consenta di valutare i membri e fornire suggerimenti relativi a offerte di nuovi prodotti o servizi.  
  
 Tramite la procedura guidata viene inoltre creato un foglio di lavoro in cui vengono archiviati tutti i calcoli sottostanti, in modo che sia possibile interagire con il modello e vedere in che modo valori di input diversi influiscono sul punteggio finale.  
  
 Se si desidera, la procedura guidata consente inoltre di creare una versione stampata del foglio di lavoro da utilizzare per l'assegnazione dei punteggi offline. Non è possibile interagire con il modello come si può fare con la cartella di lavoro di Excel online, ma la versione stampata fornisce tutti i calcoli necessari per immettere i valori e calcolare un punteggio finale.  
  
## <a name="using-the-prediction-calculator-tool"></a>Utilizzo dello strumento Calcolo stime  
  
1.  Aprire una tabella di Excel contenente i dati che si desidera analizzare.  
  
2.  Fare clic su **Calcolo stime** nella scheda **analizza** .  
  
3.  Nella finestra di dialogo **Calcolo stime** per destinazione scegliere la colonna che si desidera stimare, ad esempio comportamento di acquisto.  
  
4.  Specificare il valore di destinazione. Se il valore è numerico, utilizzare l'opzione **in intervallo**, quindi digitare i valori minimo e massimo per l'intervallo desiderato. Se il valore è discreto, selezionare l'opzione **exact** , quindi selezionare il valore nell'elenco a discesa.  
  
5.  Fare clic su **scegliere le colonne da utilizzare per l'analisi**.  
  
6.  Nella finestra di dialogo **selezione avanzata colonne** selezionare le colonne contenenti informazioni utili. Rimuovere eventuali colonne non rilevanti per l'analisi. Fare clic su **OK**.  
  
     Per evitare di distorcere i risultati, rimuovere anche le colonne contenenti informazioni duplicate. Se, ad esempio, sono presenti una colonna Income contenente dati numerici e una colonna Income Group contenente le etichette High, Medium e Low, non includere entrambe le colonne nello stesso modello. Creare invece un modello separato per ogni colonna.  
  
7.  Nella sezione **Opzioni di output** selezionare **calcolatrice operativa** per creare l'analisi e la scorecard in una cartella di lavoro di Excel. Selezionare **calcolatore pronto** per la stampa per creare l'analisi e generare un report che può essere stampato e usato per la valutazione manuale.  
  
8.  Fare clic su **Esegui**.  
  
     Tramite lo strumento vengono creati nuovi fogli di lavoro contenenti i report e le scorecard.  
  
### <a name="requirements"></a>Requisiti  
 Lo strumento **Calcolo stime** usa l'algoritmo di regressione logistica Microsoft, che può funzionare con valori discreti, nonché dati numerici Discretizzazione e continui.  
  
## <a name="understanding-the-scoring-reports"></a>Informazioni sui report per l'assegnazione dei punteggi  
 Se si selezionano entrambe le opzioni di output, tramite lo strumento Calcolo stime vengono creati nella cartella di lavoro corrente i tre nuovi fogli di lavoro seguenti:  
  
-   **Report di stima**che contiene i risultati dell'analisi, completi di tabelle e grafici interattivi che consentono di sperimentare interazioni e profitti.  
  
-   **Calcolo stime** interattiva che consente di creare punteggi.  
  
-   Un **calcolatore stampabile** con istruzioni e coefficienti da usare per l'assegnazione dei punteggi.  
  
-   In questa sezione vengono descritte le informazioni incluse in ogni report e viene illustrato come utilizzare le varie opzioni dei report.  
  
### <a name="prediction-report-with-graphs"></a>Report di stima con grafici  
 Il primo report di stima è denominato **Calcolo stime report per lo \<stato di destinazione> della \<>degli attributi di destinazione **. Questo report contiene una tabella di fattori derivati dall'analisi, insieme agli strumenti che consentono di valutare l'impatto finanziario di una determinata analisi.  
  
#### <a name="table-for-specifying-costs-and-profits"></a>Tabella per la specifica di costi e profitti  
 Il primo strumento di questo report, che si trova in alto a sinistra nel report, è una tabella in cui è possibile specificare i costi e i profitti associati alla stima corretta e non corretta di un valore.  Questi costi e profitti sono necessari per calcolare il valore di soglia ottimale per il punteggio per lo strumento di calcolo.  
  
|Elemento|Descrizione ed esempio|  
|----------|-----------------------------|  
|Costo falso positivo|Costo da sostenere quando si presuppone che il modello abbia stimato correttamente un risultato positivo mentre in realtà la stima è errata.<br /><br /> Questo avviene, ad esempio, quando tramite il modello viene stimato che un cliente acquisterà un determinato oggetto e, in base a tale stima, si concepisce una campagna destinata a tale cliente. In questo caso è possibile immettere in questo campo il costo sostenuto per raggiungere il cliente.|  
|Costo falso negativo|Costo da sostenere quando si presuppone che il modello abbia stimato correttamente un risultato negativo mentre in realtà la stima è errata.<br /><br /> Questo avviene, ad esempio, quando tramite il modello viene stimato che è improbabile che i clienti meno giovani acquistino una bicicletta, ma ci si accorge di una distorsione del modello a causa della quale si è persa l'opportunità di rivolgersi ai clienti meno giovani. In questo caso è possibile immettere in questo campo il costo legato all'opportunità persa.|  
|Profitto vero positivo|Profitto ottenuto grazie alla stima corretta di un risultato positivo. Se, ad esempio, ci si rivolge ai clienti appropriati e se si superano i risultati di vendita prefissati, in questo campo è possibile immettere il profitto ottenuto per ogni cliente.|  
|Profitto vero negativo|Profitto ottenuto grazie alla stima corretta di un risultato negativo.<br /><br /> Se, ad esempio, è possibile identificare correttamente i clienti a cui non ci si deve rivolgere, in questo campo è possibile immettere un determinata somma di denaro destinata alla pubblicità per ogni cliente.|  
  
#### <a name="chart-for-viewing-maximum-profit"></a>Grafico per la visualizzazione del profitto massimo  
 Man mano che si immettono i valori nella tabella, i grafici correlati vengono aggiornati automaticamente per indicare il punto migliore per massimizzare il profitto in base al modello corrente. Nel grafico a linee a destra di questa tabella è visualizzato il profitto per diversi valori di soglia per il punteggio. Il profitto viene stimato utilizzando le cifre relative a profitto e costo digitate nella tabella, in base alle stime e alle probabilità del modello.  
  
 Se, ad esempio, nella tabella in alto a sinistra la cella per la **soglia suggerita per massimizzare il profitto** Mostra il valore 500, il grafico sul lato destro indicherà 500 come punto più alto sul grafico a linee. Questo valore 500 significa che per massimizzare i profitti è necessario utilizzare le prime 500 indicazioni del modello di data mining, ordinate in base alla probabilità.  
  
#### <a name="table-listing-scores-for-each-attribute-and-value"></a>Tabella con i punteggi per ogni attributo e valore  
 La tabella in basso a sinistra nel report mostra una suddivisione dettagliata dei valori rilevati e indica in che modo ogni valore influisce sul risultato. Non è possibile modificare i valori in questa tabella, che sono visualizzati solo per semplificare la comprensione della stima.  
  
 Nella tabella seguente è illustrato un esempio dei risultati quando il risultato che si desidera ottenere è l'acquisto di una bicicletta da parte di un cliente. Nella tabella viene elencata ogni colonna di input utilizzata nel modello, indipendentemente dal fatto che l'input influisca sul modello. Nella tabella vengono inoltre elencati i valori discreti e i valori discretizzati nel caso in cui la colonna di input contenesse dati numerici continui.  
  
 I valori nella colonna **Impact relativa** sono probabilità, rappresentati come percentuali. La cella è ombreggiata per rappresentare visivamente l'impatto di questo valore sui risultati.  
  
|Attributo|valore|Impatto relativo|  
|---------------|-----------|---------------------|  
|Marital Status|Married|0|  
|Marital Status|Single|71|  
|Sesso|Femmina|13|  
|Sesso|Maschio|0|  
  
 È possibile interpretare questi fattori come indicato di seguito:  
  
-   Il fatto di essere sposato non influisce sulla probabilità di acquisto di una bicicletta da parte di un cliente.  
  
-   Il fatto di non essere sposato è tuttavia un importante indicatore (70%) della probabilità di acquisto di una bicicletta da parte di un cliente.  
  
-   Il sesso del cliente ha solo un effetto marginale (13%) sul comportamento di acquisto di una bicicletta stimato nel caso in cui il cliente sia una donna e non ha alcun effetto su tale comportamento nel caso in cui il cliente sia un uomo.  
  
#### <a name="chart-of-cumulative-misclassification-cost"></a>Grafico del costo cumulativo di classificazione non corretta  
 Il grafico ad area in basso a destra nel report indica il costo cumulativo di classificazione non corretta per diversi valori di soglia per il punteggio. In questo grafico vengono utilizzate anche le cifre immesse relative a falsi positivi, veri positivi, falsi negativi e veri negativi.  
  
 A differenza del grafico in alto a destra nel report, che è incentrato sul raggiungimento del profitto massimo, questo grafico incorpora il costo legato all'esecuzione di una stima errata. Questo grafico è particolarmente utile in scenari come la prevenzione, dove il costo di una decisione errata supera significativamente il costo di un'ipotesi corretta.  
  
 Anche se, ad esempio, il primo grafico suggerisce che rivolgendosi ai primi 500 clienti stimati dal modello è possibile ottenere il massimo profitto, dopo aver analizzato il secondo grafico è possibile stabilire che i costi da sostenere rivolgendosi ai clienti errati sono troppo elevati e decidere pertanto di limitare la campagna di marketing ai primi 400 clienti.  
  
### <a name="interactive-prediction-calculator"></a>Calcolo stime interattivo  
 Il secondo foglio di lavorazione creato dallo strumento Calcolo stime è denominato **Calcolo stime per lo \<stato di destinazione> \<dell'attributo di destinazione>**. Si tratta di un foglio di lavoro interattivo che è possibile utilizzare per calcolare i singoli punteggi. Poiché in questo foglio di lavoro vengono utilizzati modelli e statistiche archiviati nel modello, è possibile provare a utilizzare valori diversi e vedere in che modo questi influiscono sul punteggio stimato. Anche questo report è costituito da due sezioni, una interattiva e una fornita come riferimento.  
  
#### <a name="first-table"></a>Prima tabella  
 È possibile selezionare o digitare un nuovo valore nella colonna **valore** della tabella per vedere come la modifica del valore influisca sul punteggio.  
  
 Se, ad esempio, il report contiene i valori seguenti, è possibile ridurre il valore di Cars a 1, quindi a 0 per vedere in che modo questo valore influisce sul comportamento di acquisto del cliente. Quando si imposta il valore di **Cars** su 0, la stima nella parte inferiore diventa true.  
  
|Attributo|valore|Impatto relativo|  
|---------------|-----------|---------------------|  
|Marital Status|Married|0|  
|Sesso|Maschio|0|  
|Income|39050-71062|117|  
|Children|0|157|  
|Formazione|Bachelors|22|  
|Occupation|Skilled Manual|33|  
|Home Owner|Sì|8|  
|Cars|2|50|  
|Commute Distance|0-1 Miles|99|  
|Region|America del Nord|0|  
|Age|37-46|5|  
|Totale||491|  
|Prediction for 'Yes'||FALSE|  
  
 Quando si digita il nuovo valore, viene aggiornato anche il Punteggio visualizzato nella cella, la stima per Sì, le modifiche a TRUE e i punteggi di **conseguenze relative** per i diversi attributi.  
  
> [!NOTE]  
>  Anche se si modifica un solo valore, ad esempio il numero di auto, i valori e gli impatti degli altri attributi possono cambiare. Questo avviene in quanto i modelli di data mining spesso consentono di individuare relazioni complesse tra i dati e la modifica di una variabile qualsiasi può avere effetti imprevisti. Per questo motivo, è consigliabile utilizzare lo strumento Calcolo stime interattivo per provare valori diversi o esplorare il modello di data mining per comprendere meglio le interazioni. Per ulteriori informazioni, vedere [Browse Models](prediction-calculator-table-analysis-tools-for-excel.md).  
  
#### <a name="score-breakdown"></a>Suddivisione punteggio  
 In questa tabella sono indicati i singoli punteggi per ogni possibile stato delle colonne di input e l'impatto relativo del punteggio sui risultati. Questa tabella è statica e serve solo come riferimento.  
  
### <a name="printable-prediction-calculator"></a>Calcolo stime stampabile  
 Il terzo foglio di calcolo creato dallo strumento Calcolo stime è denominato **PrintablePrediction Calculator per lo \<stato di destinazione> \<dell'attributo di destinazione>**. Questa scorecard può essere stampata e utilizzata per calcolare manualmente i punteggi quando non si è al computer.  
  
##### <a name="to-print-and-use-the-scoring-report-generated-by-the-prediction-calculator"></a>Per stampare e utilizzare il report per l'assegnazione dei punteggi generato da Calcolo stime  
  
1.  Fare clic sulla scheda denominata **stampabile Calcolo stime per \<attributo>**.  
  
2.  Scegliere **Anteprima di stampa**dal menu file di Excel.  
  
3.  Modificare l'orientamento della pagina, i margini e altre opzioni di stampa fino a posizionare la scorecard nella pagina nel modo desiderato.  
  
     Questa scorecard non è dinamica e non è connessa in alcun modo al modello, pertanto è possibile spostare le colonne o le righe per migliorare la formattazione senza influire sui dati sottostanti.  
  
4.  Stampare la scorecard.  
  
5.  Per ogni attributo, scegliere un solo valore. Per il valore scelto, inserire un segno di spunta nella casella e scrivere il numero corrispondente nella colonna **Score** .  
  
6.  Inserire il maggior numero di attributi possibile per garantire l'accuratezza.  
  
7.  Calcolare la somma dei punteggi per ogni attributo e immettere tale numero nella riga del **totale** .  
  
8.  Convertire il punteggio in un risultato stimato usando i criteri stampati nel foglio immediatamente dopo la riga del **totale** .  
  
## <a name="related-tools"></a>Strumenti correlati  
 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] fornisce l'algoritmo Microsoft Logistic Regression per l'utilizzo con questo tipo di analisi. Se si ha già familiarità con la regressione logistica, è possibile creare facilmente modelli di regressione logistica utilizzando l'opzione **Avanzate** del client di data mining per Excel. Per ulteriori informazioni, vedere la pagina relativa alla [modellazione avanzata &#40;componenti aggiuntivi Data mining per&#41;Excel ](advanced-modeling-data-mining-add-ins-for-excel.md). Per ulteriori informazioni sulle opzioni e sui parametri per i modelli di regressione logistica, vedere l'argomento "algoritmo di regressione logistica [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Microsoft" nella documentazione online di.  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)  
  
  
