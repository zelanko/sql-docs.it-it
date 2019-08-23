---
title: Gestione connessione OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbconnection.f1
helpviewer_keywords:
- OLE DB connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], OLE DB
- connections [Integration Services], OLE DB
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d3b1526d55321e5f32a243a48f64bde2f579caa6
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028789"
---
# <a name="ole-db-connection-manager"></a>gestione connessione OLE DB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una gestione connessione OLE DB consente la connessione di un pacchetto a un'origine dati tramite un provider OLE DB. In una gestione connessione OLE DB tramite che si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio, è possibile usare il provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
> [!NOTE]
>  Il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 non supporta le nuove parole chiave per le stringhe di connessione (MultiSubnetFailover=True) per il clustering di failover su più subnet. Per altre informazioni, vedere le [note sulla versione di SQL Server](https://go.microsoft.com/fwlink/?LinkId=247824) e il post di blog [Always On Multi-Subnet Failover and SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/)(Failover su più subnet Always On e SSIS) nel sito www.mattmasson.com.    
> 
> [!NOTE]
>  Se l'origine dati è [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, è richiesto un provider di dati diverso rispetto alle versioni precedenti di Excel o Access. Per altre informazioni, vedere [Connettersi a una cartella di lavoro di Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) e [Connettersi a un database di Access](../../integration-services/connection-manager/connect-to-an-access-database.md).    
    
 La gestione connessione OLE DB viene usata da diversi componenti di flusso di dati e attività di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . L'origine e la destinazione OLE DB, ad esempio, usano questa gestione connessione per estrarre e caricare i dati, mentre l'attività Esegui SQL può usarla per connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'esecuzione delle query.    
    
 La gestione connessione OLE DB viene inoltre utilizzata per accedere alle origini dei dati OLE DB nelle attività personalizzate scritte in codice non gestito che utilizza un linguaggio quale C++.    
    
 Quando si aggiunge una gestione connessione OLE DB a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione OLE DB, imposta le proprietà di tale gestione connessione e quindi la aggiunge alla raccolta **Connessioni** del pacchetto.    
    
 La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **OLEDB**.    
    
 Per configurare la gestione connessione OLE DB, procedere nel modo seguente:    
    
-   Specificare una stringa di connessione configurata in modo da soddisfare i requisiti del provider selezionato.    
    
-   Se richiesto dal provider, includere il nome dell'origine dei dati a cui connettersi.    
    
-   Specificare le credenziali di sicurezza come previsto dal provider selezionato.    
    
-   Indicare se la connessione creata dalla gestione connessione deve essere mantenuta in fase di esecuzione.    
    
## <a name="logging"></a>Registrazione    
 È possibile registrare le chiamate eseguite dalla gestione connessione OLE DB a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi alle connessioni stabilite dalla gestione connessione OLE DB a origini dati esterne. Per registrare le chiamate eseguite dalla gestione connessione OLE DB a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello di pacchetto. Per altre informazioni, vedere [Strumenti per la risoluzione dei problemi relativi all'esecuzione dei pacchetti](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).    
    
## <a name="configuration-of-the-oledb-connection-manager"></a>Configurazione della gestione connessione OLEDB    
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice. Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md). Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere la documentazione per la classe **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** nella Guida per gli sviluppatori.    
    
## <a name="related-content"></a>Contenuto correlato    
    
-   Articolo di Wiki [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670) (Connettori SSIS con Oracle) nel sito Web social.technet.microsoft.com.    
    
-   Articolo tecnico [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744)(Stringhe di connessione per i provider OLE DB) nel sito Web carlprothman.net.    
    
## <a name="configure-ole-db-connection-manager"></a>Configura gestione connessione OLE DB
  Usare la finestra di dialogo **Configura gestione connessione OLE DB** per aggiungere una nuova connessione o una copia di una connessione esistente a un'origine dati.  
  
> [!NOTE]  
>  Se l'origine dati è [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, è richiesta una gestione connessione diversa rispetto alle versioni precedenti di Excel. Per altre informazioni, vedere [Connessione a una cartella di lavoro di Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
>   
>  Se l'origine dati è [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, è richiesto un provider OLE DB diverso rispetto alle versioni precedenti di Access. Per altre informazioni, vedere [Connessione a un database di Access](../../integration-services/connection-manager/connect-to-an-access-database.md).  
  
 Per sapere di più sulla gestione connessione OLE DB, vedere [Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Connessioni dati**  
 Consente di selezionare una connessione dati OLE DB esistente nell'elenco.  
  
 **Proprietà connessione dati**  
 Consente di visualizzare proprietà e valori per la connessione dati OLE DB selezionata.  
  
 **Nuova**  
 Consente di creare una connessione dati OLE DB tramite la finestra di dialogo **Gestione connessione** .  
  
 **Elimina**  
 Selezionare una connessione dati, quindi eliminarla usando il pulsante **Elimina** .  
  
### <a name="managed-identities-for-azure-resources-authentication"></a>Identità gestite per l'autenticazione delle risorse di Azure
Quando si eseguono pacchetti SSIS nel [runtime di integrazione Azure-SSIS in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), è possibile usare l'[identità gestita](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) associata alla data factory per l'autenticazione del database SQL di Azure (o istanza gestita). La factory specificata può accedere e copiare i dati dal database o nel database usando questa identità.

> [!NOTE]
>  Quando si usa l'autenticazione Azure AD (inclusa l'autenticazione identità gestita) per connettersi al database SQL di Azure (o istanza gestita), esistono problemi noti che possono causare un errore di esecuzione del pacchetto o una modifica del comportamento imprevista. Per altre informazioni, vedere [Funzionalità e limitazioni di Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication#azure-ad-features-and-limitations).

Per usare l'autenticazione identità gestita per il database SQL di Azure, seguire questa procedura per configurare il database:

1. **Creare un gruppo in Azure AD.** Impostare l'identità gestita come membro del gruppo.
    
   1. [Trovare l'identità gestita della data factory dal portale di Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). Visualizzare le **Proprietà** della data factory. Copiare l'**ID oggetto identità gestita**.
    
   1. Installare il modulo [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2). Accedere usando il comando `Connect-AzureAD`. Eseguire i comandi seguenti per creare un gruppo e aggiungere l'identità gestita come membro.
      ```powershell
      $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
      Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory managed identity object ID>"
      ```
    
1. **[Effettuare il provisioning di un amministratore di Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** per il server SQL Azure nel portale di Azure, se non è già stato effettuato. L'amministratore di Azure AD può essere un utente di Azure AD o gruppo di Azure AD. Se si concede al gruppo con identità gestita un ruolo di amministratore, ignorare i passaggi 3 e 4. L'amministratore avrà accesso completo al database.

1. **[Creare utenti del database indipendente](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** per il gruppo di Azure AD. Connettersi al database da cui o in cui si vuole copiare i dati usando strumenti come SQL Server Management Studio con un'identità di Azure AD che abbia almeno l'autorizzazione ALTER ANY USER. Eseguire il codice T-SQL seguente: 
    
    ```sql
    CREATE USER [your AAD group name] FROM EXTERNAL PROVIDER;
    ```

1. **Concedere le autorizzazioni necessarie al gruppo di Azure AD** come si farebbe normalmente per gli utenti SQL e altri utenti. Per i ruoli appropriati, vedere [Ruoli a livello di database](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles).  Ad esempio, eseguire il codice seguente:

    ```sql
    ALTER ROLE [role name] ADD MEMBER [your AAD group name];
    ```

Per usare l'autenticazione identità gestita per Istanza gestita di database SQL, seguire questa procedura per configurare il database:
    
1. **[Effettuare il provisioning di un amministratore di Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance)** per l'istanza gestita nel portale di Azure, se non è già stato effettuato. L'amministratore di Azure AD può essere un utente di Azure AD o gruppo di Azure AD. Se si concede al gruppo con identità gestita un ruolo di amministratore, ignorare i passaggi 2-5. L'amministratore avrà accesso completo al database.

1. **[Trovare l'identità gestita della data factory dal portale di Azure](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)** . Visualizzare le **Proprietà** della data factory. Copiare l'**ID applicazione dell'identità gestita** (NON l'**ID oggetto identità gestita**).

1. **Convertire l'identità gestita della data factory in tipo binario**. Connettersi al database **master** nell'istanza gestita usando strumenti come SQL Server Management Studio con l'account amministratore SQL/Active Directory. Eseguire il codice T-SQL seguente nel database **master** per ottenere l'ID applicazione dell'identità gestita in formato binario:
    
    ```sql
    DECLARE @applicationId uniqueidentifier = '{your managed identity application ID}'
    select CAST(@applicationId AS varbinary)
    ```

1. **Aggiungere l'identità gestita delle data factory come utente** in Istanza gestita di database SQL di Azure. Eseguire il codice T-SQL seguente nel database **master**:
    
    ```sql
    CREATE LOGIN [{a name for the managed identity}] FROM EXTERNAL PROVIDER with SID = {your managed identity application ID as binary}, TYPE = E
    ```

1. **Concedere all'identità gestita della data factory le autorizzazioni necessarie**. Per i ruoli appropriati, vedere [Ruoli a livello di database](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles). Eseguire il codice T-SQL seguente nel database da cui o in cui si vuole copiare i dati:

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE [role name] ADD MEMBER [{the managed identity name}]
    ```

Quindi **configurare il provider OLE DB** per la gestione connessione OLE DB. Sono disponibili due opzioni.
    
1. Configurare in fase di progettazione. In Progettazione SSIS fare doppio clic sulla gestione connessione OLE DB per aprire la finestra **Gestione connessione**. Nell'elenco a discesa **Provider** selezionare [**Microsoft OLE DB Driver for SQL Server**](https://go.microsoft.com/fwlink/?linkid=871294).
    > [!NOTE]
    >  È possibile che altri provider inclusi nell'elenco a discesa NON supportino l'autenticazione identità gestita.
    
1. Configurare in fase di esecuzione. Quando si esegue il pacchetto tramite [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) oppure l'[attività Esegui pacchetto SSIS di Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), trovare la proprietà della gestione connessione **ConnectionString**  per la gestione connessione OLE DB e aggiornare la proprietà di connessione **Provider** impostandola su **MSOLEDBSQL**, ovvero Microsoft OLE DB Driver for SQL Server.
    ```vb
    Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
    ```

Infine **configurare l'autenticazione identità gestita** per la gestione connessione OLE DB. Sono disponibili due opzioni.
    
1. Configurare in fase di progettazione. In Progettazione SSIS fare clic con il pulsante destro del mouse sulla gestione connessione OLE DB e fare clic su **Proprietà** per aprire la **finestra Proprietà**. Aggiornare la proprietà **ConnectUsingManagedIdentity** impostandola su **True**.
    > [!NOTE]
    >  Attualmente la proprietà di gestione connessione **ConnectUsingManagedIdentity** NON ha effetto (ovvero l'autenticazione identità gestita non funziona) quando il pacchetto SSIS viene eseguito in Progettazione SSIS o [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server.

1. Configurare in fase di esecuzione. Quando il pacchetto viene eseguito tramite SQL Server Management Studio (SSMS) o l'attività Esegui pacchetto SSIS, individuare la gestione connessione OLE DB e aggiornarne la proprietà **ConnectUsingManagedIdentity** impostandola su **True**.
    > [!NOTE]
    >  Nel runtime di integrazione Azure-SSIS tutti gli altri metodi di autenticazione, ad esempio la sicurezza integrata e la password, preconfigurati nella gestione connessione OLE DB verranno **ignorati** quando viene usata l'autenticazione identità gestita per stabilire la connessione al database.

> [!NOTE]
>  Per configurare l'autenticazione identità gestita nei pacchetti esistenti, il metodo consigliato consiste nel ricompilare almeno una volta il progetto SSIS con l'[ultima versione di Progettazione SSIS](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) e ridistribuire il progetto SSIS nel runtime di integrazione Azure-SSIS in modo che la nuova proprietà di gestione connessione **ConnectUsingManagedIdentity** venga aggiunta automaticamente in tutte le gestioni connessione OLE DB nel progetto SSIS. In alternativa, è possibile usare direttamente l'override della proprietà con il percorso della proprietà **\Package.Connections[{nome della gestione connessione}].Properties[ConnectUsingManagedIdentity]** in fase di esecuzione.

## <a name="see-also"></a>Vedere anche    
 [Origine OLE DB](../../integration-services/data-flow/ole-db-source.md)     
 [Destinazione OLE DB](../../integration-services/data-flow/ole-db-destination.md)     
 [Attività Esegui SQL](../../integration-services/control-flow/execute-sql-task.md)     
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
