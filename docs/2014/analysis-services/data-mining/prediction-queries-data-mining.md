---
title: Query di stima (Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: e5e6686c-1360-480e-8c0d-8a56204fbed9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 935cd8ec3f4e5069807e914e5af20e39b645deb3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733197"
---
# <a name="prediction-queries-data-mining"></a>Prediction Queries (Data Mining)
  L'obiettivo di un progetto di data mining tipico consiste nell'utilizzare il modello di data mining per eseguire stime. Ad esempio, potrebbe essere necessario stimare la quantità di tempo di inattività prevista per un determinato cluster di server o generare un punteggio che indichi se è probabile che segmenti di clienti rispondano a una campagna pubblicitaria. Per effettuare tutte queste operazioni, è necessario creare una query di stima.  
  
 A livello funzionale esistono diversi tipi di query di stima supportati in SQL Server, a seconda del tipo di input per la query:  
  
|Tipo di query|Opzioni query|  
|----------------|-------------------|  
|Query di stima singleton|Utilizzare una query singleton se si desidera eseguire una stima dei risultati per uno o più case nuovi. I valori di input devono essere immessi direttamente nella query e quest'ultima viene eseguita come singola sessione.|  
|Stime in batch|Utilizzare le stime in batch quando si dispone di dati esterni che si desidera inserire nel modello per utilizzarli come base per le stime. Per eseguire stime per un intero set di dati, è necessario eseguire il mapping dei dati nell'origine esterna alle colonne del modello, quindi specificare il tipo di dati predittivi che si desidera restituire.<br /><br /> La query per l'intero set di dati viene eseguita in una singola sessione, rendendo questa opzione molto più efficiente rispetto all'invio di più query ripetute.|  
|Stime basate su serie temporali|Utilizzare una query di serie temporale se si desidera stimare un valore in diversi passaggi futuri. Tramite Data mining di SQL Server, nelle query di serie temporali è disponibile anche la funzionalità seguente:<br /><br /> È possibile estendere un modello esistente aggiungendo nuovi dati come parte della query ed eseguire stime basate sulla serie composta.<br /><br /> È possibile applicare il modello esistente a una nuova serie di dati utilizzando l'opzione REPLACE_MODEL_CASES.<br /><br /> È possibile eseguire una stima incrociata.|  
  
 Nelle sezioni seguenti viene descritta la sintassi generale delle query di stima, i relativi tipi differenti nonché come utilizzare i risultati di tali query.  
  
 [Progetto di query di stima di base](#bkmk_PredQuery)  
  
-   [Aggiunta di funzioni di stima](#bkmk_PredFunc)  
  
-   [Query singleton](#bkmk_SingletonQuery)  
  
-   [Query di stima in batch](#bkmk_BatchQuery)  
  
 [Utilizzo dei risultati delle query](#bkmk_WorkResults)  
  
##  <a name="bkmk_PredQuery"></a> Progetto di query di stima di base  
 Quando si crea una stima, si forniscono in genere alcuni nuovi dati e si chiede al modello di generare una stima in base ai nuovi dati.  
  
-   In una query di stima in batch viene eseguito il mapping del modello a un'origine esterna di dati utilizzando un *PREDICTION JOIN*.  
  
-   In una query di stima singleton digitare uno o più valori da utilizzare come input. È possibile creare più stime utilizzando una query di stima singleton. Tuttavia, se è necessario creare molte stime, le prestazioni sono migliori se si utilizza una query in batch.  
  
 Sia nelle query di stima singleton sia in quelle di stima in batch viene utilizzata la sintassi PREDICTION JOIN per definire i nuovi dati. La differenza consiste nella modalità di specifica dell'input.  
  
-   In una query di stima in batch, i dati provengono da un'origine dati esterna specificata tramite la sintassi OPENQUERY.  
  
-   In una query di stima singleton, i dati vengono forniti inline come parte della query.  
  
 Per i modelli Time Series, i dati di input non sono sempre richiesti; è possibile eseguire stime utilizzando semplicemente i dati già presenti nel modello. Tuttavia, se si specificano nuovi dati di input, è necessario decidere se si utilizzeranno i nuovi dati per aggiornare ed estendere il modello o per sostituire la serie originale di dati utilizzata nel modello.  Per altre informazioni su queste opzioni, vedere [Time Series Model Query Examples](time-series-model-query-examples.md).  
  
###  <a name="bkmk_PredFunc"></a> Aggiunta di funzioni di stima  
 Oltre a stimare un valore, è possibile personalizzare una query di stima per restituire vari tipi di informazioni correlate alla stima. Ad esempio, se tramite la stima viene creato un elenco di prodotti da consigliare a un cliente, è necessario restituire anche la probabilità per ogni stima, in modo che sia possibile classificarli e presentare all'utente solo i prodotti consigliati.  
  
 A tale scopo, aggiungere *funzioni di stima* alla query. Ogni tipo di modello o di query supporta funzioni specifiche. Ad esempio, i modelli di clustering supportano funzioni di stima speciali che forniscono dettagli aggiuntivi sui cluster creati dal modello, mentre i modelli Time Series dispongono di funzioni che consentono di calcolare le differenze nel corso del tempo. Sono inoltre disponibili funzioni di stima generali che funzionano con quasi tutti i tipi di modello. Per un elenco di funzioni di stima supportate nei diversi tipi di query, vedere l'argomento di riferimento DMX:  [Funzioni di stima generale &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx).  
  
###  <a name="bkmk_SingletonQuery"></a> Creazione di query di stima singleton  
 Una query di stima singleton risulta utile se si desidera creare stime rapide in tempo reale. Uno scenario comune potrebbe essere l'acquisizione di informazioni da un cliente tramite, ad esempio, un form in un sito Web, e il successivo invio di tali dati come input a una query di stima singleton. Ad esempio, quando un cliente sceglie un prodotto da un elenco, è possibile utilizzare tale selezione come input per una query che consente di stimare i migliori prodotti da consigliare.  
  
 Per le query di stima singleton non è necessaria una tabella separata contenente l'input. Al contrario, vengono fornite una o più righe di valori come input del modello e le stime vengono restituite in tempo reale.  
  
> [!WARNING]  
>  Nonostante il nome, le query di stima singleton non solo stime singole-è possibile generare più stime per ogni set di input. Specificare più case di input creando un'istruzione SELECT per ogni case di input e combinandoli con l'operatore UNION.  
  
 Quando si crea una query di stima singleton, è necessario fornire i nuovi dati al modello sotto forma di PREDICTION JOIN. Questo significa che anche se non si esegue il mapping a una tabella effettiva, è necessario assicurarsi che i nuovi dati corrispondano alle colonne esistenti nel modello di data mining. Se le nuove colonne di dati e i nuovi dati corrispondono in modo esatto, il mapping delle colonne verrà eseguito automaticamente in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questa funzione è denominata *NATURAL PREDICTION JOIN*. Se tuttavia le colonne non corrispondono o se nei nuovi dati non è contenuto lo stesso tipo e la stessa quantità di dati presenti nel modello, è necessario specificare di quali colonne del modello eseguire il mapping ai nuovi dati oppure specificare i valori mancanti.  
  
###  <a name="bkmk_BatchQuery"></a> Query di stima in batch  
 Una query di stima in batch è utile quando si dispone di dati esterni che si desidera utilizzare per l'esecuzione di stime. Ad esempio, è probabile che sia stato compilato un modello che consente di suddividere in categorie i clienti in base all'attività online e alla cronologia di acquisto. È possibile applicare tale modello a un elenco di potenziali clienti appena acquisiti per creare proiezioni per le vendite o identificare destinazioni per le campagne proposte.  
  
 Quando si esegue un PREDICTION JOIN, è necessario eseguire il mapping delle colonne del modello alle colonne nella nuova origine dati. Pertanto, nell'origine dati scelta per un input devono essere presenti dati simili ai dati del modello. Le nuove informazioni non devono corrispondere esattamente e possono essere incomplete. Si supponga ad esempio che il training del modello sia stato eseguito utilizzando le informazioni sul reddito e sull'età, ma che nell'elenco clienti utilizzato per le stime siano disponibili le informazioni sull'età, ma non sul reddito. In questo scenario è ancora possibile eseguire il mapping dei nuovi dati al modello e creare una stima per ogni cliente. Tuttavia, se il reddito fosse un fattore di stima importante per il modello, la mancanza di informazioni complete influirebbe sulla qualità delle stime.  
  
 Per ottenere i migliori risultati, è necessario unire in join il numero massimo possibile di colonne corrispondenti tra i nuovi dati e il modello. Tuttavia, la query riuscirà anche se non sono presenti corrispondenze. Se nessuna delle colonne è unita in join, tramite la query verrà restituita la stima marginale, che è l'equivalente dell'istruzione `SELECT <predictable-column> FROM <model>` senza una clausola PREDICTION JOIN.  
  
 Dopo aver eseguito correttamente il mapping di tutte le colonne attinenti, viene eseguita la query e tramite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono eseguite le stime per ogni riga nei nuovi dati basati sugli schemi del modello. È possibile salvare i risultati in una nuova tabella nella vista origine dati contenente i dati esterni oppure copiare e incollare i dati in uso in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!WARNING]  
>  Se si usa la finestra di progettazione in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], l'origine dati esterna deve innanzitutto essere definita come una vista origine dati.  
  
 Se si utilizza DMX per creare un prediction join, è possibile specificare l'origine dati esterna utilizzando il comando OPENQUERY, OPENROWSET o SHAPE. Il metodo predefinito di accesso ai dati nei modelli DMX è OPENQUERY. Per informazioni su questi metodi, vedere [&#60;source data query&#62;](/sql/dmx/source-data-query).  
  
###  <a name="bkmk_TSQuery"></a> Stime nei modelli di data mining Time Series  
 I modelli Time Series sono diversi dagli altri tipi di modelli. È possibile utilizzare il modello originale per creare stime oppure fornire nuovi dati al modello per aggiornarlo e creare stime basate sulle tendenze recenti. Se si aggiungono nuovi dati, è possibile specificare la modalità di utilizzo dei nuovi dati.  
  
-   L'*estensione dei case del modello* prevede l'aggiunta di nuovi dati nella serie esistente di dati nel modello Time Series. Da questo momento in poi, le stime sono basate sulla nuova serie combinata. Questa opzione è utile se si desidera aggiungere semplicemente alcuni punti dati a un modello esistente.  
  
     Si supponga ad esempio che un modello Time Series esistente sia stato sottoposto a training sui dati delle vendite relativi all'anno precedente. Dopo aver raccolto diversi mesi di nuovi dati delle vendite, si decide di aggiornare le previsioni di vendita per l'anno corrente. È possibile creare un PREDICTION JOIN che consente di aggiornare il modello aggiungendo nuovi dati e di estendere il modello per creare nuove stime.  
  
-   La*sostituzione dei case del modello* consente di mantenere il modello sottoposto a training, ma i case sottostanti vengono sostituiti con un nuovo set di dati del case. Questa opzione è utile se si desidera mantenere la tendenza nel modello applicandola però a un set di dati diverso.  
  
     Ad esempio, è possibile che sia stato eseguito il training del modello originale in un set di dati con volumi di vendite molto elevati. Quando si sostituiscono i dati sottostanti con una nuova serie, ad esempio di un archivio con volume di vendite inferiore, si mantiene la tendenza, ma le stime iniziano dai valori della serie di sostituzione.  
  
 Indipendentemente dall'approccio adottato, il punto iniziale per le stime corrisponde sempre alla fine della serie originale.  
  
 Per altre informazioni sulla creazione di prediction join sui modelli Time Series, vedere [Time Series Model Query Examples](time-series-model-query-examples.md) o [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx).  
  
##  <a name="bkmk_WorkResults"></a> Utilizzo dei risultati di una query di stima  
 Le opzioni per salvare i risultati di una query di stima di data mining sono diverse a seconda della modalità di creazione della query.  
  
-   Quando si compila una query utilizzando il generatore delle query di stima in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], è possibile salvare i risultati di una query di stima in un'origine dati [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esistente. Per altre informazioni, vedere [Visualizzare e salvare i risultati di una query di stima](view-and-save-the-results-of-a-prediction-query.md).  
  
-   Quando si creano query di stima utilizzando DMX nel riquadro query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], è possibile utilizzare le opzioni di output della query per salvare i risultati in un file o nel riquadro dei risultati della query come testo o in una griglia. Per altre informazioni, vedere [Editor di query e di testo &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
-   Quando si esegue una query di stima utilizzando i componenti di Integration Services, le attività consentono di scrivere i risultati in un database tramite una gestione connessione ADO.NET o OLE DB disponibile. Per altre informazioni, vedere [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md).  
  
 È importante comprendere che i risultati di una query di stima non sono come i risultati di una query su un database relazionale che restituisce sempre una sola riga di valori correlati. Ogni funzione di stima DMX aggiunta alla query restituisce un set di righe specifico. Pertanto, quando si esegue una stima su un singolo case, il risultato può essere un valore stimato insieme a diverse colonne di tabelle nidificate contenenti ulteriori dettagli.  
  
 Se si combinano più funzioni in un'unica query, i risultati restituiti vengono combinati in un set di righe gerarchico. Si supponga ad esempio di utilizzare un modello Time Series per stimare valori futuri per l'importo e la quantità delle vendite tramite una query come questa istruzione DMX:  
  
```  
SELECT  
  PredictTimeSeries([Forecasting].[Amount]) as [PredictedAmount]  
, PredictTimeSeries([Forecasting].[Quantity]) as [PredictedQty]  
FROM  
  [Forecasting]  
  
```  
  
 I risultati di questa query sono dati da due colonne, una per ogni serie stimata, dove ogni riga contiene una tabella nidificata con i valori stimati:  
  
 **PredictedAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|201101|172067.11|  
  
|$TIME|Amount|  
|-----------|------------|  
|201102|363390.68|  
  
 **PredictedQty**  
  
|$TIME|Quantity|  
|-----------|--------------|  
|201101|77|  
  
|$TIME|Quantity|  
|-----------|--------------|  
|201102|260|  
  
 Se il provider non è in grado di gestire i set di righe gerarchici, è possibile fare in modo che i risultati vengano restituiti in formato flat utilizzando la parola chiave FLATTEN nella query di stima. Per altre informazioni, inclusi esempi di set di righe bidimensionali, vedere [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
## <a name="see-also"></a>Vedere anche  
 [Query sul contenuto &#40;Data mining&#41;](content-queries-data-mining.md)   
 [Query di definizione dei dati &#40;Data mining&#41;](data-definition-queries-data-mining.md)  
  
  
