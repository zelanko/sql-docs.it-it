---
title: Configurazione superficie di attacco | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- reducing attackable surface area
- upgrading SQL Server, security
- surface area configuration [SQL Server]
- surface area configuration [SQL Server], about surface area configuration
- attackable surface area [SQL Server]
- installing SQL Server, security
ms.assetid: f741169c-1453-4ad2-830b-bf2be27d712f
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 811db11aecb5e6c0f4c68d272040aea3f8e38ca4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63184533"
---
# <a name="surface-area-configuration"></a>Configurazione superficie di attacco
  Nella configurazione predefinita delle nuove installazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]molte funzionalità non sono abilitate. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installa in modo selettivo e avvia solo le funzionalità e i servizi chiave in modo da ridurre al minimo il numero di funzionalità che potrebbero essere attaccate da un utente malintenzionato. L'amministratore di sistema può modificare i valori predefiniti al momento dell'installazione e abilitare o disabilitare in modo selettivo le caratteristiche di un'istanza in esecuzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Alcuni componenti, inoltre, potrebbero non essere disponibili durante la connessione da altri computer fino a quando non si configurano i protocolli.  
  
> [!NOTE]  
>  Diversamente dalle nuove installazioni, durante un aggiornamento non è disabilitato alcun servizio o caratteristica esistente, ma è possibile applicare opzioni di configurazione della superficie di attacco aggiuntive al termine dell'aggiornamento.  
  
## <a name="protocols-connection-and-startup-options"></a>Protocolli e opzioni di connessione e avvio  
 Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di avviare e arrestare servizi, configurare le opzioni di avvio e abilitare protocolli e altre opzioni di connessione.  
  
#### <a name="to-start-sql-server-configuration-manager"></a>Per avviare Gestione configurazione SQL Server  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
    -   Usare l'area **Servizi di SQL Server** per avviare i componenti e configurare le opzioni iniziali automatiche.  
  
    -   Usare l'area **Configurazione di rete SQL Server** per abilitare protocolli e opzioni di connessione, ad esempio le porte TCP/IP fisse, o per forzare la crittografia.  
  
 Per altre informazioni, vedere [Gestione configurazione SQL Server](../sql-server-configuration-manager.md). La connettività remota può dipendere anche dalla corretta configurazione di un firewall. Per altre informazioni, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="enabling-and-disabling-features"></a>Abilitazione e disabilitazione di caratteristiche  
 L'abilitazione e la disabilitazione delle caratteristiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere configurata tramite facet in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-configure-surface-area-using-facets"></a>Per configurare la superficie di attacco tramite facet  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] connettersi a un componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  In Esplora oggetti fare clic con il pulsante destro del mouse sul server, quindi scegliere **Facet**.  
  
3.  Nella finestra di dialogo **Visualizza facet** espandere l'elenco **Facet** e selezionare il facet **Surface Area Configuration** appropriato tra**Configurazione superficie di attacco**, **Configurazione superficie di attacco per Analysis Services**o **Configurazione superficie di attacco per Reporting Services**.  
  
4.  Nell'area **Proprietà facet** selezionare i valori desiderati per ogni proprietà.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Per controllare periodicamente la configurazione di un facet, utilizzare la gestione basata su criteri. Per altre informazioni sulla gestione basata su criteri, vedere [Amministrazione di server tramite la gestione basata su criteri](../policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
 È possibile impostare le opzioni del [!INCLUDE[ssDE](../../includes/ssde-md.md)] anche tramite la stored procedure `sp_configure`. Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
 Per modificare la proprietà **EnableIntegrated Security** di [!INCLUDE[ssRS](../../includes/ssrs.md)], usare le impostazioni delle proprietà in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per modificare la proprietà **Pianificazione eventi e recapito report** e la proprietà **Accesso HTTP e servizi Web** , modificare il file di configurazione **RSReportServer.config** .  
  
## <a name="command-prompt-options"></a>Opzioni del prompt dei comandi  
 Usare il cmdlet **Invoke-PolicyEvaluation**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di PowerShell per richiamare i criteri di configurazione della superficie di attacco. Per altre informazioni, vedere [Utilizzo di cmdlet del motore di database](../../database-engine/use-the-database-engine-cmdlets.md).  
  
## <a name="soap-and-service-broker-endpoints"></a>Endpoint SOAP e di Service Broker  
 Per disabilitare gli endpoint, utilizzare la gestione basata su criteri. Per creare e modificare le proprietà degli endpoint, usare [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql) e [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql).  
  
## <a name="related-content"></a>Contenuto correlato  
 [Centro sicurezza per il motore di Database di SQL Server e il Database SQL di Azure](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
