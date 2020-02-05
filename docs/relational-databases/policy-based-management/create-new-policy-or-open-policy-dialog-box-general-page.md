---
title: Finestra di dialogo "Crea nuovi criteri" o "Apri criteri", pagina Generale
descripton: Describes the 'General Page' of the 'Create New Policy' and 'Open Policy' dialog boxes for Policy-Based Management in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.policy.f1
- sql13.swb.dmf.policy.filter.f1
- sql13.swb.dmf.newgroup.f1
ms.assetid: c00bebd0-d04b-4c64-840e-8b7a2c603436
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 50334a6b64319a280d34df9fbd4907aa82e82111
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558306"
---
# <a name="create-new-policy-or-open-policy-dialog-box-general-page"></a>Finestra di dialogo Crea nuovi criteri o Apri criteri, pagina Generale
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare questa finestra di dialogo per creare nuovi criteri della gestione basata su criteri o per modificarne uno esistente. Utilizzare le aree **In base alle destinazioni** e **Restrizione server** come filtro per limitare i criteri a un subset di tutte le destinazioni possibili. Per poter utilizzare le condizioni come filtri delle destinazioni, è necessario che siano definite in un facet fisico, che non contengano funzioni e che non contengano l'operatore LIKE. Durante il calcolo del set di oggetti per i criteri, per impostazione predefinita gli oggetti di sistema sono esclusi.  Ad esempio, se il set di oggetti dei criteri si riferisce a tutte le tabelle, i criteri non verranno applicati alle tabelle di sistema. Se gli utenti desiderano valutare i criteri negli oggetti di sistema, possono aggiungere in modo esplicito questi oggetti al set di oggetti. Tuttavia, sebbene tutti i criteri siano supportati per la modalità di valutazione **Controllo su pianificazione** , per motivi di prestazioni, non tutti i criteri con i set di oggetti arbitrari sono supportati per la modalità di valutazione **Controllo su modifiche** . Per altre informazioni, vedere [https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 In caso di criteri nuovi digitare il relativo nome. In caso di criteri esistenti, il nome è già visualizzato.  
  
 **Enabled**  
 Selezionare la casella di controllo **Abilitato** per abilitare i criteri. Deselezionare la casella di controllo **Abilitato** per disabilitarli. La casella **Abilitato** si applica all'automazione dei criteri. Consente di creare o rimuovere il sistema di automazione per i criteri. Per l'automazione vengono utilizzati i meccanismi seguenti:  
  
 **Su modifica: impedisci esecuzione**  
 Un trigger del database applica la conformità.  
  
 **Su modifica: solo log**  
 Un evento dei servizi di notifica verifica la conformità.  
  
 **Su pianificazione**  
 Viene creato un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per verificare la conformità in base a una pianificazione.  
  
 I criteri eseguiti in modalità di valutazione **Su richiesta** non utilizzano questa casella di controllo.  
  
 **Condizioni di controllo**  
 Selezionare la condizione della gestione basata su criteri utilizzata dai criteri correnti. Vengono elencate tutte le condizioni del server relative al facet della gestione basata su criteri associato. Fare clic su **Nuova condizione** per creare una nuova condizione. Fare clic sul pulsante con i puntini di sospensione ( **...** ) per modificarla.  
  
 **In base alle destinazioni**  
 Selezionare i tipi di destinazione disponibili per il facet per completare un'espressione di filtro.  
  
 **Modalità di valutazione**  
 Consente di selezionare la modalità di valutazione per i criteri. Alcuni criteri possono essere controllati ma non applicati. Di seguito vengono elencate le modalità di valutazione:  
  
 **Su richiesta**  
 I criteri verranno eseguiti solo se vengono avviati dalla finestra di dialogo **Valuta** .  
  
 **Su pianificazione**  
 I criteri vengono valutati periodicamente. Viene registrata una voce di log per i criteri non conformi e viene creato un report. La casella **Pianificazione** viene abilitata.  
  
 **Su modifica: solo log**  
 Quando l'utente tenta di apportare modifiche, questa opzione non impedisce le modifiche non conformi, ma registra le violazioni dei criteri.  
  
 **Su modifica: impedisci esecuzione**  
 Quando l'utente tenta di apportare modifiche, questa opzione impedisce le modifiche che violerebbero i criteri.  
  
 **Pianificare**  
 Questa opzione viene visualizzata quando è selezionata la modalità di valutazione **Su pianificazione** . Digitare il nome della pianificazione, fare clic su **Seleziona** per effettuare una selezione da un elenco oppure scegliere **Nuova** per creare una nuova pianificazione. Per abilitare l'area di pianificazione, è necessario che l'opzione **Su pianificazione** sia selezionata.  
  
 **Restrizione server**  
 Selezionare i tipi di server appropriati per i criteri. Le opzioni disponibili sono **Nessuno** o la selezione di una condizione che filtra i server possibili.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
