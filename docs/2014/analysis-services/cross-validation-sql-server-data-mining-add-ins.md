---
title: Convalida incrociata (componenti aggiuntivi Data mining SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cross-validation
- partitioning data [data mining]
- mining models, testing
ms.assetid: bf9483b3-4099-41c4-bbc5-da7005e07bcd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cc3a132792cca8ecdf5a33a2fe4e4d40116c497
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086645"
---
# <a name="cross-validation-sql-server-data-mining-add-ins"></a>Convalida incrociata (componenti aggiuntivi Data mining di SQL Server)
  ![Pulsante Convalida incrociata, barra multifunzione Data mining](media/dmc-xvalid.gif "Pulsante Convalida incrociata, barra multifunzione Data mining")  
  
 La convalida incrociata è un strumento standard di analisi e costituisce un'importante funzionalità per lo sviluppo e l'ottimizzazione dei modelli di data mining. La convalida incrociata viene utilizzata dopo aver creato un modello di data mining per verificare la validità del modello e confrontarne i risultati con altri modelli di data mining correlati.  
  
 La convalida incrociata è costituita da due fasi, training e generazione del report. I passaggi eseguiti sono i seguenti:  
  
-   Selezione di un modello o di una struttura di data mining di destinazione.  
  
-   Definizione del valore di destinazione, se applicabile.  
  
-   Consente di specificare il numero di sezioni incrociate, o *riduzioni*, in cui partizionare i dati della struttura.  
  
 Tramite la procedura guidata **convalida incrociata** viene quindi creato un nuovo modello in ognuna delle riduzioni, viene testato il modello sulle altre riduzioni e quindi viene segnalata l'accuratezza del modello. Al termine della procedura guidata **convalida incrociata** viene creato un report in cui vengono illustrate le metriche per ogni riduzioni e viene fornito un riepilogo del modello in modo aggregato. Queste informazioni possono essere utilizzate per determinare l'efficacia dei dati sottostanti per un modello o per confrontare modelli diversi creati in base agli stessi dati.  
  
## <a name="using-the-cross-validation-wizard"></a>Utilizzo della procedura guidata Convalida incrociata  
 È possibile utilizzare la convalida incrociata sia per modelli temporanei che per modelli archiviati in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
#### <a name="to-create-a-cross-validation-report"></a>Per creare un report di convalida incrociata  
  
1.  Nel gruppo **accuratezza e convalida** della barra multifunzione **data mining** fare clic su **convalida incrociata**.  
  
2.  Nella finestra di dialogo **selezione struttura o modello** selezionare una struttura o un modello di data mining esistente. Se si seleziona una struttura, tramite la procedura guidata viene utilizzata la convalida incrociata per tutti i modelli basati su tale struttura con lo stesso attributo stimabile. Se si seleziona un modello, la convalida incrociata viene utilizzata solo per tale modello.  
  
3.  Nella casella **conteggio di riduzioni** della finestra di dialogo **Specifica parametri di convalida incrociata** scegliere il numero di riduzioni tra le quali dividere il set di dati. Una riduzione è una sezione trasversale dei dati selezionata in modo casuale.  
  
4.  Facoltativamente, impostare il numero massimo di righe da utilizzare per la convalida incrociata digitando un numero nella casella di testo numero **massimo di righe** .  
  
    > [!NOTE]  
    >  Maggiore è il numero di righe utilizzato, più accurati saranno i risultati. Il tempo di elaborazione potrebbe tuttavia aumentare significativamente. Il numero scelto dipende dai dati, ma in generale è consigliabile scegliere il numero più elevato possibile senza influire negativamente sulle prestazioni. Per migliorare le prestazioni, è anche possibile specificare un numero minore di riduzioni.  
  
5.  Selezionare una colonna dall'elenco a discesa **attributo di destinazione** . Nell'elenco sono visualizzate solo le colonne configurate come attributi stimabili al momento della creazione iniziale del modello. Il modello può contenere più attributi stimabili, ma è possibile sceglierne uno solo.  
  
6.  Selezionare un valore dall'elenco a discesa **stato di destinazione** .  
  
     Se la colonna stimabile contiene dati numerici continui, questa opzione non è disponibile.  
  
7.  Facoltativamente, specificare un valore da usare come **soglia di destinazione** per conteggiare le stime come accurate. Questo valore viene espresso come probabilità, con un numero compreso tra 0 e 1, dove 1 indica che la stima è sicuramente accurata, 0 indica che non vi sono possibilità che la stima sia corretta e 0,5 corrisponde a un'ipotesi casuale.  
  
     Se la colonna stimabile contiene dati numerici continui, questa opzione non è disponibile.  
  
8.  Fare clic su **Fine**. Viene creato un nuovo foglio di vita, denominato **convalida incrociata**.  
  
    > [!NOTE]  
    >  Durante il partizionamento del modello in riduzioni e il test di ogni riduzione, Microsoft Excel potrebbe non rispondere.  
  
### <a name="requirements"></a>Requisiti  
 Per creare un report di convalida incrociata, è necessario avere già creato una struttura di data mining e i modelli correlati. Nella procedura guidata è disponibile una finestra di dialogo che consente di scegliere tra la struttura e i modelli esistenti.  
  
 Se si sceglie una struttura di data mining che supporta più modelli di data mining e nei modelli vengono utilizzati attributi stimabili diversi, tramite la procedura guidata Convalida incrociata vengono testati solo i modelli che condividono lo stesso attributo stimabile.  
  
 Se si sceglie una struttura che supporta sia i modelli di clustering che altri tipi di modelli, i modelli di clustering non vengono testati.  
  
## <a name="understanding-cross-validation-results"></a>Informazioni sui risultati della convalida incrociata  
 I risultati della convalida incrociata vengono visualizzati in un nuovo foglio di dati, denominato **report di convalida \<incrociata per nome attributo>**. Il nuovo foglio di lavoro contiene diverse sezioni. La prima sezione è un riepilogo che fornisce importanti metadati sul modello testato, in modo che sia possibile sapere a quale modello o struttura si riferiscono i risultati.  
  
 La seconda sezione del report fornisce un riepilogo statistico che indica l'efficacia del modello originale. In questo riepilogo, le differenze tra i modelli creati per ogni sezione vengono analizzate per tre misure chiave: *radice errore quadratico*medio, *errore assoluto medio*e *Punteggio di log*. Si tratta di misure statistiche standard utilizzate non solo nel data mining, ma anche nella maggior parte dei tipi di analisi statistica.  
  
 Per ognuna di queste misure, la procedura guidata Convalida incrociata consente di calcolare la deviazione media e standard dell'intero modello. Queste informazioni indicano la coerenza del modello quando si eseguono stime in diversi subset dei dati. Se, ad esempio, la deviazione standard è molto grande, significa che i modelli creati per ogni riduzione presentano risultati molto diversi e pertanto il training nel modello potrebbe essere stato eseguito in maniera troppo focalizzata su un gruppo specifico di dati e non essere applicabile agli altri set di dati.  
  
 Nella sezione seguente vengono illustrate le misure utilizzate per valutare i modelli.  
  
### <a name="tests-and-measures"></a>Test e misure  
 Oltre ad alcune informazioni di base relative al numero di riduzioni nei dati e alla quantità di dati in ciascuna riduzione, nel foglio di lavoro viene visualizzato un set di misure relative a ogni modello, suddivise in categorie in base al tipo di test. I test utilizzati per valutare l'accuratezza di un modello di clustering sono ad esempio diversi da quelli utilizzati per un modello di previsione.  
  
 Nella tabella seguente vengono elencati i test e le misure, con una spiegazione del significato della misura.  
  
#### <a name="aggregates-and-general-statistical-measures"></a>Aggregazioni e misure statistiche generali  
 Le misure di aggregazione incluse nel report indicano le differenze tra le riduzioni create nei dati.  
  
-   Deviazione media e standard.  
  
-   Media della deviazione rispetto al valore medio per una misura specifica, calcolata in tutte le partizioni di un modello.  
  
#### <a name="classification-passfail"></a>Classificazione: Test superato/Test non superato  
 Questa misura è utilizzata nei modelli di classificazione quando non si specifica un valore di destinazione per l'attributo stimabile. Se, ad esempio, si crea un modello per la stima di più possibilità, questa misura indica l'efficacia del modello nella stima di tutti i valori possibili.  
  
 Il superamento o l'esito negativo viene calcolato per conteggio dei case che soddisfano le condizioni seguenti: **passare** se lo stato stimato con la probabilità più elevata corrisponde allo stato di input e la probabilità è maggiore del valore specificato per **soglia di stato**; in caso contrario, **avrà esito negativo**.  
  
#### <a name="classification-true-or-false-positives-and-negatives"></a>Classificazione: veri o falsi positivi e negativi  
 Questo test viene utilizzato per tutti i modelli di classificazione con una destinazione specificata. La misura indica come viene classificato ogni case in risposta a domande relative a ciò che è stato stimato dal modello e al risultato effettivo ottenuto.  
  
|Measure|Descrizione|  
|-------------|-----------------|  
|Vero positivo|Numero di case che soddisfano le condizioni seguenti:<br /><br /> Il case contiene il valore di destinazione.<br /><br /> Tramite il modello è stato stimato che il case contiene il valore di destinazione.|  
|Falso positivo|Numero di case che soddisfano le condizioni seguenti:<br /><br /> Il valore effettivo è uguale a quello di destinazione.<br /><br /> Tramite il modello è stato stimato che il case contiene il valore di destinazione.|  
|Vero negativo|Numero di case che soddisfano le condizioni seguenti:<br /><br /> Il case non contiene il valore di destinazione.<br /><br /> Tramite il modello è stato stimato che il case non contiene il valore di destinazione.|  
|Falso negativo|Numero di case che soddisfano le condizioni seguenti:<br /><br /> Il valore effettivo non è uguale a quello di destinazione.<br /><br /> Tramite il modello è stato stimato che il case non contiene il valore di destinazione.|  
  
#### <a name="lift"></a>Accuratezza  
 *Lift* è una misura associata alla probabilità. Se un risultato è più probabile quando si usa il modello rispetto a una supposizione casuale, viene detto che il modello fornisce un *Lift positivo*. Tuttavia, se il modello esegue stime che sono meno probabili della probabilità casuale, il Punteggio di accuratezza è *negativo*. Questa metrica indica pertanto il livello di miglioramento che è possibile ottenere utilizzando il modello, dove un punteggio più alto indica un risultato migliore.  
  
 L'accuratezza viene calcolata come il rapporto tra la probabilità della stima effettiva e la probabilità marginale nei case di testing.  
  
#### <a name="log-score"></a>Punteggio in forma logaritmica  
 Il *Punteggio di log*, detto anche *Punteggio di probabilità dei log* per la stima, rappresenta il rapporto tra due probabilità, convertito in una scala logaritmica. Poiché le probabilità sono rappresentate come frazione decimale, il punteggio in forma logaritmica è sempre un numero negativo. Un punteggio più vicino a 0 corrisponde a un punteggio migliore.  
  
 Mentre punteggi non elaborati possono avere distribuzioni non regolari o non simmetriche, un punteggio in forma logaritmica è analogo a una percentuale.  
  
#### <a name="root-mean-square-error"></a>Radice errore quadratico medio  
 *Radice errore quadratico medio* (valori RMSE) è un metodo standard in statistica per esaminare il modo in cui i diversi set di dati vengono confrontati e smussare le differenze che possono essere introdotte dalla scala degli input.  
  
 Il metodo Radice errore quadratico medio rappresenta l'errore medio del valore stimato rispetto al valore effettivo. Il valore viene calcolato come la radice quadrata dell'errore medio per tutti i case della partizione divisa per il numero di case nella partizione, escluse le righe associate a valori mancanti per gli attributi di destinazione.  
  
#### <a name="mean-absolute-error"></a>Errore assoluto medio  
 L' *errore assoluto* medio è l'errore medio del valore stimato sul valore effettivo. Il valore viene calcolato ottenendo la somma assoluta degli errori e individuando la media di tali errori.  
  
 Questo valore consente di comprendere la variazione dei punteggi rispetto alla media.  
  
#### <a name="case-likelihood"></a>Probabilità del case  
 Questa misura è utilizzata solo per i modelli di clustering e indica la probabilità che un nuovo case appartenga a un cluster specifico.  
  
 Nei modelli di clustering sono previsti due tipi di appartenenza al cluster, a seconda del metodo utilizzato per creare il modello. In alcuni modelli, basati sull'algoritmo K-medie, è previsto che un nuovo case appartenga a un solo cluster. Per impostazione predefinita, tuttavia, l'algoritmo Microsoft Clustering utilizza il metodo EM (Expectation Maximization) che presuppone che un nuovo case possa potenzialmente appartenere a qualsiasi cluster. In questi modelli pertanto un case può avere più valori `CaseLikelihood`, ma il valore indicato per impostazione predefinita corrisponde alla probabilità che il case appartenga al cluster che meglio corrisponde al nuovo case.  
  
## <a name="see-also"></a>Vedi anche  
 [Convalida di modelli e utilizzo di modelli per la stima &#40;componenti aggiuntivi Data mining per Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
