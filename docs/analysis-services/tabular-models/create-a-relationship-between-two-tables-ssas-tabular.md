---
title: Creare una relazione nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7e9ee96a04aa6b023be51f8e1e8d913e26a7e2a8
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072098"
---
# <a name="create-a-relationship"></a>Creare una relazione 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Se per le tabelle presenti nell'origine dati non sono attualmente disponibili relazioni o se si aggiungono nuove tabelle, è possibile creare nuove relazioni utilizzando gli strumenti di Progettazione modelli. Per informazioni sull'utilizzo delle relazioni nei modelli tabulari, vedere [relazioni](../../analysis-services/tabular-models/relationships-ssas-tabular.md).  
  
## <a name="create-a-relationship-between-two-tables"></a>Creare una relazione tra due tabelle  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-click-and-drag"></a>Per creare una relazione tra due tabelle in Vista diagramma, visualizzabile facendo clic e trascinando  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]scegliere **Vista modelli** dal menu **Modello**, quindi fare clic su **Vista diagramma**.  
  
2.  Fare clic su una colonna all'interno di una tabella e, tenendo premuto il pulsante, trascinare il cursore in una colonna di ricerca correlata di una relativa tabella, quindi rilasciarlo. La relazione verrà creata automaticamente nell'ordine corretto.  
  
#### <a name="to-create-a-relationship-between-two-tables-in-diagram-view-right-click"></a>Per creare una relazione tra due tabelle in Vista diagramma, visualizzabile facendo clic con il pulsante destro del mouse  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]scegliere **Vista modelli** dal menu **Modello**, quindi fare clic su **Vista diagramma**.  
  
2.  Fare clic con il pulsante destro del mouse sull'intestazione di una tabella o su una colonna, quindi scegliere **Crea relazione**.  
  
3.  Nella finestra di dialogo **Crea relazione** fare clic sulla freccia in giù accanto a **Tabella**e selezionare una tabella nell'elenco a discesa.  
  
     Questa tabella deve trovarsi sul lato "molti" di una relazione "uno-a-molti".  
  
4.  Per **Colonna**, selezionare la colonna che contiene i dati correlata a **Colonna di ricerca correlata**. La colonna viene selezionata automaticamente se è stato fatto clic con il pulsante destro del mouse su una colonna per creare la relazione.  
  
5.  Per **Tabella di ricerca correlata**, selezionare una tabella che dispone almeno di una colonna di dati correlata alla tabella appena selezionata per **Tabella**.  
  
     Questa tabella deve trovarsi sul lato "uno" di una relazione "uno-a-molti", per indicare che i valori nella colonna selezionata non contengono duplicati. Se si tenta di creare la relazione nell'ordine errato (uno-a-molti anziché molti-a-uno), verrà visualizzata un'icona accanto al campo **Colonna di ricerca correlata** . Invertire l'ordine per creare una relazione valida.  
  
6.  Per **Colonna di ricerca correlata**, selezionare una colonna che dispone di valori univoci che corrispondono ai valori della colonna selezionata per **Colonna**.  
  
7.  Fare clic su **Crea**.  
  
#### <a name="to-create-a-relationship-between-two-tables-in-data-view"></a>Per creare una relazione tra due tabelle in Vista dati  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]scegliere **Crea relazioni** dal menu **Tabella**.  
  
2.  Nella finestra di dialogo **Crea relazione** fare clic sulla freccia in giù accanto a **Tabella**e selezionare una tabella nell'elenco a discesa.  
  
     Questa tabella deve trovarsi sul lato "molti" di una relazione "uno-a-molti".  
  
3.  Per **Colonna**, selezionare la colonna che contiene i dati correlata a **Colonna di ricerca correlata**.  
  
4.  Per **Tabella di ricerca correlata**, selezionare una tabella che dispone almeno di una colonna di dati correlata alla tabella appena selezionata per **Tabella**.  
  
     Questa tabella deve trovarsi sul lato "uno" di una relazione "uno-a-molti", per indicare che i valori nella colonna selezionata non contengono duplicati. Se si tenta di creare la relazione nell'ordine errato (uno-a-molti anziché molti-a-uno), verrà visualizzata un'icona accanto al campo **Colonna di ricerca correlata** . Invertire l'ordine per creare una relazione valida.  
  
5.  Per **Colonna di ricerca correlata**, selezionare una colonna che dispone di valori univoci che corrispondono ai valori della colonna selezionata per **Colonna**.  
  
6.  Fare clic su **Crea**.  
  
## <a name="see-also"></a>Vedere anche  
 [Eliminare relazioni](../../analysis-services/tabular-models/delete-relationships-ssas-tabular.md)   
 [Relazioni](../../analysis-services/tabular-models/relationships-ssas-tabular.md)  
  
  
