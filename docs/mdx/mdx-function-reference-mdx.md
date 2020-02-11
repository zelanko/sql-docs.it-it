---
title: Guida di riferimento alle funzioni MDX (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ff14718e09fa3732a40ea245430f33c599325eea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003507"
---
# <a name="mdx-function-reference-mdx"></a>Guida di riferimento alle funzioni MDX (MDX)


  Analysis Services fornisce l'utilizzo di funzioni nella sintassi MDX (Multidimensional Expressions). È possibile utilizzare le funzioni in qualsiasi istruzione MDX valida e all'interno di query, definizioni di rollup personalizzate e altri calcoli. In questa sezione vengono fornite informazioni sulle funzioni MDX.  
  
 È possibile utilizzare le tabelle seguenti per la ricerca delle funzioni in base alla categoria del valore restituito oppure selezionare una funzione in base al nome dall'elenco alfabetico nel sommario.  
  
## <a name="array-functions"></a>Funzioni di matrice  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[SetToArray &#40;&#41;MDX](../mdx/settoarray-mdx.md)|Converte uno o più set in una matrice da utilizzare in una funzione definita dall'utente.|  
  
## <a name="hierarchy-functions"></a>Funzioni di gerarchia  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[Gerarchia &#40;MDX&#41;](../mdx/hierarchy-mdx.md)|Restituisce la gerarchia contenente il membro o il livello specificato.|  
|[&#41;MDX della dimensione &#40;](../mdx/dimension-mdx.md)|Restituisce la dimensione contenente il membro, il livello o la gerarchia specificata.|  
|[Dimensioni &#40;MDX&#41;](../mdx/dimensions-mdx.md)|Restituisce la gerarchia specificata da un'espressione numerica o stringa.|  
  
## <a name="level-functions"></a>Funzioni di livello  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[Livello &#40;MDX&#41;](../mdx/level-mdx.md)|Restituisce il livello di un membro.|  
|[Livelli &#40;&#41;MDX](../mdx/levels-mdx.md)|Restituisce il livello la cui posizione all'interno di una dimensione o gerarchia è specificata da un'espressione numerica oppure il cui nome è specificato da un'espressione stringa.|  
  
## <a name="logical-functions"></a>Funzioni logiche  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[Predecessore &#40;MDX&#41;](../mdx/isancestor-mdx.md)|Indica se il membro specificato è un predecessore di un altro membro specificato.|  
|[IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)|Indica se l'espressione valutata corrisponde al valore di cella vuota.|  
|[&#41;MDX &#40;di generazione](../mdx/isgeneration-mdx.md)|Indica se il membro specificato è incluso in una generazione specifica.|  
|[&#40;MDX&#41;](../mdx/isleaf-mdx.md)|Indica se il membro specificato è un membro foglia.|  
|[&#40;MDX&#41;](../mdx/issibling-mdx.md)|Indica se il membro specificato è di pari livello rispetto a un altro membro specificato.|  
  
## <a name="member-functions"></a>Funzioni di membro  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[Predecessore &#40;MDX&#41;](../mdx/ancestor-mdx.md)|Restituisce il predecessore di un membro al livello o alla distanza specificata.|  
|[ClosingPeriod &#40;&#41;MDX](../mdx/closingperiod-mdx.md)|Restituisce l'ultimo elemento di pari livello tra i discendenti di un membro al livello specificato.|  
|[Cugino &#40;MDX&#41;](../mdx/cousin-mdx.md)|Restituisce il membro figlio con la stessa posizione relativa del membro figlio specificato rispetto a un membro padre.|  
|[CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md)|Restituisce il membro corrente in una dimensione o gerarchia specificata durante l'iterazione.|  
|[DataMember &#40;MDX&#41;](../mdx/datamember-mdx.md)|Restituisce il membro dei dati generato dal sistema associato a un membro non foglia di una dimensione.|  
|[DefaultMember &#40;&#41;MDX](../mdx/defaultmember-mdx.md)|Restituisce il membro predefinito di una dimensione o di una gerarchia.|  
|[FirstChild &#40;MDX&#41;](../mdx/firstchild-mdx.md)|Restituisce il primo membro figlio di un membro.|  
|[FirstSibling &#40;&#41;MDX](../mdx/firstsibling-mdx.md)|Restituisce il primo membro figlio del padre di un membro.|  
|[Elemento &#40;membro&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)|Restituisce un membro da una tupla specificata.|  
|[Ritardo &#40;MDX&#41;](../mdx/lag-mdx.md)|Restituisce il membro che precede il membro specificato del numero di posizioni indicato all'interno della dimensione del membro.|  
|[LastChild &#40;&#41;MDX](../mdx/lastchild-mdx.md)|Restituisce l'ultimo membro figlio di un membro specificato.|  
|[LastSibling &#40;&#41;MDX](../mdx/lastsibling-mdx.md)|Restituisce l'ultimo membro figlio del padre di un membro specificato.|  
|[Lead &#40;MDX&#41;](../mdx/lead-mdx.md)|Restituisce il membro che segue il membro specificato del numero di posizioni indicato all'interno della dimensione del membro.|  
|[LinkMember &#40;&#41;MDX](../mdx/linkmember-mdx.md)|Restituisce il membro equivalente a un membro specificato in una gerarchia specifica.|  
|[Membri &#40;stringa&#41; &#40;MDX&#41;](../mdx/members-string-mdx.md)|Restituisce un membro specificato da un'espressione stringa.|  
|[NextMember &#40;&#41;MDX](../mdx/nextmember-mdx.md)|Restituisce il membro successivo nel livello contenente il membro specificato.|  
|[OpeningPeriod &#40;&#41;MDX](../mdx/openingperiod-mdx.md)|Restituisce il primo elemento di pari livello tra i discendenti di un livello specificato, facoltativamente in corrispondenza di un membro specificato.|  
|[ParallelPeriod &#40;&#41;MDX](../mdx/parallelperiod-mdx.md)|Restituisce un membro di un periodo precedente nella stessa posizione relativa del membro specificato.|  
|[&#41;MDX &#40;padre](../mdx/parent-mdx.md)|Restituisce il membro padre di un membro.|  
|[PrevMember &#40;&#41;MDX](../mdx/prevmember-mdx.md)|Restituisce il membro precedente nel livello contenente un membro specificato.|  
|[StrToMember &#40;&#41;MDX](../mdx/strtomember-mdx.md)|Restituisce il membro specificato da una stringa in formato MDX.|  
|[UnknownMember &#40;&#41;MDX](../mdx/unknownmember-mdx.md)|Restituisce il membro sconosciuto associato a un livello o a un membro.|  
|[ValidMeasure &#40;&#41;MDX](../mdx/validmeasure-mdx.md)|Restituisce una misura valida in un cubo virtuale, forzando al livello principale le dimensioni inapplicabili.|  
  
## <a name="numeric-functions"></a>Funzioni numeriche  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[Aggregazione MDX &#40;&#41;](../mdx/aggregate-mdx.md)|Restituisce un valore scalare calcolato mediante l'aggregazione di misure, oppure, facoltativamente, di un'espressione numerica specificata, con le tuple di un set specificato.|  
|[&#41;MDX AVG &#40;](../mdx/avg-mdx.md)|Restituisce il valore medio delle misure o di un'espressione numerica facoltativa valutata sul set specificato.|  
|[CalculationCurrentPass &#40;&#41;MDX](../mdx/calculationcurrentpass-mdx.md)|Restituisce la sessione di calcolo corrente di un cubo per il contesto di query specificato.|  
|[CalculationPassValue &#40;&#41;MDX](../mdx/calculationpassvalue-mdx.md)|Restituisce il valore di un'espressione MDX valutata sulla sessione di calcolo specificata di un cubo.|  
|[CoalesceEmpty &#40;&#41;MDX](../mdx/coalesceempty-mdx.md)|Assegna un numero o una stringa a un valore di cella vuota e restituisce il valore assegnato.|  
|[Correlazione &#40;MDX&#41;](../mdx/correlation-mdx.md)|Restituisce il coefficiente di correlazione di due serie, valutato su un set.|  
|[Conteggio &#40;dimensione&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)|Restituisce il numero di dimensioni in un cubo.|  
|[Conteggio &#40;livelli di gerarchia&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)|Restituisce il numero di livelli in una dimensione o gerarchia.|  
|[Conteggio &#40;set&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)|Restituisce il numero di celle in un set.|  
|[Conteggio &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)|Restituisce il numero di dimensioni in una tupla.|  
|[Covarianza &#40;MDX&#41;](../mdx/covariance-mdx.md)|Restituisce la covarianza della popolazione di due serie valutata su un set, utilizzando la formula della popolazione distorta.|  
|[Covarianza &#40;MDX&#41;](../mdx/covariancen-mdx.md)|Restituisce la covarianza del campione di due serie valutata su un set, utilizzando la formula della popolazione non distorta.|  
|[DistinctCount &#40;&#41;MDX](../mdx/distinctcount-mdx.md)|Restituisce il numero di tuple distinte e non vuote in un set.|  
|[IIf &#40;MDX&#41;](../mdx/iif-mdx.md)|Restituisce uno dei due valori determinati da un test logico.|  
|[LinRegIntercept &#40;&#41;MDX](../mdx/linregintercept-mdx.md)|Calcola la regressione lineare di un set e restituisce il valore dell'intercetta nella linea di regressione y = ax + b.|  
|[LinRegPoint &#40;&#41;MDX](../mdx/linregpoint-mdx.md)|Calcola la regressione lineare di un set e restituisce il valore di *y* nella retta di regressione y = ax + b.|  
|[LinRegR2 &#40;&#41;MDX](../mdx/linregr2-mdx.md)|Calcola la regressione lineare di un set e restituisce il coefficiente di determinazione R2.|  
|[LinRegSlope &#40;&#41;MDX](../mdx/linregslope-mdx.md)|Calcola la regressione lineare di un set e restituisce il valore della pendenza nella linea di regressione y = ax + b.|  
|[LinRegVariance &#40;&#41;MDX](../mdx/linregvariance-mdx.md)|Calcola la regressione lineare di un set e restituisce la varianza associata alla retta di regressione y = ax + b.|  
|[LookupCube &#40;&#41;MDX](../mdx/lookupcube-mdx.md)|Restituisce il valore di un'espressione MDX valutata su un altro cubo specificato nello stesso database.|  
|[&#41;MDX max &#40;](../mdx/max-mdx.md)|Restituisce il valore massimo di un'espressione numerica valutata su un set.|  
|[Mediana &#40;MDX&#41;](../mdx/median-mdx.md)|Restituisce la mediana di un'espressione numerica valutata su un set.|  
|[&#41;MDX min &#40;](../mdx/min-mdx.md)|Restituisce il valore minimo di un'espressione numerica valutata su un set.|  
|[Ordinale &#40;MDX&#41;](../mdx/ordinal-mdx.md)|Restituisce il valore ordinale in base zero associato a un livello.|  
|[Stima &#40;&#41;MDX](../mdx/predict-mdx.md)|Restituisce il valore di un'espressione numerica valutata su un modello di data mining.|  
|[Rango &#40;MDX&#41;](../mdx/rank-mdx.md)|Restituisce il rango in base uno di una tupla specificata in un set specificato.|  
|[RollupChildren &#40;&#41;MDX](../mdx/rollupchildren-mdx.md)|Restituisce un valore generato tramite il rollup dei valori degli elementi figlio del membro indicato, utilizzando l'operatore unario specificato.|  
|[StdDev &#40;&#41;MDX](../mdx/stddev-mdx.md)|Alias per [Stdev &#40;&#41;MDX ](../mdx/stdev-mdx.md).|  
|[StddevP &#40;&#41;MDX](../mdx/stddevp-mdx.md)|Alias per [StdevP &#40;&#41;MDX ](../mdx/stdevp-mdx.md).|  
|[StDev &#40;&#41;MDX](../mdx/stdev-mdx.md)|Restituisce la deviazione standard del campione di un'espressione numerica valutata su un set, utilizzando la formula della popolazione non distorta.|  
|[StdevP &#40;&#41;MDX](../mdx/stdevp-mdx.md)|Restituisce la deviazione standard della popolazione di un'espressione numerica valutata su un set, utilizzando la formula della popolazione distorta.|  
|[StrToValue &#40;&#41;MDX](../mdx/strtovalue-mdx.md)|Restituisce il valore specificato da una stringa in formato MDX.|  
|[Sum &#40;MDX&#41;](../mdx/sum-mdx.md)|Restituisce la somma di un'espressione numerica valutata su un set.|  
|[Valore &#40;&#41;MDX](../mdx/value-mdx.md)|Restituisce il valore di una misura.|  
|[Var &#40;&#41;MDX](../mdx/var-mdx.md)|Restituisce la varianza del campione di un'espressione numerica valutata su un set, utilizzando la formula della popolazione non distorta.|  
|[Varianza &#40;&#41;MDX](../mdx/variance-mdx.md)|Alias per [Var &#40;&#41;MDX ](../mdx/var-mdx.md).|  
|[VarianceP &#40;&#41;MDX](../mdx/variancep-mdx.md)|Alias per [VarP &#40;&#41;MDX ](../mdx/varp-mdx.md).|  
|[VarP &#40;&#41;MDX](../mdx/varp-mdx.md)|Restituisce la varianza della popolazione di un'espressione numerica valutata su un set, utilizzando la formula della popolazione distorta.|  
  
## <a name="set-functions"></a>Funzioni di set  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[AddCalculatedMembers &#40;&#41;MDX](../mdx/addcalculatedmembers-mdx.md)|Restituisce un set generato mediante l'aggiunta di membri calcolati a un set specificato.|  
|[AllMembers &#40;&#41;MDX](../mdx/allmembers-mdx.md)|Restituisce un set contenente tutti i membri della dimensione, della gerarchia o del livello specificato, inclusi i membri calcolati.|  
|[Predecessori &#40;MDX&#41;](../mdx/ancestors-mdx.md)|Restituisce un set di tutti i predecessori di un membro al livello o alla distanza specificata.|  
|[Predecessori &#40;MDX&#41;](../mdx/ascendants-mdx.md)|Restituisce il set dei predecessori del membro specificato, incluso il membro stesso.|  
|[&#41;MDX &#40;AXIS](../mdx/axis-mdx.md)|Restituisce un set definito in un asse.|  
|[BottomCount &#40;&#41;MDX](../mdx/bottomcount-mdx.md)|Dispone un set in ordine crescente e restituisce il numero specificato di tuple con i valori più bassi.|  
|[BottomPercent &#40;&#41;MDX](../mdx/bottompercent-mdx.md)|Dispone un set in ordine crescente e restituisce un set di tuple con i valori più bassi il cui totale cumulativo è uguale o inferiore alla percentuale specificata.|  
|[BottomSum &#40;&#41;MDX](../mdx/bottomsum-mdx.md)|Dispone un set in ordine crescente e restituisce un set di tuple con i valori più bassi il cui totale è uguale o inferiore al valore specificato.|  
|[Elementi figlio &#40;&#41;MDX](../mdx/children-mdx.md)|Restituisce i membri figlio di un membro specificato.|  
|[Crossjoin &#40;&#41;MDX](../mdx/crossjoin-mdx.md)|Restituisce il prodotto incrociato di uno o più set.|  
|[CurrentOrdinal &#40;&#41;MDX](../mdx/currentordinal-mdx.md)|Restituisce il numero di iterazioni corrente da un set durante l'iterazione.|  
|[Discendenti &#40;MDX&#41;](../mdx/descendants-mdx.md)|Restituisce il set di discendenti di un membro al livello o alla distanza specificata, includendo o escludendo facoltativamente i discendenti in altri livelli.|  
|[Distinct &#40;MDX&#41;](../mdx/distinct-mdx.md)|Restituisce un set, rimuovendo le tuple duplicate dal set specificato.|  
|[DrilldownLevel &#40;&#41;MDX](../mdx/drilldownlevel-mdx.md)|Esegue il drill-down dei membri di un set al livello immediatamente inferiore rispetto a quello più basso rappresentato nel set oppure rispetto a un livello facoltativo specificato di un membro rappresentato nel set.|  
|[DrilldownLevelBottom &#40;&#41;MDX](../mdx/drilldownlevelbottom-mdx.md)|Esegue il drill-down, fino al livello immediatamente inferiore, dei membri di livello più basso di un set al livello specificato.|  
|[DrilldownLevelTop &#40;&#41;MDX](../mdx/drilldownleveltop-mdx.md)|Esegue il drill-down, fino al livello immediatamente inferiore, dei membri di livello più alto di un set al livello specificato.|  
|[DrilldownMember &#40;&#41;MDX](../mdx/drilldownmember-mdx.md)|Esegue il drill-down dei membri di un set specificato presenti in un secondo set specificato. In alternativa, esegue il drill-down in un set di tuple.|  
|[DrilldownMemberBottom &#40;&#41;MDX](../mdx/drilldownmemberbottom-mdx.md)|Esegue il drill-down dei membri di un set specificato presenti in un secondo set specificato, limitando il set di risultati al numero specificato di membri. In alternativa, esegue il drill-down in un set di tuple.|  
|[DrilldownMemberTop &#40;&#41;MDX](../mdx/drilldownmembertop-mdx.md)|Esegue il drill-down dei membri di un set specificato presenti in un secondo set specificato, limitando il set di risultati al numero specificato di membri. In alternativa, esegue il drill-down in un set di tuple.|  
|[DrillupLevel &#40;&#41;MDX](../mdx/drilluplevel-mdx.md)|Esegue il drill-up dei membri di un set situati al livello immediatamente inferiore al livello specificato.|  
|[DrillupMember &#40;&#41;MDX](../mdx/drillupmember-mdx.md)|Esegue il drill-up dei membri di un set specificato presenti in un secondo set specificato.|  
|[Ad eccezione &#40;&#41;MDX](../mdx/except-mdx-function.md)|Individua le differenze tra due set, mantenendo facoltativamente i duplicati.|  
|[Esistente &#40;&#41;MDX](../mdx/exists-mdx.md)|Restituisce il set di membri di un set in cui esiste almeno una tupla di uno o più set diversi.|  
|[Estrai &#40;&#41;MDX](../mdx/extract-mdx.md)|Restituisce un set di tuple dagli elementi della dimensione estratti.|  
|[Filtrare &#40;&#41;MDX](../mdx/filter-mdx.md)|Restituisce il set risultante dal filtro di un set specificato in base a una condizione di ricerca.|  
|[Genera &#40;&#41;MDX](../mdx/generate-mdx.md)|Applica un set a ogni membro di un altro set e unisce i set risultanti tramite un join di unione. In alternativa, questa funzione restituisce una stringa concatenata creata valutando un'espressione stringa su un set.|  
|[Head &#40;MDX&#41;](../mdx/head-mdx.md)|Restituisce il primo numero specificato di elementi in un set, mantenendo i duplicati.|  
|[Hierarchize &#40;&#41;MDX](../mdx/hierarchize-mdx.md)|Ordina i membri di un set in una gerarchia.|  
|[Intersect &#40;&#41;MDX](../mdx/intersect-mdx.md)|Restituisce l'intersezione di due set di input, mantenendo facoltativamente i duplicati.|  
|[LastPeriods &#40;&#41;MDX](../mdx/lastperiods-mdx.md)|Restituisce il set dei membri che precedono e includono un membro specificato.|  
|[Membri &#40;set&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)|Restituisce il set di membri di una dimensione, di un livello o di una gerarchia.|  
|[MTD &#40;&#41;MDX](../mdx/mtd-mdx.md)|Restituisce un set di membri di pari livello dallo stesso livello di un membro dato, iniziando dal primo membro di pari livello e terminando con il membro dato, in base al vincolo imposto dal livello Anno della dimensione temporale.|  
|[NameToSet &#40;&#41;MDX](../mdx/nametoset-mdx.md)|Restituisce un set contenente il membro specificato da una stringa in formato MDX.|  
|[NonEmptyCrossjoin &#40;&#41;MDX](../mdx/nonemptycrossjoin-mdx.md)|Restituisce il prodotto incrociato di uno o più set, escludendo le tuple vuote e le tuple a cui non sono associati dati di tabelle dei fatti.|  
|[Ordine &#40;MDX&#41;](../mdx/order-mdx.md)|Organizza i membri di un set specificato, facoltativamente rispettando o violando la gerarchia.|  
|[PeriodsToDate &#40;&#41;MDX](../mdx/periodstodate-mdx.md)|Restituisce un set di membri di pari livello dallo stesso livello di un membro dato, iniziando dal primo membro di pari livello e terminando con il membro dato, in base al vincolo imposto dal livello specificato della dimensione temporale.|  
|[QTD &#40;&#41;MDX](../mdx/qtd-mdx.md)|Restituisce un set di membri di pari livello dallo stesso livello di un membro specificato, a partire dal primo elemento di pari livello e terminando con il membro dato, in base al vincolo del livello *trimestre* della dimensione temporale.|  
|[Elementi di pari livello &#40;MDX&#41;](../mdx/siblings-mdx.md)|Restituisce i membri di pari livello di un membro specificato, incluso il membro stesso.|  
|[StripCalculatedMembers &#40;&#41;MDX](../mdx/stripcalculatedmembers-mdx.md)|Restituisce un set generato dalla rimozione dei membri calcolati dal set specificato.|  
|[StrToSet &#40;&#41;MDX](../mdx/strtoset-mdx.md)|Restituisce il set specificato da una stringa in formato MDX.|  
|[Subset &#40;MDX&#41;](../mdx/subset-mdx.md)|Restituisce un subset di tuple dal set specificato.|  
|[Tail &#40;MDX&#41;](../mdx/tail-mdx.md)|Restituisce un subset dalla fine di un set.|  
|[ToggleDrillState &#40;&#41;MDX](../mdx/toggledrillstate-mdx.md)|Alterna lo stato di drill dei membri.|  
|[Conteggio &#40;MDX&#41;](../mdx/topcount-mdx.md)|Dispone un set in ordine decrescente e restituisce il numero specificato di elementi con i valori più alti.|  
|[Percentuale &#40;MDX&#41;](../mdx/toppercent-mdx.md)|Dispone un set in ordine decrescente e restituisce un set di tuple con i valori più alti il cui totale cumulativo è uguale o inferiore alla percentuale specificata.|  
|[&#41;MDX Topum &#40;](../mdx/topsum-mdx.md)|Ordina un set e restituisce gli elementi superiori il cui totale cumulativo è maggiore o uguale al valore specificato.|  
|[&#41;MDX di Union &#40;](../mdx/union-mdx.md)|Restituisce l'unione di due set, mantenendo facoltativamente i duplicati.|  
|[Non ordinare &#40;MDX&#41;](../mdx/unorder-mdx.md)|Rimuove l'ordinamento imposto da un set specificato.|  
|[VisualTotals &#40;&#41;MDX](../mdx/visualtotals-mdx.md)|Restituisce un set generato calcolando dinamicamente il totale dei membri figlio nel set specificato, utilizzando, facoltativamente, un modello per il nome del membro padre nel set di celle risultante.|  
|[WTD &#40;&#41;MDX](../mdx/wtd-mdx.md)|Restituisce un set di membri di pari livello dallo stesso livello di un membro dato, iniziando dal primo membro di pari livello e terminando con il membro dato, in base al vincolo imposto dal livello Settimana della dimensione temporale.|  
|[YTD &#40;&#41;MDX](../mdx/ytd-mdx.md)|Restituisce un set di membri di pari livello dallo stesso livello di un membro specificato, a partire dal primo elemento di pari livello e terminando con il membro dato, in base a quanto vincolato dal livello *anno* nella dimensione temporale.|  
  
## <a name="string-functions"></a>Funzioni di stringa  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[CalculationPassValue &#40;&#41;MDX](../mdx/calculationpassvalue-mdx.md)|Restituisce il valore di un'espressione MDX valutata sulla sessione di calcolo specificata di un cubo.|  
|[CoalesceEmpty &#40;&#41;MDX](../mdx/coalesceempty-mdx.md)|Assegna un numero o una stringa a un valore di cella vuota e restituisce il valore assegnato.|  
|[Genera &#40;&#41;MDX](../mdx/generate-mdx.md)|Applica un set a ogni membro di un altro set e unisce i set risultanti tramite un join di unione. In alternativa, questa funzione restituisce una stringa concatenata creata valutando un'espressione stringa su un set.|  
|[IIf &#40;MDX&#41;](../mdx/iif-mdx.md)|Restituisce uno dei due valori determinati da un test logico.|  
|[LookupCube &#40;&#41;MDX](../mdx/lookupcube-mdx.md)|Restituisce il valore di un'espressione MDX valutata su un altro cubo specificato nello stesso database.|  
|[MemberToStr &#40;&#41;MDX](../mdx/membertostr-mdx.md)|Restituisce una stringa in formato MDX corrispondente a un membro specificato.|  
|[Nome &#40;&#41;MDX](../mdx/name-mdx.md)|Restituisce il nome di una dimensione, una gerarchia, un livello o un membro.|  
|[Proprietà &#40;&#41;MDX](../mdx/properties-mdx.md)|Restituisce una stringa o un valore fortemente tipizzato contenente il valore delle proprietà di un membro.|  
|[SetToStr &#40;&#41;MDX](../mdx/settostr-mdx.md)|Restituisce una stringa in formato MDX corrispondente al set specificato.|  
|[TupleToStr &#40;&#41;MDX](../mdx/tupletostr-mdx.md)|Restituisce una stringa in formato MDX che corrisponde alla tupla specificata.|  
|[UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)|Restituisce il nome univoco del livello, della dimensione, del membro o della gerarchia specificata.|  
|[Nome utente &#40;&#41;MDX](../mdx/username-mdx.md)|Restituisce il nome utente e di dominio della connessione corrente.|  
  
## <a name="subcube-functions"></a>Funzioni di sottocubo  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[Questo &#40;&#41;MDX](../mdx/this-mdx.md)|Restituisce il sottocubo corrente.|  
|[Lascia &#40;&#41;MDX](../mdx/leaves-mdx.md)|Restituisce il set di membri foglia nella dimensione, nel membro o nella tupla specificata.|  
  
## <a name="tuple-functions"></a>funzioni di tupla  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[&#41;MDX &#40;corrente](../mdx/current-mdx.md)|Restituisce la tupla corrente da un set durante l'iterazione.|  
|[Elemento &#40;tupla&#41; &#40;MDX&#41;](../mdx/item-tuple-mdx.md)|Restituisce una tupla da un set.|  
|[&#41;MDX radice &#40;](../mdx/root-mdx.md)|Restituisce una tupla costituita da **tutti** i membri di ogni gerarchia dell'attributo in un cubo, una dimensione o una tupla.|  
|[StrToTuple &#40;&#41;MDX](../mdx/strtotuple-mdx.md)|Restituisce la tupla specificata da una stringa in formato MDX.|  
  
## <a name="other-functions"></a>Altre funzioni  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[Errore &#40;&#41;MDX](../mdx/error-mdx.md)|Genera un errore, visualizzando facoltativamente il messaggio di errore specificato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento al linguaggio MDX &#40;&#41;MDX](../mdx/mdx-language-reference-mdx.md)  
  
  
