---
title: Consente di selezionare una &lt; struttura &gt; . CASI | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2e0fc30945396f22184e1d18c6b132d8e2e2d781
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970437"
---
# <a name="select-from-ltstructuregtcases"></a>Consente di selezionare una &lt; struttura &gt; . CASI
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Restituisce i case utilizzati per creare la struttura di data mining.  
  
 Se nella struttura non è attivato il drill-through, l'istruzione non riesce. Inoltre, l'istruzione non riuscirà se l'utente non dispone di autorizzazioni drill-through sulla struttura di data mining.  
  
 In [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] il drill-through sulle nuove strutture di data mining è abilitato per impostazione predefinita. Per verificare se il drill-through è abilitato per una determinata struttura, controllare se il valore della proprietà **CacheMode** è impostato su **KeepTrainingCases**.  
  
 Se il valore di **CacheMode** viene modificato in **ClearAfterProcessing**, i case della struttura vengono cancellati dalla cache e non è possibile utilizzare il drill-through.  
  
> [!NOTE]  
>  Non è possibile attivare o disabilitare il drill-through sulla struttura di data mining mediante DMX (Data Mining Extensions).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT [TOP n] <expression list> FROM <structure>.CASES  
[WHERE <condition expression>][ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *n*  
 Facoltativa. Valore intero mediante il quale viene specificato il numero di righe da restituire.  
  
 *elenco di espressioni*  
 Elenco di espressioni separate da virgola.  
  
 Un'espressione può includere identificatori di colonna, funzioni definite dall'utente e funzioni VBA.  
  
 *struttura*  
 Nome della struttura.  
  
 *espressione della condizione*  
 Condizione per limitare i valori restituiti dall'elenco di colonne.  
  
 *expression*  
 Facoltativa. Espressione che restituisce un valore scalare.  
  
## <a name="remarks"></a>Osservazioni  
 Se il drill-through è attivato sia nella struttura che nel modello, qualsiasi membro di un ruolo che dispone di autorizzazioni drill-through per il modello di data mining e per la struttura di data mining può restituire le colonne della struttura non incluse nel modello utilizzando la sintassi seguente:  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 Pertanto, per proteggere dati sensibili o informazioni personali, è necessario costruire la vista origine dati in modo da mascherare le informazioni personali e concedere l'autorizzazione **AllowDrillThrough** per una struttura di data mining o un modello di data mining solo quando necessario.  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti si basano sulla struttura di data mining, Targeted mailing, basata sul [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] database e sui modelli di data mining associati. Per ulteriori informazioni, vedere [esercitazione di base sul data mining](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
### <a name="example-1-drill-through-to-structure-cases"></a>Esempio 1: Esecuzione del drill-through nei case della struttura  
 Nell'esempio seguente viene restituito l'elenco dei 500 clienti meno recenti nella struttura di data mining, Targeted Mailing. La query restituisce tutte le colonne nel modello di data mining, ma limita le righe ai clienti che hanno acquistato una bicicletta e li ordina per età. È anche possibile modificare l'elenco di espressioni per specificare le colonne da restituire.  
  
```  
SELECT TOP 500 *  
FROM [Targeted Mailing].Cases  
WHERE [Bike Buyer] = 1  
ORDER BY Age DESC;  
```  
  
### <a name="example-2-drillthrough-to-test-or-training-cases-only"></a>Esempio 2: Esecuzione del drill-through solo in case di test o training  
 Nell'esempio seguente viene restituito l'elenco dei case della struttura per Targeted Mailing riservato per l'esecuzione di test. Se la struttura di data mining non contiene un set di test di controllo, per impostazione predefinita tutti i case sono trattati come case di training e la query restituisce 0 case.  
  
```  
SELECT [Customer Key], Gender, Age  
FROM [Targeted Mailing].Cases  
WHERE IsTestCase();  
```  
  
 Per la restituzione dei case di training, sostituire la funzione `IsTrainingCase()`.  
  
## <a name="see-also"></a>Vedere anche  
 [SELEZIONARE &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
