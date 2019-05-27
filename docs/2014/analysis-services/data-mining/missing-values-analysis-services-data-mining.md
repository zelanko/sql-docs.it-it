---
title: I valori mancanti (Analysis Services - Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [data mining]
- MISSING_VALUE_SUBSTITUTION
- MissingValueSubstitution property
- MISSING_VALUE_SUBSTITUTION parameter
- null values [Analysis Services]
- coding [Data Mining]
ms.assetid: 2b34abdc-7ed4-4ec1-8780-052a704d6dbe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85968aef6452acb6aac75c5c6d4a093964e8d923
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66083362"
---
# <a name="missing-values-analysis-services---data-mining"></a>Valori mancanti (Analysis Services - Data mining)
  Una gestione corretta dei *valori mancanti* è fondamentale per ottenere una modellazione efficace. In questa sezione vengono illustrati i valori mancanti e descritte le caratteristiche fornite in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per gestire i valori mancanti durante la compilazione di strutture e modelli di data mining.  
  
## <a name="definition-of-missing-values-in-data-mining"></a>Definizione dei valori mancanti nel data mining  
 Un valore mancante può avere diversi significati. È possibile che il campo non fosse applicabile, che l'evento non si sia verificato o che i dati non fossero disponibili. Potrebbe essere accaduto che la persona che ha immesso i dati non conoscesse il valore corretto o non abbia verificato l'effettiva compilazione di un campo.  
  
 Tuttavia, sono molti gli scenari di data mining in cui tramite i valori mancanti vengono fornite informazioni importanti. Il significato dei valori mancanti dipende in gran parte dal contesto. Ad esempio, il significato di un valore mancante per la data in un elenco di fatture è sostanzialmente diverso dalla mancanza di una data in colonna indicante la data di assunzione di un dipendente. In generale, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] i valori mancanti vengono considerati informativi e vengono adattate le probabilità per incorporarli nei calcoli. In questo modo, è possibile assicurarsi che i modelli siano bilanciati e che ai case esistenti non venga assegnato un peso eccessivo.  
  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sono pertanto disponibili due meccanismi diversi per gestire e calcolare i valori mancanti. Il primo metodo consente di controllare la gestione dei valori Null a livello di struttura di data mining. Il secondo metodo differisce per quanto riguarda l'implementazione per ogni algoritmo, tuttavia generalmente consente di definire la modalità di elaborazione e conteggio dei valori mancanti nei modelli che consentono valori Null.  
  
## <a name="specifying-handling-of-nulls"></a>Specificazione della gestione di valori Null  
 Nell'origine dati, i valori mancanti potrebbero essere rappresentati in molti modi: come valori Null, celle vuote in un foglio di calcolo, valore N/D o qualche altro codice oppure come valore artificiale quale 9999. Tuttavia, per gli scopi di data mining, sono considerati valori mancanti solo i valori Null. Se nei dati sono contenuti valori segnaposto anziché valori Null, è possibile che i risultati del modello ne vengano influenzati, pertanto è consigliabile sostituirli con valori Null o derivare valori corretti se possibile. Sono disponibili diversi strumenti che è possibile utilizzare per derivare e inserire i valori appropriati, ad esempio la trasformazione Ricerca o l'attività Profiler dati di SQL Server Integration Services oppure lo strumento Estendi da esempio disponibile nei componenti aggiuntivi Data mining per Excel.  
  
 Se per l'attività da modellare è specificato che una colonna non deve mai avere valori mancanti, è consigliabile applicare il flag di modellazione `NOT_NULL` alla colonna quando si definisce la struttura di data mining. Tramite questo flag viene indicato che l'elaborazione non verrà eseguita se a un case non è associato un valore appropriato. Se durante l'elaborazione di un modello si verifica questo errore, è possibile registrarlo ed effettuare le operazioni per correggere i dati forniti al modello.  
  
## <a name="calculation-of-the-missing-state"></a>Calcolo dello stato mancante  
 Per l'algoritmo di data mining, i valori mancanti sono informativi. Nelle tabelle del case, `Missing` è uno stato valido come qualsiasi altro. Inoltre, in un modello di data mining possono essere utilizzati altri valori per stimare se un valore è mancante. In altri termini, il fatto che un valore sia mancante non è un errore.  
  
 Quando si crea un modello di data mining, viene automaticamente aggiunto uno stato `Missing` per tutte le colonne discrete. Se ad esempio nella colonna di input [Gender] sono contenuti due valori possibili, Male e Female, viene automaticamente aggiunto un terzo valore per rappresentare il valore `Missing` e nell'istogramma indicante la distribuzione di tutti i valori per la colonna è sempre incluso un conteggio dei case con valori `Missing`. Se nella colonna Gender non manca alcun valore, nell'istogramma viene mostrato che lo stato Missing è stato rilevato in 0 case.  
  
 La logica alla base dell'inclusione dello stato `Missing` per impostazione predefinita diventa chiara se si considera che nei dati potrebbero non essere contenuti esempi di tutti i valori possibili ed è preferibile evitare che la possibilità venga esclusa nel modello solo perché non sono presenti esempi nei dati. Se ad esempio dai dati delle vendite di un negozio risulta che tutti i clienti che hanno acquistato un determinato prodotto sono di sesso femminile, non è consigliabile creare un modello che stima che solo le donne possono acquistare tale prodotto. Al contrario, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene aggiunto un segnaposto per il valore sconosciuto aggiuntivo, denominato `Missing`, in modo da tenere conto di altri stati possibili.  
  
 Ad esempio, nella tabella seguente è illustrata la distribuzione di valori per il nodo (Tutto) nel modello di albero delle decisioni creato per l'esercitazione Bike Buyer. Nello scenario di esempio la colonna [Bike Buyer] rappresenta l'attributo stimabile, dove 1 indica "Sì" e 0 indica "No".  
  
|Value|Case|  
|-----------|-----------|  
|0|9296|  
|1|9098|  
|Missing|0|  
  
 Tramite questa distribuzione viene indicato che circa la metà dei clienti ha acquistato una bicicletta, mentre l'altra metà no. Questo specifico set di dati è molto pulito; pertanto, ogni case ha un valore nella colonna [Bike Buyer] e il conteggio dei valori `Missing` è 0. Tuttavia, se nel campo [Bike Buyer] di un case è presente un valore Null, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tale riga viene conteggiata come un case con un valore `Missing`.  
  
 Se l'input è una colonna continua, il modello tabula due possibili stati per l'attributo: `Existing` e `Missing`. In altri termini, la colonna contiene un valore di un tipo di dati numerico oppure non contiene alcun valore. Per i case che contengono un valore, il modello calcola la media, la deviazione standard e altre statistiche significative. Per i case che non includono valori, il modello fornisce un conteggio dei valori `Missing` e adatta le stime di conseguenza. Il metodo per adattare la stima varia a seconda dell'algoritmo e viene descritto nella sezione seguente.  
  
> [!NOTE]  
>  Per gli attributi di una tabella nidificata, i valori mancanti non sono informativi. Se ad esempio un cliente non ha acquistato un prodotto, la tabella nidificata **Prodotti** non include una riga corrispondente a tale prodotto e il modello di data mining non crea un attributo per il prodotto mancante. Se tuttavia si è interessati ai clienti che non hanno acquistato determinati prodotti, è possibile creare un modello filtrato in base alla non esistenza dei prodotti nella tabella nidificata, utilizzando un'istruzione NOT EXISTS nel filtro del modello. Per altre informazioni, vedere [Applicare un filtro a un modello di data mining](apply-a-filter-to-a-mining-model.md).  
  
## <a name="adjusting-probability-for-missing-states"></a>Adattamento della probabilità per gli stati mancanti  
 Oltre al conteggio dei valori, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene eseguito il calcolo della probabilità di qualsiasi valore nel set di dati. Lo stesso vale per il valore `Missing`. Nella tabella seguente sono, ad esempio, illustrate le probabilità per i case dell'esempio precedente:  
  
|Value|Case|Probabilità|  
|-----------|-----------|-----------------|  
|0|9296|50,55%|  
|1|9098|49,42%|  
|Missing|0|0,03%|  
  
 Può sembrare strano che la probabilità del valore `Missing` venga calcolata come 0,03%, quando il numero di case è 0. In realtà, si tratta di un comportamento previsto che consente al modello di gestire correttamente i valori non noti.  
  
 In generale, la probabilità viene calcolata dividendo i case utili per tutti quelli possibili. In questo esempio l'algoritmo calcola la somma dei case che soddisfano una determinata condizione ([Bike Buyer] = 1 o [Bike Buyer] = 0) e divide tale numero per il conteggio totale delle righe. Tuttavia, per tenere conto dei case `Missing`, al numero di tutti i case possibili viene aggiunto 1. Di conseguenza, la probabilità per il case sconosciuto non è più uguale a zero, ma corrisponde a un numero molto basso, a indicare che lo stato è semplicemente improbabile, non impossibile.  
  
 L'aggiunta del valore `Missing` basso non modifica il risultato del criterio di stima; tuttavia consente una modellazione più efficace negli scenari in cui i dati cronologici non includono tutti i risultati possibili.  
  
> [!NOTE]  
>  I provider di data mining gestiscono i valori mancanti in modi diversi. Alcuni, ad esempio, presuppongono che in una colonna nidificata i dati mancanti siano una rappresentazione di tipo sparse, mentre in una colonna non nidificata siano mancanti in modo casuale.  
  
 Se si è certi che tutti i risultati siano specificati nei dati e si desidera evitare l'adattamento delle probabilità, è consigliabile impostare il flag di modellazione NOT_NULL sulla colonna nella struttura di data mining.  
  
> [!NOTE]  
>  Ogni algoritmo, inclusi quelli personalizzati che è possibile ottenere da un plug-in di terze parti, può consentire di gestire i valori mancanti in modo diverso.  
  
### <a name="special-handling-of-missing-values-in-decision-tree-models"></a>Gestione speciale di valori mancanti nei modelli di albero delle decisioni  
 L'algoritmo Microsoft Decision Trees calcola le probabilità per i valori mancanti in modo diverso rispetto ad altri algoritmi. Anziché aggiungere solo 1 al numero complessivo di case, l'algoritmo degli alberi delle decisioni consente di eseguire un adattamento per lo stato `Missing` utilizzando una formula leggermente diversa.  
  
 In un modello di albero delle decisioni, la probabilità dello stato `Missing` viene calcolata come segue:  
  
 ProbabilitàStato = (ProbabilitàPrecedenteNodo) * (SupportoStato + 1) / (SupportoNodo + TotaleStati)  
  
 In [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)], inoltre, tramite l'algoritmo degli alberi delle decisioni viene reso disponibile un adattamento aggiuntivo che consente di compensare la presenza di filtri nel modello, fattore che può comportare l'esclusione di molti stati durante il training.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], se uno stato è presente durante il training ma ha supporto zero in un determinato nodo, viene eseguito l'adattamento standard. Tuttavia, se uno stato non viene mai rilevato durante il training, l'algoritmo consente di impostare la probabilità esattamente su zero. Questo adattamento non si applica soltanto allo stato `Missing`, ma anche agli altri stati esistenti nei dati di training a cui corrisponde un supporto zero in seguito al filtro del modello.  
  
 Il risultato di questo adattamento aggiuntivo è la formula seguente:  
  
 StateProbability = 0.0 se tale stato ha supporto 0 nel set di training  
  
 ELSE ProbabilitàStato = (ProbabilitàPrecedenteNodo) * (SupportoStato + 1) / (SupportoNodo + TotaleStatiConSupportoNonZero  
  
 L'effetto finale di questo adattamento è di mantenere la stabilità dell'albero.  
  
## <a name="related-tasks"></a>Attività correlate  
 Negli argomenti seguenti vengono fornite ulteriori informazioni sulla gestione dei valori mancanti.  
  
|Attività|Collegamenti|  
|-----------|-----------|  
|Aggiungere flag alle singole colonne del modello per controllare la gestione dei valori mancanti|[Visualizzare o modificare flag di modellazione &#40;Data mining&#41;](modeling-flags-data-mining.md)|  
|Impostare le proprietà su un modello di data mining per controllare la gestione dei valori mancanti|[Modificare le proprietà di un modello di data mining](change-the-properties-of-a-mining-model.md)|  
|Informazioni sulla specificazione di flag di modellazione in DMX|[Flag di modellazione &#40;DMX&#41;](/sql/dmx/modeling-flags-dmx)|  
|Modificare la modalità di gestione dei valori mancanti da parte della struttura di data mining|[Modificare le proprietà di una struttura di data mining](change-the-properties-of-a-mining-structure.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Contenuto dei modelli di data mining &#40;Analysis Services - Data mining&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Flag di modellazione &#40;data mining&#41;](modeling-flags-data-mining.md)  
  
  
