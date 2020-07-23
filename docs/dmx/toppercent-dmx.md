---
title: Percentuale (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a91941241b61f74190b9ab1ef0c29dffded5dc79
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970238"
---
# <a name="toppercent-dmx"></a>TopPercent (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  La funzione **topercent** restituisce, in ordine di rango decrescente, le prime righe di una tabella il cui totale cumulativo corrisponde almeno a una percentuale specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
TopPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Espressione che restituisce una tabella, ad esempio \<table column reference> o una funzione che restituisce una tabella.  
  
## <a name="return-type"></a>Tipo restituito  
 \<table expression>  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **topercent** restituisce le righe più in alto in ordine di rango decrescente in base al valore valutato dell' \<rank expression> argomento per ogni riga, in modo che la somma dei \<rank expression> valori corrisponde almeno alla percentuale specificata dall' \<percent> argomento. La **percentuale** di restituzione restituisce il minor numero di elementi possibile mentre soddisfa ancora il valore percentuale specificato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata una query di stima sul modello di associazione compilato mediante l'esercitazione di [base sul data mining](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Per comprendere il funzionamento della percentuale di indisponibilità, potrebbe essere utile eseguire prima una query di stima che restituisca solo la tabella nidificata.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  In questo esempio il valore fornito come input contiene una virgoletta singola, e pertanto è necessario utilizzare il carattere di escape preceduto da un'altra virgoletta singola. Se non si è certi della sintassi per l'inserimento di un carattere di escape, è possibile utilizzare il generatore delle query di stima per creare la query. Quando si seleziona il valore dall'elenco a discesa, viene automaticamente inserito il carattere di escape necessario. Per ulteriori informazioni, vedere la pagina relativa alla [creazione di una query singleton in Progettazione modelli di data mining](https://docs.microsoft.com/analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer).  
  
 Risultati dell'esempio:  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,291283016|0,252695851|  
|Water Bottle|2866|0,192620472|0,175205052|  
|Patch kit|2113|0,142012232|0,132389356|  
|Mountain Tire Tube|1992|0,133879965|0,125304948|  
|Mountain-200|1755|0,117951475|0,111260823|  
|Road Tire Tube|1588|0,106727603|0,101229538|  
|Cycling Cap|1473|0,098998589|0,094256014|  
|Fender Set - Mountain|1415|0,095100477|0,090718432|  
|Mountain Bottle Cage|1367|0,091874454|0,087780332|  
|Road Bottle Cage|1195|0,080314537|0,077173962|  
  
 La funzione per la percentuale di ingrandimento accetta i risultati di questa query e restituisce le righe con i valori più grandi che vengono sommate alla percentuale specificata.  
  
```  
SELECT   
TopPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Il primo argomento della funzione di percentuale è il nome di una colonna di tabella. In questo esempio, la tabella nidificata viene restituita chiamando la funzione Predict e usando l'argomento INCLUDE_STATISTICS.  
  
 Il secondo argomento della funzione di percentuale è la colonna della tabella nidificata utilizzata per ordinare i risultati. In questo esempio l'opzione INCLUDE_STATISTICS restituisce le colonne $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. In questo esempio viene utilizzato $SUPPORT poiché i valori di supporto non sono frazionari e pertanto sono più facili da verificare.  
  
 Il terzo argomento della funzione topercent specifica la percentuale come valore Double. Per ottenere le righe dei primi prodotti che rappresentano il 50 percento del supporto totale, digitare 50.  
  
 Risultati dell'esempio:  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,29...|0,25...|  
|Water Bottle|2866|0,19...|0,17...|  
|Patch kit|2113|0,14...|0,13...|  
|Mountain Tire Tube|1992|0,133...|0,12...|  
  
 **Nota** Questo esempio viene fornito solo per illustrare l'utilizzo del prepercentuale. A seconda della dimensione del set di dati, questa query potrebbe impiegare molto tempo per l'esecuzione.  
  
> [!WARNING]  
>  Le funzioni MDX per TOPPERCENT e BOTTOMPERCENT possono generare risultati imprevisti quando i valori utilizzati per calcolare la percentuale includono numeri negativi. Questo comportamento non influisce sulle funzioni DMX. Per ulteriori informazioni, vedere [BottomPercent &#40;&#41;MDX ](../mdx/bottompercent-mdx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
