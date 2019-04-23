---
title: Concessione dell'accesso utente a un Server di Report (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- removing role assignments
- permissions [Reporting Services], granting report server access
- roles [Reporting Services], assignments
- modifying role assignments
- deleting role assignments
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ebb42ac44d26e9ad8a091795eb3f8ab7283f6bcb
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59935857"
---
# <a name="grant-user-access-to-a-report-server-report-manager"></a>Concedere l'accesso utente a un server di report (Gestione report)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa la sicurezza basata sui ruoli per concedere agli utenti l'accesso a un server di report. In una nuova installazione del server di report, solo gli utenti che appartengono al gruppo Administrators locale dispongono delle autorizzazioni per accedere al contenuto ed eseguire operazioni sul server di report. Per rendere disponibile il server di report agli altri utenti, è necessario creare assegnazioni di ruolo che associano gli account utente o gli account di gruppo a un ruolo predefinito che specifica una raccolta di attività.  
  
 **Server di report in modalità SharePoint:** Per un server di report configurato per la modalità integrata SharePoint configurare l'accesso da un sito di SharePoint utilizzando le autorizzazioni di SharePoint. I livelli di autorizzazione sul sito di SharePoint determinano l'accesso al contenuto e alle operazioni del server di report. Per concedere le autorizzazioni a un sito di SharePoint, è necessario disporre dei privilegi di amministratore. Per altre informazioni, vedere [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md).  
  
 **Server di report in modalità nativa:** Questo argomento è incentrato su un server di report configurato per la modalità nativa e l'uso di gestione Report per assegnare gli utenti a un ruolo. Sono disponibili due tipi di ruoli:  
  
-   Ruoli a livello di elemento, utilizzati per visualizzare, aggiungere e gestire contenuto del server di report, sottoscrizioni, elaborazione e cronologia dei report. I ruoli a livello di elemento vengono definiti per il nodo radice, ovvero la cartella Home, oppure per cartelle o elementi specifici nei livelli inferiori della gerarchia.  
  
-   Ruoli a livello di sistema, che concedono l'accesso a un'ampia gamma di operazioni sul sito non associate ad alcun elemento specifico, ad esempio l'utilizzo di Generatore report e di pianificazioni condivise.  
  
     I due tipi di ruoli sono complementari e devono essere utilizzati insieme. Per questa ragione, l'aggiunta di un utente a un server di report è un'operazione suddivisa in due parti. Se si assegna un utente a un ruolo a livello di elemento, è necessario assegnarlo anche a un ruolo a livello di sistema. Quando si assegna un utente a un ruolo, è necessario selezionare un ruolo già definito. Per creare, modificare o eliminare ruoli, usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Per altre informazioni, vedere [Creare, eliminare o modificare un ruolo &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md).  
  
## <a name="before-you-start"></a>Prima di iniziare  
 Esaminare l'elenco seguente prima di aggiungere utenti a un server di report in modalità nativa.  
  
-   È necessario essere un membro del gruppo Administrators locale nel computer server di report. Se si distribuisce [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] o in Windows Server 2008, la configurazione aggiuntiva è obbligatoria per amministrare un server di report localmente. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
-   Per delegare questa attività ad altri utenti, creare assegnazioni di ruolo che eseguono il mapping degli account utente ai ruoli Gestione contenuto e Amministratore sistema. Gli utenti che dispongono di queste autorizzazioni possono aggiungere utenti a un server di report.  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]visualizzare i ruoli predefiniti per i ruoli a livello di sistema e i ruoli utente, in modo da acquisire familiarità con i tipi di attività previsti da ogni ruolo. Poiché le descrizioni dell'attività non sono visibili in Gestione report, è necessario conoscere i ruoli prima di iniziare ad aggiungere utenti.  
  
-   Facoltativamente, personalizzare i ruoli o definire ruoli aggiuntivi per includere la raccolta di attività necessarie. Se ad esempio si intende utilizzare impostazioni di sicurezza personalizzate per elementi singoli, è necessario creare una nuova definizione di ruolo che consenta di visualizzare le cartelle.  
  
### <a name="to-add-a-user-or-group-to-a-system-role"></a>Per aggiungere un utente o un gruppo a un ruolo a livello di sistema  
  
1.  Avviare [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md).  
  
2.  Fare clic su **Impostazioni sito**.  
  
3.  Fare clic su **Sicurezza**.  
  
4.  Fare clic su **Nuova assegnazione ruolo**.  
  
5.  Nelle **nome utente o gruppo**, immettere un utente di dominio Windows o il gruppo di account nel formato seguente: \<dominio >\\< account\>. Se si utilizza l'autenticazione basata su form o la sicurezza personalizzata, specificare l'account utente o di gruppo nel formato corretto per la propria distribuzione.  
  
6.  Selezionare un ruolo a livello di sistema e quindi fare clic su **OK**.  
  
     Poiché i ruoli sono cumulativi, se si seleziona sia Amministratore sistema che Utente sistema, un utente o un gruppo sarà in grado di eseguire le attività in entrambi ruoli.  
  
7.  Ripetere le operazioni per creare assegnazioni per utenti o gruppi aggiuntivi.  
  
### <a name="to-add-a-user-or-group-to-an-item-role"></a>Per aggiungere un utente o un gruppo a un ruolo a livello di elemento  
  
1.  Avviare **Gestione report** e individuare l'elemento del report per il quale si vuole aggiungere un utente o un gruppo.  
  
2.  Posizionare il puntatore del mouse sull'elemento, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Sicurezza**dal menu a discesa.  
  
4.  Fare clic su **Nuova assegnazione ruolo**.  
  
    > [!NOTE]  
    >  Se un elemento eredita le impostazioni di sicurezza da un elemento padre, fare clic su **Modifica sicurezza elemento** sulla barra degli strumenti per modificare le impostazioni di sicurezza. Fare quindi clic su **Nuova assegnazione ruolo**.  
  
5.  Nelle **nome utente o gruppo**, immettere un utente di dominio Windows o il gruppo di account nel formato seguente: \<dominio >\\< account\>. Se si utilizza l'autenticazione basata su form o la sicurezza personalizzata, specificare l'account utente o di gruppo nel formato corretto per la propria distribuzione.  
  
6.  Selezionare una o più definizioni di ruolo per descrivere la modalità di accesso all'elemento consentita all'utente o al gruppo e quindi fare clic su **OK**.  
  
7.  Ripetere le operazioni per creare assegnazioni per utenti o gruppi aggiuntivi.  
  
## <a name="see-also"></a>Vedere anche  
 (create-and-manage-role-assignments.md)   
 [Nuova assegnazione ruolo: Modifica assegnazione ruolo &#40;gestione Report&#41;](../new-role-assignment-edit-role-assignment-page-report-manager.md)   
 [Pagina delle proprietà sicurezza, Elementi&#40;Gestione report&#41;](../security-properties-page-items-report-manager.md)   
 [Assegnazioni di ruolo](role-assignments.md)   
 [Definizioni di ruolo](role-definitions.md)  
  
  
