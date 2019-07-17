---
title: TopCount (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 48621e242fae86b0b9fca689149ed1364cb7ff1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079842"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce il numero specificato di righe a partire dall'alto, in ordine di rango decrescente secondo quanto specificato da una determinata espressione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Un'espressione che restituisce una tabella, ad esempio un \<riferimento a una colonna di tabella >, o una funzione che restituisce una tabella.  
  
## <a name="return-type"></a>Tipo restituito  
 \<espressione di tabella >  
  
## <a name="remarks"></a>Note  
 Il valore fornito dal \<rank expression > argomento determina l'ordine di rango decrescente per le righe che vengono forniti nel \<espressione di tabella > argomento e il numero di righe di livello superiore specificato nella \<conteggio > viene restituito l'argomento.  
  
 La funzione TopCount è stata introdotta originalmente per consentire le stime associative e in generale, produce gli stessi risultati di un'istruzione che include **seleziona le prime** e **ORDER BY** clausole. È possibile ottenere prestazioni migliori per le stime associative se si usa la **stima (DMX)** (funzione), che supporta la specifica di un numero di stime da restituire.  
  
 Tuttavia, esistono situazioni in cui potrebbe essere ancora necessario usare TopCount. Ad esempio, DMX non supporta il **TOP** qualificatore in un'istruzione Sub-select. Il [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) funzione inoltre non supporta l'aggiunta di **superiore**.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti costituiscono query di stima sul modello di associazione che si compila usando il [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Le query restituiscono gli stessi risultati, ma il primo esempio Usa TopCount e nel secondo esempio viene utilizzata la funzione Predict.  
  
 Per comprendere il funzionamento TopCount, potrebbe essere utile eseguire prima una query di stima che restituisce solo la tabella nidificata.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 10)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
> [!NOTE]  
>  In questo esempio il valore fornito come input contiene una virgoletta singola, e pertanto è necessario utilizzare il carattere di escape preceduto da un'altra virgoletta singola. Se non si è certi della sintassi per l'inserimento di un carattere di escape, è possibile utilizzare il generatore delle query di stima per creare la query. Quando si seleziona il valore dall'elenco a discesa, viene automaticamente inserito il carattere di escape necessario. Per altre informazioni, vedere [creare una Query Singleton in Progettazione modelli di Data Mining Data](../analysis-services/data-mining/create-a-singleton-query-in-the-data-mining-designer.md).  
  
 Risultati dell'esempio:  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283016|0.252695851|  
|Water Bottle|2866|0.192620472|0.175205052|  
|Patch kit|2113|0.142012232|0.132389356|  
|Mountain Tire Tube|1992|0.133879965|0.125304948|  
|Mountain-200|1755|0.117951475|0.111260823|  
|Road Tire Tube|1588|0.106727603|0.101229538|  
|Cycling Cap|1473|0.098998589|0.094256014|  
|Fender Set - Mountain|1415|0.095100477|0.090718432|  
|Mountain Bottle Cage|1367|0.091874454|0.087780332|  
|Road Bottle Cage|1195|0.080314537|0.077173962|  
  
 La funzione TopCount accetta i risultati della query e restituisce il numero specificato di righe con valori più piccolo.  
  
```  
SELECT   
TopCount  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    3)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Il primo argomento alla funzione TopCount è il nome di una colonna di tabella. In questo esempio, la tabella nidificata viene restituita chiamando la funzione Predict e usando l'argomento INCLUDE_STATISTICS.  
  
 Il secondo argomento alla funzione TopCount è la colonna nella tabella annidata che consente di ordinare i risultati. In questo esempio l'opzione INCLUDE_STATISTICS restituisce le colonne $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. In questo esempio viene utilizzato $ SUPPORT per classificare i risultati.  
  
 Il terzo argomento alla funzione TopCount specifica il numero di righe da restituire, come integer. Per ottenere i primi tre prodotti, come ordinato da $SUPPORT, digitare 3.  
  
 Risultati dell'esempio:  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,29...|valore di 0,25...|  
|Water Bottle|2866|0.19...|0,17...|  
|Patch kit|2113|0,14...|0.13...|  
  
 Tuttavia, questo tipo di query può influire sulle prestazioni nell'impostazione di un ambiente di produzione perché restituisce un set di tutte le stime dall'algoritmo, ordina queste stime e restituisce le prime tre.  
  
 Nell'esempio seguente viene fornita un'istruzione alternativa che restituisce gli stessi risultati ma in modo significativamente più veloce. In questo esempio sostituisce TopCount con la funzione di stima, che accetta un numero di stime come argomento. Questo esempio Usa anche il **$SUPPORT** parola chiave per recuperare direttamente la colonna della tabella nidificata.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 I risultati contengono le prime tre stime ordinate in base al valore di supporto. È possibile sostituire $SUPPORT con $PROBABILITY o $ADJUSTED_PROBABILITY per restituire stime classificate in base alla probabilità o alla probabilità adattata. Per altre informazioni, vedere **stima (DMX)** .  
  
## <a name="see-also"></a>Vedere anche  
 [Le funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)   
 [TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
