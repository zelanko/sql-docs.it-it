---
title: Ruoli-attività di Reporting Services e autorizzazioni-gruppi di SharePoint | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- security [Reporting Services], tasks
- roles [Reporting Services], predefined
- SharePoint integration [Reporting Services], permissions
- permissions [Reporting Services], native mode
- security [Reporting Services], predefined roles
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 429f1dbb-183a-4097-bd1b-693da9fe7a36
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 091cdef1316ace27dd2928fb9c263cbc19ea0e61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570840"
---
# <a name="reporting-services-roles-tasks-vs-sharepoint-groups-permissions"></a>Ruoli-attività di Reporting Services e autorizzazioni-gruppi di SharePoint
  In questo argomento vengono confrontate le funzionalità di autorizzazione basata su ruoli e attività nella modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con le funzionalità di sicurezza dei prodotti SharePoint. In questo argomento vengono confrontate la terminologia e le caratteristiche di ruoli, attività, gruppi di SharePoint, livelli di autorizzazione e autorizzazioni.  
  
||  
|-|  
| [!INCLUDE[applies](../../includes/applies-md.md)]<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità SharePoint &#124; SharePoint 2010 e SharePoint 2013<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa|  
  
 **Contenuto dell'argomento:**  
  
-   [Confrontare strumenti di autorizzazione e terminologia](#bkmk_compare_tools_terms)  
  
-   [Confrontare ruoli in modalità nativa e gruppi di SharePoint](#bkmk_compare_roles_groups)  
  
-   [Confrontare attività in modalità nativa e autorizzazioni di SharePoint](#bkmk_compare_tasks_permissions)  
  
##  <a name="bkmk_compare_tools_terms"></a> Confrontare strumenti di autorizzazione e terminologia  
 **Modalità nativa** : gli oggetti di autorizzazione (ruoli e attività) in modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vengono creati in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e configurati per i singoli utenti in Gestione report.  
  
 **Modalità SharePoint** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vengono usate le funzionalità di autorizzazione di SharePoint. I gruppi e le autorizzazioni di SharePoint vengono gestiti dalla seguente pagina **Impostazioni sito** .  
  
 Nella tabella seguente vengono confrontati gli oggetti e i concetti correlati all'autorizzazione tra la modalità SharePoint e nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa|SharePoint|  
|---------------------------------------------|----------------|  
|**Ruolo**: ad esempio "Gestione contenuto".|**Gruppo**: ad esempio il gruppo predefinito "Visualizzatori".|  
|---|**Gruppo livelli di autorizzazione**: ad esempio "Solo visualizzazione" per il gruppo "Visualizzatori".|  
|**Attività**: ad esempio "Gestione di report".|**Autorizzazioni**: ad esempio, nel gruppo "Solo visualizzazione" sono presenti autorizzazioni correlate all'elenco come Visualizzazione elementi, Visualizzazione versioni e Visualizzazione pagine applicazione.|  
  
 Per ulteriori informazioni sulle autorizzazioni di SharePoint, vedere [Livelli di autorizzazione e autorizzazioni](https://support.office.com/en-us/article/Understand-groups-and-permissions-on-a-SharePoint-site-258E5F33-1B5A-4766-A503-D86655CF950D) e [Determinare i livelli di autorizzazione e i gruppi in SharePoint 2013](https://technet.microsoft.com/library/cc262690.aspx).  
  
##  <a name="bkmk_compare_roles_groups"></a> Confrontare ruoli in modalità nativa e gruppi di SharePoint  
 Nella tabella seguente vengono confrontate le definizioni di ruolo predefinito in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa con i gruppi di SharePoint standard. Se i gruppi di SharePoint non corrispondono al ruolo specifico desiderato, è possibile creare un gruppo personalizzato e assegnarvi livelli di autorizzazione in SharePoint.  
  
 **Nota**: i gruppi di SharePoint predefiniti disponibili dipendono dal modello di sito utilizzato per creare il sito di SharePoint.  
  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Ruolo|Gruppi di SharePoint|  
|--------------------------------------|-----------------------|  
|**Browser**<br /><br /> Vista|Utilizzare il gruppo **Visitatori** per concedere le autorizzazioni necessarie per visualizzare i report. Il gruppo **Visitatori** dispone di autorizzazioni a livello di lettura che consentono ai membri di un gruppo di visualizzare pagine, elementi di elenco e documenti.|  
|**Gestione contenuto**<br /><br /> Autorizzazioni complete per tutti gli elementi e le operazioni a livello di elemento, incluse le autorizzazioni per l'impostazione della sicurezza.|Utilizzare il gruppo **Proprietari** per concedere controllo completo sulla gestione degli elementi del server di report in un sito di SharePoint. Il gruppo **Proprietari** dispone di autorizzazioni di controllo completo che consentono di apportare modifiche al contenuto, alle pagine o alle funzionalità del sito. È consigliabile che l'accesso con controllo completo sia limitato agli amministratori del sito.|  
|**Report personali**|Nessun gruppo equivalente. **Report personali** non è supportato nei server di report eseguiti in modalità SharePoint. Se si desidera utilizzare funzionalità equivalenti, è possibile utilizzare quelle di Sito personale in [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] .|  
|**Server di pubblicazione**<br /><br /> Consente di aggiungere, aggiornare, visualizzare ed eliminare report, modelli di report, origini dei dati condivise e risorse.|Utilizzare il gruppo **Membri** per concedere le autorizzazioni necessarie per aggiungere e modificare elementi e aggiornare i riferimenti a elementi dipendenti in un sito di SharePoint. Il gruppo **Membri** dispone delle autorizzazioni di livello Collaborazione, che consentono ai membri del gruppo di visualizzare le pagine, aggiungere e aggiornare elementi, nonché inviare richieste di approvazione delle modifiche.|  
|**Generatore report**<br /><br /> Consente di visualizzare report, gestire in autonomia sottoscrizioni individuali e aprire report in Generatore report.|Non sono disponibili livelli di autorizzazione o gruppi di SharePoint predefiniti già predisposti equivalenti alla definizione di report di Generatore report. Per impostazione predefinita, gli utenti che appartengono al gruppo **Membri** o al gruppo **Proprietari** dispongono dell'autorizzazione per utilizzare Generatore report. Se si desidera rendere Generatore report disponibile a più utenti, è necessario creare impostazioni di sicurezza personalizzate in grado di offrire un livello di autorizzazione analogo a quello del ruolo Generatore report. Per altre informazioni, vedere [Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md).|  
|-|Utilizzare il gruppo **Visualizzatori** per concedere le autorizzazioni necessarie per visualizzare i report visualizzabili. Tramite il gruppo **Visualizzatori** non è possibile scaricare né visualizzare il contenuto degli elementi del report.<br /><br /> **Nota:** a partire da SQL Server 2012 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], il gruppo **Visualizzatori** non dispone di autorizzazioni per la creazione di sottoscrizioni.|  
|**Utente sistema** e **Amministratore sistema**|Questi ruoli non sono necessari per un server di report eseguito in modalità SharePoint. **Utente sistema** e **Amministratore sistema** corrispondono a autorizzazioni a livello di applicazione Web o farm di SharePoint. Il server di report non include alcuna funzionalità per la quale siano necessarie autorizzazioni a tale livello.|  
  
##  <a name="bkmk_compare_tasks_permissions"></a> Confrontare attività in modalità nativa e autorizzazioni di SharePoint  
 Nella tabella seguente vengono confrontate le attività in modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con le autorizzazioni di SharePoint. Nella colonna **Tipo** è indicato se l'attività in modalità nativa è correlata a un ruolo di sistema o a un ruolo ed elementi standard. Tramite i ruoli di sistema è possibile gestire le autorizzazioni a livello di sistema, ad esempio le pianificazioni condivise.  
  
|Attività in modalità nativa|Tipo di ruolo|Autorizzazione di SharePoint equivalente|  
|----------------------|---------------|--------------------------------------|  
|Utilizzo di report|Elemento|Modifica elementi, Visualizzazione elementi.|  
|Creazione di report collegati|Elemento|Non supportato.|  
|Gestione di tutte le sottoscrizioni|Elemento|Gestione avvisi.|  
|Gestione di origini dei dati|Elemento|Aggiunta elementi, Modifica elementi, Eliminazione elementi, Visualizzazione elementi.|  
|Gestione di cartelle|Elemento|Aggiunta elementi, Modifica elementi, Eliminazione elementi, Visualizzazione elementi.|  
|Gestione di sottoscrizioni individuali|Elemento|Modifica elementi<br /><br /> Prima di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], il livello di autorizzazione era Creazione avvisi.|  
|Gestione di modelli|Elemento|Aggiunta elementi, Modifica elementi, Eliminazione elementi, Visualizzazione elementi.|  
|Gestione della cronologia dei report|Elemento|Modifica elementi, Visualizzazione versione, Eliminazione versioni.|  
|Gestione di report|Elemento|Aggiunta elementi, Modifica elementi, Eliminazione elementi, Visualizzazione elementi.|  
|Gestione di risorse|Elemento|Aggiunta elementi, Modifica elementi, Eliminazione elementi, Visualizzazione elementi.|  
|Impostazione della sicurezza per singoli elementi|Elemento|Gestione autorizzazioni|  
|Visualizzazione di origini dei dati|Elemento|Visualizzazione elementi.|  
|Visualizzazione di cartelle|Elemento|Visualizzazione elementi.|  
|Visualizzazione di modelli|Elemento|Visualizzazione elementi.|  
|Visualizzazione di report|Elemento|Visualizzazione elementi.|  
|Visualizzazione di risorse|Elemento|Visualizzazione elementi.|  
||||  
|Esecuzione delle definizioni dei report|Sistema|Visualizzazione elementi.|  
|Generazione di eventi|Sistema|Gestione sito Web.|  
|Gestisci processi|Sistema|Nessuna (non supportata).|  
|Gestione delle proprietà del server di report|Sistema|Nessuna (non applicabile). Il server di report non controlla se un utente dispone di autorizzazioni per la visualizzazione delle impostazioni di integrazione in Amministrazione centrale.|  
|Gestione di ruoli|Di sistema|Gestione autorizzazioni.|  
|Gestione di pianificazioni condivise|Sistema|Gestione sito Web, Apertura.|  
|Gestione della sicurezza del server di report|Sistema|Nessuna (non applicabile). Il server di report non utilizza assegnazioni di ruolo a livello di sistema in un server eseguito in modalità integrata SharePoint.|  
|Visualizzazione delle proprietà del server di report|Sistema|Nessuna (non applicabile). Il server di report non controlla se un utente dispone di autorizzazioni per la visualizzazione delle impostazioni di integrazione in Amministrazione centrale.|  
|Visualizzazione di pianificazioni condivise|Sistema|Apertura elementi.|  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare autorizzazioni per gli elementi del server di report in un sito di SharePoint &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)   
 [Impostare le autorizzazioni per le operazioni del server di report in un'applicazione Web di SharePoint](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Definizioni di ruolo](../../reporting-services/security/role-definitions.md)   
 [Predefined Roles](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
