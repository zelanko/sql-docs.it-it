---
title: Selezionare le tabelle Oracle per l'acquisizione delle modifiche | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selOraTabDia
ms.assetid: 2e295dc8-999d-4c4d-96cc-1519674b47a4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c0b962db5e005837a2e9d3fe68564fceb5bfc253
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62835266"
---
# <a name="select-oracle-tables-for-capturing-changes"></a>Selezionare le tabelle Oracle per l'acquisizione delle modifiche
  Utilizzare questa finestra di dialogo per selezionare le tabelle incluse nell'istanza di CDC. Le tabelle selezionate vengono aggiunte all'elenco nella pagina **Select Tables and Columns** della New Instance Wizard. In questa finestra di dialogo è possibile effettuare le operazioni seguenti:  
  
 Per impostazione predefinita, non viene inclusa alcuna tabella nell'elenco di tabelle della finestra di dialogo. È possibile selezionare la casella di controllo all'inizio della colonna per selezionare tutte le tabelle o cercare tabelle specifiche.  
  
 **Per cercare tabelle specifiche**  
 Immettere i criteri di ricerca nel modo illustrato di seguito, quindi scegliere **Cerca**:  
  
-   **Schema**: selezionare uno schema del database nell'elenco. Verranno incluse nell'elenco solo le tabelle aventi questo schema.  
  
-   **Table Name Pattern** (Modello nome tabella): immettere qualsiasi stringa di caratteri. Verranno visualizzate solo le tabelle che includono la stringa di caratteri immessa.  
  
> [!NOTE]  
>  È possibile immettere criteri in uno o entrambi questi campi.  
  
-   **Display first 1000 matching tables** (Visualizza prima 1000 tabelle corrispondenti): questa casella di controllo è selezionata per impostazione predefinita. La visualizzazione è limitata alle prime 1000 tabelle corrispondenti. Se si deseleziona la casella di controllo, vengono visualizzate tutte le tabelle che soddisfano i criteri. Se sono presenti molte tabelle, la visualizzazione dell'elenco potrebbe richiedere molto tempo.  
  
 **Per selezionare le tabelle da includere nell'istanza di CDC**  
 Fare clic sulla casella di controllo accanto alle tabelle che si desidera includere, quindi scegliere **Aggiungi**. Le tabelle vengono aggiunte all'elenco nella pagina **Select Tables and Columns** della New Instance Wizard.  
  
 Fare clic su **Close** per chiudere la finestra di dialogo senza aggiungere tabelle aggiuntive.  
  
> [!NOTE]  
>  Se si seleziona una tabella che include un tipo di dati non supportato, verrà visualizzato un messaggio di errore e la tabella non verrà inclusa.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura di creazione dell'istanza del database delle modifiche di SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Selezionare tabelle e colonne Oracle](select-oracle-tables-and-columns.md)  
  
  
