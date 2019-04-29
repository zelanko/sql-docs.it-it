---
title: Creare una nuova condizione della gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policy conditions
ms.assetid: 8a612f7e-6c70-49db-a4de-48431e097cc5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 942a0be0503cd728defb6800a516b0cb0c85c13f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856835"
---
# <a name="create-a-new-policy-based-management-condition"></a>Creare una nuova condizione della gestione basata su criteri
  In questo argomento verrà descritto come creare una condizione della gestione basata su criteri in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per creare una condizione tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-condition"></a>Per creare una condizione  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui creare una condizione della gestione basata su criteri.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic sul segno più per espandere la cartella **Gestione criteri**.  
  
4.  Fare clic sul segno più per espandere la cartella **Facet** .  
  
5.  Fare clic con il pulsante destro del mouse sul facet nel quale creare una nuova condizione e selezionare **Nuova condizione**.  
  
6.  Nella casella **Nome** della finestra di dialogo **Crea nuova condizione** digitare il nome della nuova condizione.  
  
7.  Confermare il facet corretto nell'elenco **Facet** oppure selezionare un facet diverso.  
  
8.  In **Espressione**creare le espressioni della condizione selezionando una proprietà facet nella casella **Campo** , insieme all'operatore e al valore associati. Se si aggiungono più espressioni, è possibile crearne un join utilizzando **And** oppure **Or**. Per altre informazioni sulle opzioni disponibili in questa finestra di dialogo, vedere [Finestra di dialogo Crea nuova condizione o Apri condizione, pagina Generale](../../integration-services/general-page-of-integration-services-designers-options.md), [Finestra di dialogo Crea nuova condizione o Apri condizione, pagina Descrizione](create-new-condition-or-open-condition-dialog-box-description-page.md) [Finestra di dialogo Modifica avanzata &#40;Condizione&#41;](advanced-edit-condition-dialog-box.md).  
  
9. Al termine, fare clic su **OK**.  
  
  
