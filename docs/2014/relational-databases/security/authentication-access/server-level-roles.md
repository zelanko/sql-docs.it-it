---
title: Ruoli a livello di server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.Security.BUILTIN.administrators
- sql12.Security.NT_AUTHORITY.SYSTEM
helpviewer_keywords:
- roles [SQL Server], server-level
- principals [SQL Server], server-level
- CONTROL SERVER permission
- fixed server roles [SQL Server]
- credentials [SQL Server], roles
- sysadmin fixed server role
- server-level roles [SQL Server]
- authentication [SQL Server], roles
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4e8f2e75eb5272f30153814e923048b4f5c4f8b1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016211"
---
# <a name="server-level-roles"></a>Ruoli a livello di server
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornisce ruoli a livello di server per semplificare la gestione delle autorizzazioni in un server. Questi ruoli sono entità di sicurezza che raggruppano altre entità. L'ambito delle autorizzazioni dei ruoli a livello di server è l'intero server. I*ruoli* equivalgono ai *gruppi* nel sistema operativo Windows.  
  
 I ruoli predefiniti del server vengono forniti per motivi di praticità e compatibilità con le versioni precedenti. Laddove possibile, assegnare autorizzazioni più specifiche.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornisce nove ruoli predefiniti del server. Le autorizzazioni concesse ai ruoli predefiniti del server non possono essere modificate. A partire da [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], è possibile creare ruoli del server definiti dall'utente e aggiungere autorizzazioni a livello di server a tali ruoli.  
  
 È possibile aggiungere entità a livello di server, ad esempio account di accesso di[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , account di Windows e gruppi di Windows, nei ruoli a livello di server. Tutti i membri di un ruolo predefinito del server possono aggiungere altri account di accesso allo stesso ruolo. I membri dei ruoli del server definiti dall'utente non possono aggiungere altre entità del server al ruolo.  
  
## <a name="fixed-server-level-roles"></a>Ruoli predefiniti a livello di server  
 Nella tabella seguente vengono illustrati i ruoli predefiniti a livello di server e le relative funzionalità.  
  
|Ruolo predefinito a livello di server|Descrizione|  
|------------------------------|-----------------|  
|sysadmin|I membri del ruolo predefinito del server sysadmin possono eseguire qualsiasi attività nel server.|  
|serveradmin|I membri del ruolo predefinito del server serveradmin sono autorizzati a modificare le opzioni di configurazione a livello di server e ad arrestare il server.|  
|securityadmin|I membri del ruolo predefinito del server securityadmin gestiscono gli account di accesso e le relative proprietà. Possono concedere, negare e revocare le autorizzazioni a livello di server e a livello di database se hanno accesso a un database. Questi membri sono inoltre autorizzati a reimpostare le password per gli account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Nota sulla sicurezza la possibilità di concedere l'accesso al e di configurare le autorizzazioni utente consente all'amministratore della sicurezza di assegnare la maggior parte delle autorizzazioni server. ** \* \* \* \* ** [!INCLUDE[ssDE](../../../includes/ssde-md.md)] Il `securityadmin` ruolo deve essere considerato equivalente al `sysadmin` ruolo.|  
|processadmin|I membri del ruolo predefinito del server processadmin sono autorizzati a terminare processi in esecuzione in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|setupadmin|I membri del ruolo predefinito del server setupadmin sono autorizzati ad aggiungere e rimuovere server collegati usando istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] . L'appartenenza a sysadmin è necessaria per l'uso di [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].|  
|bulkadmin|I membri del ruolo predefinito del server bulkadmin sono autorizzati a eseguire l'istruzione BULK INSERT.|  
|diskadmin|Il ruolo predefinito del server diskadmin consente di gestire i file su disco.|  
|dbcreator|I membri del ruolo predefinito del server dbcreator sono autorizzati a creare, modificare, eliminare e ripristinare qualsiasi database.|  
|public|Ogni accesso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] appartiene al ruolo del server public. Quando a un'entità del server non sono state concesse o sono state negate autorizzazioni specifiche per un oggetto a protezione diretta, l'utente eredita le autorizzazioni concesse a public su tale oggetto. Assegnare le autorizzazioni public per un oggetto solo quando si desidera che l'oggetto sia disponibile a tutti gli utenti. Non è possibile modificare l'appartenenza a public.<br /><br /> Nota: public viene implementato in modo diverso rispetto agli altri ruoli. È possibile, tuttavia, concedere, negare o revocare autorizzazioni da public.|  
  
## <a name="permissions-of-fixed-server-roles"></a>Autorizzazioni dei ruoli predefiniti del server  
 A ogni ruolo predefinito del server vengono assegnate autorizzazioni specifiche. Per un grafico delle autorizzazioni assegnate ai ruoli del server, vedere la pagina relativa ai [ruoli predefiniti del server e del database del motore di database](https://social.technet.microsoft.com/wiki/contents/articles/2024.database-engine-fixed-server-and-fixed-database-roles.aspx).  
  
> [!IMPORTANT]  
>  L'autorizzazione `CONTROL SERVER` è simile ma non identica al ruolo predefinito del server `sysadmin`. Le autorizzazioni non implicano le appartenenze ai ruoli e le appartenenze ai ruoli non concedono autorizzazioni. Ad esempio, `CONTROL SERVER`non implica l'appartenenza al `sysadmin` ruolo predefinito del server. Tuttavia, talvolta è possibile rappresentare tra ruoli e autorizzazioni equivalenti. La maggior parte dei comandi `DBCC` e molte stored procedure di sistema richiedono l'appartenenza al ruolo predefinito del server `sysadmin`. Per un elenco delle stored procedure di sistema 171 che richiedono `sysadmin` l'appartenenza, vedere il post di Blog seguente di Andreas Wolter [Control Server e sysadmin/SA: autorizzazioni, procedure di sistema, DBCC, creazione automatica dello schema ed escalation dei privilegi-avvertenze](http://www.insidesql.org/blogs/andreaswolter/2013/08/control-server-vs-sysadmin-sa-permissions-privilege-escalation-caveats).  
  
## <a name="server-level-permissions"></a>Autorizzazioni a livello di server  
 Ai ruoli del server definiti dall'utente è possibile aggiungere solo autorizzazioni a livello di server. Per elencare le autorizzazioni a livello di server, eseguire la seguente istruzione. Di seguito sono elencate le autorizzazioni a livello di server:  
  
```sql  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 Per altre informazioni sulle autorizzazioni, vedere [Autorizzazioni &#40;Motore di database&#41;](../permissions-database-engine.md) e [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql).  
  
## <a name="working-with-server-level-roles"></a>Lavorare con i ruoli a livello di server.  
 Nella tabella seguente vengono illustrati i comandi, le viste e le funzioni che consentono di utilizzare ruoli a livello di server.  
  
|Funzionalità|Type|Descrizione|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql)|Metadati|Restituisce un elenco di ruoli a livello di server.|  
|[sp_helpsrvrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql)|Metadati|Restituisce informazioni sui membri di un ruolo a livello di server.|  
|[sp_srvrolepermission &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql)|Metadati|Visualizza le autorizzazioni di un ruolo a livello di server.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-srvrolemember-transact-sql)|Metadati|Indica se un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è un membro del ruolo a livello di server specificato.|  
|[sys.server_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)|Metadati|Restituisce una riga per ogni membro di ogni ruolo a livello di server.|  
|[sp_addsrvrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql)|Comando|Aggiunge un account di accesso come membro di un ruolo a livello di server. Operazione deprecata. Usare [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) .|  
|[sp_dropsrvrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql)|Comando|Rimuove un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o un utente o un gruppo di Windows da un ruolo a livello di server. Operazione deprecata. Usare [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) .|  
|[CREATE SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-role-transact-sql)|Comando|Crea un ruolo del server definito dall'utente.|  
|[ALTER SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-role-transact-sql)|Comando|Modifica l'appartenenza di un ruolo del server o il nome di un ruolo del server definito dall'utente.|  
|[DROP SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-role-transact-sql)|Comando|Rimuove un ruolo del server definito dall'utente.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-srvrolemember-transact-sql)|Funzione|Determina l'appartenenza del ruolo del server.|  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli a livello di database](../authentication-access/database-level-roles.md)   
 [Viste del catalogo di sicurezza &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)   
 [Funzioni di sicurezza &#40;&#41;Transact-SQL](/sql/t-sql/functions/security-functions-transact-sql)   
 [Sicurezza di SQL Server](../securing-sql-server.md)   
 [CONCEDERE autorizzazioni per entità server &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-server-principal-permissions-transact-sql)   
 [REVOKE-autorizzazioni per entità server &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-server-principal-permissions-transact-sql)   
 [DENY-autorizzazioni per entità server &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-server-principal-permissions-transact-sql)   
 [Creazione di un ruolo del server](../authentication-access/create-a-server-role.md)  
  
  
