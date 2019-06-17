---
title: Esiste (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 99f6db275fcddaff3e739311ed588fb0ec776aaf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62506095"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce **true** se la sottoquery specificata restituisce almeno una riga.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>Argomenti  
 *subquery*  
 Un'istruzione SELECT del form SELECT * FROM \<nome colonna > [dove \<elenco predicati >].  
  
## <a name="result-type"></a>Tipo di risultato  
 Restituisce **true** se il set di risultati restituito dalla sottoquery contiene almeno una riga; in caso contrario, restituisce **false**.  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare la parola chiave NOT prima di EXISTS: ad esempio, `WHERE NOT EXISTS (<subquery>)`.  
  
 L'elenco di colonne aggiunte all'argomento della sottoquery di EXISTS è irrilevante. Viene solo verificata l'esistenza di una riga che soddisfa la condizione.  
  
## <a name="examples"></a>Esempi  
 È possibile utilizzare EXISTS e NOT EXISTS per verificare le condizioni in una tabella nidificata. Ciò è utile durante la creazione di un filtro che controlla i dati utilizzati per eseguire il training o il testing di un modello di data mining. Per altre informazioni, vedere [Filtri per i modelli di data mining &#40;Analysis Services - Data mining&#41;](../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md).  
  
 Nell'esempio seguente si basa sul `[Association]` struttura di data mining e modello di data mining che è stato creato nel [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). La query restituisce solo i casi in cui il cliente ha acquistato almeno un Patch kit.  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 Un altro modo per visualizzare gli stessi dati che viene restituiti da questa query è possibile accedere il modello nel visualizzatore associazioni, fare doppio clic su set di elementi **Patch kit = Existing**, selezionare la **drill-Through** opzione e quindi Selezionare **solo case del modello**.  
  
## <a name="see-also"></a>Vedere anche  
 [Functions &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Esempi e sintassi del filtro del modello &#40;Analysis Services - Data Mining&#41;](../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)  
  
  
