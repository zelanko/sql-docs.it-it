---
title: Aggiungere tabelle a un'istanza di CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- addTabs
ms.assetid: ad260e19-c021-4035-9311-c02fc96ceaea
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 505699164f49511adb95465e0b74e9e90c8f7dc6
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65729116"
---
# <a name="add-tables-to-a-cdc-instance"></a>Aggiungere tabelle a un'istanza di CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare la finestra di dialogo Table Selection per aggiungere tabelle aggiuntive dall'origine Oracle all'istanza di CDC. Le tabelle selezionate vengono aggiunte all'elenco presente nella scheda **Tables** dell'editor delle proprietà.  
  
 Per impostazione predefinita, non viene inclusa alcuna tabella nell'elenco di tabelle della finestra di dialogo. È possibile selezionare la casella di controllo **(Select All)** o cercare tabelle specifiche.  
  
 **Per cercare tabelle specifiche**  
 Immettere i criteri di ricerca nel modo illustrato di seguito, quindi scegliere **Cerca**:  
  
-   **Schema**: selezionare uno schema del database nell'elenco. Verranno incluse nell'elenco solo le tabelle aventi questo schema.  
  
-   **Table Name Pattern** (Modello nome tabella): immettere qualsiasi stringa di caratteri. Verranno visualizzate solo le tabelle che includono la stringa di caratteri immessa.  
  
> [!NOTE]  
>  È possibile immettere criteri in uno o entrambi questi campi.  
  
-   **Display first 1000 matching tables** (Visualizza prima 1000 tabelle corrispondenti): questa casella di controllo è selezionata per impostazione predefinita. La visualizzazione è limitata alle prime 1000 tabelle corrispondenti. Se si deseleziona la casella di controllo, vengono visualizzate tutte le tabelle che soddisfano i criteri. Se sono presenti molte tabelle, la visualizzazione dell'elenco potrebbe richiedere molto tempo.  
  
 **Per selezionare le tabelle da includere nell'istanza di CDC**  
 Fare clic sulla casella di controllo accanto alle tabelle che si desidera includere, quindi scegliere **Aggiungi**. Le tabelle vengono aggiunte all'elenco nella pagina **Select Tables and Columns** della New Instance Wizard.  
  
 Fare clic su **Chiudi** per chiudere la finestra di dialogo senza aggiungere tabelle.  
  
> [!NOTE]  
>  Se si seleziona una tabella che include un tipo di dati non supportato, verrà visualizzato un messaggio di errore e la tabella non verrà inclusa.  
  
> [!NOTE]  
>  È possibile visualizzare l'elenco di tabelle nel visualizzatore. Quando si utilizza il visualizzatore le informazioni sono in sola lettura. Nel visualizzatore è inoltre incluso un elenco delle colonne acquisite nella tabella. Per informazioni su come accedere al visualizzatore, vedere [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di modifica delle proprietà dell'istanza di CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [Selezionare le tabelle Oracle per l'acquisizione delle modifiche](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md)  
  
  
