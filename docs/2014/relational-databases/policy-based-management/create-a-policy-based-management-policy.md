---
title: Creare i criteri della gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policies
ms.assetid: b28bf963-89f9-4941-b6c1-6004fec347f1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2b81fb13b8b8635bd5e5cecde801b4123fc74c99
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253531"
---
# <a name="create-a-policy-based-management-policy"></a>Creare i criteri della gestione basata su criteri
  In questo argomento verrà descritto come creare i criteri della gestione basata su criteri in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per creare i criteri tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-create-a-policy"></a>Per creare criteri  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui creare un nuovo criterio della gestione basata su criteri.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic sul segno più per espandere la cartella **Gestione criteri**.  
  
4.  Fare clic con il pulsante destro del mouse sulla cartella **Criteri** e scegliere **Nuovi criteri**.  
  
5.  Nella casella **Nome** della finestra di dialogo **Crea nuovi criteri** digitare il nome dei nuovi criteri.  
  
6.  Se si desidera che i criteri siano abilitati non appena vengono creati, selezionare la casella di controllo **Abilitati** . Se la modalità di valutazione è **Su richiesta**, la casella di controllo **Abilitati** non è disponibile.  
  
7.  Nell'elenco **Condizione di controllo** selezionare una delle condizioni esistenti oppure **Nuova condizione**. Per modificare una condizione, selezionarla, quindi fare clic sui puntini di sospensione ( **...** ). Per altre informazioni, vedere [Creare una nuova condizione della gestione basata su criteri](create-a-new-policy-based-management-condition.md) o [Visualizzare o modificare le proprietà di una condizione della gestione basata su criteri](view-or-modify-the-properties-of-a-policy-based-management-condition.md).  
  
8.  Nella casella **In base alle destinazioni** selezionare uno o più tipi di destinazione per i criteri. Alcune condizioni e facet possono essere applicati solo a determinati tipi di destinazioni. I set di destinazioni disponibili vengono visualizzati nella casella associata. Espandere **Ogni** per selezionare una condizione di filtro per tipi specifici delle destinazioni. Se in questa casella non viene visualizzata alcuna destinazione, l'ambito della condizione è costituito dal livello server.  
  
9. Nella casella **Modalità di valutazione** selezionare il comportamento dei criteri. Condizioni diverse possono essere associate a diverse modalità di valutazione valide. Per altre informazioni sulle modalità di valutazione valide, vedere [Amministrare server tramite la gestione basata su criteri](administer-servers-by-using-policy-based-management.md).  
  
10. Se i criteri verranno valutato in una pianificazione, impostare la modalità di valutazione su **Su pianificazione**e quindi fare clic su **Seleziona** per selezionare una pianificazione oppure su **Nuova** per crearne una nuova.  
  
11. Per limitare i criteri a un subset dei tipi di destinazione, nella casella **Restrizione server** selezionare le condizioni di restrizione oppure creare una nuova condizione.  
  
     Per ulteriori informazioni sulle opzioni disponibili nella finestra di dialogo **Crea nuovi criteri** , vedere [Finestra di dialogo Crea nuovi criteri o Apri criteri, pagina Generale](../../integration-services/general-page-of-integration-services-designers-options.md) o [Finestra di dialogo Crea nuovi criteri o Apri criteri, pagina Descrizione](create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
12. Al termine, fare clic su **OK**.  
  
  
