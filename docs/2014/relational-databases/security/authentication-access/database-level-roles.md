---
title: Ruoli a livello di database | Microsoft Docs
ms.custom: ''
ms.date: 09/22/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.database.f1
- sql12.swb.roleproperties.general.f1
- sql12.swb.roleproperties.object.f1
- SQL12.SWB.DBROLEPROPERTIES.GENERAL.F1
helpviewer_keywords:
- db_denydatareader role
- users [SQL Server], database roles
- database-level roles [SQL Server]
- db_denydatawriter role
- roles [SQL Server], database
- principals [SQL Server], database-level
- db_backupoperator role
- credentials [SQL Server], roles
- db_accessadmin role
- schemas [SQL Server], roles
- permissions [SQL Server], roles
- database roles [SQL Server], listed
- db_datareader role
- db_ddladmin role
- db_datawriter role
- db_securityadmin role
- db_owner role
- database roles [SQL Server]
- fixed database roles [SQL Server]
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: 7f3fa5f6-6b50-43bb-9047-1544ade55e39
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3df05bddf37970ce0ff0d796bc2b5d93d309b4dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63011728"
---
# <a name="database-level-roles"></a>Ruoli a livello di database
  Per una facile gestione delle autorizzazioni dei database, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornisce diversi *ruoli* rappresentanti entità di sicurezza all'interno delle quali sono raggruppate altre entità. I ruoli sono analoghi ai ***gruppi*** nel sistema operativo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. L'ambito delle autorizzazioni dei ruoli a livello di database è l'intero database.  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]sono disponibili due tipi di ruoli a livello di database, ovvero i *ruoli predefiniti di database* e i *ruoli flessibili di database* . Questi ultimi possono essere creati dall'utente.  
  
 I ruoli predefiniti di database vengono definiti a livello del database e sono presenti in ogni database. I membri del ruolo del database **db_owner** possono gestire l'appartenenza al ruolo predefinito del database. Nel database msdb sono presenti inoltre alcuni ruoli predefiniti del database per scopi specifici.  
  
 È possibile aggiungere qualsiasi account del database e altri ruoli [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ai ruoli a livello di database. Tutti i membri di un ruolo predefinito del database possono aggiungere altri account di accesso allo stesso ruolo.  
  
> [!IMPORTANT]  
>  Evitare di aggiungere ruoli flessibili di database come membri di ruoli predefiniti, poiché in tal modo si potrebbe provocare un'imprevista intensificazione dei privilegi.  
  
 Nella tabella seguente sono mostrati i ruoli a livello di database predefinito e le relative funzionalità. Questi ruoli esistono in tutti i database.  
  
|Nome del ruolo a livello di database|Descrizione|  
|-------------------------------|-----------------|  
|**db_owner**|I membri del ruolo predefinito del database **db_owner** possono eseguire tutte le attività di configurazione e di manutenzione sul database e anche eliminare il database.|  
|**db_securityadmin**|I membri del ruolo predefinito del database **db_securityadmin** possono modificare le appartenenze al ruolo e gestire le autorizzazioni. L'aggiunta di entità a questo ruolo potrebbe provocare un'imprevista intensificazione dei privilegi.|  
|**db_accessadmin**|I membri del ruolo predefinito del database **db_accessadmin** possono aggiungere o rimuovere le autorizzazioni di accesso al database per gli account di accesso di Windows, i gruppi di Windows e gli account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|**db_backupoperator**|I membri del ruolo predefinito del database **db_backupoperator** possono eseguire il backup del database.|  
|**db_ddladmin**|I membri del ruolo predefinito del database **db_ddladmin** possono eseguire qualsiasi comando DDL (Data Definition Language) in un database.|  
|**db_datawriter**|I membri del ruolo predefinito del database **db_datawriter** possono aggiungere, eliminare o modificare i dati di tutte le tabelle utente.|  
|**db_datareader**|Membri del ruolo predefinito del database **db_datareader** possono leggere tutti i dati di tutte le tabelle utente.|  
|**db_denydatawriter**|I membri del ruolo predefinito del database **db_denydatawriter** non possono aggiungere, modificare o eliminare dati delle tabelle utente contenute in un database.|  
|**db_denydatareader**|I membri del ruolo predefinito del database **db_denydatareader** non possono leggere i dati delle tabelle utente contenute in un database.|  
  
## <a name="msdb-roles"></a>Ruoli msdb  
 Il database msdb contiene ruoli specifici per uno scopo illustrati nella tabella seguente.  
  
|Nome del ruolo in msdb|Descrizione|  
|--------------------|-----------------|  
|`db_ssisadmin`<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|I membri di tali ruoli del database possono amministrare e utilizzare [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Le istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aggiornate da una versione precedente potrebbero contenere una versione precedente del ruolo che era stata denominata usando Data Transformation Services (DTS) anziché [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Per altre informazioni, vedere [Ruoli Integration Services &#40;servizio SSIS&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md).|  
|`dc_admin`<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|I membri di tali ruoli del database possono amministrare e utilizzare l'agente di raccolta dati. Per altre informazioni, vedere [Data Collection](../../data-collection/data-collection.md).|  
|**PolicyAdministratorRole**|I membri del ruolo del database **db_ PolicyAdministratorRole** possono eseguire tutte le attività di configurazione e manutenzione su criteri e condizioni della gestione basata su criteri. Per altre informazioni, vedere [Amministrare server usando la gestione basata su criteri](../../policy-based-management/administer-servers-by-using-policy-based-management.md).|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|I membri di questi ruoli del database possono amministrare e utilizzare gruppi di server registrati.|  
|**dbm_monitor**|Creato nel `msdb` database quando il primo database viene registrato nel monitoraggio mirroring del database. Il ruolo **dbm_monitor** non include alcun membro fino a quando un amministratore di sistema non provvede all'assegnazione di utenti al ruolo stesso.|  
  
> [!IMPORTANT]  
>  I membri dei ruoli db_ssisadmin e dc_admin potrebbero essere in grado di elevare i loro privilegi a sysadmin. Questa elevazione dei privilegi può verificarsi perché tali ruoli possono modificare i pacchetti [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] e i pacchetti [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] possono essere eseguiti da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando il contesto di sicurezza sysadmin di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. Per impedire questa elevazione dei privilegi durante l'esecuzione dei piani di manutenzione, set di raccolta dati e altri pacchetti [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , configurare i processi di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent che eseguono pacchetti in modo da utilizzare un account proxy con privilegi limitati o aggiungere solo i membri sysadmin ai ruoli db_ssisadmin e dc_admin.  
  
## <a name="working-with-database-level-roles"></a>Utilizzo di ruoli a livello di database  
 Nella tabella seguente vengono spiegati i comandi, le viste e le funzioni necessari per l'utilizzo dei ruoli a livello di database.  
  
|Funzionalità|Type|Descrizione|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql)|Metadati|Restituisce un elenco dei ruoli predefiniti del database.|  
|[sp_dbfixedrolepermission &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql)|Metadati|Visualizza le autorizzazioni di un ruolo predefinito del database.|  
|[sp_helprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprole-transact-sql)|Metadati|Restituisce informazioni sui ruoli del database corrente.|  
|[sp_helprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)|Metadati|Restituisce informazioni sui membri di un ruolo del database corrente.|  
|[sys.database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)|Metadati|Restituisce una riga per ogni membro di ogni ruolo del database.|  
|[IS_MEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-member-transact-sql)|Metadati|Indica se l'utente corrente è membro del gruppo di Microsoft Windows o del ruolo di database di Microsoft SQL Server specificato.|  
|[CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql)|Comando|Crea un nuovo ruolo di database nel database corrente.|  
|[ALTER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-role-transact-sql)|Comando|Modifica il nome di un ruolo del database.|  
|[DROP ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-role-transact-sql)|Comando|Rimuove un ruolo dal database.|  
|[sp_addrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrole-transact-sql)|Comando|Crea un nuovo ruolo di database nel database corrente.|  
|[sp_droprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprole-transact-sql)|Comando|Rimuove un ruolo del database dal database corrente.|  
|[sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)|Comando|Aggiunge un utente del database, un ruolo del database, un account di accesso di Windows o un gruppo di Windows a un ruolo del database nel database corrente.|  
|[sp_droprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)|Comando|Rimuove un account di sicurezza da un ruolo di SQL Server nel database corrente.|  
  
## <a name="public-database-role"></a>Ruolo di database public  
 Ogni utente di database appartiene al ruolo di database **public** . Quando a un utente non sono state concesse o sono state negate autorizzazioni specifiche per un oggetto a protezione diretta, l'utente eredita le autorizzazioni concesse a **public** su tale oggetto.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Viste del catalogo relative alla sicurezza &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)  
  
 [Stored procedure di sicurezza &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/security-stored-procedures-transact-sql)  
  
 [Funzioni di sicurezza &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql)  
  
 [Sicurezza di SQL Server](../securing-sql-server.md)  
  
 [sp_helprotect &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprotect-transact-sql)  
  
  
