---
title: Eliminare una colonna (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0a95e8580aa30ce34ada1c77e198eb40d767304
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66067266"
---
# <a name="delete-a-column-ssas-tabular"></a>Eliminare una colonna (SSAS tabulare)
  In questo argomento viene descritto come eliminare una colonna da una tabella di modello tabulare.  
  
## <a name="delete-a-model-table-column"></a>Eliminare una colonna dalla tabella del modello  
  
> [!NOTE]  
>  L'eliminazione di una colonna da una tabella del modello non elimina la colonna da una definizione della query della partizione. Se la colonna che si desidera eliminare fa parte di una partizione, è necessario eliminare manualmente la colonna dalla definizione della query della partizione. Se non si elimina la colonna dalla definizione della query della partizione, durante le operazioni di elaborazione verranno eseguite query sulla colonna e restituiti dati che tuttavia non saranno popolati nella tabella del modello. Per altre informazioni, vedere [Partizioni &#40;SSAS tabulare&#41;](partitions-ssas-tabular.md).  
  
#### <a name="to-delete-a-model-table-column"></a>Per eliminare una colonna dalla tabella del modello  
  
-   In Progettazione modelli, nella tabella contenente la colonna che si desidera eliminare, fare clic con il pulsante destro del mouse su tale colonna, quindi scegliere **Elimina**.  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>Per eliminare una colonna dalla tabella del modello tramite la finestra di dialogo Proprietà tabella  
  
1.  In Progettazione modelli fare clic sulla tabella contenente la colonna che si desidera eliminare, quindi scegliere **Proprietà tabella** dal menu  **Tabella**.  
  
2.  In **Nomi colonne da**selezionare **Modello** (*per usare nomi delle colonna della tabella del modello, se diversi dall'origine*).  
  
3.  Nella finestra di anteprima della tabella nella finestra di dialogo **Modifica proprietà tabella** deselezionare la colonna che si desidera eliminare, quindi scegliere **OK**.  
  
## <a name="see-also"></a>Vedi anche  
 [Aggiungere colonne a una tabella &#40;SSAS tabulare&#41;](add-columns-to-a-table-ssas-tabular.md)   
 [Partizioni &#40;SSAS tabulare&#41;](partitions-ssas-tabular.md)  
  
  
