---
title: Selezionare un account per il servizio SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- roles [SQL Server], SQL Server Agent
- SQL Server Agent, accounts
- startup accounts [SQL Server]
- SQL Server Agent service, accounts
- accounts [SQL Server], SQL Server Agent
- Windows groups [SQL Server Agent]
- SQL Server Agent, permissions
- members [SQL Server], SQL Server Agent service
- Windows domain accounts [SQL Server]
- security [SQL Server], SQL Server Agent
ms.assetid: fe658e32-9e6b-4147-a189-7adc3bd28fe7
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b65cb9f218d5ad1ba9fc98a80b007ba39e22a2f0
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67685186"
---
# <a name="select-an-account-for-the-sql-server-agent-service"></a>Selezionare un account per il servizio SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

L'account di avvio del servizio definisce l'account di [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows in cui viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, nonché le relative autorizzazioni di rete. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene eseguito con un account utente specificato. Selezionare un account per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , in cui è possibile scegliere tra le opzioni seguenti:  
  
-   **Account predefinito**. è possibile scegliere da un elenco di account di servizio Windows predefiniti riportati di seguito:  
  
    -   Account di**sistema locale** . il nome di questo account è NT AUTHORITY\System. Si tratta di un account potente con accesso illimitato a tutte le risorse del sistema locale. Questo account è membro del gruppo **Administrators** di Windows nel computer locale e, di conseguenza, anche del ruolo predefinito del server **sysadmin** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
        > [!IMPORTANT]  
        > L'opzione **Account di sistema locale** deve essere usata esclusivamente per garantire la compatibilità con le versioni precedenti. L'account di sistema locale dispone di autorizzazioni non necessarie per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Evitare di eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con l'account di sistema locale. Per migliorare la sicurezza, utilizzare un account di dominio di Windows con le autorizzazioni elencate nella sezione seguente, "Autorizzazioni dell'account di dominio di Windows".  
  
-   **Account seguente**. Consente di specificare l'account di dominio di Windows utilizzato per l'esecuzione del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. È consigliabile scegliere un account utente di Windows che non sia un membro del gruppo **Administrators** di Windows. Esistono tuttavia alcune limitazioni all'uso dell'amministrazione multiserver quando l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non è un membro del gruppo **Administrators** locale. Per ulteriori informazioni, vedere 'Tipi di account del servizio supportati' più avanti in questo argomento.  
  
## <a name="windows-domain-account-permissions"></a>Autorizzazioni dell'account di dominio di Windows  
Per migliorare la sicurezza, selezionare l'opzione **Account seguente**che consente di specificare un account di dominio di Windows. L'account di dominio di Windows specificato deve disporre delle autorizzazioni seguenti:  
  
-   In tutte le versioni di Windows è necessario disporre dell'autorizzazione per l'accesso come servizio (SeServiceLogonRight).  
  
> [!NOTE]  
> L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere membro del gruppo Accesso compatibile precedente a Windows 2000 nel controller di dominio. In caso contrario, i processi di proprietà di utenti di dominio che non sono membri del gruppo Administrators di Windows non verranno eseguiti.  
  
-   Nei server Windows, l'account con cui viene eseguito il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede le autorizzazioni seguenti per supportare i proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:  
  
    -   Autorizzazione a ignorare i controlli di attraversamento (SeChangeNotifyPrivilege)  
  
    -   Autorizzazione a sostituire un token a livello di processo (SeAssignPrimaryTokenPrivilege)  
  
    -   Autorizzazione a modificare le quote di memoria per un processo (SeIncreaseQuotaPrivilege)  
  
    -   Autorizzazione per l'accesso a questo computer dalla rete (SeNetworkLogonRight)  
  
> [!NOTE]  
> Se l'account non dispone delle autorizzazioni necessarie per supportare i proxy, solo i membri del ruolo predefinito del server **sysadmin** possono creare i processi.  
  
> [!NOTE]  
> Per ricevere una notifica di avviso WMI, è necessario che l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent abbia ricevuto l'autorizzazione per lo spazio dei nomi che contiene gli eventi WMI e disponga dell'autorizzazione ALTER ANY EVENT NOTIFICATION.  
  
## <a name="sql-server-role-membership"></a>Appartenenze ai ruoli di SQL Server  
L'account utilizzato per l'esecuzione del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un membro dei seguenti ruoli di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   L'account deve essere membro del ruolo predefinito del server **sysadmin** .  
  
-   Per usare l'elaborazione dei processi multiserver, l'account deve essere membro del ruolo **TargetServersRole** del database **msdb** nel server master.  
  
## <a name="supported-service-account-types"></a>Tipi di account di servizio supportati  
Nella tabella seguente vengono elencati i tipi di account di Windows che possono essere utilizzati per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Tipo di account di servizio|Server non di cluster|Server di cluster|Controller di dominio (non di cluster)|  
|------------------------|-------------------------|--------------------|--------------------------------------|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)] Account di dominio di Windows (membro del gruppo Administrators di Windows)|Supportato|Supportato|Supportato|  
|Account di dominio di Windows (non amministrativo)|Supportato<br /><br />Vedere Limitazione 1 di seguito.|Supportato<br /><br />Vedere Limitazione 1 di seguito.|Supportato<br /><br />Vedere Limitazione 1 di seguito.|  
|Account Servizio di rete (NT AUTHORITY\NetworkService)|Supportato<br /><br />Vedere Limitazione 1, 3 e 4 di seguito.|Non supportato|Non supportato|  
|Account Utente locale (non amministrativo)|Supportato<br /><br />Vedere Limitazione 1 di seguito.|Non supportato|Non applicabile|  
|Account Sistema locale (NT AUTHORITY\System)|Supportato<br /><br />Vedere Limitazione 2 di seguito.|Non supportato|Supportato<br /><br />Vedere Limitazione 2 di seguito.|  
|Account Servizio locale (NT AUTHORITY\NetworkService)|Non supportato|Non supportato|Non supportato|  
  
### <a name="limitation-1-using-non-administrative-accounts-for-multiserver-administration"></a>Limitazione 1: uso di account non amministrativi per l'amministrazione multiserver  
È possibile che l'integrazione nei server di destinazione non riesca e venga visualizzato il messaggio di errore "Operazione di integrazione non riuscita".  
  
Per risolvere il problema, riavviare i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per altre informazioni, vedere [Avviare, arrestare, sospendere, riprendere, riavviare i servizi SQL Server](https://msdn.microsoft.com/32660a02-e5a1-411a-9e57-7066ca459df6).  
  
### <a name="limitation-2-using-the-local-system-account-for-multiserver-administration"></a>Limitazione 2: uso dell'account Sistema locale per l'amministrazione multiserver  
Quando il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene eseguito con l'account Sistema locale, l'amministrazione multiserver è supportata solo quando sia il server master che il server di destinazione risiedono sullo stesso computer. Se si utilizza questa configurazione, quando si integrano i server di destinazione nel server master viene restituito il messaggio seguente:  
  
"Verifica che l'account di avvio dell'agente per *<target_server_computer_name>* disponga dei diritti per l'accesso come server di destinazione".  
  
Questo messaggio può essere ignorato. L'operazione di integrazione verrà completata correttamente. Per altre informazioni, vedere [Creare un ambiente multiserver](../../ssms/agent/create-a-multiserver-environment.md).  
  
### <a name="limitation-3-using-the-network-service-account-when-it-is-a-sql-server-user"></a>Limitazione 3: uso dell'account Servizio di rete quando è un utente di SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent potrebbe non essere avviato correttamente se si esegue il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con l'account Servizio di rete e a quest'ultimo è stato esplicitamente consentito l'accesso a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Per risolvere il problema, riavviare il computer in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione. È necessario eseguire questa operazione una sola volta.  
  
### <a name="limitation-4-using-the-network-service-account-when-sql-server-reporting-services-is-running-on-the-same-computer"></a>Limitazione 4: uso dell'account Servizio di rete quando SQL Server Reporting Services è in esecuzione nello stesso computer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent potrebbe non essere avviato correttamente se si esegue il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con l'account Servizio di rete sullo stesso computer in cui viene eseguito anche [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
Per risolvere il problema, riavviare il computer in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione, quindi riavviare sia il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. È necessario eseguire questa operazione una sola volta.  
  
## <a name="common-tasks"></a>Attività comuni  
**Per specificare l'account di avvio del servizio SQL Server Agent**  
  
-   [Impostazione dell'account di avvio del servizio SQL Server Agent &#40;Gestione configurazione SQL Server&#41;](../../ssms/agent/set-service-startup-account-sql-server-agent-sql-server-configuration-manager.md)  
  
**Per specificare il profilo di posta di SQL Server Agent**  
  
-   [Procedura: Configurare Posta elettronica di SQL Server Agent per l'uso di Posta elettronica database (SQL Server Management Studio)](https://msdn.microsoft.com/4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce)  
  
> [!NOTE]  
> Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di specificare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere avviato all'avvio del sistema operativo.  
  
## <a name="see-also"></a>Vedere anche  
[Impostazione di account di servizio Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
[Gestione dei servizi mediante Gestione SQL Server](https://msdn.microsoft.com/78dee169-df0c-4c95-9af7-bf033bc9fdc6)  
[Implementazione della sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
