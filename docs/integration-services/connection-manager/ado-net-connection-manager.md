---
title: Gestione connessione ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetconnection.f1
helpviewer_keywords:
- connection managers [Integration Services], ADO.NET
- ADO.NET connection manager [Integration Services]
- connections [Integration Services], ADO.NET
ms.assetid: fc5daa2f-0159-4bda-9402-c87f1035a96f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bee4d3ea71aaeacf682a6e90fad91786fa7a0c9c
ms.sourcegitcommit: e92ce0f59345fe61c0dd3bfe495ef4b1de469d4b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/25/2019
ms.locfileid: "66221179"
---
# <a name="adonet-connection-manager"></a>Gestione connessione ADO.NET

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] consente l'accesso di un pacchetto alle origini dati tramite un provider .NET. Questa gestione connessione viene di solito usata per accedere a origini dati quali [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nonché a origini dati esposte tramite OLE DB e XML in attività personalizzate scritte in codice gestito, usando un linguaggio come C#.  
  
 Quando si aggiunge una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a un pacchetto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , imposta le proprietà della gestione connessione, quindi aggiunge quest'ultima alla raccolta delle **connessioni** del pacchetto.  
  
 La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **ADO.NET**. Il valore di **ConnectionManagerType** è qualificato con il nome del provider .NET usato dalla gestione connessione.  
  
## <a name="adonet-connection-manager-troubleshooting"></a>Risoluzione dei problemi relativi alla gestione connessione ADO.NET  
 È possibile registrare le chiamate eseguite dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi alle connessioni stabilite dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a origini dati esterne. Per registrare le chiamate eseguite dalla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello di pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Durante la lettura da parte di una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , i dati di alcuni tipi di dati date di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genereranno i risultati mostrati nella tabella seguente.  
  
|Tipo di dati di SQL Server|Risultato|  
|--------------------------|------------|  
|**time**, **datetimeoffset**|L'esecuzione del pacchetto non viene completata correttamente, a meno che non vengano utilizzati comandi SQL con parametri. È necessario servirsi dell'attività Esegui SQL nel pacchetto per utilizzare i comandi SQL con parametri. Per altre informazioni, vedere [Attività Esegui SQL](../../integration-services/control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663).|  
|**datetime2**|La gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] tronca il valore relativo ai millisecondi.|  
  
> [!NOTE]  
>  Per altre informazioni sui tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sul relativo mapping nei tipi di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) e [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="adonet-connection-manager-configuration"></a>Configurazione della gestione connessione ADO.NET  
 Per configurare una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , procedere nel modo seguente:  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
-   Specificare una stringa di connessione configurata in modo da soddisfare i requisiti del provider .NET selezionato.  
  
-   Se richiesto dal provider, includere il nome dell'origine dei dati a cui connettersi.  
  
-   Specificare le credenziali di sicurezza come previsto dal provider selezionato.  
  
-   Indicare se la connessione creata dalla gestione connessione deve essere mantenuta in fase di esecuzione.  
  
 Molte delle opzioni di configurazione della gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] dipendono dal provider .NET usato dalla gestione connessione.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Configura gestione connessione ADO.NET](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="configure-adonet-connection-manager"></a>Configura gestione connessione ADO.NET
  Utilizzare la finestra di dialogo **Configura gestione connessione ADO.NET** per aggiungere una connessione a un'origine dati accessibile mediante un provider di dati .NET Framework, ad esempio il provider SqlClient. La gestione connessione può utilizzare una connessione esistente oppure è possibile crearne una nuova.  
  
 Per ulteriori informazioni sulla gestione connessione ADO.NET, vedere [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Connessioni dati**  
 Consente di selezionare una connessione dati ADO.NET esistente nell'elenco.  
  
 **Proprietà connessione dati**  
 Consente di visualizzare proprietà e valori per la connessione dati ADO.NET selezionata.  
  
 **Nuova**  
 Consente di creare una connessione dati ADO.NET tramite la finestra di dialogo **Gestione connessione** .  
  
 **Elimina**  
 Selezionare una connessione e quindi eliminarla utilizzando il pulsante **Elimina** .  
  
### <a name="managed-identities-for-azure-resources-authentication"></a>Identità gestite per l'autenticazione delle risorse di Azure
Quando si eseguono pacchetti SSIS nel [runtime di integrazione Azure-SSIS in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), è possibile usare l'[identità gestita](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) associata alla data factory per l'autenticazione del database SQL di Azure (o istanza gestita). La factory specificata può accedere e copiare i dati dal database o nel database usando questa identità.

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

1. **Concedere le autorizzazioni necessarie al gruppo di Azure AD** come si farebbe normalmente per gli utenti SQL e altri utenti. Ad esempio, eseguire il codice seguente:

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

1. **Concedere all'identità gestita della data factory le autorizzazioni necessarie**. Eseguire il codice T-SQL seguente nel database da cui o in cui si vuole copiare i dati:

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE db_owner ADD MEMBER [{the managed identity name}]
    ```

Infine **configurare l'autenticazione identità gestita** per la gestione connessione ADO.NET. Sono disponibili due opzioni.
    
1. Configurare in fase di progettazione. In Progettazione SSIS fare clic con il pulsante destro del mouse sulla gestione connessione ADO.NET e fare clic su **Proprietà** per aprire la **finestra Proprietà**. Aggiornare la proprietà **ConnectUsingManagedIdentity** impostandola su **True**.
    > [!NOTE]
    >  Attualmente la proprietà di gestione connessione **ConnectUsingManagedIdentity** NON ha effetto (ovvero l'autenticazione identità gestita non funziona) quando il pacchetto SSIS viene eseguito in Progettazione SSIS o [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server.
    
1. Configurare in fase di esecuzione. Quando il pacchetto viene eseguito tramite [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) o l'[attività Esegui pacchetto SSIS di Azure Data Factory](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), individuare la gestione connessione ADO.NET e aggiornarne la proprietà **ConnectUsingManagedIdentity** impostandola su **True**.
    > [!NOTE]
    >  Nel runtime di integrazione Azure-SSIS tutti gli altri metodi di autenticazione, ad esempio l'autenticazione integrata e la password, preconfigurati nella gestione connessione ADO.NET verranno **ignorati** quando viene usata l'autenticazione identità gestita per stabilire la connessione al database.

> [!NOTE]
>  Per configurare l'autenticazione identità gestita nei pacchetti esistenti, assicurarsi di ricompilare almeno una volta il progetto SSIS con l'[ultima versione di Progettazione SSIS](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) e di ridistribuire il progetto SSIS nel runtime di integrazione Azure-SSIS in modo che la nuova proprietà di gestione connessione **ConnectUsingManagedIdentity** venga aggiunta automaticamente in tutte le gestioni connessione ADO.NET nel progetto SSIS.

## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
