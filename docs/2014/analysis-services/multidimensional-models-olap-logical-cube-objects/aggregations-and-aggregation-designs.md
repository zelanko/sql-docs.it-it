---
title: Le aggregazioni e progettazione di aggregazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- aggregations [Analysis Services], about aggregations
- storage [Analysis Services], aggregations
- Storage Design Wizard
- data summary [Analysis Services]
- data storage [Analysis Services]
- storing data [Analysis Services], aggregations
- aggregations [Analysis Services]
ms.assetid: 35bd8589-39fa-4e0b-b28f-5a07d70da0a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3897c5e41e16af0a8162b63794760aa4d740353d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727697"
---
# <a name="aggregations-and-aggregation-designs"></a>Aggregations and Aggregation Designs
  Un oggetto <xref:Microsoft.AnalysisServices.AggregationDesign> definisce un set di definizioni di aggregazione che possono essere condivise tra più partizioni.  
  
 Un oggetto <xref:Microsoft.AnalysisServices.Aggregation> rappresenta il riepilogo dei dati dei gruppi di misure a una determinata granularità delle dimensioni.  
  
 Un oggetto <xref:Microsoft.AnalysisServices.Aggregation> semplice è composto da informazioni di base e dimensioni. Le informazioni di base includono il nome dell'aggregazione, l'ID, le annotazioni e una descrizione. Le dimensioni sono una raccolta di oggetti <xref:Microsoft.AnalysisServices.AggregationDimension> che contengono l'elenco degli attributi di granularità per la dimensione.  
  
 Le aggregazioni sono riepiloghi precalcolati dei dati delle celle foglia che consentono di migliorare il tempo di risposta alle query attraverso la preparazione delle risposte prima della formulazione delle domande. Ad esempio, quando una tabella dei fatti di un data warehouse include centinaia di migliaia di righe, una query che richiede i totali delle vendite settimanali per una particolare linea di prodotti può richiedere tempi lunghi se per fornire la risposta è necessario eseguire operazioni di analisi e somma in tutte le righe della tabella dei fatti durante l'esecuzione della query. Se invece i dati di riepilogo necessari per rispondere a questa query sono stati precalcolati, la risposta potrà essere quasi immediata. Il calcolo preliminare dei dati di riepilogo viene eseguito in fase di elaborazione ed è alla base dei rapidi tempi di risposta assicurati dalla tecnologia OLAP.  
  
 L'entità utilizzata dalla tecnologia OLAP per organizzare i dati di riepilogo in strutture multidimensionali è il cubo. Le dimensioni e le relative gerarchie di attributi riflettono le query che possono essere eseguite sul cubo. Le aggregazioni sono archiviate nella struttura multidimensionale all'interno di celle in corrispondenza delle coordinate specificate dalle dimensioni. Ad esempio, la domanda "A quanto ammontavano le vendite del prodotto X nel 1998 per l'area nord-ovest?" coinvolge tre dimensioni (il prodotto, il tempo e l'area geografica) e una misura (le vendite). La risposta a questa domanda è rappresentata dal singolo valore numerico presente nella cella all'interno del cubo in corrispondenza delle coordinate prodotto X, 1998, Nord-Ovest.  
  
 Altre domande possono restituire più valori, ad esempio la domanda "A quanto ammontavano le vendite dei prodotti hardware in ogni trimestre del 1998 per ogni singola regione?". Queste query restituiscono set di celle dalle coordinate che soddisfano le condizioni specificate. Il numero di celle restituito dalla query è determinato dal numero di elementi nel livello hardware della dimensione del prodotto, dai quattro trimestri del 1998 e dal numero di regioni nella dimensione dell'area geografica. Se tutti i dati di riepilogo sono stati precalcolati in aggregazioni, il tempo di risposta della query dipenderà esclusivamente dal tempo necessario per estrarre le celle specificate e non saranno necessari calcoli o letture di dati dalla tabella dei fatti.  
  
 Nonostante il calcolo preliminare di tutte le possibili aggregazioni in un cubo possa consentire di ottimizzare il tempo di risposta per tutte le query, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può calcolare facilmente determinati valori aggregati da altre aggregazioni precalcolate. Inoltre, il calcolo di tutte le possibili aggregazioni comporta tempi di elaborazione e spazio di archiviazione notevoli. Pertanto, è necessario raggiungere un compromesso tra i requisiti di archiviazione e la percentuale di possibili aggregazioni precalcolate. Se nessuna aggregazione viene precalcolata (0%), il tempo di elaborazione e lo spazio di archiviazione necessari per un cubo saranno ridotti al minimo, ma il tempo di risposta alle query potrebbe essere lungo, perché i dati necessari per fornire una risposta a ogni query devono essere recuperati dalle celle foglia e poi aggregati in fase di query per fornire una risposta a ogni query. La restituzione del singolo numero rappresentante la risposta alla query formulata sopra ("A quanto ammontavano le vendite del prodotto X nel 1998 per la regione Nord-Ovest"), ad esempio, potrebbe richiedere la lettura di migliaia di righe di dati, l'estrazione del valore della colonna utilizzata per specificare la misura Sales in ogni riga e quindi il calcolo della somma. Inoltre, la quantità di tempo necessaria per recuperare tali dati varierà in base alla modalità di archiviazione scelta per i dati-MOLAP, HOLAP o ROLAP.  
  
## <a name="designing-aggregations"></a>Progettazione di aggregazioni  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] include un sofisticato algoritmo che consente di selezionare aggregazioni precalcolare in modo possono calcolare rapidamente altre aggregazioni rispetto ai valori precalcolati. Se, ad esempio, le aggregazioni vengono precalcolate per il livello mese di una gerarchia temporale, il calcolo di un livello trimestre richiederà semplicemente la somma di tre numeri, un'operazione eseguibile rapidamente. Questa tecnica consente sia di ridurre il tempo di elaborazione sia di limitare i requisiti di archiviazione, con un impatto minimo sul tempo di risposta alle query.  
  
 Progettazione guidata aggregazioni include opzioni che consentono di impostare vincoli relativi allo spazio di archiviazione e alla percentuale di calcolo preliminare per l'algoritmo, in modo da raggiungere un adeguato compromesso tra il tempo di risposta alle query e i requisiti di archiviazione. L'algoritmo della Progettazione guidata aggregazioni, tuttavia, presuppone che il valore della probabilità sia lo stesso per tutte le query. L'Ottimizzazione guidata basata sulle statistiche di utilizzo consente di modificare la progettazione di un'aggregazione per un gruppo di misure tramite un'analisi delle query inviate da applicazioni client. Utilizzando la procedura guidata per ottimizzare l'aggregazione di un cubo è possibile aumentare i tempi di risposta alle query frequenti e ridurre i tempi di risposta alle query poco frequenti senza un impatto significativo sullo spazio di archiviazione necessario per il cubo.  
  
 Le aggregazioni vengono progettate utilizzando le procedure guidate, ma non vengono calcolate fino alla fase di elaborazione della partizione per cui sono state configurate. Dopo la creazione dell'aggregazione, in caso di modifica della struttura di un cubo oppure di aggiunta o modifica dei dati nelle tabelle di origine di un cubo, in genere è necessario esaminare le aggregazioni del cubo e rielaborare il cubo.  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborazione e modalità di archiviazione delle partizioni](partitions-partition-storage-modes-and-processing.md)  
  
  
