---
title: I gruppi di calcolo nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 06/05/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 58e845965bb9cd4eeba46ad30193c79b436da569
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719864"
---
# <a name="calculation-groups-preview"></a>Gruppi di calcolo (anteprima)
 
[!INCLUDE[ssas-appliesto-sql2019](../../includes/ssas-appliesto-sql2019.md)]

I gruppi di calcolo possono ridurre significativamente il numero di misure con ridondanza mediante il raggruppamento di espressioni di misura più comuni come *elementi di calcolo*. I gruppi di calcolo e sono supportati nei modelli tabulari di SQL Server Analysis Services 2019 il 1470 superiore [livello di compatibilità](compatibility-level-for-tabular-models-in-analysis-services.md). Sono attualmente in modelli a livello di compatibilità 1470 **Preview**.  

Questo articolo descrive: 

> [!div class="checklist"]
> * Vantaggi 
> * Come funzionano i gruppi di calcolo
> * Stringhe di formato dinamico
> * Precedenza
> * Strumenti
> * Limitazioni



## <a name="benefits"></a>Vantaggi

I gruppi di calcolo risolvere un problema nei modelli complessi in cui può esserci una proliferazione di misure ridondanti con stessi calcoli eseguiti - più comune con calcoli di business intelligence. Ad esempio, un analista delle vendite di visualizzare i totali delle vendite e Ordina per mese-to-date (MTD), quarter-to-date (trimestre), year-to-date (YTD), gli ordini year-to-date per l'anno precedente (PIA) e così via. I creatori di modelli di dati è necessario creare misure separate per ogni calcolo, che possono causare decine di misure. Per l'utente, questo significa che sia necessario ordinare tramite anche molte misure e applicarli singolarmente ai report. 

Diamo prima un'occhiata a come i gruppi di calcolo vengono visualizzate agli utenti in uno strumento di creazione report come Power BI. Qui verranno quindi un'occhiata a come è costituito da un gruppo di calcolo e come vengono create in un modello.

I gruppi di calcolo vengono visualizzati nei client di creazione report sotto forma di tabella con una singola colonna. La colonna non è ad esempio una tipica colonna o una dimensione, rappresenta invece uno o più calcoli riutilizzabili, oppure *elementi di calcolo* che possono essere applicati a qualsiasi misura già aggiunto al filtro i valori per una visualizzazione.

Nell'animazione seguente, un'analisi dei dati di vendita per gli anni 2012 e 2013. Prima di applicare un gruppo di calcolo, la misura di base comune **vendita** calcolare una somma delle vendite totali per ogni mese. Quindi, l'utente desidera applicare calcoli di business intelligence per ottenere i totali delle vendite per data di fine, da inizio trimestre, da inizio anno, mese e così via. Senza gruppi di calcolo, l'utente dovrà selezionare singole misure di business intelligence.

Con un gruppo di calcolo, in questo esempio denominata **Intelligence in tempo**, quando l'utente trascina il **calcolo del tempo** elemento per il **colonne** area, ogni elemento di calcolo del filtro viene visualizzata come una colonna separata. I valori per ogni riga vengono calcolati da misura di base, **Sales**.  

![Gruppo di calcolo viene applicata in Power BI](media/calculation-groups/calc-groups-pbi.gif)


Usare i gruppi di calcolo **esplicita** le misure DAX. In questo esempio **Sales** è una misura esplicita già creata nel modello. I gruppi di calcolo non funzionano con le misure implicite DAX. In Power BI, ad esempio, le misure implicite vengono create quando un utente trascina colonne su oggetti visivi per visualizzare valori aggregati, senza creare una misura esplicita. In questo momento, Power BI genera DAX per misure implicite scritte come inline calcoli DAX, vale a dire le misure implicite non è possibile usare i gruppi di calcolo. È stata introdotta una nuova proprietà del modello visibile in modello di oggetto tabulare (TOM), **DiscourageImplicitMeasures**. Attualmente, per creare i gruppi di calcolo di questa proprietà deve essere impostata su **true**. Se impostato su true, Power BI Desktop in Live Connect in modalità disabilita la creazione di misure implicite.

## <a name="how-they-work"></a>Come funzionano

Ora che si è appreso come gruppi di calcolo avvantaggiare utenti, diamo un'occhiata a come viene creata nell'esempio di gruppo calcolo tempo Intelligence illustrato.

Prima di analizzare i dettagli, è possibile introdurre alcune nuove funzioni DAX in modo specifico per i gruppi di calcolo: 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) : utilizzate dalle espressioni per elementi di calcolo fare riferimento alla misura che attualmente si trova nel contesto. In questo esempio, la misura Sales.

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) : utilizzate dalle espressioni per elementi di calcolo determinare la misura che si trova nel contesto in base al nome.

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) : utilizzate dalle espressioni per elementi di calcolo determinare la misura che si trova nel contesto è specificata in un elenco delle misure.

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) : utilizzate dalle espressioni per elementi di calcolo recuperare la stringa di formato della misura che si trova nel contesto.

### <a name="time-intelligence-example"></a>Esempio di Intelligence tempo

Nome tabella - **Intelligence tempo**   
Nome della colonna - **calcolo del tempo**   
La precedenza - **20**   

#### <a name="time-intelligence-calculation-items"></a>Ora gli elementi di calcolo di Business Intelligence

**Current**

```dax
SELECTEDMEASURE()
```

**MTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESMTD(DimDate[Date]))
```

**QTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESQTD(DimDate[Date]))
```

**YTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

**PY**

```dax
CALCULATE(SELECTEDMEASURE(), SAMEPERIODLASTYEAR(DimDate[Date]))
```

**PIA MTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "MTD"
)
```

**QTD PY**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**PIA YTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

**YOY**

```dax
SELECTEDMEASURE() –
CALCULATE(
    SELECTEDMEASURE(),
    'Time Intelligence'[Time Calculation] = "PY"
)
```

**YOY%**

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

Per testare questo gruppo di calcolo, è possibile eseguire una query DAX in SQL Server Management Studio o open source [DAX Studio](http://daxstudio.org/). YOY e YOY % vengono omesse da questo esempio di query.

#### <a name="time-intelligence-query"></a>Query di Intelligence temporale

```dax
EVALUATE
CALCULATETABLE (
    SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Current", CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "Current" ),
        "QTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "QTD" ),
        "YTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "YTD" ),
        "PY",      CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY" ),
        "PY QTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY QTD" ),
        "PY YTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY YTD" )
    ),
    DimDate[CalendarYear] IN { 2012, 2013 }
)
```

#### <a name="time-intelligence-query-return"></a>Query di Intelligence ora restituire

La tabella restituita Mostra calcoli per ogni elemento è stato applicato il calcolo. Ad esempio, è possibile visualizzare che QTD per marzo 2012 è la somma di gennaio, febbraio e marzo 2012.

![Query restituito](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>Stringhe di formato dinamico

*Le stringhe di formato dinamico* con calcolo i gruppi di consentono l'applicazione condizionale di stringhe di formato per misure senza costringerli a restituire le stringhe.

I modelli tabulari supportano la formattazione dinamica delle misure tramite DAX [formato](https://docs.microsoft.com/dax/format-function-dax) (funzione). Tuttavia, la funzione FORMAT presenta lo svantaggio di restituzione di una stringa, forzando le misure che altrimenti sarebbero numeriche da restituire anche sotto forma di stringa. Ciò può avere alcune limitazioni, ad esempio non funziona con la maggior parte degli oggetti visivi di Power BI in base a valori numerici, come i grafici.

### <a name="dynamic-format-strings-for-time-intelligence"></a>Stringhe di formato dinamico per business intelligence

Se si esamina l'esempio di Intelligence ora illustrato in precedenza, tutto il calcolo degli elementi tranne **YOY %** deve utilizzare il formato della misura corrente nel contesto. Ad esempio, **YTD** calcolato sulla misura Sales base deve essere valuta. Se si trattasse di un gruppo di calcolo per simile a una misura di base di ordini, il formato è numerico. **YOY %** , tuttavia, deve essere una percentuale indipendentemente dal formato della misura di base.

Per la **YOY %** , è possibile ignorare la stringa di formato impostando la proprietà di espressione di stringa di formato **0,00%;-0.00%; % 0,00**. Per altre informazioni sulle proprietà dell'espressione stringa di formato, vedere [proprietà delle celle MDX - contenuti di stringa di formato](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values).

In questo oggetto visivo matrice in Power BI, vedrai **vendite corrente/YOY** e **ordini corrente/YOY** mantengono le relative stringhe di formato di misura di base corrispondente. **Vendite YOY %** e **Ordina YOY %** , tuttavia, sostituisce la stringa di formato da utilizzare *percentuale* formato.

![Intelligence ora nell'oggetto visivo matrice](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>Stringhe di formato dinamico per la conversione di valuta

Le stringhe di formato dinamico forniscono la conversione di valuta semplice. Si consideri il seguente modello di dati di Adventure Works. Si è modellato per *uno-a-molti* conversione di valuta come definito dal [tipi di conversione](../currency-conversions-analysis-services.md#conversion-types).

![Frequenza di valuta in modelli tabulari](media/calculation-groups/calc-groups-currency-conversion.png)

Oggetto **FormatString** viene aggiunta la **DimCurrency** di tabella e popolato con le stringhe di formato per le rispettive valute.

![Colonna di stringhe di formato](media/calculation-groups/calc-groups-formatstringcolumn.png)

In questo esempio il seguente gruppo di calcolo viene quindi definito come:

### <a name="currency-conversion-example"></a>Esempio di conversione valuta

Nome tabella - **conversione di valuta**   
Nome della colonna - **calcoli di conversione**   
La precedenza - **5**   

#### <a name="calculation-items-for-currency-conversion"></a>Elementi di calcolo per la conversione di valuta

**Nessuna conversione**

```dax
SELECTEDMEASURE()
```

**Valuta convertito**

```dax
IF(
    //Check one currency in context & not US Dollar, which is the pivot currency:
    SELECTEDVALUE( DimCurrency[CurrencyName], "US Dollar" ) = "US Dollar",
    SELECTEDMEASURE(),
    SUMX(
        VALUES(DimDate[Date]),
        CALCULATE( DIVIDE( SELECTEDMEASURE(), MAX(FactCurrencyRate[EndOfDayRate]) ) )
    )
)
```

Espressione stringa di formato

```dax
SELECTEDVALUE(
    DimCurrency[FormatString],
    SELECTEDMEASUREFORMATSTRING()
)
```
L'espressione di stringa di formato deve restituire una stringa scalare. Viene utilizzato il nuovo [SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) funzione per ripristinare la stringa di formato della misura di base se sono presenti più valute in contesto di filtro.

L'animazione seguente mostra la conversione di valuta formato dinamico del **Sales** misure in un report.

![Stringa di formato dinamico di conversione valuta applicata](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>Precedenza

La priorità è una proprietà definita per un gruppo di calcolo. Specifica l'ordine di valutazione quando è presente più di un gruppo di calcolo. Un numero più elevato indica la precedenza maggiore, vale a dire che verrà valutata prima i gruppi di calcolo con precedenza inferiore.

Per questo esempio, verranno usare dello stesso modello come il business intelligence esempio precedente, ma anche aggiungere un **medie** gruppo di calcolo. Il gruppo di calcolo delle medie mobili contiene calcoli medi che sono indipendenti da business intelligence tradizionali tempo in quanto non modificano il contesto di filtro di data, ma solo i calcoli medi in esso contenuti.

In questo esempio viene definito un calcolo della media giornaliero. I calcoli, ad esempio barili Media olio al giorno d' sono comuni nelle applicazioni di petrolio e gas. Altri esempi di business comuni includono Media delle vendite del Negozio nella vendita al dettaglio.

Anche se tali calcoli vengono calcolati indipendentemente da calcoli di business intelligence, potrebbe anche esserci un requisito per combinarle. Ad esempio, un utente potrebbe essere necessario visualizzare fuoco dell'olio al giorno da inizio anno per visualizzare la frequenza giornaliera petrolio dall'inizio dell'anno alla data corrente. In questo scenario, la precedenza deve essere impostata per gli elementi di calcolo.

### <a name="averages-example"></a>Esempio di medie mobili

Nome della tabella **medie**.   
Nome della colonna **calcolo della media**.   
È la precedenza **10**.   

#### <a name="calculation-items-for-averages"></a>Elementi di calcolo per le medie

**Nessun Media**

```dax
SELECTEDMEASURE()
```

**Media giornaliera**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Di seguito è riportato un esempio di una query DAX e di tabella restituita:

#### <a name="averages-query"></a>Query di medie mobili

```dax
EVALUATE
    CALCULATETABLE (
        SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Sales", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "No Average"
        ),
        "YTD", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "No Average"
        ),
        "Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "Daily Average"
        ),
        "YTD Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "Daily Average"
        )
    ),
    DimDate[CalendarYear] = 2012
)
```

#### <a name="averages-query-return"></a>Query di medie mobili restituito

![Query restituito](media/calculation-groups/calc-groups-ytd-daily-avg.png)

La tabella seguente illustra come vengono calcolati i valori di marzo 2012.


|Nome colonna  |Calcolo |
|---------|---------|
|YTD     |    Somma delle vendite per Jan, Feb, Mar 2012<br />= 495,364 + 506,994 + 373,483     |
|Media giornaliera    |     Vendite per marzo 2012 diviso per n. di giorni nel mese di marzo<br />= 373,483 / 31       |
|Media giornaliera di YTD     | YTD per marzo 2012 diviso per n. di giorni in gennaio, febbraio e marzo<br />=  1,375,841 / (31 + 29 + 31)       |

Ecco la definizione dell'elemento di calcolo da inizio anno, applicata con ordine di precedenza degli **20**.

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

Di seguito è giornaliera media, applicate con una priorità pari **10**.

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Poiché la precedenza del gruppo di calcolo tempo Intelligence è superiore a quello del gruppo di calcolo delle medie mobili, viene applicato come possibile su vasta scala. Calcolo della media giornaliera di YTD applica YTD sia il numeratore e il denominatore (numero di giorni) di calcolo della media giornaliero.

Ciò equivale all'espressione seguente:

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

Non è questa espressione:

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>Ricorsione laterale

Nell'esempio Business Intelligence di tempo precedente, alcuni degli elementi di calcolo fanno riferimento ad altri utenti nello stesso gruppo di calcolo. Questa operazione viene definita *ricorsione lateralmente*. Ad esempio, **YOY %** fa riferimento a entrambi **YOY** e **PY**.

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

In questo caso, entrambe le espressioni vengono valutate separatamente perché usano diversi calcolare le istruzioni. Non sono supportati altri tipi di ricorsione.

## <a name="single-calculation-item-in-filter-context"></a>Elemento singolo calcolo nel contesto di filtro

Nel nostro esempio Intelligence in tempo, il **PY YTD** elemento di calcolo ha un unico calcolare espressione:

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

L'argomento YTD della funzione CALCULATE() sostituisce il contesto di filtro per riutilizzare la logica già definita nell'elemento di calcolo da inizio anno. Non è possibile applicare sia PY e YTD in una singola valutazione. I gruppi di calcolo vengono *applicate solo* se un elemento singolo calcolo dal gruppo di calcolo nel contesto di filtro.

## <a name="mdx-support"></a>Supporto per MDX

I gruppi di calcolo supportano le query di dati (Multidimensional Expression). Ciò significa, gli utenti di Microsoft Excel, quali modelli di dati tabulari di query tramite MDX, è possibile sfruttare al meglio di gruppi di calcolo nel foglio di lavoro di tabelle pivot e grafici.

## <a name="tools"></a>Strumenti

I gruppi di calcolo non sono ancora supportati in SQL Server Data Tools, Visual Studio con le estensioni di Analysis Services. Tuttavia, i gruppi di calcolo possono essere creati usando TMSL Tabular Model Scripting Language () o open source [Editor di modelli tabulari](https://github.com/otykier/TabularEditor).

## <a name="limitations"></a>Limitazioni

[Sicurezza a livello dell'oggetto](object-level-security.md) (amministrazione) definiti nel calcolo tabelle del gruppo non è supportato. Tuttavia, amministrazione può essere definito in altre tabelle nello stesso modello. Se un elemento di calcolo fa riferimento a un oggetto protetto di amministrazione, viene restituito un errore generico.

[Sicurezza a livello di riga](roles-ssas-tabular.md#bkmk_rowfliters) (RLS) non è supportato. È possibile definire a livello di riga nelle tabelle nel modello stesso, ma non su stessi gruppi di calcolo (direttamente o indirettamente).

[Le espressioni di righe di dettaglio](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md) non sono supportate con gruppi di calcolo.

## <a name="see-also"></a>Vedere anche  

[Il linguaggio DAX nei modelli tabulari](understanding-dax-in-tabular-models-ssas-tabular.md)   
[Riferimento a DAX](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
