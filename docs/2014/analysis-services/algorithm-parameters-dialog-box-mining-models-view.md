---
title: Finestra di dialogo parametri algoritmo (visualizzazione modelli di Data Mining) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c72a3c52da21ca7af10103010500bb43fd46a10a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062604"
---
# <a name="algorithm-parameters-dialog-box-mining-models-view"></a>Finestra di dialogo Parametri algoritmo (visualizzazione Modelli di data mining)
  Usare la finestra di dialogo **Parametri algoritmo** per modificare i parametri dell'algoritmo specifici per il modello selezionato. Quando si modifica un parametro dell'algoritmo, i risultati del modello di data mining di solito cambiano. L'influenza che ogni parametro ha sui risultati dipende dall'algoritmo utilizzato e dai dati. Per altre informazioni, vedere [Personalizzare struttura e modelli di data mining](data-mining/customize-mining-models-and-structure.md).  
  
## <a name="options"></a>Opzioni  
 **Parametri**  
 Consente di visualizzare l'elenco dei parametri disponibili per il modello di data mining selezionato.  
  
 Di seguito vengono descritte le colonne disponibili.  
  
|colonna|Descrizione|  
|------------|-----------------|  
|**Parametro**|Indica il nome del parametro.|  
|**Valore**|Immettere un valore solo se si desidera modificare quello predefinito del parametro.|  
|**Default**|Indica il valore predefinito del parametro usato dall'algoritmo se non si specifica un valore nella colonna **Valore** .|  
|**Intervallo**|Indica l'intervallo di valori che è possibile immettere nella colonna **Valore** . Gli intervalli possono essere uno dei seguenti:<br /><br /> Elenco discreto, ad esempio 1, 2, 3<br /><br /> Intervallo inclusivo, ad esempio [0, 100]<br /><br /> Intervallo esclusivo, ad esempio (0,...)<br /><br /> Una combinazione, ad esempio [0,...)|  
  
 **Descrizione**  
 Descrive il parametro selezionato nell'elenco **Parametri** .  
  
 **Aggiungi**  
 Consente di aggiungere all'elenco ulteriori parametri specifici per l'algoritmo. Dopo l'aggiunta del parametro, è possibile immetterne il nome corretto nella colonna **Parametro** e specificare un valore nella colonna **Valore** .  
  
 **Rimuovi**  
 Consente di eliminare un parametro personalizzato dall'elenco.  
  
 Se si elimina dall'elenco uno dei parametri dell'algoritmo standard di Analysis Services, il parametro verrà ancora utilizzato nel modello, ma con i valori predefiniti per quel parametro. Il parametro non è eliminato in modo permanente e verrà visualizzato la volta successiva che si apre la finestra di dialogo.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visualizzazione di modelli di data mining &#40;Progettazione modelli di Data Mining&#41;](mining-models-view-data-mining-model-designer.md)   
 [Spostamento di oggetti di data mining](data-mining/moving-data-mining-objects.md)  
  
  
