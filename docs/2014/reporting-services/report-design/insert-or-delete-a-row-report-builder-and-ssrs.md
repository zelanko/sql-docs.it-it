---
title: Inserire o eliminare una riga (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bd9f92b0128bd6280654885f79f8231570f721de
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105626"
---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>Inserire o eliminare una riga (Generatore report e SSRS)
  È possibile aggiungere o eliminare righe in un'area dati Tablix. L'area dati Tablix può essere una tabella, una matrice o un elenco. Le procedure riportate di seguito non sono applicabili alle aree dati del grafico e del misuratore.  
  
 In un'area dati Tablix è possibile aggiungere righe associate a un gruppo (interne a un gruppo) o non associate a un gruppo (esterne a un gruppo). Una riga interna a un gruppo viene ripetuta una volta per ogni valore di gruppo univoco. Ad esempio, una riga all'interno di un gruppo che si basa sul valore di una colonna di dati contenente nomi di colori, viene ripetuta una volta per ogni nome di colore distinto. Per i gruppi nidificati, una riga può essere esterna al gruppo figlio ma interna al gruppo padre. In questo caso, la riga viene ripetuta una volta per ogni valore univoco nel gruppo padre.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>Per selezionare un'area dati in modo da visualizzare gli handle di riga e di colonna  
  
-   In visualizzazione Progettazione fare clic sull'angolo superiore sinistro dell'area dati Tablix in modo da visualizzare gli handle di colonna e di riga sopra e accanto all'area.  
  
     Per altre informazioni sulle aree dati, vedere [sono elencati &#40;Generatore Report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
### <a name="to-insert-a-row-in-a-selected-data-region"></a>Per inserire una riga in un'area dati selezionata  
  
-   Fare clic con il pulsante destro del mouse su un handle di riga in corrispondenza del quale si desidera inserire una riga, scegliere **Inserisci riga**, quindi fare clic su **Sopra** o **Sotto**.  
  
     \- - oppure -  
  
-   Fare clic con il pulsante destro del mouse su una cella nell'area dati in corrispondenza della quale si desidera inserire una riga, scegliere **Inserisci riga**, quindi fare clic su **Sopra** o **Sotto**.  
  
### <a name="to-delete-a-row-from-a-selected-data-region"></a>Per eliminare una riga da un'area dati selezionata  
  
-   Selezionare la riga o le righe che si desidera eliminare, fare clic con il pulsante destro del mouse sull'handle di una delle righe selezionate, quindi scegliere **Elimina righe**.  
  
     \- - oppure -  
  
-   Fare clic con il pulsante destro del mouse su una cella nell'area dati in corrispondenza della quale si desidera eliminare una riga, quindi scegliere **Elimina righe**.  
  
### <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>Per inserire una riga in un gruppo di un'area dati selezionata  
  
-   Fare clic con il pulsante destro del mouse su una cella di un gruppo di righe nell'area dei gruppi di righe di un'area dati Tablix in corrispondenza della quale si desidera inserire una riga, scegliere **Inserisci riga**, quindi fare clic su **Sopra - Gruppo esterno**, **Sopra - Gruppo interno**, **Sotto - Gruppo interno**o **Sotto - Gruppo esterno**.  
  
     Verrà aggiunta una riga all'interno o all'esterno del gruppo rappresentato dalla cella del gruppo di righe selezionata mediante clic.  
  
### <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>Per eliminare una riga da un gruppo di un'area dati selezionata  
  
-   Fare clic con il pulsante destro del mouse su una cella di un gruppo di righe nell'area dei gruppi di righe di un'area dati Tablix in corrispondenza della quale si desidera eliminare una riga, quindi scegliere **Elimina righe**.  
  
## <a name="see-also"></a>Vedere anche  
 [Area dati Tablix &#40;Generatore report e SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Informazioni sui gruppi &#40;Generatore report e SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)   
 [Tabelle &#40;Generatore report e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrici &#40;Generatore report e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Elenchi &#40;Generatore report e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
