---
title: Creare un account di accesso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.LOGIN.SERVERROLES.F1
- sql12.swb.login.databaseaccess.f1
- sql12.swb.login.general.f1
- sql12.swb.login.effectivepermissions.f1
- sql12.swb.login.status.f1
helpviewer_keywords:
- authentication [SQL Server], logins
- logins [SQL Server], creating
- creating logins with Management Studio
- Create login [SQL Server]
- SQL Server logins
ms.assetid: fb163e47-1546-4682-abaa-8c9494e9ddc7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b765248e43dc66b9e1c038df27ca9a8b6135706d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63012025"
---
# <a name="create-a-login"></a>Creazione di un account di accesso
  In questo argomento viene descritto come creare un account di accesso in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Un account di accesso è l'identità della persona o del processo che esegue la connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Background](#Background)  
  
     [Sicurezza](#Security)  
  
-   **Per creare un account di accesso utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [passaggi da effettuare dopo aver creato un account di accesso](#FollowUp)  
  
##  <a name="background"></a>Informazioni di background sul <a name="Background"></a>  
 Un accesso è un'entità di sicurezza o un'entità che può essere autenticata da un sistema sicuro. Per connettersi a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], gli utenti necessitano di un account di accesso. È possibile creare un account di accesso basato su un'entità di Windows (quale un utente del dominio o un gruppo del dominio Windows) o è possibile creare un account di accesso che non è basato su un'entità di Windows (ad esempio, un accesso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ).  
  
> [!NOTE]  
>  Per utilizzare l'autenticazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve utilizzare l'autenticazione a modalità mista. Per altre informazioni, vedere [scegliere una modalità di autenticazione](../choose-an-authentication-mode.md).  
  
 È possibile concedere autorizzazioni agli account di accesso, in quanto entità di sicurezza. L'ambito di un account di sicurezza è l'intero [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Affinché un account di accesso possa eseguire la connessione a un database specifico nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è necessario eseguirne il mapping a un utente del database. Le autorizzazioni all'interno del database vengono concesse e negate all'utente del database, non all'account di accesso. È possibile concedere a un account di accesso le autorizzazioni il cui ambito è l'intera istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (ad esempio, l'autorizzazione `CREATE ENDPOINT`).  
  
##  <a name="security"></a><a name="Security"></a> Sicurezza  
  
### <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione `ALTER ANY LOGIN` o `ALTER LOGIN` per il server.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
##### <a name="to-create-a-sql-server-login"></a>Per creare un account di accesso di SQL Server  
  
1.  In Esplora oggetti espandere la cartella dell'istanza del server in cui si desidera creare il nuovo account di accesso.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **sicurezza** , scegliere **nuovo**e quindi **account di accesso.**  
  
3.  Nella pagina **Generale** della finestra di dialogo **Account di accesso - Nuovo** immettere il nome di un utente nella casella **Nome account di accesso**. In alternativa, fare clic su **Cerca...** per aprire la finestra di dialogo **Seleziona un utente o un gruppo**.  
  
     Se si fa clic su **Cerca...**:  
  
    1.  In **Selezionare questo tipo di oggetto** fare clic su **Tipi di oggetti...** per aprire la finestra di dialogo **Tipi di oggetto** e selezionare alcune o tutte le opzioni seguenti: **Entità di sicurezza predefinite**, **Gruppi** e **Utenti**. Le opzioni**Entità di sicurezza predefinite** e **Utenti** sono selezionate per impostazione predefinita. Al termine, fare clic su **OK**.  
  
    2.  In **Da questo percorso** fare clic su **Percorsi...** per aprire la finestra di dialogo **Percorsi** e selezionare uno dei percorsi server disponibili. Al termine, fare clic su **OK**.  
  
    3.  In **Immettere il nome dell'oggetto da selezionare (esempi)**, immettere il nome dell'utente o del gruppo che si desidera trovare. Per ulteriori informazioni, vedere [Finestra di dialogo Seleziona utenti, computer o gruppi](https://technet.microsoft.com/library/cc771712.aspx).  
  
    4.  Fare clic su **Avanzate...** per opzioni di ricerca più avanzate. Per altre informazioni, vedere [Finestra di dialogo Seleziona utenti, computer o gruppi - Pagina Avanzate](https://technet.microsoft.com/library/cc733110.aspx).  
  
    5.  Fare clic su **OK**.  
  
4.  Per creare un account di accesso basato su un'entità di Windows, selezionare **Autenticazione di Windows**. Si tratta della selezione predefinita.  
  
5.  Per creare un account di accesso salvato in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , selezionare **Autenticazione di SQL Server**.  
  
    1.  Nella casella **Password**, immettere una password per il nuovo utente. Immettere nuovamente quella password nella casella **Conferma password**.  
  
    2.  In caso di modifica di una password esistente, selezionare **Specifica vecchia password**e quindi digitare la password precedente nella casella **Vecchia password** .  
  
    3.  Per applicare le opzioni dei criteri password per la complessità e l'applicazione, selezionare **Applica criteri password**. Per ulteriori informazioni, vedere [Password Policy](../password-policy.md). Si tratta di un'opzione predefinita quando si seleziona **l'autenticazione SQL Server** .  
  
    4.  Per applicare le opzioni dei criteri password per la scadenza, selezionare **Imponi scadenza password**. Per abilitare questa casella di controllo, è necessario selezionare**Applica criteri password** . Si tratta di un'opzione predefinita quando si seleziona **l'autenticazione SQL Server** .  
  
    5.  Per forzare l'utente a creare una nuova password dopo la prima volta che l'account di accesso viene utilizzato, selezionare **Richiedi modifica della password all'accesso successivo**. Per abilitare questa casella di controllo, è necessario selezionare**Imponi scadenza password** . Si tratta di un'opzione predefinita quando si seleziona **l'autenticazione SQL Server** .  
  
6.  Per associare l'account di accesso a un certificato di sicurezza autonomo, selezionare **Mapping con certificato** , quindi selezionare il nome di un certificato esistente dall'elenco.  
  
7.  Per associare l'account di accesso a una chiave asimmetrica autonoma, selezionare **Mapping con chiave asimmetrica** , quindi selezionare il nome di una chiave esistente dall'elenco.  
  
8.  Per associare l'accesso a credenziali di sicurezza, selezionare la casella di controllo **Credenziali con mapping** , quindi selezionare credenziali esistenti dall'elenco o fare clic su **Aggiungi** per creare nuove credenziali. Per rimuovere un mapping a credenziali di sicurezza dall'account di accesso, selezionare le credenziali da **Credenziali con mapping** e fare clic su **Rimuovi**. Per altre informazioni sulle credenziali in generale, vedere [Credenziali &#40;motore di database&#41;](credentials-database-engine.md).  
  
9. Selezionare dall'elenco **Database predefinito** un database predefinito per l'account di accesso. Il valore predefinito per questa opzione è **Master** .  
  
10. Selezionare dall'elenco **Lingua predefinita** una lingua predefinita per l'account di accesso.  
  
11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Opzioni aggiuntive  
 La finestra di dialogo **account di accesso-nuovo** offre inoltre opzioni in altre quattro pagine: **ruoli del server**, **mapping utenti**, **entità a protezione diretta**e **stato**.  
  
### <a name="server-roles"></a>Ruoli del server  
 Nella pagina **Ruoli del server** sono elencati tutti i possibili ruoli che possono essere assegnati al nuovo account accesso. Sono disponibili le opzioni seguenti:  
  
 Casella di controllo**bulkadmin**  
 I membri del ruolo predefinito del server **bulkadmin** sono autorizzati a eseguire l'istruzione BULK INSERT.  
  
 Casella di controllo**dbcreator**  
 I membri del ruolo predefinito del server **dbcreator** sono autorizzati a creare, modificare, eliminare e ripristinare qualsiasi database.  
  
 Casella di controllo**diskadmin**  
 I membri del ruolo predefinito del server **diskadmin** sono autorizzati a gestire file su disco.  
  
 Casella di controllo**processadmin**  
 I membri del ruolo predefinito del server **processadmin** sono autorizzati a terminare processi in esecuzione in un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
 Casella di controllo**public**  
 Tutti gli utenti, gruppi e ruoli di SQL Server appartengono al ruolo predefinito del server **public** per impostazione predefinita.  
  
 Casella di controllo**securityadmin**  
 I membri del ruolo predefinito del server **securityadmin** gestiscono gli account di accesso e le relative proprietà. Possono concedere, negare e revocare le autorizzazioni a livello di server e a livello di database. Questi membri sono inoltre autorizzati a reimpostare le password per gli account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Casella di controllo**serveradmin**  
 I membri del ruolo predefinito del server **serveradmin** sono autorizzati a modificare le opzioni di configurazione a livello di server e ad arrestare il server.  
  
 Casella di controllo**setupadmin**  
 I membri del ruolo predefinito del server **setupadmin** possono aggiungere e rimuovere server collegati e inoltre eseguire alcune stored procedure di sistema.  
  
 Casella di controllo**sysadmin**  
 I membri del ruolo predefinito del server **sysadmin** sono autorizzati a eseguire qualsiasi attività nel [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
### <a name="user-mapping"></a>Mapping utenti  
 Nella pagina **Mapping utenti** sono elencati tutti i possibili database e le appartenenze al ruolo dei database che possono essere applicati all'account di accesso. I database selezionati determinano le appartenenze al ruolo che sono disponibili per l'account di accesso. In questa pagina sono disponibili le opzioni seguenti.  
  
 **Utenti di cui è stato eseguito il mapping all'account di accesso seguente**  
 Consente di selezionare i database ai quali può accedere l'account di accesso specificato. Quando si seleziona un database, i rispettivi ruoli validi vengono visualizzati nel riquadro **Appartenenza a ruoli del database per:** _database_name_.  
  
 **Mappa**  
 Consente all'account di accesso di accedere al database sotto indicato.  
  
 **Database**  
 Elenca i database disponibili sul server.  
  
 **Utente**  
 Consente di specificare l'utente del database a cui eseguire il mapping dell'account di accesso. Per impostazione predefinita, il nome dell'utente del database è uguale all'account di accesso.  
  
 **Schema predefinito**  
 Consente di specificare lo schema predefinito dell'utente. Lo schema predefinito dei nuovi utenti creati è **dbo**. È possibile specificare uno schema predefinito non ancora creato. Non è possibile specificare uno schema predefinito per un utente del quale è stato eseguito il mapping a un gruppo di Windows, un certificato o una chiave asimmetrica.  
  
 **Account Guest abilitato per:**  _database_name_  
 Attributo di sola lettura che indica se l'account Guest è abilitato nel database selezionato. Utilizzare la pagina **Stato** della finestra di dialogo **Proprietà account di accesso** dell'account Guest per abilitare o disabilitare tale account.  
  
 **Appartenenza a ruoli del database per:**  _database_name_  
 Consente di selezionare i ruoli per l'utente nel database specificato. Tutti gli utenti sono membri del ruolo **public** in ogni database e non possono essere eliminati. Per altre informazioni sui ruoli di database, vedere [Ruoli a livello di database](database-level-roles.md).  
  
### <a name="securables"></a>Entità a protezione diretta  
 Nella pagina **Entità a protezione diretta** sono elencate tutte le possibili entità a protezione diretta e le autorizzazioni su quelle entità a protezione diretta che possono essere concesse all'account di accesso. In questa pagina sono disponibili le opzioni seguenti.  
  
 **Griglia superiore**  
 Contiene uno o più elementi per i quali è possibile impostare le autorizzazioni. Le colonne visualizzate nella griglia superiore variano a seconda del tipo di entità o di entità a sicurezza diretta.  
  
 Per aggiungere elementi alla griglia superiore:  
  
1.  Scegliere **Cerca**.  
  
2.  Nella finestra di dialogo **Aggiungi oggetti** selezionare una delle opzioni seguenti: **oggetti specifici...**, **tutti gli oggetti di tipo...** o **il server**_server_name_. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Selezionando **il server**_server_name_ viene automaticamente riempita la griglia superiore con tutti gli oggetti a protezione diretta di tale server.  
  
3.  Se si seleziona **oggetti specifici...**:  
  
    1.  Nella finestra di dialogo **Seleziona oggetti** , in **selezionare questi tipi**di oggetti, fare clic su **tipi di oggetto...**.  
  
    2.  Nella casella del finestra di dialogo **Seleziona tipi di oggetti** e selezionare tutte le seguenti opzioni o solo alcune di esse: **Endpoint**, **Account di accesso**, **Server**, **Gruppi di disponibilità**e **Ruoli del server**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    3.  In **immettere i nomi degli oggetti da selezionare (esempi)**, fare clic su **Sfoglia..**..  
  
    4.  Nella finestra di dialogo **Cerca oggetti** , selezionare gli oggetti disponibili del tipo selezionato nella finestra di dialogo **Seleziona tipi di oggetti** , quindi fare clic su **OK**.  
  
    5.  Nella finestra di dialogo **Seleziona oggetti** fare clic su **OK**.  
  
4.  Se si seleziona **tutti gli oggetti dei tipi...**, nella finestra di dialogo **Seleziona tipi di oggetti** Selezionare uno o tutti i tipi di oggetti seguenti: **endpoint**, **account di accesso**, **Server**, **gruppi di disponibilità**e **ruoli del server**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **Nome**  
 Nome di ogni entità o entità a sicurezza diretta aggiunto alla griglia.  
  
 **Type**  
 Descrive il tipo di ogni elemento.  
  
 **Scheda Esplicita**  
 Sono elencate le possibili autorizzazioni per l'entità a protezione diretta selezionate nella griglia superiore. Non tutte le opzioni sono disponibili per tutte le autorizzazioni esplicite.  
  
 **Autorizzazioni**  
 Nome dell'autorizzazione.  
  
 **Concedente**  
 Entità che ha concesso l'autorizzazione.  
  
 **Grant**  
 Selezionare questa opzione per concedere l'autorizzazione all'account di accesso, deselezionarla per revocare l'autorizzazione.  
  
 **Con diritto di concessione**  
 Riflette lo stato dell'opzione WITH GRANT relativo all'autorizzazione elencata. Il contenuto di questa casella è di sola lettura. Per applicare questa autorizzazione, utilizzare l'istruzione [GRANT](/sql/t-sql/statements/grant-transact-sql) .  
  
 **Negare**  
 Selezionare questa opzione per negare l'autorizzazione all'account di accesso, deselezionarla per revocare l'autorizzazione.  
  
### <a name="status"></a>Stato  
 Nella pagina **Stato** sono elencate alcune opzioni di autenticazione e autorizzazione che possono essere configurate nell'account di accesso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] selezionato.  
  
 In questa pagina sono disponibili le opzioni seguenti.  
  
 **Autorizzazione per la connessione al Motore di database**  
 Quando si utilizza questa impostazione, è consigliabile pensare all'account di accesso selezionato come a un'entità a cui è possibile concedere o negare l'autorizzazione per un'entità a sicurezza diretta.  
  
 Selezionare **Concedi** per concedere l'autorizzazione CONNECT SQL all'account di accesso. Selezionare **Nega** per negare l'autorizzazione CONNECT SQL all'account di accesso.  
  
 **Accesso**  
 Quando si utilizza questa impostazione, è consigliabile pensare all'account di accesso selezionato come a un record in una tabella. Le modifiche ai valori elencati qui verranno applicate al record.  
  
 Un account di accesso che è stato disabilitato continua a esistere come record. Se tuttavia tenta di connettersi a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'account di accesso non viene autenticato.  
  
 Selezionare questa opzione per abilitare o disabilitare l'account di accesso. Questa opzione utilizza l'istruzione ALTER LOGIN insieme all'opzione ENABLE o DISABLE.  
  
 **Autenticazione di SQL Server**  
 L'account di accesso della casella di controllo **è bloccato** è disponibile solo se l'account [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di accesso selezionato si connette utilizzando l'autenticazione di e l'account di accesso è stato bloccato. Questa impostazione è di sola lettura. Per sbloccare un account di accesso bloccato, eseguire l'istruzione ALTER LOGIN con l'opzione UNLOCK.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-create-a-login-using-windows-authentication"></a>Per creare un account di accesso tramite l'autenticazione di Windows  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- Create a login for SQL Server by specifying a server name and a Windows domain account name.  
  
    CREATE LOGIN [<domainName>\<loginName>] FROM WINDOWS;  
    GO  
  
    ```  
  
#### <a name="to-create-a-login-using-sql-server-authentication"></a>Per creare un account di accesso tramite l'autenticazione di SQL Server  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- Creates the user "shcooper" for SQL Server using the security credential "RestrictedFaculty"   
    -- The user login starts with the password "Baz1nga," but that password must be changed after the first login.  
  
    CREATE LOGIN shcooper   
       WITH PASSWORD = 'Baz1nga' MUST_CHANGE,  
       CREDENTIAL = RestrictedFaculty;  
    GO  
  
    ```  
  
 Per altre informazioni, vedere [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
##  <a name="follow-up-steps-to-take-after-you-create-a-login"></a><a name="FollowUp"></a>Completamento: passaggi da eseguire dopo la creazione di un account di accesso  
 Una volta creato, un account di accesso può connettersi a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ma potrebbe non disporre delle autorizzazioni necessarie a eseguire operazioni utili. Nell'elenco seguente vengono indicati alcuni collegamenti alle operazioni più comuni degli account di accesso.  
  
-   Per consentire l'aggiunta di un account di accesso a un ruolo database, vedere [Aggiungere un ruolo](join-a-role.md).  
  
-   Per autorizzare l'utilizzo di un database da parte di un account di accesso, vedere [Creare un utente del database](../authentication-access/create-a-database-user.md).  
  
-   Per concedere un'autorizzazione a un account di accesso, vedere [Concedere un'autorizzazione a un'entità](grant-a-permission-to-a-principal.md).  
  
  
