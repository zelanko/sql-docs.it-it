---
title: Sottoscrittori | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.subscribers.f1
helpviewer_keywords:
- Subscribers [SQL Server replication]
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 725be263e30687a3f2ded90990e952e1cd97a185
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62629391"
---
# <a name="subscribers"></a>Sottoscrittori
  Specificare i [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sottoscrittori o non che riceveranno una sottoscrizione alla pubblicazione selezionata.  
  
## <a name="options"></a>Opzioni  
 **Sottoscrittori**  
 Selezionare la casella di controllo nella griglia per abilitare l'origine dei dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrispondente come Sottoscrittore della pubblicazione scelta nella pagina **Pubblicazione** . Se il Sottoscrittore non è incluso nell'elenco, fare clic su **Aggiungi Sottoscrittore** o su **Aggiungi Sottoscrittore SQL Server**.  
  
 **Database di sottoscrizione**  
 Le informazioni visualizzate e le azioni disponibili in questa colonna dipendono dal tipo di Sottoscrittore visualizzato nella colonna **Sottoscrittori** :  
  
-   Per i Sottoscrittori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionare un database di sottoscrizione nell'elenco **Database di sottoscrizione** oppure creare un nuovo database selezionando il comando **Nuovo database** nello stesso elenco.  
  
    > [!NOTE]  
    >  Se si sta abilitando il server di pubblicazione come Sottoscrittore, il database di sottoscrizione deve essere diverso dal database di pubblicazione.  
  
-   Il database di sottoscrizione non viene visualizzato per i Sottoscrittori non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Specificare il database e le altre informazioni di connessione nel campo **Nome origine dati** della finestra di dialogo **Aggiungi Sottoscrittore non SQL Server** . Questa finestra di dialogo è disponibile facendo clic su **Aggiungi Sottoscrittore** e quindi facendo clic su **Aggiungi Sottoscrittore non SQL Server**.  
  
 **Aggiungi Sottoscrittore**  
 Consente di aggiungere un server all'elenco dei server attivabili come Sottoscrittori. Questo pulsante viene visualizzato se vengono soddisfatte tutte le condizioni seguenti:  
  
-   La pubblicazione selezionata è una pubblicazione snapshot o transazionale che non supporta le sottoscrizioni aggiornabili.  
  
    > [!NOTE]  
    >  Se la pubblicazione che si sta sottoscrivendo dispone di sottoscrizioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non è ancora abilitata per i Sottoscrittori non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non è possibile aggiungere una sottoscrizione non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   La sottoscrizione è una sottoscrizione push.  
  
-   Il server della pubblicazione selezionata è [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versione successiva.  
  
 Facendo clic su **Aggiungi Sottoscrittore** viene visualizzato un menu con due opzioni: **Aggiungi Sottoscrittore SQL Server** e **Aggiungi Sottoscrittore non SQL Server**. Scegliere **Aggiungi Sottoscrittore non SQL Server** per aggiungere un Sottoscrittore Oracle o IBM DB2.  
  
 **Aggiungi Sottoscrittore SQL Server**  
 Consente di aggiungere un server all'elenco dei server attivabili come Sottoscrittori. Questo pulsante viene visualizzato se viene soddisfatta una o più delle condizioni seguenti:  
  
-   La pubblicazione selezionata è una pubblicazione di tipo merge, snapshot o transazionale che supporta le sottoscrizioni aggiornabili.  
  
-   La sottoscrizione è una sottoscrizione pull.  
  
-   Nel server di pubblicazione della pubblicazione selezionata è in esecuzione una versione di SQL Server precedente a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Per le versioni precedenti il pulsante viene visualizzato solo se viene soddisfatta una o più delle condizioni seguenti:  
  
    -   L'utente è membro del ruolo predefinito del server **sysadmin** nel server di pubblicazione.  
  
    -   Il Sottoscrittore è stato aggiunto nella pagina **Sottoscrittori** della finestra di dialogo **Proprietà server di pubblicazione** .  
  
    -   La pubblicazione consente le sottoscrizioni anonime.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Non-SQL Server Subscribers](non-sql/non-sql-server-subscribers.md)   
 [Sottoscrizione delle pubblicazioni](subscribe-to-publications.md)  
  
  
