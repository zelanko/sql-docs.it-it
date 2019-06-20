---
title: Il drill-Through nei dati del Case da un modello di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- drillthrough [Analysis Services]
ms.assetid: b4d3f350-e543-4ea9-b3a2-b4f7c0a9ae27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d683c9dc9a201b1f4351ee00d718ad0d7917606
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084605"
---
# <a name="drill-through-to-case-data-from-a-mining-model"></a>Eseguire il drill-through sui dati del case da un modello di data mining
  Se il modello di data mining è stato configurato per consentire il drill-through sui case del modello, quando si esplora il modello è possibile recuperare informazioni dettagliate sui case utilizzati per creare il modello. Inoltre, se la struttura di data mining sottostante è stata configurata per consentire il drill-through sui case della struttura e si dispone delle autorizzazioni appropriate, è possibile restituire informazioni sulla struttura di data mining. Possono anche essere incluse colonne non incluse nel modello di data mining.  
  
 Se la struttura di data mining non consente il drill-through sui dati sottostanti, mentre il modello di data mining lo consente, è possibile visualizzare le informazioni dai case del modello ma non dalla struttura di data mining.  
  
> [!NOTE]  
>  È possibile aggiungere la funzionalità di drill-through su un modello di data mining esistente impostando la proprietà `AllowDrillthrough` su `True`. Tuttavia, dopo aver attivato il drill-through, il modello deve essere rielaborato prima che sia possibile visualizzare i dati del case. Per altre informazioni, vedere [Abilitazione del drill-through per un modello di data mining](enable-drillthrough-for-a-mining-model.md).  
  
 A seconda del tipo di visualizzatore utilizzato, è possibile selezionare il nodo per il drill-through nei modi seguenti:  
  
|Nome del visualizzatore|Nome del riquadro o della scheda|Selezione nodo|  
|-----------------|----------------------|-----------------|  
|**Visualizzatore Microsoft Decision Trees**|Scheda**Albero delle decisioni**|Fare clic su un nodo dell'albero.<br /><br /> **Nota** evitare di utilizzare il drill-through su di `All` nodo, poiché potrebbe richiedere molto tempo per restituire i risultati.|  
|**Visualizzatore Microsoft Clustering**|**Diagramma dei cluster**|Fare clic su un nodo del cluster.|  
|**Visualizzatore Microsoft Clustering**|**Profili cluster**|Fare clic in un punto qualsiasi della colonna del cluster.|  
|**Visualizzatore Microsoft Association**|Scheda**Regole**|Fare clic su una riga che contiene un set di regole.|  
|**Visualizzatore Microsoft Association**|Scheda**Set di elementi**|Fare clic su una riga che contiene un set di elementi.|  
|**Visualizzatore Microsoft Sequence Clustering**|Scheda**Regole**|Fare clic su una riga che contiene un set di regole.|  
|**Visualizzatore Microsoft Sequence Clustering**|Scheda**Set di elementi**|Fare clic su una riga che contiene un set di elementi.|  
  
> [!NOTE]  
>  Con alcuni modelli non è consentito l'utilizzo del drill-through. La possibilità di eseguire il drill-through dipende dall'algoritmo utilizzato per creare il modello: Per un elenco dei tipi di modelli di data mining che supportano il drill-through, vedere [Drillthrough Queries &#40;Data Mining&#41;](drillthrough-queries-data-mining.md).  
  
### <a name="to-view-drillthrough-data-from-a-mining-model"></a>Per visualizzare i dati del drill-through da un modello di data mining  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire la struttura di data mining che contiene il modello di data mining desiderato.  
  
2.  In Progettazione modelli di data mining fare clic sulla scheda **Visualizzatore modello di data mining** .  
  
3.  Selezionare il modello dall'elenco a discesa **Modello di data mining** .  
  
4.  Selezionare un visualizzatore nell'elenco a discesa **Visualizzatore** e fare clic con il pulsante destro del mouse sul nodo specifico.  
  
5.  Selezionare **Drill-through**, quindi selezionare **Solo colonne modello**o **Colonne struttura e modello** per aprire la finestra **Drill-through** .  
  
6.  Per copiare i dati negli Appunti, fare clic con il pulsante destro del mouse su qualsiasi riga nella tabella e selezionare **Copia tutto**.  
  
## <a name="see-also"></a>Vedere anche  
 [Query drill-through &#40;Data Mining&#41;](drillthrough-queries-data-mining.md)  
  
  
