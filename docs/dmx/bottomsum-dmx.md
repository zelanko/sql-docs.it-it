---
title: BottomSum (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 51ebd164ae5c184177367f59b5643712b14718a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071129"
---
# <a name="bottomsum-dmx"></a>BottomSum (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce, in ordine di rango crescente, le ultime righe di una tabella il cui totale cumulativo corrisponde almeno a un valore specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BottomSum(<table expression>, <rank expression>, <sum>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Un'espressione che restituisce una tabella, ad esempio un \<riferimento a una colonna di tabella >, o una funzione che restituisce una tabella.  
  
## <a name="return-type"></a>Tipo restituito  
 \<espressione di tabella >  
  
## <a name="remarks"></a>Note  
 Il **BottomSum** funzione restituisce le righe più in basso nell'ordine di rango crescente. Il rango è basato sul valore valutato del \<rank expression > argomento per ogni riga, in modo che la somma del \<rank expression > valori corrisponde almeno al totale specificato dalla \<somma > argomento. **BottomSum** restituisce il più piccolo numero di elementi possibile mentre soddisfa ancora il valore totale specificato.  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente crea una query di stima sul modello di associazione che si compila usando il [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Per comprendere il funzionamento BottomSum, potrebbe essere utile eseguire prima una query di stima che restituisce solo la tabella nidificata.  
  
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
  
 La funzione BottomSum utilizza i risultati della query e restituisce le righe con i valori più bassi che vengono sommate al numero specificato.  
  
```  
SELECT   
BottomSum  
    (  
    Predict([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $PROBABILITY,  
    .1)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Il primo argomento alla funzione BottomSum è il nome di una colonna di tabella. In questo esempio, la tabella nidificata viene restituita chiamando la funzione Predict e usando l'argomento INCLUDE_STATISTICS.  
  
 Il secondo argomento alla funzione BottomSum è la colonna nella tabella annidata che consente di ordinare i risultati. In questo esempio l'opzione INCLUDE_STATISTICS restituisce le colonne $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. Viene utilizzato $ PROBABILITY per restituire le righe che rappresentano almeno la probabilità del 50%.  
  
 Il terzo argomento alla funzione BottomSum specifica la somma di destinazione, come valore double. Per ottenere le righe degli ultimi prodotti che rappresentano il 10 percento di probabilità, digitare .1.  
  
 Risultati dell'esempio:  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0,08...|0,07...|  
|Mountain Bottle Cage|1367|0.09...|0,08...|  
  
 **Nota** in questo esempio è fornito solo per illustrare l'utilizzo di BottomSum. A seconda della dimensione del set di dati, questa query potrebbe impiegare molto tempo per l'esecuzione.  
  
## <a name="see-also"></a>Vedere anche  
 [Le funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)  
  
  
