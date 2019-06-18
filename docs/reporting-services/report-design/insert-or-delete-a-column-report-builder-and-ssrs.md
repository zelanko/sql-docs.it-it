---
title: Inserire o eliminare una colonna (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: e9db79e2-7e7d-4359-a706-cb746c94182a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2796447d65a7fcabe029c67f460a76284daf242f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580211"
---
# <a name="insert-or-delete-a-column-report-builder-and-ssrs"></a>Inserire o eliminare una colonna (Generatore report e SSRS)
  È possibile aggiungere o eliminare colonne in un'area dati Tablix di un report impaginato [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . L'area dati Tablix può essere una tabella, una matrice o un elenco. Le procedure riportate di seguito non sono applicabili alle aree dati del grafico e del misuratore.  
  
 In un'area dati Tablix è possibile aggiungere colonne associate a un gruppo (interne a un gruppo) o non associate a un gruppo (esterne a un gruppo). Una colonna interna a un gruppo viene ripetuta una volta per ogni valore di gruppo univoco. Ad esempio, una colonna all'interno di un gruppo che si basa sul valore di una colonna di dati contenente nomi di colori, viene ripetuta una volta per ogni nome di colore distinto. Per i gruppi nidificati, una colonna può essere esterna al gruppo figlio ma interna al gruppo padre. In questo caso, la riga viene ripetuta una volta per ogni valore univoco nel gruppo padre.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-that-the-row-and-column-handles-appear"></a>Per selezionare un'area dati in modo da visualizzare gli handle di riga e di colonna  
  
-   In visualizzazione della struttura fare clic sull'angolo superiore sinistro dell'area dati Tablix in modo da visualizzare gli handle di colonna e di riga sopra e accanto all'area.  
  
     Per altre informazioni sulle aree dati, vedere [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
## <a name="to-insert-a-column-in-a-selected-data-region"></a>Per inserire una colonna in un'area dati selezionata  
  
-   Fare clic con il pulsante destro del mouse su un handle di colonna in corrispondenza del quale si vuole inserire una colonna, scegliere **Inserisci colonna**e quindi fare clic su **A sinistra** o **A destra**.  
  
     -oppure-  
  
-   Fare clic con il pulsante destro del mouse su una cella nell'area dati in corrispondenza della quale si vuole inserire una colonna, scegliere **Inserisci colonna**e quindi fare clic su **A sinistra** o **A destra**.  
  
## <a name="to-delete-a-column-from-a-selected-data-region"></a>Per eliminare una colonna da un'area dati selezionata  
  
-   Selezionare la colonna o le colonne da eliminare, fare clic con il pulsante destro del mouse sull'handle di una delle colonne selezionate e quindi scegliere **Elimina colonne**.  
  
     -oppure-  
  
-   Fare clic con il pulsante destro del mouse su una cella nell'area dati in corrispondenza della quale si vuole eliminare una colonna e quindi scegliere **Elimina colonne**.  
  
## <a name="to-insert-a-column-in-a-group-in-a-selected-data-region"></a>Per inserire una colonna in un gruppo di un'area dati selezionata  
  
-   Fare clic con il pulsante destro del mouse su una cella di un gruppo di colonne nell'area dei gruppi di colonne di un'area dati Tablix in corrispondenza della quale si vuole inserire una colonna, scegliere **Inserisci colonna**e quindi fare clic su **A sinistra - Gruppo esterno**, **A sinistra - Gruppo interno**, **A destra - Gruppo interno**o **A destra - Gruppo esterno**.  
  
     Verrà aggiunta una colonna all'interno o all'esterno del gruppo rappresentato dalla cella del gruppo di colonne selezionata mediante clic.  
  
## <a name="to-delete-a-column-from-a-group-in-a-selected-data-region"></a>Per eliminare una colonna da un gruppo di un'area dati selezionata  
  
-   Fare clic con il pulsante destro del mouse su una cella di un gruppo di colonne nell'area dei gruppi di colonne di un'area dati Tablix in corrispondenza della quale si vuole eliminare una colonna e quindi scegliere **Elimina colonne**.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sui gruppi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)      
 [Tabelle, matrici ed elenchi &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
