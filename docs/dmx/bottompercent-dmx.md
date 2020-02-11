---
title: BottomPercent (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9d8b1665c6e6978af7dc673f7dd51a363da5c48d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892874"
---
# <a name="bottompercent-dmx"></a>BottomPercent (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce, in ordine di rango crescente, le ultime righe di una tabella il cui totale cumulativo corrisponde almeno a una percentuale specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BottomPercent(<table expression>, <rank expression>, <percent>)  
```  
  
## <a name="arguments"></a>Argomenti  
 *\<Espressione di tabella>*  
 Nome di una colonna della tabella nidificata o espressione valutata a livello di tabella.  
  
 *\<espressione di rango>*  
 Colonna della tabella nidificata o espressione che restituisce una colonna.  
  
 *\<percentuale>*  
 Valore Double che indica la percentuale di destinazione totale.  
  
## <a name="result-type"></a>Tipo di risultato  
 Tabella.  
  
## <a name="remarks"></a>Osservazioni  
 La funzione **BottomPercent** restituisce le righe più in basso in ordine crescente di rango. Il rango è basato sul valore valutato dell'espressione di \<rango> argomento per ogni riga, in modo che la somma dei valori \<dell'espressione di rango> sia uguale almeno alla percentuale specificata dall' \<argomento percentuale>. **BottomPercent** restituisce il più piccolo numero di elementi possibile mentre soddisfa ancora il valore percentuale specificato.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creata una query di stima sul modello di associazione compilato nell'esercitazione di [base sul data mining](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
 Per comprendere il funzionamento di BottomPercent, può essere utile eseguire prima una query di stima che restituisca solo la tabella nidificata.  
  
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
  
 La funzione BottomPercent accetta i risultati di questa query e restituisce le righe con valori più piccoli che si sommano alla percentuale specificata.  
  
```  
SELECT   
BottomPercent  
    (  
    Predict ([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,10),  
    $SUPPORT,  
    50)  
FROM   
     [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Women''s Mountain Shorts' as [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 Il primo argomento della funzione BottomPercent è il nome di una colonna di tabella. In questo esempio, la tabella nidificata viene restituita chiamando la funzione Predict e usando l'argomento INCLUDE_STATISTICS.  
  
 Il secondo argomento della funzione BottomPercent è la colonna nella tabella nidificata utilizzata per ordinare i risultati. In questo esempio l'opzione INCLUDE_STATISTICS restituisce le colonne $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. In questo esempio viene utilizzato $SUPPORT poiché i valori di supporto non sono frazionari e pertanto sono più facili da verificare.  
  
 Il terzo argomento della funzione BottomPercent specifica la percentuale come valore Double. Per ottenere le righe che rappresentano il 50 percento del supporto con i valori più bassi, digitare 50.  
  
 Risultati dell'esempio:  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Road Bottle Cage|1195|0,080314537|0,077173962|  
|Mountain Bottle Cage|1367|0,091874454|0,087780332|  
|Fender Set - Mountain|1415|0,095100477|0,090718432|  
|Cycling Cap|1473|0,098998589|0,094256014|  
|Road Tire Tube|1588|0,106727603|0,101229538|  
|Mountain-200|1755|0,117951475|0,111260823|  
|Mountain Tire Tube|1992|0,133879965|0,125304948|  
  
 **Nota** Questo esempio viene fornito solo per illustrare l'uso di BottomPercent. A seconda della dimensione del set di dati, questa query potrebbe impiegare molto tempo per l'esecuzione.  
  
> [!WARNING]  
>  Le funzioni MDX per TOPPERCENT e BOTTOMPERCENT possono generare risultati imprevisti quando i valori utilizzati per calcolare la percentuale includono numeri negativi. Questo comportamento non influisce sulle funzioni DMX. Per ulteriori informazioni, vedere [BottomPercent &#40;&#41;MDX ](../mdx/bottompercent-mdx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)  
  
  
