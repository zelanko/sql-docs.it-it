---
title: DELETE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ce350c4d99fec986d8df06c364e6f6adac94324
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969872"
---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Cancella un modello di data mining, una struttura di data mining o una struttura di data mining e tutti i modelli di data mining associati, a seconda delle clausole DMX (Data Mining Extensions) utilizzate.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>Argomenti  
 *model*  
 Identificatore del modello.  
  
 *struttura*  
 Identificatore della struttura.  
  
## <a name="remarks"></a>Osservazioni  
 Se non si specifica un **modello di data mining** o una **struttura di data mining**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cerca il tipo di oggetto in base al nome ed elabora l'oggetto corretto. Se il server contiene una struttura di data mining e un modello di data mining con lo stesso nome, verrà restituito un errore.  
  
 Nella tabella seguente sono descritti i risultati ottenuti utilizzando le diverse forme della sintassi.  
  
|.|Risultato|  
|---------------|------------|  
|ELIMINA DALLA STRUTTURA DI DATA MINING*\<structure>*<br /><br /> oppure<br /><br /> Elimina dalla struttura di data MINING *\<structure>* . CONTENUTO|Esegue ProcessClear sulla struttura di data mining. Viene cancellato tutto il contenuto della struttura di data mining e dei modelli di data mining associati.|  
|Elimina dalla struttura di data MINING *\<structure>* . CASI|Esegue ProcessClearStructureOnly sulla struttura di data mining. Viene cancellato tutto il contenuto della struttura di data mining, lasciando invariati i modelli di data mining associati. Dopo la cancellazione della struttura di data mining non è possibile eseguire il drill-through sui modelli di data mining associati.|  
|ELIMINA DAL MODELLO DI DATA MINING*\<model>*<br /><br /> oppure<br /><br /> Elimina dal modello di data MINING *\<model>* . CONTENUTO|Esegue ProcessClear sul modello di data mining, ma lascia inalterati i valori di stato. I valori di stato sono i possibili stati di una colonna. Per la colonna del genere, ad esempio, i valori di stato sono maschio e femmina.|  
  
 Per ulteriori informazioni sui tipi di elaborazione, vedere [elemento Type &#40;&#41;XMLA ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/type-element-xmla).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene rimosso tutto il contenuto dal modello NB_Sample.  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di definizione dei dati](../dmx/dmx-statements-data-definition.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
