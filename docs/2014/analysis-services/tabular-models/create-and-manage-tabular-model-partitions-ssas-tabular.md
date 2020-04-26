---
title: Creare e gestire partizioni di modelli tabulari (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dab72cf0-95bc-4b63-95dc-505b5cd881c1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 72c5b69aee10d8ac1342b3f037d76ab6ef5fc36c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067394"
---
# <a name="create-and-manage-tabular-model-partitions-ssas-tabular"></a>Creare e gestire partizioni di modelli tabulari (SSAS tabulare)
  Le partizioni consentono di dividere una tabella in parti logiche. Ogni partizione può quindi essere elaborata (aggiornata) indipendentemente dalle altre. Le partizioni definite per un modello durante la relativa creazione vengono duplicate in un modello distribuito. Una volta distribuite, tali partizioni possono essere gestite tramite la finestra di dialogo **Partizioni** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o tramite uno script. Nelle attività presentate in questo argomento viene descritto come creare e gestire partizioni per un modello distribuito.  
  
 In questo argomento sono incluse le attività seguenti:  
  
-   [Per creare una nuova partizione](#bkmk_create_new)  
  
-   [Per copiare una partizione](#bkmk_copy)  
  
-   [Per unire due o più partizioni](#bkmk_merge)  
  
-   [Per eliminare una partizione](#bkmk_delete)  
  
## <a name="tasks"></a>Attività  
 Per creare e gestire partizioni per un database modello tabulare distribuito si utilizzerà la finestra di dialogo **Partizioni** in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per visualizzare la finestra di dialogo **Partizioni** , in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse su una tabella, quindi selezionare **Partizioni**.  
  
###  <a name="to-create-a-new-partition"></a><a name="bkmk_create_new"></a>Per creare una nuova partizione  
  
1.  Nella finestra di dialogo **Partizioni** fare clic sul pulsante **Nuova** .  
  
2.  In **Nome partizione**digitare un nome per la partizione. Per impostazione predefinita, il nome della partizione predefinita sarà numerato in modo incrementale per ogni nuova partizione.  
  
3.  In **Istruzione SQL**digitare o incollare un'istruzione di query SQL che consente di definire le colonne e tutte le clausole che si desidera includere nella partizione nella finestra Query.  
  
4.  Per convalidare l'istruzione, fare clic su **Controlla sintassi**.  
  
###  <a name="to-copy-a-partition"></a><a name="bkmk_copy"></a>Per copiare una partizione  
  
1.  Nell'elenco **Partizioni** della relativa finestra di dialogo selezionare la partizione che si desidera copiare, quindi fare clic sul pulsante **Copia** . ****  
  
2.  In **Nome partizione**digitare un nuovo nome per la partizione.  
  
3.  In **Istruzione SQL**modificare l'istruzione di query SQL.  
  
###  <a name="to-merge-two-or-more-partitions"></a><a name="bkmk_merge"></a> Per unire due o più partizioni  
  
-   Nell'elenco **partizioni** della finestra di dialogo **partizioni** , utilizzare CTRL + clic per selezionare le partizioni che si desidera unire, quindi fare clic sul pulsante **Unisci** .  
  
> [!IMPORTANT]  
>  L'unione delle partizioni non consente di aggiornare i metadati della partizione. Gli amministratori devono modificare l'istruzione SQL per la partizione risultante per assicurare che tramite le operazioni di elaborazione vengano elaborati tutti i dati nella partizione unita.  
  
###  <a name="to-delete-a-partition"></a><a name="bkmk_delete"></a> Per eliminare una partizione  
  
-   Nell'elenco **Partizioni** della relativa finestra di dialogo selezionare la partizione che si desidera eliminare, quindi fare clic sul pulsante **Elimina** . ****  
  
## <a name="see-also"></a>Vedi anche  
 [Partizioni di modelli tabulari &#40;SSAS tabulare&#41;](partitions-ssas-tabular.md)   
 [Elaborare partizioni di modelli tabulari &#40;SSAS tabulare&#41;](process-tabular-model-partitions-ssas-tabular.md)  
  
  
