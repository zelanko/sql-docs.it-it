---
title: Trasformazione Aggregazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregatetrans.f1
helpviewer_keywords:
- IsBig property
- aggregate functions [Integration Services]
- Aggregate transformation [Integration Services]
- large data, SSIS transformations
ms.assetid: 2871cf2a-fbd3-41ba-807d-26ffff960e81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4759050a9453e1925ea47bc3dbf66d13aa821feb
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384872"
---
# <a name="aggregate-transformation"></a>Trasformazione Aggregazione
  La trasformazione Aggregazione applica funzioni di aggregazione, ad esempio Media, ai valori delle colonne e copia i risultati nell'output della trasformazione. Oltre alle funzioni di aggregazione, per questa trasformazione è disponibile la clausola GROUP BY, che consente di specificare i gruppi su cui eseguire l'aggregazione.  
  
## <a name="operations"></a>Operazioni  
 La trasformazione Aggregazione supporta le operazioni seguenti.  
  
|Operazione|Descrizione|  
|---------------|-----------------|  
|Group by|Consente di dividere i set di dati in gruppi. Per il raggruppamento è possibile utilizzare colonne con qualsiasi tipo di dati. Per altre informazioni, vedere [GROUP BY &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-group-by-transact-sql).|  
|Sum|Consente di sommare i valori di una colonna. È possibile sommare solo le colonne con tipi di dati numerici. Per altre informazioni, vedere [SUM &#40;Transact-SQL&#41;](/sql/t-sql/functions/sum-transact-sql).|  
|Media|Consente di restituire la media dei valori di una colonna. È possibile calcolare la media soltanto delle colonne con tipi di dati numerici. Per altre informazioni, vedere [AVG &#40;Transact-SQL&#41;](/sql/t-sql/functions/avg-transact-sql).|  
|Conteggio|Consente di restituire il numero di elementi di un gruppo. Per altre informazioni, vedere [COUNT &#40;Transact-SQL&#41;](/sql/t-sql/functions/count-transact-sql).|  
|Count Distinct|Consente di restituire il numero di valori non Null univoci di un gruppo.|  
|Minimo|Restituisce il valore minimo in un gruppo. Per altre informazioni, vedere [MIN &#40;Transact-SQL&#41;](/sql/t-sql/functions/min-transact-sql). Diversamente dalla funzione Transact-SQL MIN, questa operazione può essere eseguita solo con tipi di dati numerici, di data e di ora.|  
|Massimo|Restituisce il valore massimo in un gruppo. Per altre informazioni, vedere [MAX &#40;Transact-SQL&#41;](/sql/t-sql/functions/max-transact-sql). Diversamente dalla funzione Transact-SQL MAX, questa operazione può essere eseguita solo con tipi di dati numerici, di data e di ora.|  
  
 La trasformazione Aggregazione gestisce i valori Null come il motore di database relazionale di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Questo comportamento è definito nello standard SQL-92. Sono applicabili le regole seguenti:  
  
-   In una clausola GROUP BY i valori Null vengono considerati come gli altri valori di colonna. Se la colonna di raggruppamento include più valori Null, questi verranno inseriti in un unico gruppo.  
  
-   Nelle funzioni COUNT (column name) e COUNT (DISTINCT column name) i valori Null vengono ignorati e il risultato non include le righe che contengono valori Null nella colonna specificata.  
  
-   Nella funzione COUNT (*) vengono conteggiate tutte le righe, incluse quelle con valori Null.  
  
## <a name="big-numbers-in-aggregates"></a>Valori numerici elevati nelle aggregazioni  
 Una colonna può contenere valori numerici che richiedono particolare attenzione perché hanno valori o precisione elevata. La trasformazione Aggregazione include la proprietà IsBig, che può essere impostata sulle colonne di output per richiedere una speciale modalità di gestione per i numeri con precisione o valore elevato. Se un valore di colonna può superare i 4 miliardi o richiedere una precisione superiore a quella del tipo di dati float, sarà necessario impostare la proprietà IsBig su 1.  
  
 L'impostazione della proprietà IsBig su 1 modifica l'output della trasformazione Aggregazione nel modo seguente:  
  
-   Viene utilizzato il tipo di dati DT_R8 anziché il tipo di dati DT_R4.  
  
-   I risultati dei conteggi vengono archiviati con il tipo di dati DT_UI8.  
  
-   I risultati Distinct Count vengono archiviati con il tipo di dati DT_UI4.  
  
> [!NOTE]  
>  Non è possibile impostare su 1 la proprietà IsBig delle colonne usate nelle operazioni GROUP BY, MAX e MIN.  
  
## <a name="performance-considerations"></a>Considerazioni sulle prestazioni  
 La trasformazione Aggregazione include un set di proprietà che è possibile impostare per migliorarne le prestazioni.  
  
-   Quando si esegue un'operazione **Group by** , impostare la proprietà Keys o KeysScale del componente e gli output del componente. Tramite Keys, è possibile specificare il numero esatto di chiavi che dovrà essere gestito dalla trasformazione. In questo contesto, Keys fa riferimento al numero di gruppi che dovrebbero risultare da un'operazione **Group by**. Tramite KeysScale, è possibile specificare un numero approssimativo di chiavi. Quando si specifica un valore appropriato per Keys o KeyScale, si migliorano le prestazioni in quanto la trasformazione è in grado di allocare una quantità di memoria appropriata per i dati memorizzati nella cache.  
  
-   Quando si esegue un'operazione **Distinct count** , impostare la proprietà CountDistinctKeys o CountDistinctScale del componente. Tramite CountDistinctKeys, è possibile specificare il numero esatto di chiavi che dovrà essere gestito dalla trasformazione per un'operazione Count Distinct. In questo contesto, CountDistinctKeys fa riferimento al numero di valori distinct che dovrebbero risultare da un'operazione **Distinct Count**. La proprietà CountDistinctScale consente di specificare un numero approssimativo di chiavi per un'operazione Count Distinct. Quando si specifica un valore appropriato per CountDistinctKeys o CountDistinctScale, si migliorano le prestazioni in quanto la trasformazione è in grado di allocare una quantità di memoria appropriata per i dati memorizzati nella cache.  
  
## <a name="aggregate-transformation-configuration"></a>Configurazione della trasformazione Aggregazione  
 La trasformazione Aggregazione può essere configurata a livello di trasformazione, output e colonna.  
  
-   A livello di trasformazione, è possibile configurare la trasformazione Aggregazione per ottimizzare le prestazioni specificando i valori seguenti:  
  
    -   Numero di gruppi che dovrebbero risultare da un'operazione **Group by** .  
  
    -   Numero di valori distinct che dovrebbero risultare da un'operazione **Count Distinct** .  
  
    -   Percentuale di estensione della memoria durante l'aggregazione.  
  
     La trasformazione Aggregazione può essere inoltre configurata in modo da generare un avviso anziché un errore quando il valore di un divisore è zero.  
  
-   A livello di output, è possibile configurare la trasformazione Aggregazione per ottimizzare le prestazioni specificando il numero di gruppi che dovrebbero risultare da un'operazione **Group by** . La trasformazione Aggregazione supporta più output, ognuno dei quali può essere configurato in modo diverso.  
  
-   A livello di colonna, è possibile specificare i valori seguenti:  
  
    -   Aggregazione eseguita dalla colonna.  
  
    -   Opzioni di confronto dell'aggregazione.  
  
 È inoltre possibile configurare la trasformazione Aggregazione per ottimizzare le prestazioni specificando i valori seguenti:  
  
-   Numero di gruppi che dovrebbero risultare da un'operazione **Group by** sulla colonna.  
  
-   Numero di valori distinct che dovrebbero risultare da un'operazione **Count Distinct** sulla colonna.  
  
 È inoltre possibile identificare le colonne come IsBig se una colonna contiene valori numerici elevati o valori numerici con precisione elevata.  
  
 La trasformazione Aggregazione è asincrona, pertanto non legge e pubblica i dati riga per riga, ma legge l'intero set di righe, ne esegue i raggruppamenti e le aggregazioni e quindi pubblica i risultati.  
  
 Questa trasformazione non passa alcuna colonna, ma crea nuove colonne nel flusso di dati per i dati pubblicati. Solo le colonne di input a cui vengono applicate le funzioni di aggregazione e le colonne di input utilizzate dalla trasformazione per il raggruppamento vengono copiate nell'output della trasformazione. Ad esempio, un input della trasformazione aggregazione potrebbe avere tre colonne: **CountryRegion**, **Città**, e **popolamento**. La trasformazione esegue un raggruppamento in base alla colonna **CountryRegion** e applica la funzione alla colonna **Population** . L'output non include pertanto la colonna **City** .  
  
 È inoltre possibile aggiungere più output alla trasformazione Aggregazione e indirizzare ogni aggregazione a un output diverso. Se ad esempio la trasformazione Aggregazione applica le funzioni Somma e Media, ogni aggregazione potrà essere indirizzata a un output diverso.  
  
 È possibile applicare più aggregazioni a una singola colonna di input. Se ad esempio si vuole ottenere i valori della somma e della media per una colonna di input di nome **Sales**, sarà possibile configurare la trasformazione in modo da applicare le funzioni Somma e Media alla colonna **Sales** .  
  
 La trasformazione Aggregazione include un input e uno o più output. Non supporta un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Aggregazione** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor trasformazione Aggregazione &#40;scheda Aggregazioni&#41;](../../aggregate-transformation-editor-aggregations-tab.md)  
  
-   [Editor trasformazione Aggregazione &#40;scheda Avanzate&#41;](../../aggregate-transformation-editor-advanced-tab.md)  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Aggregazione di valori in un set di dati utilizzando la trasformazione Aggregazione](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinare i dati per le trasformazioni Unione e Merge Join](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 [Aggregare valori in un set di dati tramite la trasformazione Aggregazione](aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../data-flow.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  
