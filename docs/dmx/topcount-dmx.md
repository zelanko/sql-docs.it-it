---
title: Conteggio (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f93df1c1388f6a85272ced6bf419140c74105ddc
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669957"
---
# <a name="topcount-dmx"></a>TopCount (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce il numero specificato di righe a partire dall'alto, in ordine di rango decrescente secondo quanto specificato da una determinata espressione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
TopCount(<table expression>, <rank expression>, <count>)  
```  
  
## <a name="applies-to"></a>Si applica a  
 Espressione che restituisce una tabella, ad esempio un riferimento a una \< colonna di tabella>, o una funzione che restituisce una tabella.  
  
## <a name="return-type"></a>Tipo restituito  
 \<espressione di tabella>  
  
## <a name="remarks"></a>Commenti  
 Il valore fornito dall' \< espressione di rango> argomento determina l'ordine di rango decrescente per le righe fornite nell' \< espressione di tabella> argomento e viene restituito il numero di righe in primo piano specificate nell' \< argomento count>.  
  
 La funzione tocount è stata introdotta originariamente per consentire le stime associative e in generale produce gli stessi risultati di un'istruzione che include le clausole **Select Top** e **Order by** . È possibile ottenere prestazioni migliori per le stime associative se si utilizza la funzione **Predict (DMX)** , che supporta la specifica di un numero di stime da restituire.  
  
 Tuttavia, esistono situazioni in cui potrebbe essere ancora necessario utilizzare il conteggio dei conteggi. DMX, ad esempio, non supporta il qualificatore **Top** in un'istruzione sub-SELECT. La funzione [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) non supporta inoltre l'aggiunta di **Top**.  
  
## <a name="examples"></a>Esempio  
 Gli esempi seguenti sono query di stima sul modello di associazione compilato mediante l' [esercitazione di base sul data mining](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). Le query restituiscono gli stessi risultati, ma nel primo esempio viene utilizzato il conteggio delle corrispondenze e il secondo esempio utilizza la funzione Predict.  
  
 Per comprendere il funzionamento del conteggio dei conteggi, può essere utile eseguire prima una query di stima che restituisca solo la tabella nidificata.  
  
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
  
 La funzione tocount accetta i risultati di questa query e restituisce il numero specificato di righe con valori più piccoli.  
  
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
  
 Il primo argomento della funzione tocount è il nome di una colonna di tabella. In questo esempio, la tabella nidificata viene restituita chiamando la funzione Predict e usando l'argomento INCLUDE_STATISTICS.  
  
 Il secondo argomento della funzione tocount è la colonna della tabella nidificata utilizzata per ordinare i risultati. In questo esempio l'opzione INCLUDE_STATISTICS restituisce le colonne $SUPPORT, $PROBABILTY e $ADJUSTED PROBABILITY. In questo esempio viene utilizzato $ SUPPORT per classificare i risultati.  
  
 Il terzo argomento della funzione tocount specifica il numero di righe da restituire come valore integer. Per ottenere i primi tre prodotti, come ordinato da $SUPPORT, digitare 3.  
  
 Risultati dell'esempio:  
  
|Modello|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,29...|0,25...|  
|Water Bottle|2866|0,19...|0,17...|  
|Patch kit|2113|0,14...|0,13...|  
  
 Tuttavia, questo tipo di query può influire sulle prestazioni nell'impostazione di un ambiente di produzione perché restituisce un set di tutte le stime dall'algoritmo, ordina queste stime e restituisce le prime tre.  
  
 Nell'esempio seguente viene fornita un'istruzione alternativa che restituisce gli stessi risultati ma in modo significativamente più veloce. In questo esempio viene sostituito il conteggio delle stime con la funzione Predict, che accetta un certo numero di stime come argomento. In questo esempio viene inoltre utilizzata la parola chiave **$support** per recuperare direttamente la colonna della tabella nidificata.  
  
```  
SELECT Predict ([Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3, $SUPPORT)  
```  
  
 I risultati contengono le prime tre stime ordinate in base al valore di supporto. È possibile sostituire $SUPPORT con $PROBABILITY o $ADJUSTED_PROBABILITY per restituire stime classificate in base alla probabilità o alla probabilità adattata. Per ulteriori informazioni, vedere **Predict (DMX)**.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)   
 [Percentuale &#40;DMX&#41;](../dmx/toppercent-dmx.md)   
 [&#40;DMX&#41;](../dmx/topsum-dmx.md)  
  
  
