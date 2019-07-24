---
title: Gruppi di calcolo in Analysis Services modelli tabulari | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: af63f41555a021fc720c7d1e15778265fe7de500
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419532"
---
# <a name="calculation-groups-preview"></a>Gruppi di calcolo (anteprima)
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

I gruppi di calcolo possono ridurre significativamente il numero di misure ridondanti raggruppando espressioni di misura comuni come *elementi di calcolo*. I gruppi di calcolo sono supportati in Azure Analysis Services e SQL Server Analysis Services modelli tabulari 2019 a 1470 e a un [livello di compatibilità](compatibility-level-for-tabular-models-in-analysis-services.md)superiore. I modelli con livello di compatibilità 1470 sono attualmente in **Anteprima**.  

Questo articolo descrive: 

> [!div class="checklist"]
> * Vantaggi 
> * Come funzionano i gruppi di calcolo
> * Stringhe di formato dinamico
> * Ordinare
> * Precedenza
> * Strumenti
> * Limitazioni



## <a name="benefits"></a>Vantaggi

I gruppi di calcolo si rivolgono a un problema nei modelli complessi in cui può essere presente una proliferazione di misure ridondanti utilizzando gli stessi calcoli, più comuni con i calcoli di business intelligence. Un analista delle vendite, ad esempio, vuole visualizzare i totali e gli ordini di vendita in base al mese (MTD), da trimestre a data (QTD), da inizio anno (YTD), dagli ordini da inizio anno all'anno precedente (PY) e così via. Il Data Modeler deve creare misure separate per ogni calcolo, il che può causare decine di misure. Per l'utente, questo può comportare la necessità di eseguire l'ordinamento in base a un numero così elevato di misure e di applicarle singolarmente al report. 

Esaminiamo innanzitutto il modo in cui i gruppi di calcolo vengono visualizzati agli utenti in uno strumento di creazione di report come Power BI. Verranno quindi esaminati gli elementi che costituiscono un gruppo di calcolo e il modo in cui vengono creati in un modello.

I gruppi di calcolo vengono visualizzati nei client di creazione report sotto forma di tabella con una singola colonna. La colonna non è simile a una colonna o una dimensione tipica, bensì rappresenta uno o più calcoli riutilizzabili o *elementi di calcolo* che possono essere applicati a qualsiasi misura già aggiunta al filtro valori per una visualizzazione.

Nell'animazione seguente un utente analizza i dati delle vendite per gli anni 2012 e 2013. Prima di applicare un gruppo di calcolo, le **vendite** della misura di base comuni calcolano una somma delle vendite totali per ogni mese. L'utente desidera quindi applicare calcoli relativi all'intelligence temporale per ottenere i totali delle vendite da inizio mese, da inizio trimestre, da inizio anno e così via. Senza gruppi di calcolo, l'utente deve selezionare singole misure di Business Intelligence per l'ora.

Con un gruppo di calcolo, in questo esempio denominato **Time Intelligence**, quando l'utente trascina l'elemento di **calcolo dell'ora** nell'area filtro **colonne** , ogni elemento di calcolo viene visualizzato come colonna separata. I valori per ogni riga vengono calcolati dalla misura di base **Sales**.  

![Gruppo di calcolo applicato in Power BI](media/calculation-groups/calc-groups-pbi.gif)


I gruppi di calcolo  funzionano con misure DAX esplicite. In questo esempio, **Sales** è una misura esplicita già creata nel modello. I gruppi di calcolo non funzionano con le misure DAX implicite. Ad esempio, in Power BI le misure implicite vengono create quando un utente trascina le colonne sugli oggetti visivi per visualizzare i valori aggregati, senza creare una misura esplicita. A questo punto, Power BI genera DAX per le misure implicite scritte come calcoli DAX inline, ovvero le misure implicite non possono essere utilizzate con i gruppi di calcolo. È stata introdotta una nuova proprietà del modello visibile nel modello a oggetti tabulare (TOM), **DiscourageImplicitMeasures**. Attualmente, per creare gruppi di calcolo questa proprietà deve essere impostata su **true**. Se impostato su true, Power BI Desktop in modalità di connessione dinamica Disabilita la creazione di misure implicite.

## <a name="how-they-work"></a>Come funzionano

Ora che si è appreso come i gruppi di calcolo traggono vantaggio dagli utenti, esaminiamo il modo in cui viene creato l'esempio di gruppo di calcolo dell'intelligenza temporale illustrato.

Prima di esaminare i dettagli, verranno introdotte alcune nuove funzioni DAX specifiche per i gruppi di calcolo: 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) : utilizzata dalle espressioni per gli elementi di calcolo per fare riferimento alla misura attualmente nel contesto. In questo esempio, la misura Sales.

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) : utilizzata dalle espressioni per gli elementi di calcolo per determinare la misura nel contesto in base al nome.

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) : utilizzata dalle espressioni per gli elementi di calcolo per determinare la misura nel contesto specificata in un elenco di misure.

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) : utilizzata dalle espressioni per gli elementi di calcolo per recuperare la stringa di formato della misura nel contesto.

### <a name="time-intelligence-example"></a>Esempio di Business Intelligence per l'ora

Nome tabella- **Business Intelligence in tempo**   
Calcolo nome colonna- **ora**   
Precedenza- **20**   

#### <a name="time-intelligence-calculation-items"></a>Elementi di calcolo Time Intelligence

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

**PY MTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "MTD"
)
```

**PY QTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**PY YTD**

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

Per testare questo gruppo di calcolo, è possibile eseguire una query DAX in SSMS o nell'Open Source [DAX Studio](http://daxstudio.org/). In questo esempio di query vengono omessi il% di base e annuo.

#### <a name="time-intelligence-query"></a>Query di Business Intelligence per l'ora

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

#### <a name="time-intelligence-query-return"></a>Tempo di risposta della query di Business Intelligence

La tabella return Mostra i calcoli per ogni elemento di calcolo applicato. Ad esempio, è possibile vedere QTD per il 2012 marzo è la somma di gennaio, febbraio e marzo 2012.

![Risultato della query](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>Stringhe di formato dinamico

Le *stringhe di formato dinamico* con gruppi di calcolo consentono l'applicazione condizionale di stringhe di formato alle misure senza forzare la restituzione delle stringhe.

I modelli tabulari supportano la formattazione dinamica delle misure tramite la funzione [Format](https://docs.microsoft.com/dax/format-function-dax) di DAX. Tuttavia, la funzione FORMAT presenta gli svantaggi della restituzione di una stringa, forzando le misure che altrimenti sarebbero numeric da restituire anche come stringa. Questo può presentare alcune limitazioni, ad esempio non usare la maggior parte degli oggetti visivi Power BI a seconda dei valori numerici, ad esempio i grafici.

### <a name="dynamic-format-strings-for-time-intelligence"></a>Stringhe di formato dinamico per l'intelligence del tempo

Se si esamina l'esempio di Business Intelligence per l'ora illustrato in precedenza, tutti gli elementi di calcolo ad eccezione della **percentuale** di tempo di attività devono usare il formato della misura corrente nel contesto. Ad esempio, **YTD** calcolato sulla misura Sales base deve essere Currency. Se si tratta di un gruppo di calcolo per un elemento come una misura di base Orders, il formato sarà numerico. Il valore **annuo%** , tuttavia, deve essere una percentuale indipendentemente dal formato della misura di base.

Per il **%** , è possibile eseguire l'override della stringa di formato impostando la proprietà espressione stringa di formato su **0.00%;-0.00%; 0.00%** . Per ulteriori informazioni sulle proprietà dell'espressione stringa di formato, vedere [proprietà delle celle MDX-contenuto della stringa di formato](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values).

In questo oggetto visivo matrice in Power BI, viene visualizzato **Current/annue Sales** e **Orders Current/** si mantiene le rispettive stringhe di formato della misura di base. Le **vendite a%** e **gli ordini**, invece, eseguono l'override della stringa di formato per utilizzare il formato *percentuale* .

![Business Intelligence per l'ora nell'oggetti visivi matrice](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>Stringhe di formato dinamico per la conversione di valuta

Le stringhe di formato dinamico forniscono una semplice conversione di valuta. Si consideri il modello di dati Adventure Works seguente. Viene modellato per la conversione di valuta *uno-a-molti* come definito dai [tipi di conversione](../currency-conversions-analysis-services.md#conversion-types).

![Tasso di valuta nel modello tabulare](media/calculation-groups/calc-groups-currency-conversion.png)

Una colonna **FormatString** viene aggiunta alla tabella **DimCurrency** e popolata con stringhe di formato per le rispettive valute.

![Colonna stringa formato](media/calculation-groups/calc-groups-formatstringcolumn.png)

Per questo esempio, il gruppo di calcolo seguente viene definito come:

### <a name="currency-conversion-example"></a>Esempio di conversione di valuta

Nome tabella- **conversione valuta**   
Nome colonna- **calcolo conversione**   
Precedenza- **5**   

#### <a name="calculation-items-for-currency-conversion"></a>Elementi di calcolo per la conversione di valuta

**Nessuna conversione**

```dax
SELECTEDMEASURE()
```

**Valuta convertita**

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
L'espressione stringa di formato deve restituire una stringa scalare. Usa la nuova funzione [SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) per ripristinare la stringa di formato della misura di base se sono presenti più valute nel contesto di filtro.

Nell'animazione seguente viene illustrata la conversione di valuta del formato dinamico della misura **Sales** in un report.

![Stringa di formato dinamico per la conversione di valuta applicata](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>Precedenza

La precedenza è una proprietà definita per un gruppo di calcolo. Specifica l'ordine di valutazione quando è presente più di un gruppo di calcolo. Un numero più alto indica una maggiore precedenza, ovvero verrà valutato prima dei gruppi di calcolo con precedenza più bassa.

Per questo esempio verrà usato lo stesso modello dell'esempio di business intelligence precedente, ma viene aggiunto anche un gruppo di calcolo delle **medie** . Il gruppo calcolo medio contiene calcoli medi indipendenti dalle funzionalità di Business Intelligence per l'ora tradizionale, in quanto non modificano il contesto del filtro di data, ma semplicemente applicano calcoli medi al suo interno.

In questo esempio viene definito un calcolo medio giornaliero. I calcoli, ad esempio i barilotti medi di petrolio al giorno, sono comuni nelle applicazioni di petrolio e gas. Altri esempi aziendali comuni includono la media delle vendite dei negozi in vendita al dettaglio.

Sebbene questi calcoli vengano calcolati in modo indipendente dai calcoli relativi all'intelligence temporale, potrebbe essere necessario combinarli. Ad esempio, è possibile che un utente desideri visualizzare i barili di petrolio al giorno YTD per visualizzare la tariffa di petrolio giornaliera dall'inizio dell'anno alla data corrente. In questo scenario è necessario impostare la precedenza per gli elementi di calcolo.

### <a name="averages-example"></a>Esempio di medie

Il nome della tabella corrisponde alle **medie**.   
Il nome della colonna è **calcolo medio**.   
La precedenza è **10**.   

#### <a name="calculation-items-for-averages"></a>Elementi di calcolo per le medie

**Nessuna Media**

```dax
SELECTEDMEASURE()
```

**Media giornaliera**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Di seguito è riportato un esempio di una query DAX e di una tabella restituita:

#### <a name="averages-query"></a>Query medie

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

#### <a name="averages-query-return"></a>Valore medio restituito dalla query

![Risultato della query](media/calculation-groups/calc-groups-ytd-daily-avg.png)

Nella tabella seguente viene illustrato come vengono calcolati i valori del 2012 marzo.


|Nome colonna  |Calcolo |
|---------|---------|
|YTD     |    Somma delle vendite per Jan, feb, mar 2012<br />= 495.364 + 506.994 + 373.483     |
|Media giornaliera    |     Vendite per il mar 2012 divise per il numero di giorni nel marzo<br />= 373.483/31       |
|Media giornaliera YTD     | YTD per il mar 2012 diviso per il numero di giorni di gennaio, febbraio e marzo<br />= 1.375.841/(31 + 29 + 31)       |

Di seguito è illustrata la definizione dell'elemento di calcolo YTD, applicato con precedenza pari a **20**.

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

Questa è la media giornaliera, applicata con una precedenza di **10**.

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Poiché la precedenza del gruppo di calcoli Time Intelligence è superiore a quella del gruppo di calcolo Averages, viene applicata nel modo più ampio possibile. Il calcolo della media giornaliera YTD applica YTD sia al numeratore che al denominatore (numero di giorni) del calcolo medio giornaliero.

Equivale all'espressione seguente:

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

Non questa espressione:

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>Ricorsione laterale

Nell'esempio di intelligenza temporale precedente, alcuni elementi di calcolo fanno riferimento ad altri nello stesso gruppo di calcolo. Questa operazione viene definita ricorsione *laterale*. Ad esempio, la **percentuale** di tempo di riferimento è sia **annua** che **py**.

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

In questo caso, entrambe le espressioni vengono valutate separatamente perché utilizzano istruzioni Calculate diverse. Altri tipi di ricorsione non sono supportati.

## <a name="single-calculation-item-in-filter-context"></a>Singolo elemento di calcolo nel contesto di filtro

Nell'esempio di Business Intelligence per il tempo, l'elemento di calcolo **py YTD** ha una singola espressione CALCULATE:

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

L'argomento YTD della funzione CALCULATE () esegue l'override del contesto di filtro per riutilizzare la logica già definita nell'elemento di calcolo YTD. Non è possibile applicare sia PY che YTD in una singola valutazione. I gruppi di calcolo vengono *applicati solo* se un singolo elemento di calcolo del gruppo di calcolo è in contesto di filtro.

## <a name="mdx-support"></a>Supporto MDX

I gruppi di calcolo supportano le query MDX (Multidimensional Data Expressions). Questo significa che gli utenti di Microsoft Excel, che eseguono query su modelli di dati tabulari tramite MDX, possono sfruttare appieno i gruppi di calcolo nelle tabelle pivot e nei grafici del foglio di lavoro.

## <a name="tools"></a>Strumenti

I gruppi di calcolo non sono ancora supportati in SQL Server Data Tools, Visual Studio con Analysis Services estensioni. È tuttavia possibile creare gruppi di calcoli utilizzando Tabular Model Scripting Language (TMSL) o l' [Editor tabulare](https://github.com/otykier/TabularEditor)open source.

## <a name="limitations"></a>Limitazioni

[Sicurezza a livello di oggetto](object-level-security.md) (OLS) definito nelle tabelle del gruppo di calcolo non è supportato. Tuttavia, OLS può essere definito in altre tabelle nello stesso modello. Se un elemento di calcolo fa riferimento a un oggetto protetto con OLS, viene restituito un errore generico.

[Sicurezza a livello di riga](roles-ssas-tabular.md#bkmk_rowfliters) (RLS) non è supportato. È possibile definire la sicurezza a livello di riga nelle tabelle nello stesso modello, ma non nei gruppi di calcolo stessi (direttamente o indirettamente).

## <a name="see-also"></a>Vedere anche  

[DAX nei modelli tabulari](understanding-dax-in-tabular-models-ssas-tabular.md)   
[Riferimento DAX](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
