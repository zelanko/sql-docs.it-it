---
title: Extensible Key Management TDE di SQL Server con Azure Key Vault - Passaggi di configurazione | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2018
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault setup
- SQL Server Connector, setup
- SQL Server Connector
ms.assetid: c1f29c27-5168-48cb-b649-7029e4816906
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: d25a38a0c7bd274e07d0932d6b8ef451a22dda06
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2019
ms.locfileid: "58306079"
---
# <a name="sql-server-tde-extensible-key-management-using-azure-key-vault---setup-steps"></a>Extensible Key Management TDE di SQL Server con Azure Key Vault - Passaggi di configurazione
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Questa procedura dettagliata spiega come installare e configurare il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per Azure Key Vault.  
  
## <a name="before-you-start"></a>Prima di iniziare  
 Per usare l'insieme di credenziali delle chiavi di Azure con SQL Server, vanno soddisfatti alcuni prerequisiti:  
  
-   È necessaria una sottoscrizione di Azure  
  
-   Installare la versione più recente di [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) 5.2.0 o successiva.  

-   Creare Azure Active Directory  

-   Acquisire familiarità con le entità di archiviazione EKM che usano l'insieme di credenziali delle chiavi di Azure leggendo l'argomento [Extensible Key Management con l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  

-   Verificare che sia installata la versione appropriata di Visual Studio C++ Redistributable nella versione di SQL Server in esecuzione:
  
Versione di SQL Server  |Collegamento di installazione ridistribuibile    
---------|--------- 
2008, 2008 R2, 2012, 2014 | [Visual C++ Redistributable Package per Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=40784)    
2016 | [Visual C++ Redistributable per Visual Studio 2015](https://www.microsoft.com/download/details.aspx?id=48145)    
 
  
## <a name="part-i-set-up-an-azure-active-directory-service-principal"></a>Parte 1: Configurare un'entità servizio di Azure Active Directory  
 Per concedere le autorizzazioni di accesso di SQL Server all'insieme di credenziali delle chiavi di Azure, è necessario un account dell'entità servizio in Azure Active Directory (AAD).  
  
1.  Andare al [portale di Azure ](https://ms.portal.azure.com/) ed eseguire l'accesso.  
  
2.  Registrare un'applicazione con Azure Active Directory. Per istruzioni dettagliate su come registrare un'applicazione, vedere la sezione **Get an identity for the application** (Ottenere un'identità per l'applicazione) del post di blog [Azure Key Vault](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)(Insieme di credenziali delle chiavi di Azure).  
  
3.  Copiare l' **ID client** e il **segreto client** per un passaggio successivo durante il quale verranno usati per concedere l'accesso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] all'insieme di credenziali delle chiavi.  
  
 ![ekm-client-id](../../../relational-databases/security/encryption/media/ekm-client-id.png "ekm-client-id")  
  
 ![ekm-key-id](../../../relational-databases/security/encryption/media/ekm-key-id.png "ekm-key-id")  
  
## <a name="part-ii-create-a-key-vault-and-key"></a>Parte 2: Creare un insieme di credenziali delle chiavi e una chiave  
 L'insieme di credenziali delle chiavi e la chiave creata in questo passaggio verranno usate dal motore di database di SQL Server per la protezione della chiave di crittografia.  
  
> [!IMPORTANT]  
>  La sottoscrizione in cui viene creato l'insieme di credenziali delle chiavi deve trovarsi nella stessa istanza predefinita di Azure Active Directory in cui è stata creata l'entità servizio di Azure Active Directory. Per usare un'istanza di Active Directory diversa da quella predefinita per la creazione di un'entità servizio per il Connettore SQL Server, è necessario modificare Active Directory predefinito nell'account di Azure prima di creare l'insieme di credenziali delle chiavi. Per informazioni su come cambiare da Active Directory predefinito all'istanza desiderata, vedere le [Domande frequenti](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB)di Connettore SQL Server.  
  
1.  **Aprire e accedere a PowerShell**  
  
     Installare e avviare la versione più recente di [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) 5.2.0 o successiva. Accedere al proprio account Azure con il comando seguente:  
  
    ```powershell  
    Connect-AzAccount  
    ```  
  
     L'istruzione restituisce:  
  
    ```  
    Environment           : AzureCloud  
    Account               : <account_name>  
    TenantId              : <tenant_id>  
    SubscriptionId        : <subscription_id>  
    CurrentStorageAccount :  
    ```  
  
    > [!NOTE]  
    >  Se si hanno più sottoscrizioni e si vuole specificare quale usare per l'insieme di credenziali, usare `Get-AzSubscription` per visualizzare le sottoscrizioni e `Select-AzSubscription` per scegliere quella appropriata. In caso contrario, PowerShell ne selezionerà automaticamente una per impostazione predefinita.  
  
2.  **Creare un nuovo gruppo di risorse**  
  
     Tutte le risorse di Azure create con Azure Resource Manager devono essere incluse in gruppi di risorse. Creare un gruppo di risorse per ospitare l'insieme di credenziali delle chiavi. In questo esempio viene utilizzato `ContosoDevRG`. Scegliere un nome **univoco** per il gruppo di risorse e l'insieme di credenziali delle chiavi perché tutti i nomi di insiemi di credenziali delle chiavi sono univoci a livello globale.  
  
    ```powershell  
    New-AzResourceGroup -Name ContosoDevRG -Location 'East Asia'  
    ```  
  
     L'istruzione restituisce:  
  
    ```  
    ResourceGroupName: ContosoDevRG  
    Location         : eastasia  
    ProvisioningState: Succeeded  
    Tags             :   
    ResourceId       : /subscriptions/<subscription_id>/  
                        resourceGroups/ContosoDevRG  
    ```  
  
    > [!NOTE]  
    >  Per `-Location parameter`usare il comando `Get-AzureLocation` per determinare come specificare un percorso alternativo rispetto a quello di questo esempio. Per altre informazioni, digitare: `Get-Help Get-AzureLocation`  
  
3.  **Creare un insieme di credenziali delle chiavi**  
  
     Il cmdlet `New-AzKeyVault` richiede il nome di un gruppo di risorse, un nome dell'insieme di credenziali delle chiavi e una posizione geografica. Ad esempio, per un insieme di credenziali delle chiavi denominato `ContosoDevKeyVault`, digitare:  
  
    ```powershell  
    New-AzKeyVault -VaultName 'ContosoDevKeyVault' `  
       -ResourceGroupName 'ContosoDevRG' -Location 'East Asia'  
    ```  
  
     Registrare il nome dell'insieme di credenziali delle chiavi.  
  
     L'istruzione restituisce:  
  
    ```  
    Vault Name                       : ContosoDevKeyVault  
    Resource Group Name              : ContosoDevRG  
    Location                         : East Asia  
    ResourceId                       : /subscriptions/<subscription_id>/  
                                        resourceGroups/ContosoDevRG/providers/  
                                        Microsoft/KeyVault/vaults/ContosoDevKeyVault  
    Vault URI: https://ContosoDevKeyVault.vault.azure.net  
    Tenant ID                        : <tenant_id>  
    SKU                              : Standard  
    Enabled For Deployment?          : False  
    Enabled For Template Deployment? : False  
    Enabled For Disk Encryption?     : False  
    Access Policies                  :  
             Tenant ID              : <tenant_id>  
             Object ID              : <object_id>  
             Application ID         :   
             Display Name           : <display_name>  
             Permissions to Keys    : get, create, delete, list, update, import,   
                                      backup, restore  
             Permissions to Secrets : all  
    Tags                             :  
    ```  
  
4.  **Concedere le autorizzazioni per consentire all'entità servizio di Azure Active Directory di accedere all'insieme di credenziali delle chiavi**  
  
     È possibile autorizzare altri utenti e applicazioni a usare l'insieme di credenziali delle chiavi.   
    In questo caso, l'entità servizio di Azure Active Directory creata nella parte 1 viene usata per autorizzare l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    > [!IMPORTANT]  
    >  L'entità servizio di Azure Active Directory deve avere almeno le autorizzazioni `get`, `wrapKey` e `unwrapKey` per l'insieme di credenziali delle chiavi.  
  
     Come illustrato di seguito, usare l' **ID client** della parte 1 per il parametro `ServicePrincipalName` . `Set-AzKeyVaultAccessPolicy` viene eseguito automaticamente e non produce output se riesce.  
  
    ```powershell  
    Set-AzKeyVaultAccessPolicy -VaultName 'ContosoDevKeyVault'`  
      -ServicePrincipalName EF5C8E09-4D2A-4A76-9998-D93440D8115D `  
      -PermissionsToKeys get, wrapKey, unwrapKey  
    ```  
  
     Chiamare il cmdlet `Get-AzKeyVault` per verificare le autorizzazioni. Nella sezione "Criteri di accesso" dell'output dell'istruzione il nome dell'applicazione AAD dovrebbe essere elencato come un altro tenant che ha accesso a questo insieme di credenziali delle chiavi.  
  
       
5.  **Generare una chiave asimmetrica nell'insieme di credenziali delle chiavi**  
  
     Esistono due modi per generare una chiave in Azure Key Vault: 1) importare una chiave esistente o 2) creare una nuova chiave.  
                  
      > [!NOTE]
        >  SQL Server supporta solo chiavi RSA a 2048 bit.
        
    ### <a name="best-practice"></a>Procedura consigliata:
    
    Per garantire un ripristino rapido della chiave e accedere ai dati all'esterno di Azure, si consiglia la procedura consigliata seguente:
 
    1. Creare la chiave di crittografia in locale in un dispositivo HSM locale. Verificare che si tratti di una chiave RSA 2048 asimmetrica, in modo che sia supportata da SQL Server.
    2. Importare la chiave di crittografia nell'insieme di credenziali delle chiavi di Azure. Vedere i passaggi seguenti per informazioni su come eseguire questa operazione.
    3. Prima di usare la chiave nell'insieme di credenziali delle chiavi di Azure per la prima volta, eseguire un backup di questa chiave. Altre informazioni sul comando [Backup-AzureKeyVaultKey](/sql/relational-databases/security/encryption/setup-steps-for-extensible-key-management-using-the-azure-key-vault) .
    4. Ogni volta che vengono apportate modifiche alla chiave, ad esempio si aggiungono elenchi di controllo di accesso, tag o attributi chiave, assicurarsi di eseguire un altro backup della chiave di Azure Key Vault.

        > [!NOTE]  
        >  Il backup di una chiave è un'operazione relativa alla chiave di Azure Key Vault che restituisce un file che può essere salvato in qualsiasi posizione.

    ### <a name="types-of-keys"></a>Tipi di chiavi:
    In Azure Key Vault è possibile generare due tipi di chiavi che funzioneranno con SQL Server. Entrambe sono chiavi asimmetriche RSA a 2048 bit.  
  
    -   **Protetta da software:** elaborata nel software e crittografata quando inattiva. Le operazioni sulle chiavi protette da software vengono eseguite in Macchine virtuali di Azure. Consigliato per le chiavi non usate in una distribuzione di produzione.  
  
    -   **Protetta da HSM:** creata e protetta da un modulo di protezione hardware (HSM) per una maggiore sicurezza. Il costo è di circa 1 dollaro per ogni versione della chiave.  
  
        > [!IMPORTANT]  
        >  Connettore SQL Server richiede che il nome della chiave usi solo i caratteri "a-z", "A-Z", "0-9" e "-", con un limite di 26 caratteri.   
        > Versioni diverse della chiave con lo stesso nome di chiave nell'insieme di credenziali delle chiavi di Azure non funzioneranno con il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per ruotare una chiave di Azure Key Vault usata da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere i passaggi relativi al rollover della chiave in [Manutenzione e risoluzione dei problemi di Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md).  

    ### <a name="import-an-existing-key"></a>Importare una chiave esistente   
  
    Se si ha una chiave protetta da software RSA a 2048 bit, è possibile caricarla nell'insieme di credenziali delle chiavi di Azure. Ad esempio, se si vuole caricare nell'insieme di credenziali delle chiavi di Azure un file PFX salvato nell'unità `C:\\` in un file denominato `softkey.pfx` , digitare quanto segue per impostare la variabile `securepfxpwd` per una password di `12987553` per il file PFX:  
  
    ``` powershell  
    $securepfxpwd = ConvertTo-SecureString -String '12987553' `  
      -AsPlainText -Force  
    ```  
  
    Quindi digitare quanto segue per importare la chiave dal file PFX, che protegge la chiave con l'hardware (consigliato) nel servizio dell'insieme di credenziali delle chiavi:  
  
    ``` powershell  
        Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' `  
          -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' `  
          -KeyFilePassword $securepfxpwd $securepfxpwd  -Destination 'HSM'  
    ```  
 
    > [!IMPORTANT]  
    > L'importazione della chiave asimmetrica è consigliata per gli scenari di produzione in quanto consente all'amministratore di depositare la chiave in un sistema di deposito delle chiavi. Se la chiave asimmetrica viene creata nell'insieme di credenziali, non potrà essere depositata perché la chiave privata non può mai lasciare l'insieme di credenziali. È consigliabile depositare le chiavi usate per proteggere i dati critici. La perdita di una chiave asimmetrica causa una perdita dei dati permanente.  

    ### <a name="create-a-new-key"></a>Creare una nuova chiave
    #### <a name="example"></a>Esempio:  
    In alternativa, è possibile creare una nuova chiave di crittografia direttamente in Azure Key Vault e proteggerla con il software o con il modulo di protezione hardware (HSM).  In questo esempio viene creata una chiave protetta da software con `Add-AzureKeyVaultKey cmdlet`:  

    ``` powershell  
    Add-AzureKeyVaultKey -VaultName 'ContosoDevKeyVault' `  
      -Name 'ContosoRSAKey0' -Destination 'Software'  
    ```  
  
    L'istruzione restituisce:  
  
    ```  
    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes  
    Key        :  {"kid":"https:contosodevKeyVault.azure.net/keys/  
                   ContosoRSAKey0/<guid>","dty":"RSA:,"key_ops": ...  
    VaultName  : contosodevkeyvault  
    Name       : contosoRSAKey0  
    Version    : <guid>  
    Id         : https://contosodevkeyvault.vault.azure.net:443/  
                 keys/ContosoRSAKey0/<guid>  
    ```  
 > [!IMPORTANT]  
    >  L'insieme di credenziali delle chiavi supporta più versioni della stessa chiave denominata, ma le chiavi da usare con il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non devono essere con controllo delle versioni o rollback. Se l'amministratore vuole eseguire il rollback della chiave usata per la crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , sarà necessario creare una nuova chiave con un nome diverso nell'insieme di credenziali e usarla per crittografare la chiave DEK.  
   
  
## <a name="part-iii-install-the-includessnoversionincludesssnoversion-mdmd-connector"></a>Parte 3: Installare il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 È possibile scaricare il Connettore SQL Server dall' [Area download Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=521700). Questa operazione deve essere eseguita dall'amministratore del computer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  

> [!NOTE]  
>  Le versioni 1.0.0.440 e precedenti sono state sostituite e non sono più supportate negli ambienti di produzione. Eseguire l'aggiornamento alla versione 1.0.1.0 o successiva visitando l'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=45344) e seguendo le istruzioni nella pagina [Manutenzione e risoluzione dei problemi di Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md) in "Aggiornamento del Connettore SQL Server".

> [!NOTE]  
> La versione 1.0.5.0 presenta una modifica che causa un'interruzione, associata all'algoritmo di identificazione personale. Dopo l'aggiornamento alla versione 1.0.5.0 può verificarsi un errore di ripristino del database. Consultare l'articolo della KB [447099](https://support.microsoft.com/help/4470999/db-backup-problems-to-sql-server-connector-for-azure-1-0-5-0).
  
 ![ekm-connector-install](../../../relational-databases/security/encryption/media/ekm-connector-install.png "ekm-connector-install")  
  
 Per impostazione predefinita, il connettore viene installato in C:\Programmi\Connettore SQL Server per Insieme credenziali chiavi Microsoft Azure. Questo percorso può essere modificato durante l'installazione. Se si modifica il percorso, apportare la modifica negli script riportati di seguito.  
  
 Non è disponibile alcuna interfaccia per il Connettore, ma se l'installazione è stata eseguita correttamente, nel computer viene installato **Microsoft.AzureKeyVaultService.EKM.dll** . Si tratta della DLL del provider di crittografia EKM che deve essere registrata con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando l'istruzione `CREATE CRYPTOGRAPHIC PROVIDER` .  
  
 L'installazione del Connettore SQL Server consente anche di scaricare facoltativamente gli script di esempio per la crittografia di SQL Server.  
  
 Nell'appendice alla fine di questo argomento sono riportate le spiegazioni dei codici di errore, le impostazioni di configurazione o le attività di manutenzione di SQL Server Connector:  
  
-   [A. Istruzioni di manutenzione per Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixA)  
  
-   [C. Spiegazione dei codici di errore per Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixC)  
  
  
## <a name="part-iv-configure-includessnoversionincludesssnoversion-mdmd"></a>Parte 4: Configurare[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 Vedere [B. Domande frequenti](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md#AppendixB) per visualizzare una nota sui livelli minimi di autorizzazione necessari per ogni azione in questa sezione.  
  
1.  **Avviare sqlcmd.exe o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Studio**  
  
2.  **Configurare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per usare EKM**  
  
     Eseguire lo script [!INCLUDE[tsql](../../../includes/tsql-md.md)] seguente per configurare [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e usare un provider EKM.  
  
    ```sql  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1;  
    GO  
    RECONFIGURE;  
    GO  
  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1;  
    GO  
    RECONFIGURE;  
    ```  
  
3.  **Registrare (creare) il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come provider EKM con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     -- Creare un provider di crittografia usando il Connettore [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che rappresenta un provider EKM per Azure Key Vault.    
    Questo esempio usa il nome `AzureKeyVault_EKM_Prov`.  
  
    ```sql  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO  
    ```  
  
    > [!NOTE]  
    >  La lunghezza del percorso file non può superare i 256 caratteri.  
  
  
4.  **Configurare le credenziali [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per usare l'insieme di credenziali delle chiavi**  
  
     È necessario aggiungere le credenziali a ogni account di accesso che esegue la crittografia usando una chiave dall'insieme di credenziali delle chiavi. Ciò potrebbe includere:  
  
    -   L'account di accesso dell'amministratore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che usa l'insieme di credenziali delle chiavi per configurare e gestire gli scenari di crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   Altri account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che possono abilitare Transparent Data Encryption (TDE) o altre funzionalità di crittografia di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
     Esiste un mapping uno-a-uno tra le credenziali e gli account di accesso. In altre parole, ogni account di accesso deve avere credenziali univoche.  
  
     Modificare lo script [!INCLUDE[tsql](../../../includes/tsql-md.md)] sottostante nei modi seguenti:  
  
    -   Modificare l'argomento `IDENTITY` (`ContosoDevKeyVault`) in modo che punti all'insieme di credenziali delle chiavi di Azure.
        - Se si usa **Azure globale**, sostituire l'argomento `IDENTITY` con il nome di Azure Key Vault dalla parte II.
        - Se si usa un **cloud privato di Azure** , ad esempio Azure per enti pubblici, Azure Cina o Azure Germania, sostituire l'argomento `IDENTITY` con l'URI dell'insieme di credenziali restituito nella parte II, passaggio 3. Non includere "https://" nell'URI dell'insieme di credenziali.   
    -   Sostituire la prima parte dell'argomento `SECRET` con l' **ID client** di Azure Active Directory della parte 1. In questo esempio l' **ID client** è `EF5C8E094D2A4A769998D93440D8115D`.  
  
        > [!IMPORTANT]  
        >  È necessario rimuovere i trattini dall' **ID Client**.  
  
    -   Completare la seconda parte dell'argomento `SECRET` con il **segreto client** della parte I. In questo esempio il **segreto client** della parte I è `Replace-With-AAD-Client-Secret`. La stringa finale dell'argomento `SECRET` sarà una lunga sequenza di lettere e numeri *senza trattini*.  
  
    ```sql  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoDevKeyVault', -- for public Azure
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.usgovcloudapi.net', -- for Azure Government
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.azure.cn', -- for Azure China
        -- WITH IDENTITY = 'ContosoDevKeyVault.vault.microsoftazure.de', -- for Azure Germany   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DReplace-With-AAD-Client-Secret'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;  
  
    -- Add the credential to the SQL Server administrator's domain login   
    ALTER LOGIN [<domain>\<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     Per un esempio dell'uso delle variabili per gli argomenti **CREATE CREDENTIAL** e della rimozione dei trattini dall'ID client a livello di codice, vedere [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md).  
  
5.  **Aprire la chiave dell'insieme di credenziali delle chiavi di Azure in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**  
  
     Se è stata importata una chiave asimmetrica come descritto nella parte 2, aprire la chiave fornendo il nome della chiave nello script [!INCLUDE[tsql](../../../includes/tsql-md.md)] seguente.  
  
    -   Sostituire `CONTOSO_KEY` con il nome che si vuole assegnare alla chiave in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    -   Sostituire `ContosoRSAKey0` con il nome della chiave nell'insieme di credenziali delle chiavi di Azure.  
  
    ```sql  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoRSAKey0',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
## <a name="next-step"></a>Passaggio successivo  
  
Ora che è stata completata la configurazione di base, vedere come [Usare Connettore SQL Server con le funzionalità di crittografia SQL](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)   
  
## <a name="see-also"></a>Vedere anche  
 [Extensible Key Management tramite l'insieme di credenziali delle chiavi di Azure](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)   
[Manutenzione e risoluzione dei problemi di Connettore SQL Server](../../../relational-databases/security/encryption/sql-server-connector-maintenance-troubleshooting.md)
