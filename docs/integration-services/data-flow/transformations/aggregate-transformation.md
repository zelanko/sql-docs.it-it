---
title: Trasformazione Aggregazione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.aggregatetrans.f1
- sql13.dts.designer.aggregationtransformation.aggregations.f1
- sql13.dts.designer.aggregationtransformation.advanced.f1
helpviewer_keywords:
- IsBig property
- aggregate functions [Integration Services]
- Aggregate transformation [Integration Services]
- large data, SSIS transformations
ms.assetid: 2871cf2a-fbd3-41ba-807d-26ffff960e81
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0580c61bae4fdca1d311e4ccaee88f05a8b6ecd0
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726282"
---
# <a name="aggregate-transformation"></a>Trasformazione Aggregazione

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione Aggregazione applica funzioni di aggregazione, ad esempio Media, ai valori delle colonne e copia i risultati nell'output della trasformazione. Oltre alle funzioni di aggregazione, per questa trasformazione è disponibile la clausola GROUP BY, che consente di specificare i gruppi su cui eseguire l'aggregazione.  
  
## <a name="operations"></a>Operazioni  
 La trasformazione Aggregazione supporta le operazioni seguenti.  
  
|Operazione|Descrizione|  
|---------------|-----------------|  
|Group by|Consente di dividere i set di dati in gruppi. Per il raggruppamento è possibile utilizzare colonne con qualsiasi tipo di dati. Per altre informazioni, vedere [GROUP BY &#40;Transact-SQL&#41;](../../../t-sql/queries/select-group-by-transact-sql.md).|  
|SUM|Consente di sommare i valori di una colonna. È possibile sommare solo le colonne con tipi di dati numerici. Per altre informazioni, vedere [SUM &#40;Transact-SQL&#41;](../../../t-sql/functions/sum-transact-sql.md).|  
|Medio|Consente di restituire la media dei valori di una colonna. È possibile calcolare la media soltanto delle colonne con tipi di dati numerici. Per altre informazioni, vedere [AVG &#40;Transact-SQL&#41;](../../../t-sql/functions/avg-transact-sql.md).|  
|Count|Consente di restituire il numero di elementi di un gruppo. Per altre informazioni, vedere [COUNT &#40;Transact-SQL&#41;](../../../t-sql/functions/count-transact-sql.md).|  
|Count Distinct|Consente di restituire il numero di valori non Null univoci di un gruppo.|  
|Minimo|Restituisce il valore minimo in un gruppo. Per altre informazioni, vedere [MIN &#40;Transact-SQL&#41;](../../../t-sql/functions/min-transact-sql.md). Diversamente dalla funzione Transact-SQL MIN, questa operazione può essere eseguita solo con tipi di dati numerici, di data e di ora.|  
|Massimo|Restituisce il valore massimo in un gruppo. Per altre informazioni, vedere [MAX &#40;Transact-SQL&#41;](../../../t-sql/functions/max-transact-sql.md). Diversamente dalla funzione Transact-SQL MAX, questa operazione può essere eseguita solo con tipi di dati numerici, di data e di ora.|  
  
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
  
 Questa trasformazione non passa alcuna colonna, ma crea nuove colonne nel flusso di dati per i dati pubblicati. Solo le colonne di input a cui vengono applicate le funzioni di aggregazione e le colonne di input utilizzate dalla trasformazione per il raggruppamento vengono copiate nell'output della trasformazione. L'input di una trasformazione Aggregazione può includere ad esempio tre colonne: **CountryRegion**, **City** e **Population**. La trasformazione esegue un raggruppamento in base alla colonna **CountryRegion** e applica la funzione alla colonna **Population** . L'output non include pertanto la colonna **City** .  
  
 È inoltre possibile aggiungere più output alla trasformazione Aggregazione e indirizzare ogni aggregazione a un output diverso. Se ad esempio la trasformazione Aggregazione applica le funzioni Somma e Media, ogni aggregazione potrà essere indirizzata a un output diverso.  
  
 È possibile applicare più aggregazioni a una singola colonna di input. Se ad esempio si vuole ottenere i valori della somma e della media per una colonna di input di nome **Sales**, sarà possibile configurare la trasformazione in modo da applicare le funzioni Somma e Media alla colonna **Sales** .  
  
 La trasformazione Aggregazione include un input e uno o più output. Non supporta un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Aggregazione di valori in un set di dati utilizzando la trasformazione Aggregazione](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinare i dati per le trasformazioni Unione e Merge Join](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 [Aggregare valori in un set di dati tramite la trasformazione Aggregazione](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
## <a name="aggregate-transformation-editor-aggregations-tab"></a>Editor trasformazione Aggregazione (scheda Aggregazioni)
  Usare la scheda **Aggregazioni** della finestra di dialogo **Editor trasformazione Aggregazione** per specificare le colonne per l'aggregazione e le proprietà di aggregazione. È possibile applicare più aggregazioni. Questa trasformazione non genera output degli errori.  
  
> [!NOTE]  
>  Le opzioni per il conteggio delle chiavi, la scala delle chiavi, il conteggio delle chiavi distinct e la scala delle chiavi distinct vengono applicate a livello di componente quando vengono specificate nella scheda **Avanzate** , a livello di output quando vengono specificate nella sezione delle opzioni avanzate della scheda **Aggregazioni** e a livello di colonna quando vengono specificate nell'elenco delle colonne nella parte inferiore della scheda **Aggregazioni** .  
>   
>  Nella trasformazione Aggregazione **Chiavi** e **Scala chiavi** fanno riferimento al numero di gruppi che dovrebbero risultare da un'operazione **Group by** . **Chiavi conteggio valori distinct** e **Scala conteggio valori distinct** fanno riferimento al numero di valori distinct che dovrebbero risultare da un'operazione **Distinct count** .  
  
### <a name="options"></a>Opzioni  
 **Avanzate/Standard**  
 Consente di visualizzare o nascondere le opzioni per la configurazione di più aggregazioni per più output. Le opzioni avanzate sono nascoste per impostazione predefinita.  
  
 **Nome aggregazione**  
 Consente di digitare un nome descrittivo per l'aggregazione nella sezione delle opzioni avanzate.  
  
 **Colonne GROUP BY**  
 Nella sezione delle opzioni avanzate, selezionare le colonne da raggruppare usando l'elenco **Colonne di input disponibili** come descritto di seguito.  
  
 **Scala chiavi**  
 Nella sezione delle opzioni avanzate è inoltre possibile specificare il numero approssimativo di chiavi che possono essere scritte dall'aggregazione. Per impostazione predefinita, il valore di questa opzione è **Non specificata**. Se le proprietà **Scala chiavi** e **Chiavi** sono entrambe impostate, il valore della proprietà **Chiavi** ha la precedenza.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Non specificata|La proprietà Scala chiavi non viene utilizzata.|  
|Bassa|L'aggregazione può scrivere circa 500.000 chiavi.|  
|Media|L'aggregazione può scrivere circa 5.000.000 di chiavi.|  
|Alto|L'aggregazione può scrivere oltre 25.000.000 di chiavi.|  
  
 **Chiavi**  
 Nella sezione delle opzioni avanzate è inoltre possibile specificare il numero esatto di chiavi che possono essere scritte dall'aggregazione. Se le proprietà **Scala chiavi** e **Chiavi** sono entrambe specificate, la proprietà **Chiavi** ha la precedenza.  
  
 **Colonne di input disponibili**  
 Consente di selezionare le colonne di input nell'elenco delle colonne di input disponibili utilizzando le caselle controllo presenti nella tabella.  
  
 **Colonna di input**  
 Consente di selezionare una colonna di input nell'elenco delle colonne di input disponibili.  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna. Per impostazione predefinita viene suggerito il nome della colonna di input. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Operazione**  
 Selezionare un'operazione nell'elenco delle operazioni disponibili utilizzando la tabella seguente come guida.  
  
|Operazione|Descrizione|  
|---------------|-----------------|  
|**GroupBy**|Consente di dividere i set di dati in gruppi. Per il raggruppamento è possibile utilizzare colonne con qualsiasi tipo di dati. Per ulteriori informazioni, vedere GROUP BY.|  
|**Sum**|Consente di sommare i valori di una colonna. È possibile sommare solo le colonne con tipi di dati numerici. Per ulteriori informazioni, vedere SUM.|  
|**Medio**|Consente di restituire la media dei valori di una colonna. È possibile calcolare la media soltanto delle colonne con tipi di dati numerici. Per ulteriori informazioni, vedere AVG.|  
|**Count**|Consente di restituire il numero di elementi di un gruppo. Per ulteriori informazioni, vedere COUNT.|  
|**CountDistinct**|Consente di restituire il numero di valori non Null univoci di un gruppo. Per ulteriori informazioni, vedere COUNT e Distinct.|  
|**Minimo**|Restituisce il valore minimo in un gruppo. Limitata soltanto ai tipi di dati numerici.|  
|**Massimo**|Restituisce il valore massimo in un gruppo. Limitata soltanto ai tipi di dati numerici.|  
  
 **Flag di confronto**  
 Se si scegliere **Group By**, usare le caselle di controllo per controllare la modalità con cui la trasformazione esegue il confronto. Per altre informazioni sulle opzioni per il confronto di stringhe, vedere [Confronto di dati stringa](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Count Distinct Scale**  
 È possibile specificare il numero approssimativo di valori distinct che l'aggregazione può scrivere. Per impostazione predefinita, il valore di questa opzione è **Non specificata**. Se le proprietà **CountDistinctScale** e **CountDistinctKeys** sono entrambe specificate, la proprietà **CountDistinctKeys** ha la precedenza.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Non specificata|La proprietà **CountDistinctScale** non viene usata.|  
|Bassa|L'aggregazione può scrivere circa 500.000 valori distinct.|  
|Media|L'aggregazione può scrivere circa 5.000.000 di valori distinct.|  
|Alto|L'aggregazione può scrivere oltre 25.000.000 di valori distinct.|  
  
 **Count Distinct Keys**  
 È possibile specificare il numero esatto di valori distinct che l'aggregazione può scrivere. Se le proprietà **CountDistinctScale** e **CountDistinctKeys** sono entrambe specificate, la proprietà **CountDistinctKeys** ha la precedenza.  
  
## <a name="aggregate-transformation-editor-advanced-tab"></a>Editor trasformazione Aggregazione (scheda Avanzate)
  Usare la scheda **Avanzate** della finestra di dialogo **Editor trasformazione Aggregazione** per impostare le proprietà dei componenti, specificare le aggregazioni, nonché impostare le proprietà delle colonne di input e output.  
  
> [!NOTE]  
>  Le opzioni per il conteggio delle chiavi, la scala delle chiavi, il conteggio delle chiavi distinct e la scala delle chiavi distinct vengono applicate a livello di componente quando vengono specificate nella scheda **Avanzate** , a livello di output quando vengono specificate nella sezione delle opzioni avanzate della scheda **Aggregazioni** e a livello di colonna quando vengono specificate nell'elenco delle colonne nella parte inferiore della scheda **Aggregazioni** .  
>   
>  Nella trasformazione Aggregazione **Chiavi** e **Scala chiavi** fanno riferimento al numero di gruppi che dovrebbero risultare da un'operazione **Group by** . **Chiavi conteggio valori distinct** e **Scala conteggio valori distinct** fanno riferimento al numero di valori distinct che dovrebbero risultare da un'operazione **Distinct count** .  
  
### <a name="options"></a>Opzioni  
 **Scala chiavi**  
 Consente di specificare facoltativamente il numero approssimativo di chiavi previste dall'aggregazione. La trasformazione utilizza tale informazione per ottimizzare la dimensione iniziale della cache. Per impostazione predefinita, il valore di questa opzione è **Non specificata**. Se vengono specificate sia **Scala chiavi** sia **Numero di chiavi**, **Numero di chiavi** ha priorità.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Non specificata|La proprietà **Scala chiavi** non viene usata.|  
|Bassa|L'aggregazione può scrivere circa 500.000 chiavi.|  
|Media|L'aggregazione può scrivere circa 5.000.000 di chiavi.|  
|Alto|L'aggregazione può scrivere oltre 25.000.000 di chiavi.|  
  
 **Numero di chiavi**  
 Consente di specificare facoltativamente il numero esatto di chiavi previste dall'aggregazione. La trasformazione utilizza tale informazione per ottimizzare la dimensione iniziale della cache. Se vengono specificate sia **Scala chiavi** sia **Numero di chiavi**, **Numero di chiavi** ha priorità.  
  
 **Scala conteggio valori distinct**  
 È possibile specificare il numero approssimativo di valori distinct che l'aggregazione può scrivere. Per impostazione predefinita, il valore di questa opzione è **Non specificata**. Se vengono specificate sia **Scala conteggio valori distinct** sia **Chiavi conteggio valori distinct**, **Numero di chiavi** ha priorità.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Non specificata|La proprietà CountDistinctScale non viene utilizzata.|  
|Bassa|L'aggregazione può scrivere circa 500.000 valori distinct.|  
|Media|L'aggregazione può scrivere circa 5.000.000 di valori distinct.|  
|Alto|L'aggregazione può scrivere oltre 25.000.000 di valori distinct.|  
  
 **Chiavi conteggio valori distinct**  
 È possibile specificare il numero esatto di valori distinct che l'aggregazione può scrivere. Se vengono specificate sia **Scala conteggio valori distinct** sia **Chiavi conteggio valori distinct**, **Numero di chiavi** ha priorità.  
  
 **Fattore di estensione automatica**  
 Consente di utilizzare un valore compreso tra 1 e 100 per specificare la percentuale di estensione possibile della memoria durante l'aggregazione. Il valore predefinito di questa opzione è **25%**.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
