---
title: Autorizzazioni
description: Questo articolo descrive i requisiti e le opzioni per la gestione delle autorizzazioni di database per data warehouse parallele.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 499ac56d8a462f62dac92b97654a9ace12bd356e
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257447"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>Gestione delle autorizzazioni in parallelo data warehouse
Questo articolo descrive i requisiti e le opzioni per la gestione delle autorizzazioni di database per SQL Server PDW.

## <a name="database-engine-permission-basics"></a><a name="BackupRestoreBasics"></a>Nozioni di base sulle autorizzazioni motore di database
Motore di database autorizzazioni per SQL Server PDW vengono gestite a livello di server tramite gli account di accesso e a livello di database tramite gli utenti del database e i ruoli del database definiti dall'utente.

**Account di accesso** Gli account di accesso sono account utente singoli per accedere al SQL Server PDW. SQL Server PDW supporta gli account di accesso che utilizzano l'autenticazione di Windows e l'autenticazione SQL Server.  Gli account di accesso con autenticazione di Windows possono essere utenti di Windows o gruppi di Windows di qualsiasi dominio ritenuto attendibile da SQL Server PDW. Gli account di accesso con autenticazione SQL Server vengono definiti e autenticati da SQL Server PDW e devono essere creati specificando una password.

I membri del ruolo predefinito del server **sysadmin** , ad esempio l'account di accesso **sa** , possono connettersi a un database senza che sia stato eseguito il mapping a un utente del database. Viene eseguito il mapping all'utente **dbo** . Anche il proprietario del database viene mappato come utente **dbo** .

**Ruoli del server** Sono disponibili quattro ruoli server speciali con un set di ruoli preconfigurati che forniscono un gruppo di autorizzazioni a livello di server appropriato. I ruoli del server **sysadmin**, **MediumRC**, **LargeRC**e **XLargeRCfixed** sono gli unici ruoli server attualmente implementati in SQL Server PDW. L'account di accesso **sa** è l'unico membro del ruolo predefinito del server **sysadmin** e non è possibile aggiungere altri account di accesso al ruolo **sysadmin** . Agli account di accesso è possibile concedere l'autorizzazione **Control Server** , che è simile, ma non identica, al ruolo predefinito del server **sysadmin** . Utilizzare [ALTER Server Role](../t-sql/statements/alter-server-role-transact-sql.md) per aggiungere membri agli altri ruoli del server. SQL Server PDW non supporta i ruoli del server definiti dall'utente.

**Utenti del database** Agli account di accesso viene concesso l'accesso a un database mediante la creazione di un utente di database in un database e il mapping dell'utente del database a un account di accesso. In genere, il nome utente di database è identico al nome dell'account di accesso, anche se non è necessario. Ogni utente di database esegue il mapping a un singolo account di accesso. Il mapping di un account di accesso può essere eseguito a un solo utente in un database, ma può essere eseguito come utente di database in diversi database.

**Ruoli** predefiniti del database I ruoli predefiniti del database sono un set di ruoli preconfigurati che forniscono un comodo gruppo di autorizzazioni a livello di database. Gli utenti del database e i ruoli del database definiti dall'utente possono essere aggiunti ai ruoli predefiniti del database utilizzando la procedura [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) . Per ulteriori informazioni sui ruoli predefiniti del database, vedere ruoli predefiniti del [database](#fixed-database-roles).

**Ruoli del database definiti dall'utente** Gli utenti con l'autorizzazione **Crea ruolo** possono creare nuovi ruoli del database definiti dall'utente per rappresentare gruppi di utenti con autorizzazioni comuni. In genere, le autorizzazioni vengono concesse o negate per l'intero ruolo, semplificando la gestione e il monitoraggio delle autorizzazioni.

Le autorizzazioni vengono concesse alle entità di sicurezza (account di accesso, utenti e ruoli) utilizzando l'istruzione **Grant** . Le autorizzazioni vengono negate in modo esplicito tramite il comando **Deny** . Un'autorizzazione precedentemente concessa o negata viene rimossa utilizzando l'istruzione **Revoke** . Le autorizzazioni sono cumulative, con l'utente che riceve tutte le autorizzazioni concesse all'utente, all'account di accesso e a qualsiasi appartenenza a un gruppo. Tuttavia, la negazione di un'autorizzazione prevale su tutte le concessioni. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->

L'esempio seguente rappresenta un metodo comune e consigliato di configurazione delle autorizzazioni.

1.  Se si usa l'autenticazione di Windows, creare un account di accesso per ogni utente di Windows o gruppo di Windows che si connetterà a SQL Server PDW. Se si usa l'autenticazione SQL Server, creare un account di accesso per ogni persona che si connetterà al SQL Server PDW.

2.  Creare un utente di database per ogni account di accesso in tutti i database necessari.

3.  Creare uno o più ruoli del database definiti dall'utente, ognuno dei quali rappresenta una funzione simile. ad esempio analista finanziario e analista vendite.

4.  Aggiungere utenti di database a uno o più ruoli del database definiti dall'utente.

5.  Concedere le autorizzazioni ai ruoli del database definiti dall'utente.

Gli account di accesso sono oggetti a livello di server e possono essere elencati visualizzando [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Alle entità server è possibile concedere solo autorizzazioni a livello di server.

Gli utenti e i ruoli del database sono oggetti a livello di database e possono essere elencati visualizzando [sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Alle entità di database è possibile concedere solo autorizzazioni a livello di database.

## <a name="default-permissions"></a><a name="BackupTypes"></a>Autorizzazioni predefinite
L'elenco seguente descrive le autorizzazioni predefinite:

-   Quando viene creato un account di accesso tramite l'istruzione **Create Login** , l'account di accesso riceve l'autorizzazione **Connect SQL** che consente all'account di accesso di connettersi al SQL Server PDW.

-   Quando un utente del database viene creato utilizzando l'istruzione **Create User** , l'utente riceve l'autorizzazione **Connect on database::** _<database_name>_ , consentendo all'account di accesso di connettersi al database come utente.

-   Per impostazione predefinita, tutte le entità, incluso il ruolo PUBLIC, non dispongono di autorizzazioni esplicite o implicite perché le autorizzazioni implicite vengono ereditate dalle autorizzazioni esplicite. Pertanto, quando non è presente alcuna autorizzazione esplicita, non possono essere presenti autorizzazioni implicite.

-   Quando un account di accesso diventa il proprietario di un oggetto o di un database, l'account di accesso dispone sempre di tutte le autorizzazioni per l'oggetto o il database. Le autorizzazioni di proprietà non sono visibili come autorizzazioni esplicite. Le istruzioni **Grant**, **Revoke**e **Deny** non hanno effetto sulle autorizzazioni di proprietà. La proprietà può essere modificata tramite l'istruzione [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) .

-   L'account di accesso sa ha tutte le autorizzazioni nell'appliance. Analogamente alle autorizzazioni di proprietà, le autorizzazioni sa non possono essere modificate e non sono visibili come autorizzazioni esplicite. Le istruzioni **Grant**, **Revoke**e **Deny** non hanno effetto sulle autorizzazioni SA.

-   Per impostazione predefinita, il ruolo server pubblico non riceve alcuna autorizzazione e non eredita le autorizzazioni da altri ruoli del server. Al ruolo server pubblico possono essere concesse autorizzazioni esplicite con le istruzioni **Grant**, **Revoke**e **Deny** .

-   Le transazioni non richiedono autorizzazioni. Tutte le entità possono eseguire i comandi **BEGIN TRANSACTION**, **commit**e **rollback** Transaction. Tuttavia, un'entità deve disporre delle autorizzazioni appropriate per eseguire ogni istruzione all'interno della transazione.

-   L'istruzione **USE** non richiede autorizzazioni. Tutte le entità possono eseguire l'istruzione **use** in qualsiasi database, tuttavia per accedere a un database è necessario che sia presente un'entità utente nel database o che l'utente Guest sia abilitato.

### <a name="the-public-role"></a>Ruolo PUBLIC
Tutti i nuovi account di accesso di appliance appartengono automaticamente al ruolo PUBLIC. Il ruolo del server PUBLIC presenta le caratteristiche seguenti:

-   Per impostazione predefinita, il ruolo del server PUBLIC non dispone di alcuna autorizzazione.

-   Tutte le entità sono membri del ruolo del server PUBLIC e il ruolo del server PUBLIC non è un membro di un altro ruolo del server.

-   Il ruolo del server PUBLIC non può ereditare le autorizzazioni implicite. È necessario concedere in modo esplicito tutte le autorizzazioni concesse al ruolo PUBLIC.

## <a name="determining-permissions"></a><a name="BackupProc"></a>Determinazione delle autorizzazioni
Il fatto che un account di accesso disponga o meno dell'autorizzazione per eseguire un'azione specifica dipende dalle autorizzazioni concesse o negate per l'accesso, l'utente e i ruoli di cui l'utente è membro. Le autorizzazioni a livello di server, ad esempio **Crea account di accesso** e **Visualizza stato del server**, sono disponibili per le entità a livello di server (account di accesso). Le autorizzazioni a livello di database, ad esempio la **selezione** di una tabella o l' **esecuzione** di una procedura, sono disponibili per le entità a livello di database (utenti e ruoli del database).

### <a name="implicit-and-explicit-permissions"></a>Autorizzazioni implicite ed esplicite
Un'*autorizzazione esplicita* è un'autorizzazione **GRANT** o **DENY** concessa a un'entità di sicurezza tramite un'istruzione **GRANT** o **DENY**. Le autorizzazioni a livello di database sono elencate nella visualizzazione [sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) . Le autorizzazioni a livello di server sono elencate nella visualizzazione [sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) .

Un' *autorizzazione implicita* è un'autorizzazione **Grant** o **Deny** che è stata ereditata da un'entità (account di accesso o ruolo del server). Un'autorizzazione può essere ereditata nei modi seguenti.

-   Un'entità può ereditare un'autorizzazione da un ruolo se l'entità è un membro del ruolo anche se l'entità non dispone di un'autorizzazione esplicita **Grant** o **Deny** .

-   Un'entità può ereditare un'autorizzazione per un oggetto subordinato, ad esempio una tabella, se l'entità dispone di un'autorizzazione per uno degli ambiti padre degli oggetti, ad esempio lo schema della tabella o l'autorizzazione per l'intero database.

-   Un'entità può ereditare un'autorizzazione disponendo di un'autorizzazione che include un'autorizzazione subordinata. L'autorizzazione **ALTER ANY USER** , ad esempio, include sia l' **utente create** sia l' **istruzione ALTER on User::** _<name>_ Permissions.

### <a name="determining-permissions-when-performing-actions"></a>Determinazione delle autorizzazioni durante l'esecuzione delle azioni
Il processo di determinazione dell'autorizzazione da assegnare a un'entità è complesso. La complessità si verifica quando si determinano le autorizzazioni implicite perché le entità possono essere membri di più ruoli e le autorizzazioni possono essere passate a più livelli nella gerarchia dei ruoli.

Nell'elenco seguente vengono descritte le regole generali per determinare le autorizzazioni:

-   La proprietà implica l'autorizzazione.

    Il proprietario di un oggetto dispone di tutte le autorizzazioni per l'oggetto. Analogamente, un proprietario del database dispone di tutte le autorizzazioni per il database e tutte le autorizzazioni per gli oggetti nel database. Queste autorizzazioni non possono essere modificate.

-   Le autorizzazioni possono essere ereditate in più livelli nella gerarchia delle appartenenze ai ruoli del server.

    Si supponga, ad esempio, che si verifichi la situazione seguente:

    -   Login David è un membro del ruolo del database PerfAnalysts.

    -   PerfAnalysts è un membro del ruolo di database Production.

    -   David e PerfAnalysts non dispongono dell'autorizzazione **Select** per la tabella Customer. L'autorizzazione è stata revocata o non è mai stata concessa in modo esplicito.

    -   Produzione dispone dell'autorizzazione **Select** per la tabella Customer.

    In questo caso, PerfAnalysts erediterà l'autorizzazione **Grant** per la tabella Customer dalla produzione e David erediterà l'autorizzazione **Grant** per la tabella Customer dalla produzione.

-   **Nega** override **Concedi** quando le autorizzazioni sono in conflitto.

    Si supponga, ad esempio, che login David non disponga delle autorizzazioni per la tabella Customer ed è membro di due ruoli del database: dbgroup1, che dispone dell'autorizzazione **Deny** per la tabella Customer e dbgroup2, che dispone dell'autorizzazione **Grant** per la tabella Customer. In questo caso Davide erediterà l'autorizzazione **Deny** per la tabella Customer. Questo è il caso se i ruoli hanno acquisito le autorizzazioni in modo esplicito o implicito.

### <a name="auditing-permissions"></a>Controllo delle autorizzazioni
Per ricercare le autorizzazioni di un utente, controllare quanto segue.

-   Eseguire la query seguente per determinare gli account di accesso che sono amministratori di sistema.

    ```sql
    SELECT SPLogins.name, 'is a member of ', SPRoles.name 
    FROM sys.server_role_members AS SRM 
    JOIN sys.server_principals AS SPRoles 
        ON SRM.role_principal_id = SPRoles.principal_id 
    JOIN sys.server_principals AS SPLogins 
        ON SRM.member_principal_id = SPLogins.principal_id;
    ```

-   Eseguire la query seguente per determinare gli account di accesso a cui sono state concesse autorizzazioni esplicite.

    ```sql
    SELECT name, 'has the ', state_desc , permission_name, ' permission'
    FROM sys.server_permissions AS SP
    JOIN sys.server_principals AS SPRoles 
        ON SP.grantee_principal_id = SPRoles.principal_id;
    ```

-   Eseguire la query seguente in un database utente per determinare gli utenti del database che sono membri di un ruolo del database.

    ```sql
    SELECT DPUsers.name, 'is a member of ', DPRoles.name  
    FROM sys.database_role_members AS DRM
    JOIN sys.database_principals AS DPRoles 
        ON DRM.role_principal_id = DPRoles.principal_id
    JOIN sys.database_principals AS DPUsers
        ON DRM.member_principal_id = DPUsers.principal_id;
    ```

-   Eseguire la query seguente in un database utente per determinare a quali utenti e ruoli del database sono state concesse o negate autorizzazioni specifiche. Sarà necessario eseguire una query su viste aggiuntive, ad esempio sys. Objects e sys. schemas, per identificare gli elementi descritti con la major_id.

    ```sql
    SELECT DPUsers.name, 'has the ', permission_name, 
    'permission on the item described as class = ', class, 'id = ', major_id
    FROM sys.database_permissions AS DP
    JOIN sys.database_principals AS DPUsers
        ON DP.grantee_principal_id = DPUsers.principal_id;
    ```

## <a name="database-permissions-best-practices"></a><a name="RestoreProc"></a>Procedure consigliate per le autorizzazioni del database

-   Concedere le autorizzazioni a un livello più granulare pratico. La concessione delle autorizzazioni a livello di tabella o di visualizzazione potrebbe diventare non gestibile. Tuttavia, la concessione di autorizzazioni a livello di database potrebbe essere troppo permissiva. Se il database è progettato con schemi per definire i limiti di lavoro, è possibile che l'autorizzazione concessa allo schema sia un compromesso appropriato tra il livello di tabella e il livello del database.

-   Concedere autorizzazioni ai ruoli, anziché a utenti o account di accesso. La gestione dei diritti tramite ruoli anziché utenti semplifica la concessione o la revoca rapida di un set di autorizzazioni per un utente o un account di accesso, spostando tali autorizzazioni all'interno o all'esterno del ruolo. Quando una funzione passa da una persona all'altra, le autorizzazioni possono rimanere intatte a livello di ruolo mentre l'appartenenza al ruolo viene modificata.

-   Concedere le autorizzazioni ai ruoli in base alla funzione job e ai ruoli del gruppo di livello superiore che combinano i ruoli della funzione job in base al gruppo aziendale che esegue le azioni.

-   Ogni utente finale deve avere un account di accesso univoco. Non consentire agli utenti di condividere gli account di accesso. La fornitura di un account di accesso per ogni utente garantisce una audit trail e semplifica la gestione delle autorizzazioni.

## <a name="fixed-database-roles"></a>Ruoli predefiniti del database
SQL Server fornisce ruoli a livello di database preconfigurati (fissi) per semplificare la gestione delle autorizzazioni in un server. I ruoli preconfigurati sono corretti in quanto non è possibile modificare le autorizzazioni assegnate. È anche possibile creare ruoli del database definiti dall'utente. È possibile modificare le autorizzazioni assegnate ai ruoli del database definiti dall'utente.

I ruoli sono entità di sicurezza che raggruppano altre entità. I ruoli del database sono a livello di database nell'ambito delle autorizzazioni. Gli utenti del database e altri ruoli del database possono essere aggiunti come membri dei ruoli del database. I ruoli predefiniti del database non possono essere aggiunti tra loro. I*ruoli* equivalgono ai *gruppi* nel sistema operativo Windows.

Sono presenti 9 ruoli predefiniti del database.

-   **db_owner**

-   **db_securityadmin**

-   **db_accessadmin**

-   **db_backupoperator**

-   **db_ddladmin**

-   **db_datawriter**

-   **db_datareader**

-   **db_denydatawriter**

-   **db_denydatareader**

### <a name="permissions-of-the-fixed-database-roles"></a>Autorizzazioni dei ruoli predefiniti del database
Il sistema dei ruoli predefiniti del server e dei ruoli predefiniti del database è un sistema legacy originato nel 1980. I ruoli predefiniti sono ancora supportati e sono utili in ambienti in cui sono presenti pochi utenti e le esigenze di sicurezza sono semplici. A partire da SQL Server 2005, è stato creato un sistema più dettagliato di concessione dell'autorizzazione. Questo nuovo sistema è più granulare e offre molte più opzioni per la concessione e la negazione delle autorizzazioni. La complessità aggiuntiva del sistema più granulare rende più difficile l'apprendimento, ma la maggior parte dei sistemi aziendali dovrebbe concedere le autorizzazioni invece di usare i ruoli predefiniti. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->Nel grafico seguente vengono illustrate le autorizzazioni associate a ogni ruolo predefinito del database. Tutte le autorizzazioni in questa SQL Server grafica non sono disponibili (o necessarie) in APS.

![Ruoli predefiniti del database per la sicurezza APS](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")

### <a name="related-content"></a>Contenuto correlato

-   Per creare ruoli definiti dall'utente, vedere [creare un ruolo](../t-sql/statements/create-role-transact-sql.md).


## <a name="fixed-server-roles"></a>Ruoli predefiniti del server
I ruoli predefiniti del server vengono creati automaticamente da SQL Server. SQL Server PDW dispone di un'implementazione limitata di SQL Server ruoli predefiniti del server. Solo i membri del **ruolo sysadmin** e **public** dispongono di account di accesso utente. I ruoli **setupadmin** e **dbcreator** vengono usati internamente da SQL Server PDW. Non è possibile aggiungere o rimuovere membri aggiuntivi da alcun ruolo.

### <a name="sysadmin-fixed-server-role"></a>Ruolo predefinito del server sysadmin
I membri del ruolo predefinito del server **sysadmin** possono eseguire qualsiasi attività nel server. L'account di accesso **sa** è l'unico membro del ruolo predefinito del server **sysadmin** . Non è possibile aggiungere altri account di accesso al ruolo predefinito del server **sysadmin** . La concessione dell'autorizzazione **CONTROL SERVER** è simile all'appartenenza al ruolo predefinito del server **sysadmin**. Nell'esempio seguente viene concessa l'autorizzazione **Control Server** a un account di accesso denominato Fay.

```sql
USE master;
GO
GRANT CONTROL SERVER TO Fay;
```

> [!IMPORTANT]
> L'autorizzazione **Control Server** fornisce un controllo quasi completo dei SQL Server PDW. Laddove possibile, fornire autorizzazioni più granulari per gli account di accesso. Si consideri, ad esempio, la concessione delle autorizzazioni **View Server state**, **ALTER ANY LOGIN**, **View any database**o **create any database** .

### <a name="public-server-role"></a>Ruolo server public
Ogni account di accesso che può connettersi a SQL Server PDW è un membro del ruolo del server **public** . Tutti gli account di accesso ereditano le autorizzazioni concesse a **public** su qualsiasi oggetto. Assegnare autorizzazioni **pubbliche** a un oggetto solo quando si desidera che l'oggetto sia disponibile per tutti gli utenti. Non è possibile modificare l'appartenenza al ruolo **public** .

> [!NOTE]
> **public** viene implementato in modo diverso rispetto agli altri ruoli. Poiché tutte le entità server sono membri di Public, l'appartenenza al ruolo **public** non viene elencata in **sys.server_role_members** DMV.

### <a name="fixed-server-roles-vs-granting-permissions"></a>Ruoli predefiniti del server rispetto alla concessione di autorizzazioni
Il sistema dei ruoli predefiniti del server e dei ruoli predefiniti del database è un sistema legacy originato nel 1980. I ruoli predefiniti sono ancora supportati e sono utili in ambienti in cui sono presenti pochi utenti e le esigenze di sicurezza sono semplici. A partire da SQL Server 2005, è stato creato un sistema più dettagliato di concessione dell'autorizzazione. Questo nuovo sistema è più granulare e offre molte più opzioni per la concessione e la negazione delle autorizzazioni. La complessità aggiuntiva del sistema più granulare rende più difficile l'apprendimento, ma la maggior parte dei sistemi aziendali dovrebbe concedere le autorizzazioni invece di usare i ruoli predefiniti. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->

## <a name="related-topics"></a>Argomenti correlati

- [Concedi autorizzazioni](grant-permissions.md)

<!-- MISSING LINKS
## See Also
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)
-->

