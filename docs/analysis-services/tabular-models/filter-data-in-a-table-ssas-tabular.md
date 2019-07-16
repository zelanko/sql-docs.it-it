---
title: Filtrare i dati in una tabella di modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9b1fcdda5bd49f8056a6035ec10da8fb52f1c5d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162813"
---
# <a name="filter-data-in-a-table"></a>Filtrare i dati di una tabella 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  È possibile applicare filtri quando si importano dati per controllare le righe caricate in una tabella. Dopo aver importato i dati, non è possibile eliminare righe singole. Tuttavia, è possibile applicare filtri personalizzati per controllare la modalità in cui visualizzare tali righe. Le righe che non soddisfano i criteri di filtro sono nascoste. È possibile filtrare i dati in base a una o più colonne. I filtri sono additivi, pertanto ciascun filtro aggiuntivo è basato sul filtro corrente e consente di ridurre ulteriormente il subset di dati.  
  
> [!NOTE]  
>  La finestra di anteprima del filtro consente di limitare il numero di valori diversi visualizzati. Se il limite viene superato, viene visualizzato un messaggio.  
  
### <a name="to-filter-data-based-on-column-values"></a>Per filtrare dati in base ai valori della colonna  
  
1.  In Progettazione modelli selezionare una tabella, quindi fare clic sulla freccia nell'intestazione della colonna in base alla quale filtrare i dati.  
  
2.  Nel menu Filtro automatico effettuare uno dei passaggi seguenti:  
  
    -   Nell'elenco di valori delle colonne selezionare o deselezionare uno o più valori da utilizzare come filtri, quindi fare clic su **OK**.  
  
         Se il numero di valori è estremamente elevato, singoli elementi potrebbero non essere visualizzati nell'elenco. Verrà invece visualizzato il messaggio, "Troppi elementi da visualizzare".  
  
    -   Fare clic su **Filtri per numeri** o su **Filtri per testo** (a seconda del tipo di colonna) e quindi fare clic su uno dei comandi di operatore di confronto (ad esempio **Uguale a**) o su **Filtro personalizzato**. Nella finestra di dialogo **Filtro personalizzato** creare il filtro, quindi fare clic su **OK**.  
  
### <a name="to-clear-a-filter-for-a-column"></a>Per cancellare un filtro per una colonna  
  
1.  Fare clic sulla freccia nell'intestazione della colonna per la quale si desidera cancellare un filtro.  
  
2.  Fare clic su **Cancella filtro da \<nome colonna >** .  
  
### <a name="to-clear-all-filters-for-a-table"></a>Per cancellare tutti i filtri per una tabella  
  
1.  In Progettazione modelli selezionare la tabella per la quale si desidera cancellare i filtri.  
  
2.  Fare clic sul menu **Colonna** , quindi scegliere **Cancella tutti i filtri**.  
  
## <a name="see-also"></a>Vedere anche  
 [Filtrare e ordinare dati](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [Prospettive](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
