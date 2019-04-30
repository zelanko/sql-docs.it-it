---
title: Concessione di autorizzazioni in un server di report in modalità nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
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
manager: kfile
ms.openlocfilehash: 1188f0d5cb68a86b6e3f3305ec9b5a40e51a8d3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242464"
---
# <a name="granting-permissions-on-a-native-mode-report-server"></a>Concessione di autorizzazioni in un server di report in modalità nativa
  In SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si utilizzano l'autorizzazione basata sui ruoli e un sottosistema di autenticazione per determinare gli utenti cui è consentito eseguire operazioni e accedere agli elementi in un server di report. L'autorizzazione basata sui ruoli consente di suddividere in ruoli il set di azioni che un utente può eseguire. L'autenticazione è basata sull'autenticazione di Windows incorporata o su un modulo di autenticazione personalizzato fornito dall'utente. È possibile utilizzare ruoli predefiniti o personalizzati con entrambi i tipi di autenticazione.  
  
## <a name="using-roles-to-grant-report-server-access"></a>Utilizzo dei ruoli per concedere l'accesso al server di report  
 Tutti gli utenti interagiscono con un server di report all'interno del contesto di un ruolo che definisce un livello specifico di accesso. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono inclusi ruoli predefiniti che è possibile assegnare a utenti e gruppi per fornire accesso immediato a un server di report. **Gestione contenuto**, **Pubblicazione**e **Visualizzazione** sono esempi di ruoli predefiniti. Ogni ruolo definisce una raccolta di attività correlate. Ad esempio, il ruolo **Pubblicazione** dispone di autorizzazioni per aggiungere report e creare cartelle in cui archiviarli.  
  
 Le assegnazioni di ruolo vengono in genere ereditate da un nodo padre, ma è possibile interrompere l'ereditarietà delle autorizzazioni creando una nuova assegnazione di ruolo per un determinato elemento. Un utente membro del ruolo **Gestione contenuto** per un report può essere membro del ruolo **Visualizzazione** per un altro report.  
  
 Per concedere l'accesso agli elementi e alle operazioni per il server di report, attenersi alle indicazioni seguenti:  
  
1.  Rivedere i ruoli predefiniti per determinare se è possibile utilizzarli così come sono. Se è necessario modificare le attività o definire ruoli aggiuntivi, eseguire queste operazioni prima di iniziare ad assegnare gli utenti a ruoli specifici. Per altre informazioni su ogni ruolo, vedere [Predefined Roles](role-definitions-predefined-roles.md)(Ruoli predefiniti).  
  
2.  Individuare gli utenti e i gruppi che devono accedere al server di report e il livello di autorizzazioni richiesto. La maggior parte degli utenti dovrebbe essere assegnata al ruolo **Visualizzazione** o al ruolo **Generatore report** . Il ruolo **Server di pubblicazione** dovrebbe essere utilizzato per un numero più limitato di utenti. Il ruolo **Gestione contenuto**dovrebbe essere assegnato a pochissimi utenti.  
  
3.  Utilizzare Gestione report per assegnare ruoli nella cartella Home, ovvero la cartella di livello principale della gerarchia di cartelle del server di report.  
  
4.  A questo livello del sito, nella pagina Impostazioni sito di Gestione report, creare un'assegnazione di ruolo a livello di sistema per ogni utente e gruppo usando i ruoli predefiniti **Utente sistema** e **Amministratore sistema**.  
  
5.  Creare assegnazioni di ruolo aggiuntive secondo necessità per cartelle, report e altri elementi specifici. Evitare di creare un numero elevato di assegnazioni di ruolo. Se si creano troppi ruoli, sarà difficile tenere traccia dei diversi livelli di autorizzazione per ogni utente.  
  
> [!NOTE]  
>  Se il server di report è configurato per l'integrazione con SharePoint, è necessario impostare le autorizzazioni nel sito di SharePoint per concedere l'accesso agli elementi del server di report. Per altre informazioni, vedere [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md).  
  
## <a name="who-sets-permissions"></a>Responsabili dell'impostazione delle autorizzazioni  
 Inizialmente, solo gli utenti che sono membri del gruppo Administrators locale possono accedere a un server di report. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene installato con due assegnazioni di ruolo predefinite che concedono l'accesso a livello di elemento e a livello di sistema ai membri del gruppo Administrators locale. Con queste assegnazioni di ruolo incorporate, gli amministratori locali possono concedere l'acceso al server di report ad altri utenti e gestire gli elementi del server di report. Le assegnazioni di ruolo incorporate non possono essere eliminate. Un amministratore locale dispone sempre delle autorizzazioni per la gestione completa di un'istanza del server di report.  
  
 Poiché le autorizzazioni complete su un server di report includono autorizzazioni a livello di elemento e a livello di sistema, a un amministratore locale sono assegnati i ruoli seguenti:  
  
 Prima di poter amministrare un'istanza del server di report in un computer locale che esegue Windows Vista o Windows Server 2008, sarà necessario eseguire passaggi di configurazione aggiuntivi. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="how-permissions-are-stored"></a>Archiviazione delle autorizzazioni  
 Le assegnazioni e le definizioni di ruolo vengono archiviate nel database del server di report. Se si utilizza una varietà di strumenti client o interfacce di programmazione, ogni accesso è soggetto alle autorizzazioni definite per l'istanza del server di report nell'insieme. Se si configurano più server di report in una distribuzione con scalabilità orizzontale, le assegnazioni di ruolo definite in un'istanza vengono archiviate in un database condiviso e utilizzate da tutte le altre istanze nella stessa distribuzione con scalabilità orizzontale. Poiché le assegnazioni di ruolo sono archiviate con gli elementi che proteggono, è possibile spostare il database in un'altra istanza del server di report senza perdere le autorizzazioni definite.  
  
## <a name="tasks-and-tools-for-managing-permissions"></a>Attività e strumenti per la gestione delle autorizzazioni  
 Per gestire le definizioni e le assegnazioni di ruolo, utilizzare gli strumenti seguenti.  
  
|Strumento|Attività|  
|----------|-----------|  
|Management Studio: consente di visualizzare, modificare, creare ed eliminare definizioni di ruolo.|[Creare, eliminare o modificare un ruolo &#40;Management Studio&#41;](role-definitions-create-delete-or-modify.md)|  
|Gestione report: consente di assegnare utenti e gruppi a ruoli.|[Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](grant-user-access-to-a-report-server.md)<br /><br /> [Modificare o eliminare un'assegnazione di ruolo &#40;Gestione report&#41;](role-assignments-modify-or-delete.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Predefined Roles](role-definitions-predefined-roles.md)   
 [Concessione di autorizzazioni per elementi del server di report in un sito di SharePoint](granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Autenticazione con il server di report](authentication-with-the-report-server.md)   
 (create-and-manage-role-assignments.md)   
 [Sicurezza e protezione di Reporting Services](reporting-services-security-and-protection.md)   
 [Gestione contenuto del server di report &#40;modalità nativa SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
