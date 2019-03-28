---
title: 'Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS | Microsoft Docs'
ms.custom: ''
ms.date: 10/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: a24f7577a5ac01b3bc035bd68056de3a95fa156c
ms.sourcegitcommit: 2111068372455b5ec147b19ca6dbf339980b267d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/25/2019
ms.locfileid: "58417153"
---
# <a name="tutorial-getting-started-with-always-encrypted-with-secure-enclaves-using-ssms"></a>Esercitazione: Introduzione ad Always Encrypted con enclave sicuri tramite SSMS
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa esercitazione illustra come iniziare a usare [Always Encrypted con enclave sicuri](encryption/always-encrypted-enclaves.md). L'esercitazione spiega:
- Come creare un ambiente di base per i test e la valutazione di Always Encrypted con enclave sicuri.
- Come crittografare i dati in locale ed eseguire query avanzate su colonne crittografate usando SQL Server Management Studio (SSMS).

## <a name="prerequisites"></a>Prerequisites

Per iniziare a usare Always Encrypted con enclave sicuri sono necessari almeno due computer (possono essere macchine virtuali):

- Il computer SQL Server per ospitare SQL Server e SSMS.
- Il computer del servizio Sorveglianza host (HGS) in cui eseguire il servizio, necessario per l'attestazione dell'enclave.

### <a name="sql-server-computer-requirements"></a>Requisiti per il computer SQL Server

- [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] o versioni successive
- Windows 10 Enterprise versione 1809 o Windows Server 2019 Datacenter
- [SQL Server Management Studio (SSMS) 18.0 o versioni successive](../../ssms/download-sql-server-management-studio-ssms.md).

In alternativa è possibile installare SSMS in un altro computer.

>[!WARNING] 
>Negli ambienti di produzione non si dovrebbe mai usare SSMS o altri strumenti per la gestione di chiavi Always Encrypted o l'esecuzione di query su dati crittografati nel computer SQL Server, in quanto ciò può ridurre o annullare completamente lo scopo dell'uso di Always Encrypted.

### <a name="hgs-computer-requirements"></a>Requisiti per il computer HGS

- Windows Server 2019 Standard o Datacenter Edition
- 2 CPU
- 8 GB di RAM
- 100 GB di spazio di archiviazione

>[!NOTE]
>Il computer HGS non deve appartenere a un dominio prima di iniziare la procedura.

## <a name="step-1-configure-the-hgs-computer"></a>Passaggio 1: Configurare il computer HGS

In questo passaggio si configura il computer HGS per eseguire il servizio Sorveglianza host che supporta l'attestazione chiave host.

1. Accedere al computer del servizio HGS come amministratore (amministratore locale), aprire una console di Windows PowerShell con privilegi elevati e aggiungere il ruolo del servizio Sorveglianza host eseguendo il comando seguente:

   ```powershell
   Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
   ```

2. Dopo il riavvio del computer HGS, accedere nuovamente con l'account di amministratore, aprire una console di Windows PowerShell con privilegi elevati ed eseguire i comandi seguenti per installare il servizio Sorveglianza host e configurare il dominio corrispondente. La password specificata in questo contesto verrà applicata solo come password Modalità di ripristino dei servizi directory per Active Directory, ma non modificherà la password di accesso dell'account amministratore. È possibile specificare qualsiasi nome di dominio per -HgsDomainName.

   ```powershell
   $adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force
   Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
   ```

3. Dopo un ulteriore riavvio del computer, accedere con l'account di amministratore (ora anche amministratore di dominio), aprire una console di Windows PowerShell con privilegi elevati e configurare l'attestazione chiave host per l'istanza del servizio HGS. 

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey  
   ```

4. Trovare l'indirizzo IP del computer HGS eseguendo il comando seguente. Salvare questo indirizzo IP per i passaggi successivi.

   ```powershell
   Get-NetIPAddress  
   ```

>[!NOTE]
>In alternativa, per fare riferimento al computer HGS mediante un nome DNS, è possibile configurare un server di inoltro dai server DNS aziendali al nuovo controller di dominio HGS.  

## <a name="step-2-configure-the-sql-server-computer-as-a-guarded-host"></a>Passaggio 2: Configurare il computer SQL Server come host sorvegliato
In questo passaggio si configura il computer SQL Server come host controllato registrato con HGS usando l'attestazione chiave host.
>[!NOTE]
>L'attestazione chiave host è consigliata solo per l'uso in ambienti di test. Per gli ambienti di produzione è consigliabile usare l'attestazione TPM.

1. Accedere al computer SQL Server come amministratore, aprire una console di Windows PowerShell con privilegi elevati e recuperare il nome del computer in uso eseguendo l'accesso alla variabile computername.

   ```powershell
   $env:computername 
   ```

2. Installare la funzionalità Host sorvegliato, che consente anche di installare Hyper-V (se non è già installato).

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
   ```

3. Al prompt riavviare il computer SQL Server per completare l'installazione di Hyper-V.

4. Accedere ancora al computer SQL Server come amministratore, aprire una console di Windows PowerShell con privilegi elevati, generare una chiave host univoca ed esportare la chiave pubblica risultante in un file.

   ```powershell
   Set-HgsClientHostKey 
   Get-HgsClientHostKey -Path $HOME\Desktop\hostkey.cer
   ```

5. Copiare manualmente il file della chiave host generato nel passaggio precedente e incollarlo nel computer HGS. Le istruzioni seguenti presuppongono che il nome del file sia hostkey.cer e che il file sia stato copiato sul desktop del computer HGS.

6. Nel computer HGS, aprire una console di Windows PowerShell con privilegi elevati e registrare la chiave host del computer SQL Server con HGS:

   ```powershell
   Add-HgsAttestationHostKey -Name <your SQL Server computer name> -Path $HOME\Desktop\hostkey.cer
   ```

7. Nel computer SQL Server eseguire il comando seguente in una console di Windows PowerShell con privilegi elevati, per indicare al computer SQL Server dove eseguire l'attestazione. Assicurarsi di specificare l'indirizzo IP o il nome DNS del computer HGS in uso in entrambe le posizioni degli indirizzi. 

   ```powershell
   # use http, and not https
   Set-HgsClientConfiguration -AttestationServerUrl http://<IP address or DNS name>/Attestation -KeyProtectionServerUrl http://<IP address or DNS name>/KeyProtection/  
   ```

Il risultato del comando precedente visualizzerà AttestationStatus = Passed.

Se si verifica un errore HostUnreachable, il computer SQL Server non può comunicare con HGS. Verificare che sia possibile effettuare il ping del computer HGS.

Un errore UnauthorizedHost indica che la chiave pubblica non è stata registrata nel server HGS. Per risolvere l'errore ripetere i passaggi 5 e 6.

In caso di qualsiasi altro errore, eseguire Clear-HgsClientHostKey e ripetere i passaggi 4-7.

## <a name="step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server"></a>Passaggio 3: Abilitare Always Encrypted con enclave sicuri in SQL Server

In questo passaggio si abilita la funzionalità Always Encrypted con enclave sicuri nell'istanza di SQL Server.

1. Aprire SSMS, connettersi all'istanza di SQL Server come amministratore di sistema e aprire una nuova finestra query.
2. Impostare il tipo di enclave sicuro sulla sicurezza basata sulla virtualizzazione (VBS).

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1;
   RECONFIGURE;
   ```

3. Riavviare l'istanza di SQL Server per rendere effettive le modifiche. Per riavviare l'istanza in SQL Server Management Studio, fare clic con il pulsante destro del mouse su di essa in Esplora oggetti e scegliere Riavvia. Dopo il riavvio dell'istanza, riconnettersi.

4. Verificare che l'enclave sicuro sia ora caricato eseguendo la query seguente:

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```

    La query deve restituire il risultato seguente:  

    | NAME                           | Valore | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | column encryption enclave type | 1     | 1              |

5. Per abilitare i calcoli avanzati sulle colonne crittografate, eseguire la query seguente:

   ```sql
   DBCC traceon(127,-1);
   ```

    > [!NOTE]
    > I calcoli avanzati sono disabilitati per impostazione predefinita in [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)]. Devono essere abilitati tramite l'istruzione precedente dopo ogni riavvio dell'istanza di SQL Server.

## <a name="step-4-create-a-sample-database"></a>Passaggio 4: Creare un database di esempio
In questo passaggio si crea un database con alcuni dati di esempio e quindi si procede alla crittografia dei dati.

1. Connettersi all'istanza di SQL Server tramite SSMS.
2. Creare un nuovo database con il nome ContosoHR.

    ```sql
    CREATE DATABASE [ContosoHR];
    ```

3. Accertarsi di essere connessi al database appena creato. Creare una nuova tabella con nome Employees.

    ```sql
    USE [ContosoHR];
    GO
    
    CREATE TABLE [dbo].[Employees]
    (
        [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
        [SSN] [char](11) NOT NULL,
        [FirstName] [nvarchar](50) NOT NULL,
        [LastName] [nvarchar](50) NOT NULL,
        [Salary] [money] NOT NULL
    ) ON [PRIMARY];
    ```

4. Aggiungere alcuni record dei dipendenti alla tabella Employees.

    ```sql
    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('795-73-9838'
            , N'Catherine'
            , N'Abel'
            , $31692);
 
    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('990-00-6818'
            , N'Kim'
            , N'Abercrombie'
            , $55415);
    ```

## <a name="step-5-provision-enclave-enabled-keys"></a>Passaggio 5: Effettuare il provisioning delle chiavi abilitate per l'enclave

In questo passaggio si crea una chiave master della colonna e una chiave di crittografia di colonna che consentono i calcoli di enclave.

1. Connettersi al database tramite SQL Server Management Studio.
2. In **Esplora oggetti** espandere il database e passare a **Sicurezza** > **Chiavi Always Encrypted**.
3. Effettuare il provisioning di una nuova chiave master della colonna abilitata per l'enclave:
    1. Fare clic con il pulsante destro del mouse su **Chiavi Always Encrypted** e scegliere **Nuova chiave master della colonna**.
    2. Selezionare il nome della chiave master della colonna: CMK1.
    3. Assicurarsi di selezionare **Archivio certificati Windows (Utente corrente o Computer locale)** o **Azure Key Vault**.
    4. Selezionare **Consenti calcoli enclave**.
    5. Se si seleziona Azure Key Vault, accedere ad Azure e selezionare l'insieme di credenziali delle chiavi. Per altre informazioni su come creare un insieme di credenziali delle chiavi per Always Encrypted, vedere [Manage your key vaults from Azure portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/) (Gestire gli insiemi di credenziali delle chiavi dal portale di Azure).
    6. Selezionare la chiave se esiste già o seguire le istruzioni nel modulo per creare una nuova chiave.
    7. Fare clic su **OK**.

        ![Consenti calcoli enclave](encryption/media/always-encrypted-enclaves/allow-enclave-computations.png)
    
4. Creare una nuova chiave di crittografia di colonna abilitata per l'enclave:

    1. Fare clic con il pulsante destro del mouse su **Chiavi Always Encrypted** e scegliere **Nuova chiave di crittografia della colonna**.
    2. Immettere un nome per la nuova chiave di crittografia della colonna: CEK1.
    3. Nell'elenco a discesa **Chiave master della colonna** selezionare la chiave master della colonna creata nei passaggi precedenti.
    4. Fare clic su **OK**.

## <a name="step-6-encrypt-some-columns-in-place"></a>Passaggio 6: Crittografare alcune colonne sul posto

In questo passaggio si esegue la crittografia dei dati archiviati nelle colonne SSN e Salary all'interno dell'enclave lato server, quindi si esegue il test di una query SELECT dei dati.

1. In SSMS configurare una nuova finestra query con Always Encrypted e i calcoli dell'enclave abilitati per la connessione al database.
    1. In SSMS aprire una nuova finestra di query.
    2. Fare clic con il pulsante destro del mouse in un punto qualsiasi all'interno della nuova finestra di query.
    3. Selezionare Connessione \> Cambia connessione.
    4. Selezionare **Opzioni**. Passare alla scheda **Always Encrypted**, selezionare **Abilita Always Encrypted** e specificare l'URL di attestazione dell'enclave, ad esempio ht<span>tp://</span>hgs.bastion.local/Attestation.
    5. Selezionare **Connetti**.
    6. Impostare il contesto di database sul database ContosoHR.
1. In SSMS configurare un'altra finestra di query con Always Encrypted disabilitata per la connessione al database.
    1. In SSMS aprire una nuova finestra di query.
    2. Fare clic con il pulsante destro del mouse in un punto qualsiasi all'interno della nuova finestra di query.
    3. Selezionare Connessione \> Cambia connessione.
    4. Selezionare **Opzioni**. Passare alla scheda **Always Encrypted** e verificare che **Abilita Always Encrypted** non sia selezionata.
    5. Selezionare **Connetti**.
    6. Impostare il contesto di database sul database ContosoHR.
1. Crittografare le colonne SSN e Salary. Nella finestra di query con Always Encrypted abilitato incollare ed eseguire lo script seguente:

    ```sql
    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [SSN] [char] (11) COLLATE Latin1_General_BIN2
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);
     
    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [Salary] [money]
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON);
 
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > Si noti l'istruzione ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE per cancellare la cache del piano di query per il database nello script precedente. Dopo aver modificato la tabella è necessario cancellare i piani per tutti i batch e le stored procedure che accedono alla tabella per aggiornare le informazioni di crittografia dei parametri. 

4. Per verificare che le colonne SSN e Salary ora sono crittografate, incollare ed eseguire l'istruzione seguente nella finestra di query con Always Encrypted disabilitata. La finestra di query restituirà valori crittografati nelle colonne SSN e Salary. Nella finestra di query con Always Encrypted abilitata, provare a eseguire la stessa query per visualizzare i dati decrittografati.

    ```sql
    SELECT * FROM [dbo].[Employees];
    ```

## <a name="step-7-run-rich-queries-against-encrypted-columns"></a>Passaggio 7: Eseguire query avanzate su colonne crittografate

Ora è possibile eseguire query avanzate sulle colonne crittografate. Vengono eseguite alcune operazioni di elaborazione query nell'enclave lato server. 

1. Abilitare Parametrizzazione per Always Encrypted.
    1. Selezionare **Query** dal menu principale di SQL Server Management Studio.
    2. Selezionare **Opzioni query**.
    3. Passare a **Esecuzione** > **Avanzata**.
    4. Selezionare **Abilita parametrizzazione per Always Encrypted**.
    5. Fare clic su **OK**.
2. Nella finestra della query con Always Encrypted abilitata, incollare ed eseguire la query seguente. La query restituisce valori di testo non crittografato e righe che soddisfano i criteri di ricerca specificati.

    ```sql
    DECLARE @SSNPattern [char](11) = '%6818';
    DECLARE @MinSalary [money] = $1000;
    SELECT * FROM [dbo].[Employees]
    WHERE SSN LIKE @SSNPattern AND [Salary] >= @MinSalary;
    ```
3. Riprovare la stessa query nella finestra di query senza Always Encrypted abilitata e notare l'errore che si verifica.

## <a name="next-steps"></a>Next Steps
Per idee su altri casi d'uso, vedere [Configurare Always Encrypted con enclave sicuri](encryption/configure-always-encrypted-enclaves.md). È anche possibile provare quanto segue:

- [Configurazione dell'attestazione TPM.](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode)
- [Configurazione di HTTPS per l'istanza del servizio HGS.](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-https)
- Sviluppo di applicazioni che eseguono query avanzate su colonne crittografate.
