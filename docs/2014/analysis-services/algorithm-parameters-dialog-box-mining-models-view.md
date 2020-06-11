---
title: Finestra di dialogo parametri algoritmo (visualizzazione modelli di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.models.algorithmparameters.f1
helpviewer_keywords:
- Algorithm Parameters dialog box
ms.assetid: 57f9f6f8-8ca4-4a6e-8f18-85f0571b7060
author: minewiskan
ms.author: owend
ms.openlocfilehash: b942210e653bc3e0a7309a98a4e75e84c5f82168
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528137"
---
# <a name="algorithm-parameters-dialog-box-mining-models-view"></a>Finestra di dialogo Parametri algoritmo (visualizzazione Modelli di data mining)
  Usare la finestra di dialogo **Parametri algoritmo** per modificare i parametri dell'algoritmo specifici per il modello selezionato. Quando si modifica un parametro dell'algoritmo, i risultati del modello di data mining di solito cambiano. L'influenza che ogni parametro ha sui risultati dipende dall'algoritmo utilizzato e dai dati. Per altre informazioni, vedere [Personalizzare struttura e modelli di data mining](data-mining/customize-mining-models-and-structure.md).  
  
## <a name="options"></a>Opzioni  
 **Parameters**  
 Consente di visualizzare l'elenco dei parametri disponibili per il modello di data mining selezionato.  
  
 Di seguito vengono descritte le colonne disponibili.  
  
|Colonna|Descrizione|  
|------------|-----------------|  
|**Parametro**|Indica il nome del parametro.|  
|**Valore**|Immettere un valore solo se si desidera modificare quello predefinito del parametro.|  
|**Default**|Indica il valore predefinito del parametro usato dall'algoritmo se non si specifica un valore nella colonna **Valore** .|  
|**Range**|Indica l'intervallo di valori che è possibile immettere nella colonna **Valore** . Gli intervalli possono essere uno dei seguenti:<br /><br /> Elenco discreto, ad esempio 1, 2, 3<br /><br /> Un intervallo inclusivo, ad esempio [0, 100]<br /><br /> Intervallo esclusivo, ad esempio (0,...)<br /><br /> Combinazione, ad esempio [0,...)|  
  
 **Descrizione**  
 Descrive il parametro selezionato nell'elenco **Parametri** .  
  
 **Aggiungere**  
 Consente di aggiungere all'elenco ulteriori parametri specifici per l'algoritmo. Dopo l'aggiunta del parametro, è possibile immetterne il nome corretto nella colonna **Parametro** e specificare un valore nella colonna **Valore** .  
  
 **Rimuovi**  
 Consente di eliminare un parametro personalizzato dall'elenco.  
  
 Se si elimina dall'elenco uno dei parametri dell'algoritmo standard di Analysis Services, il parametro verrà ancora utilizzato nel modello, ma con i valori predefiniti per quel parametro. Il parametro non è eliminato in modo permanente e verrà visualizzato la volta successiva che si apre la finestra di dialogo.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services-&#41;di data mining](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzazione modelli di data mining &#40;Progettazione modelli di data mining&#41;](mining-models-view-data-mining-model-designer.md)   
 [Spostamento di oggetti di data mining](data-mining/moving-data-mining-objects.md)  
  
  
