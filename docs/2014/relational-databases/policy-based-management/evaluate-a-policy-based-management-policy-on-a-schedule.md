---
title: Valutare i criteri della gestione basata su criteri in una pianificazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4355245af62817b7ab675241f5df9db77500daa3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705148"
---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>Valutare i criteri della gestione basata su criteri in una pianificazione
  In questo argomento verrà descritto come valutare i criteri della gestione basata su criteri in una pianificazione in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per valutare i criteri in una pianificazione tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-evaluate-a-policy-on-a-schedule"></a>Per valutare i criteri in una pianificazione  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server contenente la pianificazione dei criteri da valutare.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic sul segno più per espandere la cartella **Gestione criteri**.  
  
4.  Fare clic sul segno più per espandere la cartella **Criteri** .  
  
5.  Fare clic con il pulsante destro del mouse sui criteri di cui si desidera valutare la pianificazione, quindi scegliere **Proprietà**.  
  
6.  Nella finestra di dialogo **Apri criteri -** _nome_criterio_ selezionare **Su pianificazione** nell'elenco **Modalità di valutazione**.  
  
7.  In **Pianificazione**fare clic su **Seleziona** per specificare una pianificazione esistente o su **Nuova** per creare una nuova pianificazione.  
  
8.  Al termine, fare clic su **OK**.  
  
  
