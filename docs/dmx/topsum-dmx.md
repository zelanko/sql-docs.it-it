---
title: TopSum (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 373fe2f1458b30412f4ee5852baa57b930af4878
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68893038"
---
# <a name="topsum-dmx"></a>TopSum (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce, in ordine di rango decrescente, le prime righe di una tabella il cui totale cumulativo corrisponde almeno a un valore specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
TopSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Espressione che restituisce una tabella, ad esempio un riferimento \<a una colonna di tabella>, o una funzione che restituisce una tabella.  
  
## <a name="return-type"></a>Tipo restituito  
 \<espressione di tabella>  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **TopSum** restituisce le righe più in alto in ordine di rango decrescente in base al valore valutato dell'espressione \<di rango> argomento per ogni riga, in modo che la somma dell' \<espressione di rango> valori sia almeno il totale specificato dall'argomento \<Sum>. **TopSum** restituisce il più piccolo numero di elementi possibile mentre soddisfa ancora il valore della somma specificato.  
  
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
  
 La funzione **TopSum** accetta i risultati di questa query e restituisce le righe con i valori massimi che sommano al conteggio specificato.  
  
```  
SELECT   
TopSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .5)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Il primo argomento della funzione **TopSum** è il nome di una colonna di tabella. In questo esempio, la tabella nidificata viene restituita chiamando la funzione Predict e usando l'argomento INCLUDE_STATISTICS.  
  
 Il secondo argomento della funzione **TopSum** è la colonna nella tabella nidificata utilizzata per ordinare i risultati. In questo esempio l'opzione INCLUDE_STATISTICS restituisce le colonne $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. Viene utilizzato $ PROBABILITY per restituire le righe che rappresentano almeno la probabilità del 50%.  
  
 Il terzo argomento della funzione **TopSum** specifica la somma di destinazione, come valore Double. Per ottenere le righe dei primi prodotti che rappresentano il 50 percento di probabilità, digitare .5.  
  
 Risultati dell'esempio:  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,29...|0,25...|  
|Water Bottle|2866|0,19...|0,17...|  
|Patch kit|2113|0,14...|0,13...|  
  
 **Nota** Questo esempio viene fornito solo per illustrare l'utilizzo di **TopSum**. A seconda della dimensione del set di dati, questa query potrebbe impiegare molto tempo per l'esecuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Percentuale &#40;DMX&#41;](../dmx/toppercent-dmx.md)  
  
  
