---
title: Le autorizzazioni in Parallel Data Warehouse | Microsoft Docs
description: Questo articolo descrive i requisiti e le opzioni per la gestione delle autorizzazioni di database per Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1ac058e42b8bad4f499210835a1f85c3cc7a08a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639510"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>Gestione delle autorizzazioni in Parallel Data Warehouse
Questo articolo descrive i requisiti e le opzioni per la gestione delle autorizzazioni di database per SQL Server PDW.  
  
## <a name="BackupRestoreBasics"></a>Nozioni di base dell'autorizzazione di database del motore  
Autorizzazioni del motore di database in SQL Server PDW sono gestite a livello di server tramite gli account di accesso e a livello di database tramite gli utenti del database e i ruoli di database definiti dall'utente.  
  
**Account di accesso**  
Gli account di accesso sono account utente singoli per l'accesso a SQL Server PDW. SQL Server PDW supporta gli account di accesso usando l'autenticazione di SQL Server e l'autenticazione di Windows.  Accesso con autenticazione di Windows può essere utenti di Windows o i gruppi di Windows di qualsiasi dominio che è considerato attendibile da SQL Server PDW. Gli account di accesso di autenticazione di SQL Server sono definiti e autenticati da SQL Server PDW e devono essere create specificando una password.  
  
I membri del **sysadmin** ruolo predefinito del server (ad esempio il **sa** account di accesso) può connettersi a un database senza che sia in corso il mapping a un utente del database. Queste vengono mappate al **dbo** utente. Il proprietario del database è mappato anche come il **dbo** utente.  
  
**Ruoli del server**  
Esistono quattro ruoli di server speciale con un set di ruoli preconfigurati che forniscono una serie appropriata di autorizzazioni a livello di server. Il **sysadmin**, **MediumRC**, **LargeRC**, e **XLargeRCfixed** ruoli del server sono i ruoli del server solo attualmente implementati in SQL Server PDW. Il **sa** account di accesso è l'unico membro del **sysadmin** ruolo predefinito del server e altri account di accesso non è possibile aggiungere per il **sysadmin** ruolo. Gli account di accesso possono essere concesse le **CONTROL SERVER** autorizzazione, che è simile, ma non identiche, per il **sysadmin** ruolo predefinito del server. Uso [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) per aggiungere membri ai ruoli del server. SQL Server PDW non supporta i ruoli server definiti dall'utente.  
  
**Utenti del database**  
Gli account di accesso viene concesso l'accesso a un database tramite la creazione di un utente del database in un database e il mapping di tale utente del database a un account di accesso. In genere, il nome utente di database è identico al nome dell'account di accesso, anche se non è necessario. Ogni utente di database esegue il mapping a un singolo account di accesso. Il mapping di un account di accesso può essere eseguito a un solo utente in un database, ma può essere eseguito come utente di database in diversi database.  
  
**Ruoli predefiniti del Database**  
Ruoli predefiniti del database sono un set di ruoli preconfigurati che forniscono una serie appropriata di autorizzazioni a livello di database. Gli utenti del database e i ruoli del database definito dall'utente possono essere aggiunti ai ruoli predefiniti del database usando il [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) procedure. Per altre informazioni sui ruoli predefiniti del database, vedere [ruoli di Database predefiniti](#fixed-database-roles).  
  
**Ruoli predefiniti del Database definito dall'utente**  
Gli utenti con il **CREATE ROLE** autorizzazione possa creare nuovi ruoli del database definito dall'utente per rappresentare i gruppi di utenti con autorizzazioni comuni. In genere, le autorizzazioni vengono concesse o negate per l'intero ruolo, semplificando la gestione e il monitoraggio delle autorizzazioni.  
  
Le autorizzazioni vengono concesse alle entità di sicurezza (account di accesso, utenti e ruoli) usando il **Concedi** istruzione. Le autorizzazioni vengono negate in modo esplicito tramite il **DENY** comando. Un oggetto precedentemente concessa o negata l'autorizzazione viene rimosso usando il **revocare** istruzione. Le autorizzazioni sono cumulative, con l'utente che riceve tutte le autorizzazioni concesse all'utente, all'account di accesso e a qualsiasi appartenenza a un gruppo. Tuttavia, la negazione di un'autorizzazione prevale su tutte le concessioni. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
L'esempio seguente rappresenta un metodo comune e consigliato di configurazione delle autorizzazioni.  
  
1.  Se si usa l'autenticazione di Windows, creare un account di accesso per ogni utente di Windows o un gruppo di Windows che si connetterà a SQL Server PDW. Se si usa l'autenticazione di SQL Server, creare un account di accesso per ogni persona che si connetterà a SQL Server PDW.  
  
2.  Creare un utente di database per ogni account di accesso in tutti i database necessari.  
  
3.  Creare uno o più ruoli di database definiti dall'utente, ognuno dei quali rappresenta una funzione simile. ad esempio analista finanziario e analista vendite.  
  
4.  Aggiungere gli utenti del database a uno o più ruoli di database definiti dall'utente.  
  
5.  Concedere le autorizzazioni ai ruoli del database definiti dall'utente.  
  
Gli account di accesso sono oggetti a livello di server e possono essere elencati visualizzando [Sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Solo le autorizzazioni a livello di server possono essere concesse alle entità del server.  
  
Gli utenti e ruoli del database sono oggetti a livello di database e possono essere elencati visualizzando [Sys. database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Le autorizzazioni a livello di database possono essere concesso solo alle entità di database.  
  
## <a name="BackupTypes"></a>Autorizzazioni predefinite  
L'elenco seguente descrive le autorizzazioni predefinite:  
  
-   Quando viene creato un account di accesso per le direttive using **CREATE LOGIN** istruzione, l'account di accesso riceve il **CONNECT SQL** autorizzazione che consente l'accesso per connettersi a SQL Server PDW.  
  
-   Quando un utente del database viene creato usando il **CREATE USER** istruzione, l'utente riceve il **CONNECT ON DATABASE::**_< database_name >_ autorizzazione, che consente la account di accesso per connettersi al database come un utente.  
  
-   Tutte le entità, tra cui il ruolo PUBLIC, non avere alcuna autorizzazione esplicite o implicite per impostazione predefinita, poiché le autorizzazioni implicite vengono ereditate dalle autorizzazioni esplicite. Pertanto, quando non sono presente alcuna autorizzazione esplicitare, non può anche essere presente alcuna autorizzazione implicite.  
  
-   Quando un account di accesso diventa il proprietario di un oggetto o un database, l'account di accesso dispone di tutte le autorizzazioni per l'oggetto o il database. Le autorizzazioni di proprietà non sono visibili come autorizzazioni esplicite. Il **concessione**, **REVOKE**, e **DENY** istruzioni non hanno alcun effetto sulle autorizzazioni per la proprietà. La proprietà può essere modificata usando il [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) istruzione.  
  
-   L'account di accesso sa ha tutte le autorizzazioni nell'appliance. Simile alle autorizzazioni di proprietà e le autorizzazioni di amministratore di sistema non possono essere modificate e non sono visibili come autorizzazioni esplicite. Il **concessione**, **REVOKE**, e **DENY** istruzioni non hanno alcun effetto sulle autorizzazioni di amministratore di sistema.  
  
-   Ruolo del server PUBLIC non riceve alcuna autorizzazione per impostazione predefinita e non eredita le autorizzazioni da altri ruoli del server. Ruolo del server PUBLIC possa essere concesse le autorizzazioni esplicite con le **concessione**, **REVOKE**, e **DENY** istruzioni.  
  
-   Le transazioni non richiedono le autorizzazioni. Tutte le entità possono eseguire la **BEGIN TRANSACTION**, **COMMIT**, e **ROLLBACK** i comandi della transazione. Tuttavia, un'entità deve disporre delle autorizzazioni appropriate per eseguire ogni istruzione all'interno della transazione.  
  
-   L'istruzione **USE** non richiede autorizzazioni. Tutte le entità può essere eseguito il **utilizzare** istruzione in qualsiasi database, tuttavia per accedere a un database devono avere un'entità utente nel database o l'utente guest deve essere abilitato.  
  
### <a name="the-public-role"></a>Il ruolo PUBLIC  
Tutti i nuovi account di accesso appliance automaticamente appartenere al ruolo PUBLIC. Ruolo del server PUBLIC ha le caratteristiche seguenti:  
  
-   Ruolo del server PUBLIC non dispone di autorizzazioni per impostazione predefinita.  
  
-   Tutte le entità sono membri del ruolo del server PUBLIC e ruolo del server PUBLIC non è un membro di un altro ruolo del server.  
  
-   Ruolo del server PUBLIC non può ereditare autorizzazioni implicite. Le autorizzazioni concesse al ruolo PUBLIC devono essere concessa esplicitamente.  
  
## <a name="BackupProc"></a>Determinare le autorizzazioni  
Se un account di accesso è autorizzato a eseguire un'azione specifica dipende dalle autorizzazioni concesse o negate all'account di accesso, utenti e ruoli di che utente è membro. Le autorizzazioni a livello di server (ad esempio **CREATE LOGIN** e **VIEW SERVER STATE**) sono disponibili per le entità a livello di server (accessi). Le autorizzazioni a livello di database (ad esempio **selezionate** da una tabella o **EXECUTE** una stored procedure) sono disponibili per le entità a livello di database (utenti e ruoli del database).  
  
### <a name="implicit-and-explicit-permissions"></a>Autorizzazioni implicite ed esplicite  
Un'*autorizzazione esplicita* è un'autorizzazione **GRANT** o **DENY** concessa a un'entità di sicurezza tramite un'istruzione **GRANT** o **DENY**. Sono elencate le autorizzazioni a livello di database nel [Sys. database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) visualizzazione. Sono elencate le autorizzazioni a livello di server nel [Sys. server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) visualizzazione.  
  
Un' *autorizzazione implicita* è un **GRANT** oppure **DENY** autorizzazione che un'entità di sicurezza (ruolo del server o account di accesso) ha ereditato. Un'autorizzazione può essere ereditata nei modi seguenti.  
  
-   Un'entità può ereditare un'autorizzazione da un ruolo se l'entità è un membro del ruolo, anche se l'entità non dispone di un'esplicita **concessione** oppure **DENY** l'autorizzazione.  
  
-   Un'entità può ereditare un'autorizzazione su un oggetto subordinato, quale una tabella, se l'entità ha un'autorizzazione su uno degli ambiti padre oggetti (ad esempio, lo schema della tabella o l'autorizzazione per l'intero database).  
  
-   Un'entità può ereditare un'autorizzazione facendo in modo che un'autorizzazione che include un'autorizzazione subordinata. Ad esempio la **ALTER ANY USER** autorizzazione include entrambi gli le **CREATE USER** e il **ALTER ON USER::** _<name>_ autorizzazioni.  
  
### <a name="determining-permissions-when-performing-actions"></a>Determinare le autorizzazioni per eseguire le azioni  
Il processo volto a determinare l'autorizzazione per assegnare a un'entità è complesso. La complessità si verifica durante la determinazione delle autorizzazioni implicite in quanto le entità possono essere membri di più ruoli e autorizzazioni possono essere passate attraverso più livelli nella gerarchia dei ruoli.  
  
L'elenco seguente descrive le regole generali per determinare le autorizzazioni:  
  
-   La proprietà implica l'autorizzazione.  
  
    Proprietario di un oggetto dispone di tutte le autorizzazioni sull'oggetto. Analogamente, un proprietario del database dispone di tutte le autorizzazioni per il database e tutte le autorizzazioni per gli oggetti nel database. Queste autorizzazioni non possono essere modificate.  
  
-   Le autorizzazioni possono essere ereditate attraverso più livelli nella gerarchia delle appartenenze a un ruolo server.  
  
    Ad esempio, si supponga la situazione seguente:  
  
    -   Account di accesso David è un membro del ruolo predefinito del database PerfAnalysts.  
  
    -   PerfAnalysts è un membro del ruolo predefinito del database ambiente di produzione.  
  
    -   David e PerfAnalysts non hanno alcuna **seleziona** l'autorizzazione per la tabella Customer. L'autorizzazione è stata mai esplicitamente concesso o revocato.  
  
    -   Ambiente di produzione ha **seleziona** l'autorizzazione per la tabella Customer.  
  
    In questo caso, erediterà PerfAnalysts **concessione** erediterà l'autorizzazione per la tabella Customer dalla produzione e David **Concedi** autorizzazione per la tabella dei clienti dall'ambiente di produzione.  
  
-   **DENY** esegue l'override **concessione** le autorizzazioni sono in conflitto.  
  
    Si supponga ad esempio account di accesso David non dispone delle autorizzazioni per la tabella Customer e sia un membro di due ruoli predefiniti del database-dbgroup1, che ha **DENY** autorizzazione per la tabella Customer e dbgroup2, che ha **Concedi** autorizzazione per la tabella Customer. In questo caso, David erediteranno le **DENY** l'autorizzazione per la tabella Customer. Questo è il caso se i ruoli ottenuto le autorizzazioni in modo esplicito o implicito.  
  
### <a name="auditing-permissions"></a>Il controllo delle autorizzazioni  
Per identificare le autorizzazioni di un utente, verificare quanto segue.  
  
-   Eseguire la query seguente per determinare quali account di accesso sono gli amministratori di sistema.  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   Eseguire la query seguente per determinare quali account sono state concesse autorizzazioni esplicite.  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   Eseguire la query seguente in un database utente per determinare gli utenti di database che sono membri di un ruolo del database.  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   Eseguire la query seguente in un database utente per determinare quali utenti e ruoli concessi o negati autorizzazioni specifiche. Dovrai le visualizzazioni di query aggiuntive, ad esempio Sys. Objects e Sys. Schemas per identificare gli elementi descritti, con la major_id.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>Procedure consigliate per le autorizzazioni di database  
  
-   Concedere le autorizzazioni di livello più granulare risulta più comodo. Concedono autorizzazioni nella tabella o le autorizzazioni a livello di visualizzazione può diventare difficile da gestire. Ma potrebbe essere troppo permissive concedono autorizzazioni a livello di database. Se il database è progettato con gli schemi per definire i limiti di lavoro, ad esempio la concessione di un'autorizzazione per lo schema è un compromesso tra il livello di tabella e il livello di database appropriato.  
  
-   Concedere autorizzazioni ai ruoli anziché agli utenti o account di accesso. La gestione dei diritti usando ruoli anziché agli utenti semplifica rapidamente concedere o revocare un set di autorizzazioni per un utente o un account di accesso per lo spostamento da e verso il ruolo. Quando una funzione passa da una persona a altra, a livello di ruolo durante le modifiche di appartenenza al ruolo le autorizzazioni possono rimangono invariate.  
  
-   Concedere autorizzazioni ai ruoli in base a mansione e su ruoli dei gruppi di livello superiore che consentono di combinare i ruoli di funzione di processo basati sul gruppo di società eseguendo le azioni.  
  
-   Ogni utente finale deve avere un account di accesso univoco. Non consentono agli utenti di condividere gli account di accesso. Fornire un account di accesso per ogni utente garantisce un audit trail e semplifica la gestione delle autorizzazioni.  
  
## <a name="fixed-database-roles"></a>Ruoli predefiniti del database
SQL Server fornisce ruoli a livello di database (predefiniti) preconfigurati che consentono di gestire le autorizzazioni su un server. I ruoli configurati in precedenza vengono corretti in quanto non è possibile modificare le autorizzazioni assegnate. Inoltre è possibile creare ruoli del database definito dall'utente. È possibile modificare le autorizzazioni assegnate ai ruoli predefiniti del database definito dall'utente.  
  
I ruoli sono entità di sicurezza che raggruppano altre entità. Ruoli predefiniti del database sono a livello di database nel proprio ambito di autorizzazioni. Gli utenti del database e altri ruoli del database possono essere aggiunti come membri dei ruoli predefiniti del database. Non è possibile aggiungere i ruoli predefiniti del database tra loro. I*ruoli* equivalgono ai *gruppi* nel sistema operativo Windows.  
  
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
  
### <a name="permissions-of-the-fixed-database-roles"></a>Autorizzazioni dei ruoli predefiniti del Database  
Il sistema dei ruoli predefiniti del server e ruoli predefiniti del database è un sistema legacy ha avuto origine in anni ' 80. Ruoli predefiniti sono ancora supportati e sono utili in ambienti in cui sono presenti alcuni utenti e alle esigenze di sicurezza sono semplici. A partire da SQL Server 2005, è stato creato un sistema più dettagliato della concessione di autorizzazione. Questo nuovo sistema è più granulare, che fornisce molte più opzioni per la concessione e la negazione di autorizzazioni. La complessità aggiuntiva del sistema più granulare rende più difficile per ulteriori informazioni, ma la maggior parte dei sistemi aziendali devono concedere le autorizzazioni anziché utilizzare i ruoli predefiniti. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->Il grafico seguente mostra le autorizzazioni associate a ogni ruolo predefinito del database. Tutte le autorizzazioni in questa immagine di SQL Server non sono disponibili (o necessario) in punti di accesso.  
  
![Ruoli predefiniti del database per la sicurezza APS](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>Contenuto correlato  
  
-   Per creare i ruoli definiti dall'utente, vedere [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md).  
  
  
## <a name="fixed-server-roles"></a>Ruoli predefiniti del server
Ruoli predefiniti del server vengono creati automaticamente da SQL Server. SQL Server PDW è un'implementazione limitata di ruoli predefiniti del server di SQL Server. Solo le **sysadmin** e **pubblico** includere account di accesso utente come membri. Il **setupadmin** e **dbcreator** vengono utilizzati internamente da SQL Server PDW. Membri aggiuntivi non possono essere aggiunto o rimosso da alcun ruolo.  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin ruolo Server predefinito  
I membri del ruolo predefinito del server **sysadmin** possono eseguire qualsiasi attività nel server. Il **sa** account di accesso è l'unico membro delle **sysadmin** ruolo predefinito del server. Non è possibile aggiungere altri account di accesso per il **sysadmin** ruolo predefinito del server. La concessione dell'autorizzazione **CONTROL SERVER** è simile all'appartenenza al ruolo predefinito del server **sysadmin**. Nell'esempio seguente viene concessa di **CONTROL SERVER** dell'autorizzazione per un account di accesso denominato Fay.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> Il **CONTROL SERVER** autorizzazione fornisce il controllo quasi completo di SQL Server PDW. Quando possibile, specificare invece autorizzazioni più granulari agli account di accesso. Ad esempio, provare a concedere il **VIEW SERVER STATE**, **ALTER ANY LOGIN**, **VIEW ANY DATABASE**, oppure **CREATE ANY DATABASE** autorizzazioni.  
  
### <a name="public-server-role"></a>Ruolo Server Public  
Ogni account di accesso che possono connettersi a SQL Server PDW è un membro del **pubblica** ruolo del server. Tutti gli accessi ereditano le autorizzazioni concesse al **pubblica** su qualsiasi oggetto. Assegnare solo **pubblica** le autorizzazioni per un oggetto quando si desidera che l'oggetto sia disponibile per tutti gli utenti. Non è possibile modificare l'appartenenza di **pubblica** ruolo.  
  
> [!NOTE]  
> **Pubblica** viene implementato in modo diverso rispetto agli altri ruoli. Poiché tutte le entità server sono membri di pubblico, l'appartenenza del **pubbliche** ruolo non è elencato nel **Sys. server_role_members** DMV.  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>Visual Studio i ruoli del Server predefinito. Concessione di autorizzazioni  
Il sistema dei ruoli predefiniti del server e ruoli predefiniti del database è un sistema legacy ha avuto origine in anni ' 80. Ruoli predefiniti sono ancora supportati e sono utili in ambienti in cui sono presenti alcuni utenti e alle esigenze di sicurezza sono semplici. A partire da SQL Server 2005, è stato creato un sistema più dettagliato della concessione di autorizzazione. Questo nuovo sistema è più granulare, che fornisce molte più opzioni per la concessione e la negazione di autorizzazioni. La complessità aggiuntiva del sistema più granulare rende più difficile per ulteriori informazioni, ma la maggior parte dei sistemi aziendali devono concedere le autorizzazioni anziché utilizzare i ruoli predefiniti. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>Argomenti correlati  
  
- [Concedere autorizzazioni](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

