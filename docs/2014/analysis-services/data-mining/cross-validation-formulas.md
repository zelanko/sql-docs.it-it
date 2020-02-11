---
title: Formule per la convalida incrociata | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fd1ea582-29a1-4154-8de2-47bab3539b4d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ccdf0285dc110cde89e08778f6badf56f586a5ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085152"
---
# <a name="cross-validation-formulas"></a>Formule per la convalida incrociata
  Quando viene generato, un report di convalida incrociata contiene misure di accuratezza per ogni modello, a seconda del tipo di modello di data mining (ovvero dell'algoritmo utilizzato per creare il modello), del tipo di dati dell'attributo stimabile e del valore dell'attributo stimabile, se presente.  
  
 In questa sezione vengono elencate le misure utilizzate nel report di convalida incrociata e viene descritto il metodo di calcolo.  
  
 Per un elenco delle misure di accuratezza in base al tipo di modello, vedere [Misure nel report di convalida incrociata](measures-in-the-cross-validation-report.md).  
  
## <a name="formulas-used-for-cross-validation-measures"></a>Formule utilizzate per le misure di convalida incrociata  
  
> [!NOTE]  
>  **Importante:** Queste misure di accuratezza vengono calcolate per ogni attributo di destinazione. Per ogni attributo è possibile specificare o omettere un valore di destinazione. Se un case nel set di dati non dispone di alcun valore per l'attributo di destinazione, il case viene trattato come se avesse un valore speciale denominato *valore mancante*. Le righe associate a valori mancanti non vengono conteggiate durante il calcolo della misura di accuratezza per un attributo di destinazione specifico. Si noti che poiché i punteggi vengono calcolati singolarmente per ogni attributo, se i valori sono presenti per l'attributo di destinazione, ma mancanti per altri attributi, questa situazione non influisce sul punteggio per l'attributo di destinazione.  
  
|Measure|Si applica a|Implementazione|  
|-------------|----------------|--------------------|  
|**Vero positivo**|Attributo discreto, il valore viene specificato|Numero di case che soddisfano le condizioni seguenti:<br /><br /> Il case contiene il valore di destinazione.<br /><br /> Tramite il modello è stato stimato che il case contiene il valore di destinazione.|  
|**Vero negativo**|Attributo discreto, il valore viene specificato|Numero di case che soddisfano le condizioni seguenti:<br /><br /> Il case non contiene il valore di destinazione.<br /><br /> Tramite il modello è stato stimato che il case non contiene il valore di destinazione.|  
|**Falso positivo**|Attributo discreto, il valore viene specificato|Numero di case che soddisfano le condizioni seguenti:<br /><br /> Il valore effettivo è uguale a quello di destinazione.<br /><br /> Tramite il modello è stato stimato che il case contiene il valore di destinazione.|  
|**Falso negativo**|Attributo discreto, il valore viene specificato|Numero di case che soddisfano le condizioni seguenti:<br /><br /> Il valore effettivo non è uguale a quello di destinazione.<br /><br /> Tramite il modello è stato stimato che il case non contiene il valore di destinazione.|  
|**Superato/non superato**|Attributo discreto, nessuna destinazione specificata|Numero di case che soddisfano le condizioni seguenti:<br /><br /> Il test viene superato se lo stato stimato con la probabilità più elevata corrisponde allo stato di input e la probabilità è maggiore del valore della soglia di stato. ****<br /><br /> In caso contrario il test non viene superato.|  
|**Accuratezza**|Attributo discreto. Il valore di destinazione può essere specificato ma non è obbligatorio.|Probabilità in forma logaritmica media per tutte le righe con valori per l'attributo di destinazione in cui la probabilità in forma logaritmica per ogni case viene calcolata come Log(ActualProbability/MarginalProbability). Per calcolare la media, la somma dei valori di probabilità in forma logaritmica viene divisa per il numero di righe nel set di dati di input, escluse le righe con valori mancanti per l'attributo di destinazione.<br /><br /> Il valore dell'accuratezza può essere positivo o negativo. Un valore positivo indica un modello efficace con prestazioni migliori rispetto all'ipotesi casuale.|  
|**Punteggio di log**|Attributo discreto. Il valore di destinazione può essere specificato ma non è obbligatorio.|Logaritmo della probabilità effettiva per ciascun case, sommato e quindi diviso per il numero di righe nel set di dati di input, escluse le righe con valori mancanti per l'attributo di destinazione.<br /><br /> Poiché la probabilità è rappresentata come frazione decimale, i punteggi in forma logaritmica sono sempre numeri negativi. Un punteggio più vicino a 0 corrisponde a un punteggio migliore.|  
|**Probabilità del case**|Cluster|Somma dei punteggi di probabilità del cluster per tutti i case, divisa per il numero di case nella partizione, escluse le righe con valori mancanti per l'attributo di destinazione.|  
|**Errore assoluto medio**|Attributo continuo|Somma dell'errore assoluto per tutti i case della partizione, divisa per il numero di case nella partizione.|  
|**Radice errore quadratico medio**|Attributo continuo|Radice quadrata dell'errore quadratico medio della partizione.|  
|**Radice errore quadratico medio**|Attributo discreto. Il valore di destinazione può essere specificato ma non è obbligatorio.|Radice quadrata della media dei quadrati di complemento del punteggio di probabilità, divisa per il numero di case nella partizione, escluse le righe con valori mancanti per l'attributo di destinazione.|  
|**Radice errore quadratico medio**|Attributo discreto, nessuna destinazione specificata.|Radice quadrata della media dei quadrati di complemento del punteggio di probabilità, divisa per il numero di case nella partizione, esclusi i case con valori mancanti per l'attributo di destinazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Test e convalida &#40;&#41;di data mining](testing-and-validation-data-mining.md)   
 [Convalida incrociata &#40;Analysis Services-&#41;di data mining](cross-validation-analysis-services-data-mining.md)  
  
  
