---
title: Creare una relazione tra due tabelle (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.managereldb.f1
- sql12.asvs.bidtoolset.createrelatdb.f1
ms.assetid: 052d77b7-7922-408a-a200-786016ee4d15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 98bd7f6c904207aa6d38f2ae756a207f128707a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067543"
---
# <a name="create-a-relationship-between-two-tables-ssas-tabular"></a>Creare una relazione tra due tabelle (SSAS tabulare)
  Se per le tabelle presenti nell'origine dati non sono attualmente disponibili relazioni o se si aggiungono nuove tabelle, è possibile creare nuove relazioni utilizzando gli strumenti di Progettazione modelli. Per informazioni sulla modalità d'uso delle relazioni nei modelli tabulari, vedere [Relationships &#40;SSAS Tabular&#41;](relationships-ssas-tabular.md).  
  
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
 [Eliminare relazioni &#40;SSAS tabulare&#41;](delete-relationships-ssas-tabular.md)   
 [Relazioni &#40;SSAS tabulare&#41;](relationships-ssas-tabular.md)  
  
  
