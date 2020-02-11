---
title: Selezionare un account per il servizio SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b2fd7a22c202b1210b17f86903fce32ec8d4b5b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68811077"
---
# <a name="select-an-account-for-the-sql-server-agent-service"></a>Selezionare un account per il servizio SQL Server Agent
  L'account di avvio del servizio definisce l'account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows in cui viene eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, nonché le relative autorizzazioni di rete. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene eseguito con un account utente specificato. Selezionare un account per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , in cui è possibile scegliere tra le opzioni seguenti:  
  
-   **Account predefinito**. è possibile scegliere da un elenco di account di servizio Windows predefiniti riportati di seguito:  
  
    -   Account **sistema locale** . il nome di questo account è NT AUTHORITY\System. Si tratta di un account potente con accesso illimitato a tutte le risorse del sistema locale. Questo account è membro del gruppo **Administrators** di Windows nel computer locale e, di conseguenza, anche del ruolo predefinito del server sysadmin[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** di **  
  
        > [!IMPORTANT]  
        >  L'opzione **Account di sistema locale** deve essere usata esclusivamente per garantire la compatibilità con le versioni precedenti. L'account di sistema locale dispone di autorizzazioni non necessarie per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Evitare di eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con l'account di sistema locale. Per migliorare la sicurezza, utilizzare un account di dominio di Windows con le autorizzazioni elencate nella sezione seguente, "Autorizzazioni dell'account di dominio di Windows".  
  
-   **Questo account**. Consente di specificare l'account di dominio di Windows utilizzato per l'esecuzione del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. È consigliabile scegliere un account utente di Windows che non sia un membro del gruppo **Administrators** di Windows. Esistono tuttavia alcune limitazioni all'uso dell'amministrazione multiserver quando l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent non è un membro del gruppo **Administrators** locale. Per ulteriori informazioni, vedere 'Tipi di account del servizio supportati' più avanti in questo argomento.  
  
## <a name="windows-domain-account-permissions"></a>Autorizzazioni dell'account di dominio di Windows  
 Per migliorare la sicurezza, selezionare l'opzione **Account seguente**che consente di specificare un account di dominio di Windows. L'account di dominio di Windows specificato deve disporre delle autorizzazioni seguenti:  
  
-   In tutte le versioni di Windows è necessario disporre dell'autorizzazione per l'accesso come servizio (SeServiceLogonRight).  
  
> [!NOTE]  
>  L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere membro del gruppo Accesso compatibile precedente a Windows 2000 nel controller di dominio. In caso contrario, i processi di proprietà di utenti di dominio che non sono membri del gruppo Administrators di Windows non verranno eseguiti.  
  
-   Nei server Windows, l'account con cui viene eseguito il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede le autorizzazioni seguenti per supportare i proxy di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent:  
  
    -   Autorizzazione a ignorare i controlli di attraversamento (SeChangeNotifyPrivilege)  
  
    -   Autorizzazione a sostituire un token a livello di processo (SeAssignPrimaryTokenPrivilege)  
  
    -   Autorizzazione a modificare le quote di memoria per un processo (SeIncreaseQuotaPrivilege)  
  
    -   Autorizzazione ad accedere tramite il tipo di accesso batch (SeBatchLogonRight)  
  
> [!NOTE]  
>  Se l'account non dispone delle autorizzazioni necessarie per supportare i proxy, solo i membri del ruolo predefinito del server **sysadmin** possono creare i processi.  
  
> [!NOTE]  
>  Per ricevere una notifica di avviso WMI, è necessario che l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent abbia ricevuto l'autorizzazione per lo spazio dei nomi che contiene gli eventi WMI e disponga dell'autorizzazione ALTER ANY EVENT NOTIFICATION.  
  
## <a name="sql-server-role-membership"></a>Appartenenze ai ruoli di SQL Server  
 L'account utilizzato per l'esecuzione del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere un membro dei seguenti ruoli di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   L'account deve essere membro del ruolo predefinito del server **sysadmin** .  
  
-   Per usare l'elaborazione dei processi multiserver, l'account deve essere membro del ruolo **TargetServersRole** del database **msdb** nel server master.  
  
## <a name="supported-service-account-types"></a>Tipi di account di servizio supportati  
 Nella tabella seguente vengono elencati i tipi di account di Windows che possono essere utilizzati per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
|Tipo di account di servizio|Server non cluster|Server di cluster|Controller di dominio (non cluster)|  
|--------------------------|---------------------------|----------------------|------------------------------------------|  
|
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Account di dominio di Windows (membro del gruppo Administrators di Windows)|Supportato|Supportato|Supportato|  
|Account di dominio di Windows (non amministrativo)|Supportato<sup>1</sup>|Supportato<sup>1</sup>|Supportato<sup>1</sup>|  
|Account Servizio di rete (NT AUTHORITY\NetworkService)|Supportato<sup>1, 3, 4</sup>|Non supportate|Non supportate|  
|Account Utente locale (non amministrativo)|Supportato<sup>1</sup>|Non supportate|Non applicabile|  
|Account Sistema locale (NT AUTHORITY\System)|Supportato<sup>2</sup>|Non supportate|Supportato<sup>2</sup>|  
|Account Servizio locale (NT AUTHORITY\NetworkService)|Non supportate|Non supportate|Non supportate|  
  
 <sup>1</sup> vedere la limitazione 1 riportata di seguito.  
  
 <sup>2</sup> vedere la limitazione 2 riportata di seguito.  
  
 <sup>3</sup> vedere la limitazione 3 riportata di seguito.  
  
 <sup>4</sup> vedere la limitazione 4 riportata di seguito.  
  
### <a name="limitation-1-using-non-administrative-accounts-for-multiserver-administration"></a>Limitazione 1: utilizzo di account non amministrativi per l'amministrazione multiserver  
 È possibile che l'integrazione nei server di destinazione non riesca e venga visualizzato il messaggio di errore "Operazione di integrazione non riuscita".  
  
 Per risolvere il problema, riavviare i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per altre informazioni, vedere [Avviare, arrestare, sospendere, riprendere, riavviare i servizi SQL Server](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
### <a name="limitation-2-using-the-local-system-account-for-multiserver-administration"></a>Limitazione 2: utilizzo dell'account Sistema locale per l'amministrazione multiserver  
 Quando il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene eseguito con l'account Sistema locale, l'amministrazione multiserver è supportata solo quando sia il server master che il server di destinazione risiedono sullo stesso computer. Se si utilizza questa configurazione, quando si integrano i server di destinazione nel server master viene restituito il messaggio seguente:  
  
 "Verifica che l'account di avvio dell'agente per *<target_server_computer_name>* disponga dei diritti per l'accesso come server di destinazione".  
  
 Questo messaggio può essere ignorato. L'operazione di integrazione verrà completata correttamente. Per altre informazioni, vedere [Creare un ambiente multiserver](create-a-multiserver-environment.md).  
  
### <a name="limitation-3-using-the-network-service-account-when-it-is-a-sql-server-user"></a>Limitazione 3: utilizzo dell'account Servizio di rete quando è un utente di SQL Server  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent potrebbe non essere avviato correttamente se si esegue il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con l'account Servizio di rete e a quest'ultimo è stato esplicitamente consentito l'accesso a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per risolvere il problema, riavviare il computer in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione. È necessario eseguire questa operazione una sola volta.  
  
### <a name="limitation-4-using-the-network-service-account-when-sql-server-reporting-services-is-running-on-the-same-computer"></a>Limitazione 4: utilizzo dell'account Servizio di rete quando SQL Server Reporting Services è in esecuzione sullo stesso computer  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent potrebbe non essere avviato correttamente se si esegue il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent con l'account Servizio di rete sullo stesso computer in cui viene eseguito anche [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Per risolvere il problema, riavviare il computer in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in esecuzione, quindi riavviare sia il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. È necessario eseguire questa operazione una sola volta.  
  
## <a name="common-tasks"></a>Attività comuni  
 **Per specificare l'account di avvio per il servizio SQL Server Agent**  
  
-   [Impostare l'account di avvio del servizio per SQL Server Agent &#40;Gestione configurazione SQL Server&#41;](set-service-startup-account-sql-server-agent-sql-server-configuration-manager.md)  
  
 **Per specificare il profilo di posta per SQL Server Agent**  
  
-   [Configurare Posta elettronica di SQL Server Agent per l'uso di Posta elettronica database](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
  
> [!NOTE]  
>  Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di specificare che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere avviato all'avvio del sistema operativo.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Procedure per la gestione dei servizi &#40;Gestione configurazione SQL Server&#41;](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)   
 [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md)  
  
  
