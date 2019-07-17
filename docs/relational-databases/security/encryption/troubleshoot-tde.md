---
title: Errori comuni relativi a Transparent Data Encryption (TDE) con chiavi gestite dal cliente in Azure Key Vault | Microsoft Docs
description: Risolvere i problemi relativi a Transparent Data Encryption (TDE) con una configurazione di Azure Key Vault.
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
manager: craigg
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f963e15d674115029fce78b98ba280fe75da2cd1
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716672"
---
# <a name="common-errors-for-transparent-data-encryption-with-customer-managed-keys-in-azure-key-vault"></a>Errori comuni relativi a Transparent Data Encryption (TDE) con chiavi gestite dal cliente in Azure Key Vault

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
Questo articolo descrive i requisiti per l'uso di Transparent Data Encryption (TDE) con chiavi gestite dal cliente in Azure Key Vault e come identificare e risolvere gli errori più comuni.

## <a name="requirements"></a>Requisiti

Per risolvere i problemi relativi a TDE con una protezione TDE gestita dal cliente in Azure Key Vault, è necessario soddisfare questi requisiti:

- L'istanza di SQL Server logica e l'insieme di credenziali delle chiavi devono trovarsi nella stessa area.
- L'identità dell'istanza di SQL Server logica fornita da Azure Active Directory (Azure AD), ovvero l'AppId in Azure Key Vault, deve essere un tenant nella sottoscrizione originale. Se il server è stato spostato in una sottoscrizione diversa da quella in cui è stato creato, l'identità del server (AppId) deve essere ricreata.
- L'insieme di credenziali delle chiavi deve essere attivo e in esecuzione. Per informazioni su come controllare lo stato dell'insieme di credenziali delle chiavi, vedere [Integrità risorse di Azure](https://docs.microsoft.com/azure/service-health/resource-health-overview). Per iscriversi per le notifiche, vedere i [gruppi di azioni](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups).
- Per il failover corretto in uno scenario di ripristino di emergenza geografico entrambi gli insiemi di credenziali delle chiavi devono contenere lo stesso materiale per le chiavi.
- Il server logico deve avere un'identità di Azure AD (AppId) per l'autenticazione nell'insieme di credenziali delle chiavi.
- L'AppId deve avere accesso all'insieme di credenziali delle chiavi, nonché disporre delle autorizzazioni Ottieni chiave, Esegui il wrapping della chiave e Annulla il wrapping della chiave per le chiavi selezionate come protezione TDE.

Per altre informazioni, vedere [Linee guida per la configurazione di TDE con Azure Key Vault](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault).

## <a name="common-misconfigurations"></a>Errori di configurazione comuni

La maggior parte dei problemi che si verificano quando si usa TDE con Azure Key Vault è causata da uno degli errori di configurazione seguenti:

### <a name="the-key-vault-is-unavailable-or-doesnt-exist"></a>L'insieme di credenziali delle chiavi non è disponibile o non esiste

- L'insieme di credenziali delle chiavi è stato eliminato per errore.
- Il firewall è stato configurato per Azure Key Vault, ma non consente l'accesso ai servizi Microsoft.

### <a name="no-permissions-to-access-the-key-vault-or-the-key-doesnt-exist"></a>Non sono disponibili le autorizzazioni per accedere all'insieme di credenziali delle chiavi o la chiave non esiste

- La chiave è stata eliminata per errore.
- L'AppId dell'istanza di SQL Server logica è stato eliminato per errore.
- L'istanza di SQL Server logica è stata spostata in un'altra sottoscrizione. Se il server logico viene spostato in una sottoscrizione diversa, è necessario creare un nuovo AppId.
- Le autorizzazioni concesse all'AppId per le chiavi non sono sufficienti (non includono le autorizzazioni Ottieni chiave, Esegui il wrapping della chiave e Annulla il wrapping della chiave).
- Le autorizzazioni per l'AppId dell'istanza di SQL Server logica sono state revocate.

## <a name="identify-and-resolve-common-errors"></a>Identificare e risolvere gli errori comuni

In questa sezione sono elencati i passaggi di risoluzione dei problemi per gli errori più comuni.

### <a name="missing-server-identity"></a>Identità del server mancante

**Messaggio di errore**

_401 AzureKeyVaultNoServerIdentity - L'identità del server non è configurata correttamente nel server. Contattare il supporto tecnico._

**Rilevamento**

Usare il cmdlet o il comando seguente per assicurarsi che all'istanza di SQL Server logica sia stata assegnata un'identità:

- Azure PowerShell: [Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 

- Interfaccia della riga di comando di Azure: [az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

**Mitigazione**

Usare il cmdlet o il comando seguente per configurare un'identità di Azure AD (AppId) per l'istanza di SQL Server logica:

- Azure PowerShell: [Set-AzureRmSqlServer](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0) con l'opzione `-AssignIdentity`.

- Interfaccia della riga di comando di Azure: [az sql server update](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update) con l'opzione `--assign_identity`.

Nel portale di Azure passare all'insieme di credenziali delle chiavi e quindi passare a **Criteri di accesso**. Seguire questa procedura: 

 1. Usare il pulsante **Aggiungi nuovo** per aggiungere l'AppId per il server creato nel passaggio precedente. 
 1. Assegnare le autorizzazioni seguenti: Ottieni chiave, Esegui il wrapping della chiave e Annulla il wrapping della chiave 

Per altre informazioni, vedere [Assegnare un'identità Azure AD al server](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server).

> [!IMPORTANT]
> Se l'istanza di SQL Server logica è stata spostata in una nuova sottoscrizione dopo la configurazione iniziale di TDE con Azure Key Vault, è necessario ripetere il passaggio di configurazione dell'identità di Azure AD per creare il nuovo AppId. Aggiungere quindi l'AppId all'insieme di credenziali delle chiavi e assegnare le autorizzazioni corrette alla chiave. 
>

### <a name="missing-key-vault"></a>Insieme di credenziali delle chiavi mancante

**Messaggio di errore**

_503 AzureKeyVaultConnectionFailed - Non è stato possibile completare l'operazione nel server perché i tentativi di connettersi all'insieme di credenziali delle chiavi di Azure non sono riusciti._

**Rilevamento**

Per identificare l'URI della chiave e l'insieme di credenziali delle chiavi:

1. Usare il cmdlet o il comando seguente per ottenere l'URI della chiave di un'istanza di SQL Server logica specifica:

    - Azure PowerShell: [Get-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

    - Interfaccia della riga di comando di Azure: [az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

1. Usare l'URI della chiave per identificare l'insieme di credenziali delle chiavi:

    - Azure PowerShell: è possibile esaminare le proprietà della variabile $MyServerKeyVaultKey per ottenere dettagli sull'insieme di credenziali delle chiavi.

    - Interfaccia della riga di comando di Azure: esaminare la protezione della crittografia server restituita per ottenere dettagli sull'insieme di credenziali delle chiavi.

**Mitigazione**

Verificare che l'insieme di credenziali delle chiavi sia disponibile:

- Assicurarsi che l'insieme di credenziali delle chiavi sia disponibile e che l'istanza di SQL Server logica disponga dell'accesso.
- Se l'insieme di credenziali delle chiavi è protetto da un firewall, assicurarsi che sia selezionata la casella di controllo per consentire ai servizi Microsoft di accedere all'insieme di credenziali delle chiavi.
- Se l'insieme di credenziali delle chiavi è stato eliminato per errore, è necessario ripetere la configurazione dall'inizio.


### <a name="missing-key"></a>Chiave mancante

**Messaggi di errore**

_404 ServerKeyNotFound - La chiave server richiesta non è stata trovata nella sottoscrizione corrente._ 

_409 ServerKeyDoesNotExists - La chiave server non esiste._

**Rilevamento**

Per identificare l'URI della chiave e l'insieme di credenziali delle chiavi:

- Usare il cmdlet o i comandi in [Insieme di credenziali delle chiavi mancante](#missing-key-vault) per identificare l'URI della chiave aggiunto all'istanza di SQL Server logica. L'esecuzione dei comandi restituisce l'elenco delle chiavi.

**Mitigazione**

Verificare che la protezione TDE sia presente in Azure Key Vault:

1. Identificare l'insieme di credenziali delle chiavi, quindi passare all'insieme di credenziali delle chiavi nel portale di Azure.
1. Assicurarsi che la chiave identificata dall'URI della chiave sia presente.

### <a name="missing-permissions"></a>Autorizzazioni mancanti

**Messaggio di errore**

_401 AzureKeyVaultMissingPermissions - Nel server mancano le autorizzazioni obbligatorie per Azure Key Vault._

**Rilevamento**

Per identificare l'URI della chiave e l'insieme di credenziali delle chiavi: 

- Usare il cmdlet o i comandi in [Insieme di credenziali delle chiavi mancante](#missing-key-vault) per identificare l'insieme di credenziali delle chiavi usato dall'istanza di SQL Server logica.

**Mitigazione**

Verificare che l'istanza di SQL Server logica abbia le autorizzazioni per l'insieme di credenziali delle chiavi e le autorizzazioni corrette per accedere alla chiave:

- Nel portale di Azure passare all'insieme di credenziali delle chiavi e quindi passare a **Criteri di accesso**. Trovare l'AppId dell'istanza di SQL Server logica.  
- Se l'AppId è presente, verificare che abbia le autorizzazioni per le chiavi seguenti: Ottieni chiave, Esegui il wrapping della chiave e Annulla il wrapping della chiave.
- Se l'AppId non è presente, aggiungerlo facendo clic sul pulsante **Aggiungi nuovo**. 

## <a name="next-steps"></a>Passaggi successivi

- Rivedere le [linee guida per la configurazione di TDE con Azure Key Vault](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault).
- Scoprire [Integrità risorse di Azure](https://docs.microsoft.com/azure/service-health/resource-health-overview).
- Vedere come [assegnare un'identità di Azure AD al server](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server).
