---
title: Creare e archiviare chiavi master della colonna per Always Encrypted
description: Informazioni su come selezionare un archivio chiavi e creare chiavi master della colonna per SQL Server Always Encrypted.
ms.custom: seo-lt-2019
ms.date: 10/31/2019
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 856e8061-c604-4ce4-b89f-a11876dd6c88
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 63be7df50b6dd590d0ec90346d27f6601e15cf45
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "79287095"
---
# <a name="create-and-store-column-master-keys-for-always-encrypted"></a>Creare e archiviare chiavi master della colonna per Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Le*chiavi master della colonna* proteggono le chiavi usate in Always Encrypted per crittografare le chiavi di crittografia della colonna. Le chiavi master della colonna devono essere archiviate in un archivio attendibile e devono essere accessibili alle applicazioni che le richiedono per crittografare o decrittografare i dati e agli strumenti per la configurazione di Always Encrypted e la gestione delle chiavi di Always Encrypted.

Questo articolo fornisce informazioni dettagliate per la selezione di un archivio chiavi e la creazione di chiavi master della colonna per Always Encrypted. Per una panoramica dettagliata, vedere [Overview of Key Management for Always Encrypted (Panoramica della gestione delle chiavi per Always Encrypted)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

## <a name="selecting-a-key-store-for-your-column-master-key"></a>Scelta di un archivio chiavi per la chiave master della colonna

Always Encrypted supporta più archivi chiavi per l'archiviazione di chiavi master della colonna Always Encrypted. Gli archivi chiavi supportati variano a seconda dei driver e della versione in uso.

Esistono due categorie generali di archivi da considerare: gli *archivi chiavi locali*e gli *archivi chiavi centralizzati*.

###  <a name="local-or-centralized-key-store"></a>Archivio chiavi centralizzato o locale?

* Gli**archivi chiavi locali** possono essere usati solo dalle applicazioni nei computer che contengono l'archivio chiavi locale. In altre parole, è necessario replicare l'archivio chiavi e la chiave per ogni computer che esegue l'applicazione. Un esempio di archivio chiavi locale è l'archivio certificati Windows. Quando si usa un archivio chiavi locale, è necessario verificare che l'archivio chiavi esista in ogni computer che ospita l'applicazione e che il computer contenga le chiavi master della colonna richieste dall'applicazione per accedere ai dati protetti con Always Encrypted. Quando si esegue il provisioning di una chiave master della colonna per la prima volta o quando si modifica (ruota) la chiave, è necessario verificare che la chiave venga distribuita a tutti i computer che ospitano una o più applicazioni.

* Gli**archivi chiavi centralizzati** vengono usati dalle applicazioni in più computer. Un esempio di archivio chiavi centralizzato è un [insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/services/key-vault/). Un archivio chiavi centralizzato in genere facilita la gestione delle chiavi perché non è necessario avere più copie delle chiavi master della colonna in più computer. Verificare che le applicazioni siano configurate per la connessione all'archivio chiavi centralizzato.

### <a name="which-key-stores-are-supported-in-always-encrypted-enabled-client-drivers"></a>Quali sono gli archivi chiavi supportati nei driver dei client abilitati per Always Encrypted?

I driver dei client abilitati per Always Encrypted sono driver dei client di SQL Server con un supporto predefinito che consente di incorporare Always Encrypted nelle applicazioni client. I driver abilitati per Always Encrypted includono alcuni provider predefiniti per gli archivi chiavi più diffusi. Alcuni driver consentono anche di implementare e registrare un provider di archivio della chiave master della colonna personalizzato, in modo che sia possibile usare qualsiasi archivio chiavi, anche se non è disponibile un provider predefinito specifico. Quando si sceglie tra un provider predefinito e un provider personalizzato considerare che l'utilizzo un provider predefinito in genere implica meno modifiche alle applicazioni. In alcuni casi, è richiesta solo la modifica a una stringa di connessione del database.

I provider predefiniti disponibili dipendono dal driver, dalla versione del driver e dal sistema operativo selezionati.  Consultare la documentazione di Always Encrypted per il driver specifico per determinare quali archivi chiavi sono supportati in modo predefinito e se il driver supporta provider di archivi chiavi personalizzati - [Sviluppare applicazioni usando Always Encrypted](always-encrypted-client-development.md).

### <a name="which-key-stores-are-supported-in-sql-tools"></a>Quali archivi chiavi sono supportati negli strumenti SQL?
SQL Server Management Studio e il modulo PowerShell SqlServer supportano solo chiavi master della colonna archiviate in Azure Key Vault, nell'archivio certificati Windows e negli archivi di chiavi che implementano l'API CNG (Cryptography Next Generation) o CAPI (Cryptography API). 

## <a name="creating-column-master-keys-in-windows-certificate-store"></a>Creazione di chiavi master della colonna nell'archivio certificati Windows    

Una chiave master della colonna può essere un certificato archiviato nell'archivio certificati Windows. Un driver abilitato per Always Encrypted non verifica la data di scadenza o una catena di autorità di certificazione. Un certificato viene usato semplicemente come una coppia di chiavi composta da una chiave pubblica e da una privata.

Per essere una chiave master della colonna valida, un certificato deve:
* essere un certificato X.509.
* essere archiviato in uno dei percorsi dell'archivio certificati: *computer locale* o *utente corrente*. Per creare un certificato nel percorso dell'archivio certificati del computer locale, è necessario essere un amministratore nel computer di destinazione.
* contenere una chiave privata. La lunghezza consigliata delle chiavi nel certificato è di 2048 bit o superiore.
* essere creato per lo scambio di chiavi.


Esistono diversi modi per creare un certificato che corrisponda a una chiave master della colonna valida, ma l'opzione più semplice consiste nel creare un certificato autofirmato.


### <a name="create-a-self-signed-certificate-using-powershell"></a>Creare un certificato autofirmato usando PowerShell

Usare il cmdlet [New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate) per creare un certificato autofirmato. L'esempio seguente mostra come generare un certificato che può essere usato come chiave master della colonna per Always Encrypted.

```
# New-SelfSignedCertificate is a Windows PowerShell cmdlet that creates a self-signed certificate. The below examples show how to generate a certificate that can be used as a column master key for Always Encrypted.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048 

# To create a certificate in the local machine certificate store location you need to run the cmdlet as an administrator.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:LocalMachine\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048
```

### <a name="create-a-self-signed-certificate-using-sql-server-management-studio-ssms"></a>Creare un certificato autofirmato usando SQL Server Management Studio (SSMS)

Per informazioni dettagliate, vedere [Effettuare il provisioning di chiavi Always Encrypted con SQL Server Management Studio](configure-always-encrypted-keys-using-ssms.md).
Per un'esercitazione dettagliata che usa SQL Server Management Studio e archivia le chiavi di Always Encrypted nell'archivio certificati Windows, vedere l' [esercitazione guidata su Always Encrypted (archivio certificati Windows)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/).


### <a name="making-certificates-available-to-applications-and-users"></a>Rendere disponibili i certificati a utenti e applicazioni

Se la chiave master della colonna è un certificato archiviato nel percorso dell'archivio certificati del *computer locale* , è necessario esportare il certificato con la chiave privata e importarlo in tutti i computer che ospitano le applicazioni che si prevede eseguiranno la crittografia o la decrittografia dei dati archiviati nelle colonne crittografate oppure negli strumenti per la configurazione di Always Encrypted e per la gestione delle chiavi di Always Encrypted. Inoltre, a ogni utente deve essere concessa un'autorizzazione di lettura per il certificato archiviato nel percorso dell'archivio certificati del computer locale per poter usare il certificato come una chiave master della colonna.

Se la chiave master della colonna è un certificato archiviato nel percorso dell'archivio certificati dell' *utente corrente* , è necessario esportare il certificato con la chiave privata e importarlo nel percorso dell'archivio certificati dell'utente corrente di tutti gli account che eseguono le applicazioni che si prevede eseguiranno la crittografia o la decrittografia dei dati archiviati nelle colonne crittografate oppure negli strumenti per la configurazione di Always Encrypted e per la gestione delle chiavi di Always Encrypted, in tutti i computer che contengono tali applicazioni/strumenti. Non è necessaria la configurazione dell'autorizzazione: dopo l'accesso a un computer, un utente può accedere a tutti i certificati nel percorso dell'archivio certificati dell'utente corrente.

#### <a name="using-powershell"></a>Utilizzo di PowerShell
Usare i cmdlet [Import-PfxCertificate](/powershell/module/pkiclient/import-pfxcertificate) ed [Export-PfxCertificate](/powershell/module/pkiclient/export-pfxcertificate) per importare ed esportare un certificato.

#### <a name="using-microsoft-management-console"></a>Uso di Microsoft Management Console 

Per concedere all'utente l'autorizzazione di *lettura* per un certificato archiviato nel percorso dell'archivio certificati del computer locale, seguire questi passaggi:

1.  Aprire un prompt dei comandi e digitare **mmc**.
2.  Nella console MMC scegliere **Aggiungi/Rimuovi snap-in** dal menu **File**.
3.  Nella finestra di dialogo **Aggiungi/Rimuovi snap-in** fare clic su **Aggiungi**.
4.  Nella finestra di dialogo **Aggiungi snap-in autonomo** fare clic su **Certificati**e quindi su **Aggiungi**.
5.  Nella finestra di dialogo **Snap-in certificati** fare clic su **Account del computer**e quindi su **Fine**.
6.  Nella finestra di dialogo **Aggiungi snap-in autonomo** fare clic su **Chiudi**.
7.  Nella finestra di dialogo **Aggiungi/Rimuovi snap-in** fare clic su **OK**.
8.  In **Snap-in certificati** trovare il certificato nella cartella **Certificati > Personale**, fare clic con il pulsante destro del mouse sul certificato, scegliere **Tutte le attività** e quindi fare clic su **Gestisci chiavi private**.
9.  Nella finestra di dialogo **Sicurezza** aggiungere le autorizzazioni di lettura per un account utente, se necessario.

## <a name="creating-column-master-keys-in-azure-key-vault"></a>Creazione di chiavi master della colonna nell'insieme di credenziali delle chiavi di Azure

L'insieme di credenziali delle chiavi di Azure contribuisce a proteggere i segreti e le chiavi di crittografia e rappresenta una scelta valida per l'archiviazione delle chiavi master della colonna per Always Encrypted, soprattutto se le applicazioni sono ospitate in Azure. Per creare una chiave nell' [insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/), è necessario una [sottoscrizione di Azure](https://azure.microsoft.com/free/) e un insieme di credenziali delle chiavi di Azure.

### <a name="using-powershell"></a>Utilizzo di PowerShell

L'esempio seguente crea un nuovo insieme di credenziali delle chiavi di Azure e una chiave, quindi concede le autorizzazioni all'utente desiderato.

```
# Create a column master key in Azure Key Vault.
Connect-AzAccount
$SubscriptionId = "<Azure subscription ID>"
$resourceGroup = "<resource group name>"
$azureLocation = "<key vault location>"
$akvName = "<key vault name>"
$akvKeyName = "<column master key name>"
$azureCtx = Set-AzContext -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation -SKU premium # Creates a new key vault - skip if your vault already exists.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey, unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination HSM
```

### <a name="using-sql-server-management-studio-ssms"></a>Utilizzo di SQL Server Management Studio (SSMS)

Per informazioni dettagliate su come creare una chiave master della colonna in Azure Key Vault tramite SSMS, vedere [Effettuare il provisioning di chiavi Always Encrypted con SQL Server Management Studio](configure-always-encrypted-keys-using-ssms.md).
Per un'esercitazione dettagliata che usa SSMS e archivia le chiavi di Always Encrypted in un insieme di credenziali delle chiavi di Azure, vedere l' [esercitazione guidata su Always Encrypted (insieme di credenziali delle chiavi di Azure)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault).

### <a name="making-azure-key-vault-keys-available-to-applications-and-users"></a>Rendere disponibili le chiavi dell'insieme di credenziali delle chiavi di Azure ad applicazioni e utenti

Quando si usa una chiave dell'insieme di credenziali delle chiavi di Azure come chiave master della colonna, l'applicazione deve eseguire l'autenticazione in Azure e l'identità dell'applicazione deve avere le autorizzazioni seguenti per l'insieme di credenziali delle chiavi: *get*, *unwrapKey*e *verify*. 

Per eseguire il provisioning delle chiavi di crittografia della colonna protette con una chiave master della colonna archiviata nell'insieme di credenziali delle chiavi di Azure, sono necessarie le autorizzazioni *get*, *unwrapKey*, *wrapKey*, *sign*e *verify* . Inoltre, per creare una nuova chiave in un insieme di credenziali delle chiavi di Azure, è necessaria l'autorizzazione *create* , mentre per elencare il contenuto dell'insieme di credenziali delle chiavi è necessaria l'autorizzazione *list* .

#### <a name="using-powershell"></a>Utilizzo di PowerShell

Per consentire a utenti e applicazioni di accedere alle chiavi effettive in Azure Key Vault, è necessario impostare i criteri di accesso all'insieme di credenziali ([Set-AzKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy)):

```
$vaultName = "<vault name>"
$resourceGroupName = "<resource group name>"
$userPrincipalName = "<user to grant access to>"
$clientId = "<client Id>"

# grant users permissions to the keys:
Set-AzKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
# grant applications permissions to the keys:
Set-AzKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list
```

## <a name="creating-column-master-keys-in-hardware-security-modules-using-cng"></a>Creazione di chiavi master della colonna nei moduli di protezione hardware con CNG

Una chiave master della colonna per Always Encrypted può essere archiviata in un archivio chiavi che implementa l'API Cryptography Next Generation (CNG). In genere, questo tipo di archivio è un modulo di protezione hardware (HSM). Un modulo di protezione hardware (HSM) è un dispositivo fisico che protegge e gestisce le chiavi digitali e fornisce l'elaborazione della crittografia. I moduli di protezione hardware vengono generalmente forniti come schede plug-in o dispositivi esterni collegati direttamente a un computer (HSM locale) o a un server di rete.

Per rendere disponibile un modulo di protezione hardware alle applicazioni di un determinato computer, è necessario installare e configurare un provider di archiviazione chiavi (KSP) che implementa CNG nel computer. Un driver del client Always Encrypted, ovvero un provider di archivio della chiave master della colonna interno al driver, usa il provider di archiviazione chiavi per crittografare e decrittografare le chiavi di crittografia della colonna, protette con la chiave master della colonna archiviata nell'archivio chiavi.

Windows include il provider di archiviazione chiavi del software Microsoft, un provider di archiviazione chiavi basato su software che è possibile usare per i test. Vedere [CNG Key Storage Providers (Provider di archiviazione chiavi CNG)](/windows/desktop/SecCertEnroll/cng-key-storage-providers).

### <a name="creating-column-master-keys-in-a-key-store-using-cngksp"></a>Creazione di chiavi master della colonna in un archivio chiavi con CNG/KSP

Una chiave master della colonna deve essere una chiave asimmetrica, ovvero una coppia di chiavi pubblica/privata, che usa l'algoritmo RSA. La lunghezza della chiave consigliata è di almeno 2048.

#### <a name="using-hsm-specific-tools"></a>Utilizzo degli strumenti specifici per il modulo di protezione hardware
Vedere la documentazione per il modulo di protezione hardware.

#### <a name="using-powershell"></a>Utilizzo di PowerShell

È possibile usare le API .NET per creare una chiave in un archivio chiavi usando CNG in PowerShell.


```
$cngProviderName = "Microsoft Software Key Storage Provider" # If you have an HSM, you can use a KSP for your HSM instead of a Microsoft KSP
$cngAlgorithmName = "RSA"
$cngKeySize = 2048 # Recommended key size for Always Encrypted column master keys
$cngKeyName = "AlwaysEncryptedKey" # Name identifying your new key in the KSP
$cngProvider = New-Object System.Security.Cryptography.CngProvider($cngProviderName)
$cngKeyParams = New-Object System.Security.Cryptography.CngKeyCreationParameters
$cngKeyParams.provider = $cngProvider
$cngKeyParams.KeyCreationOptions = [System.Security.Cryptography.CngKeyCreationOptions]::OverwriteExistingKey
$keySizeProperty = New-Object System.Security.Cryptography.CngProperty("Length", [System.BitConverter]::GetBytes($cngKeySize), [System.Security.Cryptography.CngPropertyOptions]::None);
$cngKeyParams.Parameters.Add($keySizeProperty)
$cngAlgorithm = New-Object System.Security.Cryptography.CngAlgorithm($cngAlgorithmName)
$cngKey = [System.Security.Cryptography.CngKey]::Create($cngAlgorithm, $cngKeyName, $cngKeyParams)
```

#### <a name="using-sql-server-management-studio"></a>Utilizzare SQL Server Management Studio

Vedere [Effettuare il provisioning di chiavi Always Encrypted con SQL Server Management Studio](configure-always-encrypted-keys-using-ssms.md).

### <a name="making-cng-keys-available-to-applications-and-users"></a>Rendere disponibili le chiavi CNG a utenti e applicazioni

Vedere la documentazione per il modulo di protezione hardware e il provider di archiviazione chiavi per informazioni su come configurare il provider di archiviazione chiavi in un computer e su come concedere l'accesso al modulo di protezione hardware a utenti e applicazioni.

## <a name="creating-column-master-keys-in-hardware-security-modules-using-capi"></a>Creazione di chiavi master della colonna nei moduli di protezione hardware con CAPI

Una chiave master della colonna per Always Encrypted può essere archiviata in un archivio chiavi che implementa l'API Cryptography (CAPI). In genere, questo tipo di archivio è un modulo di protezione hardware (HSM), ovvero un dispositivo fisico che protegge e gestisce le chiavi digitali e fornisce l'elaborazione della crittografia. I moduli di protezione hardware vengono generalmente forniti come schede plug-in o dispositivi esterni collegati direttamente a un computer (HSM locale) o a un server di rete.

Per rendere disponibile un modulo di protezione hardware alle applicazioni di un determinato computer, è necessario installare e configurare un provider del servizio di crittografia (CSP) che implementa CAPI nel computer. Un driver del client Always Encrypted, ovvero un provider di archivio della chiave master della colonna interno al driver, usa il provider del servizio di crittografia per crittografare e decrittografare le chiavi di crittografia della colonna, protette con la chiave master della colonna archiviata nell'archivio chiavi. 

> [!NOTE]
> CAPI è un'API legacy deprecata. Se è disponibile un provider di archiviazione chiavi per il modulo di protezione hardware, è necessario usare quello invece di CSP/CAPI.

Un provider del servizio di crittografia deve supportare l'algoritmo RSA da usare con Always Encrypted.

Windows include i provider del servizio di crittografia seguenti basati su software, ovvero non supportati da un modulo di protezione hardware, che supportano RSA e che possono essere usati per i test: Microsoft Enhanced RSA e AES Cryptographic Provider.

### <a name="creating-column-master-keys-in-a-key-store-using-capicsp"></a>Creazione di chiavi master della colonna in un archivio chiavi con CAPI/CSP

Una chiave master della colonna deve essere una chiave asimmetrica, ovvero una coppia di chiavi pubblica/privata, che usa l'algoritmo RSA. La lunghezza della chiave consigliata è di almeno 2048.

#### <a name="using-hsm-specific-tools"></a>Utilizzo degli strumenti specifici per il modulo di protezione hardware
Vedere la documentazione per il modulo di protezione hardware.

#### <a name="using-sql-server-management-studio-ssms"></a>Utilizzo di SQL Server Management Studio (SSMS)
Vedere [Effettuare il provisioning di chiavi Always Encrypted con SQL Server Management Studio](configure-always-encrypted-keys-using-ssms.md).

### <a name="making-cng-keys-available-to-applications-and-users"></a>Rendere disponibili le chiavi CNG a utenti e applicazioni
Vedere la documentazione per il modulo di protezione hardware e il provider del servizio di crittografia per informazioni su come configurare il provider del servizio di crittografia in un computer e su come concedere l'accesso al modulo di protezione hardware a utenti e applicazioni.
 
## <a name="next-steps"></a>Passaggi successivi  
- [Effettuare il provisioning di chiavi Always Encrypted con SQL Server Management Studio](configure-always-encrypted-keys-using-ssms.md)
- [Effettuare il provisioning di chiavi Always Encrypted con PowerShell](configure-always-encrypted-keys-using-powershell.md)
  
## <a name="see-also"></a>Vedere anche 
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Panoramica della gestione delle chiavi per Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)  
