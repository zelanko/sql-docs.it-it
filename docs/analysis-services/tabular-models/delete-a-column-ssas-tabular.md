---
title: Eliminare una colonna in un modello tabulare di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f61aea9e4751094dafd37fe3b9ca8ed8d6ef0fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207705"
---
# <a name="delete-a-column"></a>Eliminare una colonna 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo descrive come eliminare una colonna da una tabella del modello tabulare.  
  
## <a name="delete-a-model-table-column"></a>Eliminare una colonna dalla tabella del modello  
  
> [!NOTE]  
>  L'eliminazione di una colonna da una tabella del modello non elimina la colonna da una definizione della query della partizione. Se la colonna che si desidera eliminare fa parte di una partizione, è necessario eliminare manualmente la colonna dalla definizione della query della partizione. Se non si elimina la colonna dalla definizione della query della partizione, durante le operazioni di elaborazione verranno eseguite query sulla colonna e restituiti dati che tuttavia non saranno popolati nella tabella del modello. Per altre informazioni, vedere [partizioni](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### <a name="to-delete-a-model-table-column"></a>Per eliminare una colonna dalla tabella del modello  
  
-   In Progettazione modelli, nella tabella contenente la colonna che si desidera eliminare, fare clic con il pulsante destro del mouse su tale colonna, quindi scegliere **Elimina**.  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>Per eliminare una colonna dalla tabella del modello tramite la finestra di dialogo Proprietà tabella  
  
1.  In Progettazione modelli fare clic sulla tabella contenente la colonna che si desidera eliminare, quindi scegliere **Proprietà tabella** dal menu  **Tabella**.  
  
2.  In **Nomi colonne da**selezionare **Modello** (*per usare nomi delle colonna della tabella del modello, se diversi dall'origine*).  
  
3.  Nella finestra di anteprima della tabella nella finestra di dialogo **Modifica proprietà tabella** deselezionare la colonna che si desidera eliminare, quindi scegliere **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere colonne a una tabella](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [Partizioni](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
