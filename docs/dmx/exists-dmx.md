---
description: Exists (DMX)
title: Exists (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1f45a4a1d0e709c6b8eb9bb7217d268420f31d07
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726232"
---
# <a name="exists-dmx"></a>Exists (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Restituisce **true** se la sottoquery specificata restituisce almeno una riga.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
EXISTS(<subquery>)  
```  
  
## <a name="arguments"></a>Argomenti  
 *subquery*  
 Un'istruzione SELECT nel formato SELECT * FROM \<column name> [WHERE \<predicate list> ].  
  
## <a name="result-type"></a>Tipo di risultato  
 Restituisce **true** se il set di risultati restituito dalla sottoquery contiene almeno una riga. in caso contrario, restituisce **false**.  
  
## <a name="remarks"></a>Osservazioni  
 È possibile utilizzare la parola chiave NOT prima di EXISTS: ad esempio, `WHERE NOT EXISTS (<subquery>)`.  
  
 L'elenco di colonne aggiunte all'argomento della sottoquery di EXISTS è irrilevante. Viene solo verificata l'esistenza di una riga che soddisfa la condizione.  
  
## <a name="examples"></a>Esempi  
 È possibile utilizzare EXISTS e NOT EXISTS per verificare le condizioni in una tabella nidificata. Ciò è utile durante la creazione di un filtro che controlla i dati utilizzati per eseguire il training o il testing di un modello di data mining. Per altre informazioni, vedere [Filtri per i modelli di data mining &#40;Analysis Services - Data mining&#41;](/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining).  
  
 L'esempio seguente si basa sulla struttura di data mining e sul modello di data mining `[Association]` creato nell' [esercitazione di base sul data mining](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130)). La query restituisce solo i casi in cui il cliente ha acquistato almeno un Patch kit.  
  
```  
SELECT * FROM [Association].CASES  
WHERE EXISTS  
(  
SELECT * FROM [v Assoc Seq Line Numbers]  
WHERE [[Model] = 'Patch kit'  
)  
```  
  
 Un altro modo per visualizzare gli stessi dati restituiti da questa query consiste nell'aprire il modello nel Visualizzatore associazione, fare clic con il pulsante destro del mouse sul set di elementi **patch kit = esistente**, selezionare l'opzione **drill-through** , quindi selezionare **solo case del modello**.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Sintassi ed esempi di filtri dei modelli &#40;Analysis Services - Data mining&#41;](/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining)  
  
