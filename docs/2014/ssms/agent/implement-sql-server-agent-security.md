---
title: Implementare la sicurezza di SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, security
- security [SQL Server Agent], about security
- security [SQL Server Agent]
- security [SQL Server], SQL Server Agent
ms.assetid: d770d35c-c8de-4e00-9a85-7d03f45a0f0d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 52537ac126115fbde3d7d0fb1a13f61f1d25cf15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63137522"
---
# <a name="implement-sql-server-agent-security"></a>Implementazione della sicurezza di SQL Server Agent
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent consente all'amministratore del database di eseguire ciascun passaggio del processo in un contesto di sicurezza che dispone solo delle autorizzazioni necessarie per eseguire tale passaggio, determinato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un proxy di Agent. Per impostare le autorizzazioni per un particolare passaggio di un processo, è necessario creare un proxy che disponga delle autorizzazioni necessarie e quindi assegnare questo proxy al passaggio del processo. È possibile specificare un proxy per più di un passaggio di processo. Per i passaggi che richiedono le medesime autorizzazioni, viene utilizzato lo stesso proxy.  
  
 Nella sezione che segue viene spiegato quale ruolo di database concedere agli utenti affinché possano creare o eseguire processi utilizzando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="granting-access-to-sql-server-agent"></a>Concessione dell'accesso a SQL Server Agent  
 Per poter utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, l'utente deve essere membro di uno o più dei seguenti ruoli predefiniti di database:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Questi ruoli sono archiviati nel database **msdb** . Per impostazione predefinita, nessun utente è membro di questi ruoli di database. L'appartenenza a questi ruoli deve essere concessa esplicitamente. Gli utenti membri del ruolo di server predefinito **sysadmin** hanno accesso completo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e non hanno bisogno di essere membri di questi ruoli di database predefiniti per poter usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se un utente non è membro di uno di questi ruoli di database o del ruolo **sysadmin** , il nodo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non è disponibile quando l'utente si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 I membri di questi ruoli di database possono visualizzare ed eseguire processi di cui sono proprietari e possono creare passaggi di processo eseguibili come un account proxy esistente. Per altre informazioni sulle autorizzazioni specifiche associate a ognuno di questi ruoli, vedere [Ruoli di database predefiniti di SQL Server Agent](sql-server-agent-fixed-database-roles.md).  
  
 I membri del ruolo predefinito del server **sysadmin** sono autorizzati a creare, modificare ed eliminare account proxy. I membri del ruolo **sysadmin** sono autorizzati a creare passaggi di processo che non specificano un proxy ma che invece vengono eseguiti come account di servizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, vale a dire l'account usato per avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="guidelines"></a>Indicazioni  
 Per migliorare la sicurezza dell'implementazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, attenersi alle seguenti indicazioni generali:  
  
-   Creare appositi account utente dedicati per i proxy e utilizzare questi account solo per eseguire passaggi di processo.  
  
-   Concedere le autorizzazioni necessarie solo agli account utente proxy. Concedere solo le autorizzazioni effettivamente richieste per eseguire i passaggi di processo assegnati a un particolare account proxy.  
  
-   Non eseguire il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usando un account Microsoft Windows che è membro del gruppo **Administrators** di Windows.  
  
-   I proxy hanno lo stesso livello di sicurezza dell'archivio credenziali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Se le operazioni di scrittura dell'utente possono scrivere nel registro eventi NT, possono generare avvisi tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   Non specificare l'account amministratore NT come account di servizio o account proxy.  
  
-   Notare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent dispongono dell'accesso reciproco alle proprie risorse. I due servizi condividono un unico spazio di elaborazione e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è un sysadmin sul servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Quando un processo TSX viene integrato con un processo MSX, sysadmins di MSX assume il controllo totale dell'istanza TSX di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Il processo ACE è un'estensione e non può richiamare se stesso. ACE viene richiamato da Chainer ScenarioEngine.exe, anche noto come Microsoft.SqlServer.Chainer.Setup.exe, o può essere richiamato da un altro processo host.  
  
-   ACE dipende dalle DLL di configurazione seguenti di proprietà di SSDP, perché le API delle DLL vengono richiamate da ACE:  
  
    -   **SCO** -Microsoft. SqlServer. Configuration. sco. dll, incluse le nuove convalide SCO per gli account virtuali  
  
    -   **Cluster** -Microsoft. SqlServer. Configuration. cluster. dll  
  
    -   **SFC** -Microsoft. SqlServer. Configuration. SqlConfigBase. dll  
  
    -   **Estensione** -Microsoft. SqlServer. Configuration. ConfigExtension. dll  
  
## <a name="see-also"></a>Vedere anche  
 [Predefined Roles](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [sp_addrolemember &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)   
 [sp_droprolemember &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)   
 [Centro sicurezza per il motore di Database di SQL Server e il Database SQL di Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
