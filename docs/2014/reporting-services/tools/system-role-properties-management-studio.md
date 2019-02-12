---
title: Proprietà ruolo a livello di sistema (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.systemroleproperties.f1
ms.assetid: 0210fc2a-74fb-41dd-8e39-4830047ec417
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3d19b145daaf3e599e96e6b4b02fac179b27e028
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019612"
---
# <a name="system-role-properties-management-studio"></a>Proprietà ruolo a livello di sistema (Management Studio)
  La pagina Ruoli a livello di sistema consente di visualizzare le definizioni di ruolo a livello di sistema attualmente definite per il server di report. Una definizione di ruolo a livello di sistema contiene una raccolta denominata di attività eseguite in relazione all'intero sito, anziché a un singolo elemento. Le definizioni di ruolo vengono assegnate a un utente o a gruppi per creare un'assegnazione di ruolo. Le attività indicate nella definizione di ruolo specificano le operazioni consentite per un utente o un gruppo.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] presenta due definizioni di ruolo di sistema predefiniti: **Amministratore di sistema** e **utente sistema**. Tali definizioni di ruolo possono essere personalizzate modificando l'elenco di attività oppure è possibile creare nuovi ruoli a livello di sistema per supportare combinazioni di attività diverse. Le modifiche apportate a una definizione di ruolo vengono propagate a tutte le assegnazioni di ruolo che includono tale definizione.  
  
> [!NOTE]  
>  Le assegnazioni di ruolo a livello di sistema vengono utilizzate solo in un server di report in esecuzione in modalità nativa. Se il server di report è configurato per l'integrazione con SharePoint, questa pagina non è disponibile.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di specificare il nome della definizione di ruolo a livello di sistema.  
  
 **Descrizione**  
 Consente di visualizzare una descrizione della definizione di ruolo a livello di sistema. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]la descrizione viene visualizzata solo in questa pagina. Gli utenti che visualizzano questo elemento tramite Gestione report potrebbero vedere questa descrizione durante l'esplorazione della gerarchia di cartelle.  
  
 **Attività**  
 Elenca tutte le attività di sistema che è possibile selezionare per la definizione di ruolo. È possibile aggiungere o rimuovere elementi dall'elenco di attività predefinite per specificare il modo in cui gli utenti accedono a un determinato elemento tramite questo ruolo. Non è possibile creare nuove attività, né modificare quelle esistenti.  
  
 **Descrizione**  
 Offre informazioni su ogni attività. Non è possibile modificare le descrizioni delle attività.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto del server di report in Management Studio](report-server-in-management-studio-f1-help.md)   
 [Attività a livello di sistema](../security/tasks-and-permissions-system-level-tasks.md)   
 [Attività e autorizzazioni](../security/tasks-and-permissions.md)   
 [Predefined Roles](../security/role-definitions-predefined-roles.md)  
  
  
