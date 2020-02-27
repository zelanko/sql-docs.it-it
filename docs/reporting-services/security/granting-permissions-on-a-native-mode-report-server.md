---
title: Concessione di autorizzazioni in un server di report in modalità nativa | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- authorization [Reporting Services]
- server security [Reporting Services]
- role-based security [Reporting Services]
- items [Reporting Services], security
- permissions [Reporting Services], native mode
- published reports [Reporting Services], security
- reports [Reporting Services], security
- report items [Reporting Services], security
- role-based security [Reporting Services], about role-based security
- security [Reporting Services], role-based
ms.assetid: 260dc2e9-546c-4f04-9fa1-977e23c9d68c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: be6b0825244dee9f80f88a1b211eee5881d2a96a
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2020
ms.locfileid: "77147370"
---
# <a name="grant-permissions-on-a-native-mode-report-server"></a>Concessione di autorizzazioni in un server di report in modalità nativa
  In SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si utilizzano l'autorizzazione basata sui ruoli e un sottosistema di autenticazione per determinare gli utenti cui è consentito eseguire operazioni e accedere agli elementi in un server di report. L'autorizzazione basata sui ruoli consente di suddividere in ruoli il set di azioni che un utente può eseguire. L'autenticazione è basata sull'autenticazione di Windows incorporata o su un modulo di autenticazione personalizzato fornito dall'utente. È possibile utilizzare ruoli predefiniti o personalizzati con entrambi i tipi di autenticazione.
  
## <a name="use-roles-to-grant-report-server-access"></a>Usare i ruoli per concedere l'accesso al server di report
 Tutti gli utenti interagiscono con un server di report all'interno del contesto di un ruolo che definisce un livello specifico di accesso. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono inclusi ruoli predefiniti che è possibile assegnare a utenti e gruppi per fornire accesso immediato a un server di report. **Gestione contenuto**, **Pubblicazione** e **Visualizzazione** sono esempi di ruoli predefiniti. Ogni ruolo definisce una raccolta di attività correlate. Ad esempio, il ruolo **Pubblicazione** dispone di autorizzazioni per aggiungere report e creare cartelle in cui archiviarli.
  
 Le assegnazioni di ruolo vengono in genere ereditate da un nodo padre, ma è possibile interrompere l'ereditarietà delle autorizzazioni creando una nuova assegnazione di ruolo per un determinato elemento. Un utente membro del ruolo **Gestione contenuto** per un report può essere membro del ruolo **Visualizzazione** per un altro report.
  
 Per concedere l'accesso a operazioni ed elementi del server di report:
  
1. Rivedere i ruoli predefiniti per determinare se è possibile utilizzarli così come sono. Se è necessario modificare le attività o definire ruoli aggiuntivi, eseguire queste azioni prima di assegnare gli utenti a ruoli specifici. Per altre informazioni su ogni ruolo, vedere [Ruoli predefiniti](../../reporting-services/security/role-definitions-predefined-roles.md).
  
1. Individuare gli utenti e i gruppi che devono accedere al server di report e il livello di autorizzazioni richiesto. Assegnare la maggior parte degli utenti al ruolo **Visualizzazione** o al ruolo **Generatore report**. Assegnare un numero minore di utenti al ruolo **Pubblicazione**. Assegnare solo alcuni utenti al ruolo **Gestione contenuto**.
  
1. Usare il portale Web per assegnare i ruoli nella cartella Home per ogni utente o gruppo che richiede l'accesso. La cartella Home è la cartella di livello superiore della gerarchia di cartelle del server di report.
  
1. A questo livello del sito, nella pagina **Impostazioni sito** del portale Web, creare un'assegnazione di ruolo a livello di sistema per ogni utente e gruppo usando i ruoli predefiniti **Utente sistema** e **Amministratore sistema**.
  
1. Creare assegnazioni di ruolo aggiuntive secondo necessità per cartelle, report e altri elementi specifici. Evitare di creare un numero elevato di assegnazioni di ruolo. Se si creano troppi ruoli, è difficile tenere traccia dei diversi livelli di autorizzazione per ogni utente.
  
> [!NOTE]  
>  Se il server di report è configurato per l'integrazione con SharePoint, è necessario impostare le autorizzazioni nel sito di SharePoint per concedere l'accesso agli elementi del server di report. Per altre informazioni, vedere [Concedere autorizzazioni per elementi del server di report in un sito di SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md).
> 
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.
  
## <a name="who-sets-permissions"></a>Responsabili dell'impostazione delle autorizzazioni
 Inizialmente, solo gli utenti che sono membri del gruppo Administrators locale possono accedere a un server di report. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene installato con due assegnazioni di ruolo predefinite che concedono l'accesso a livello di elemento e a livello di sistema ai membri del gruppo Administrators locale. Gli amministratori locali possono usare queste assegnazioni di ruolo predefinite per concedere l'accesso al server di report ad altri utenti e gestire gli elementi del server di report. Le assegnazioni di ruolo predefinite non possono essere eliminate. Un amministratore locale dispone sempre delle autorizzazioni per la gestione completa di un'istanza del server di report.
 
 Prima di poter amministrare un'istanza del server di report in un computer locale che esegue Windows Vista o Windows Server 2008, sarà necessario eseguire passaggi di configurazione aggiuntivi. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).
  
## <a name="how-permissions-are-stored"></a>Archiviazione delle autorizzazioni
 Le assegnazioni e le definizioni di ruolo vengono archiviate nel database del server di report. Se si usano svariati strumenti client o interfacce di programmazione, ogni accesso è soggetto alle autorizzazioni definite per l'istanza del server di report nell'insieme. Se si configurano più server di report in una distribuzione con scalabilità orizzontale, le assegnazioni di ruolo definite in un'istanza vengono archiviate in un database condiviso e usate da tutte le altre istanze nella stessa distribuzione con scalabilità orizzontale. Poiché le assegnazioni di ruolo sono archiviate con gli elementi che proteggono, è possibile spostare il database in un'altra istanza del server di report senza perdere le autorizzazioni definite.
  
## <a name="tasks-and-tools-for-managing-permissions"></a>Attività e strumenti per la gestione delle autorizzazioni
 Per gestire le definizioni e le assegnazioni di ruolo, utilizzare gli strumenti seguenti.
  
|Strumento|Attività|  
|----------|-----------|  
|Management Studio: consente di visualizzare, modificare, creare ed eliminare definizioni di ruolo|[Creare, eliminare o modificare un ruolo &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)|  
|Portale Web: consente di assegnare i ruoli a utenti e gruppi|[Concedere l'accesso utente a un server di report](../../reporting-services/security/grant-user-access-to-a-report-server.md)<br /><br /> [Modificare o eliminare un'assegnazione di ruolo](../../reporting-services/security/role-assignments-modify-or-delete.md)|  
  
## <a name="see-also"></a>Vedere anche
 - [Ruoli predefiniti](../../reporting-services/security/role-definitions-predefined-roles.md)  
 - [Concedere autorizzazioni per elementi del server di report in un sito di SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 - [Autenticazione con il server di report](../../reporting-services/security/authentication-with-the-report-server.md)  
 - [Creare e gestire le assegnazioni di ruoli](../../reporting-services/security/create-and-manage-role-assignments.md)  
 - [Sicurezza e protezione di Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md)  
 - [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
