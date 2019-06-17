---
title: Risoluzione dei problemi relativi a Transparent Data Encryption (TDE) con chiavi gestite dal cliente in Azure Key Vault (AKV) | Microsoft Docs
description: Informazioni sulla risoluzione dei problemi relativi a Transparent Data Encryption (TDE) con la configurazione Azure Key Vault.
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
ms.openlocfilehash: 1366d0a20ed39b466d1a2f6cb3e84f0f30e17f9f
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718091"
---
# <a name="common-errors-and-resolutions-with-transparent-data-encryption-tde-with-customer-managed-keys-in-azure-key-vault-akv"></a>Risoluzione dei problemi relativi a Transparent Data Encryption (TDE) con chiavi gestite dal cliente in Azure Key Vault (AKV)

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
In questo argomento sono disponibili informazioni sugli argomenti seguenti:  
  
- Requisiti  
- Come identificare e risolvere gli errori più comuni

## <a name="requirements"></a>Requisiti
Per risolvere i problemi relativi a [Transparent Data Encryption con protezione Transparent Data Encryption nella configurazione Azure Key Vault](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault), è opportuno verificare prima i requisiti seguenti:
- Il server SQL logico e l'insieme di credenziali delle chiavi devono trovarsi nella stessa area.
- L'identità del server SQL logico fornita da Azure Active Directory (APPID in Azure Key Vault) è limitato a un unico tenant nella sottoscrizione originale.  Se il server è stato spostato in un'altra sottoscrizione, è necessario creare di nuovo l'identità del server (APPID).
- L'insieme di credenziali delle chiavi deve essere funzionante. Vedere [Integrità risorse di Azure](https://docs.microsoft.com/azure/service-health/resource-health-overview) per informazioni su come verificare lo stato dell'insieme di credenziali delle chiavi e [Gruppi di azioni](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups) per informazioni su come effettuare l'iscrizione per le notifiche.
- Per un failover corretto nello scenario di ripristino di emergenza geografico entrambi gli insiemi di credenziali delle chiavi devono contenere le stesse impostazioni di chiave.
- Per potersi autenticare con l'insieme di credenziali delle chiavi, il server logico deve includere un'identità Azure Active Directory (AAD) (APPID).
- L'APPID deve accedere all'insieme di credenziali delle chiavi, nonché disporre delle autorizzazioni per eseguire il wrapping, annullare il wrapping e ottenere le chiavi selezionate come protezione Transparent Data Encryption.

La maggior parte dei problemi riscontrati quando si usa Transparent Data Encryption con Azure Key Vault è dovuta a uno degli errori di configurazione seguenti:

### <a name="key-vault-unavailable-or-doesnt-exist"></a>Insieme di credenziali delle chiavi non disponibile o inesistente?
- Insieme di credenziali delle chiavi eliminato per errore
- Firewall configurato per Azure Key Vault, senza consentire l'accesso ai servizi Microsoft

### <a name="no-permissions-to-access-the-key-vault-or-key-doesnt-exist"></a>Autorizzazioni di accesso all'insieme di credenziali delle chiavi mancanti o chiave inesistente?
- Chiave eliminata per errore
- APPID SQL eliminato per errore
- SQL spostato in un'altra sottoscrizione, con conseguente necessità di un nuovo APPID
- Autorizzazioni insufficienti concesse ad APPID per le chiavi (eseguire il wrapping, annullare il wrapping, ottenere)
- Autorizzazioni revocate per l'APPID SQL


Nella sezione successiva verranno illustrate le operazioni da eseguire per risolvere gli errori più comuni.


## <a name="how-to-identify-and-resolve-the-most-common-errors"></a>Come identificare e risolvere gli errori più comuni

## <a name="missing-server-identity"></a>Identità del server mancante
Messaggio di errore: "401 AzureKeyVaultNoServerIdentity - L'identità del server non è configurata correttamente nel server. Contattare il supporto tecnico."

Rilevamento: usare il comando seguente per assicurarsi che al server SQL logico sia stata assegnata un'identità:

- [Azure PowerShell: Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 
- [Interfaccia della riga di comando di Azure: az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

Mitigazione: configurare un'identità di Azure Active Directory (Azure AD) (APPID) per il server SQL logico

Per PowerShell: usare il comando Set-AzureRmSqlServer con l'opzione [-AssignIdentity](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0) 

Per l'interfaccia della riga di comando: usare il comando az sql server update con l'opzione [--assign_identity](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update) 

Nel portale di Azure accedere all'insieme di credenziali delle chiavi e passare a Criteri di accesso:  
 - Fare clic sul pulsante Aggiungi nuovo e aggiungere l'APPID per il server creato nel passaggio precedente. 
 - Assegnare le autorizzazioni seguenti: Ottieni chiave, Esegui il wrapping della chiave e Annulla il wrapping della chiave 

[Scopri di più](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)

> [!IMPORTANT]
> Se il server SQL logico è stato spostato in una nuova sottoscrizione dopo la configurazione iniziale di Transparent Data Encryption con Azure Key Vault, è necessario ripetere il passaggio di configurazione dell'identità AAD per creare il nuovo APPID.  È quindi necessario aggiungere il nuovo APPID all'insieme di credenziali delle chiavi e riassegnare le autorizzazioni corrette. 
>

## <a name="missing-key-vault"></a>Insieme di credenziali delle chiavi mancante
Messaggio di errore: "503 AzureKeyVaultConnectionFailed - Non è stato possibile completare l'operazione nel server perché i tentativi di connettersi all'insieme di credenziali delle chiavi di Azure non sono riusciti"

Rilevamento: identificazione dell'URI della chiave e dell'insieme di credenziali delle chiavi 

Passaggio 1: usare il comando seguente per ottenere l'URI della chiave di un server SQL logico specifico:

-[Azure PowerShell: get-azurermsqlserverkeyvaultkey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

-[Interfaccia della riga di comando di Azure: az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

Passaggio 2: usare l'URI della chiave per identificare l'insieme di credenziali delle chiavi

PowerShell: è possibile esaminare le proprietà di $MyServerKeyVaultKey per ottenere dettagli sull'insieme di credenziali delle chiavi

Interfaccia della riga di comando: esaminare la protezione della crittografia server restituita per ottenere dettagli sull'insieme di credenziali delle chiavi

Mitigazione: verificare che l'insieme di credenziali delle chiavi sia disponibile
- Assicurarsi che l'insieme di credenziali delle chiavi sia disponibile e sia accessibile al server SQL logico
- Se l'insieme di credenziali delle chiavi è protetto da un firewall, assicurarsi che sia selezionata la casella di controllo per consentire ai servizi Microsoft di accedere all'insieme di credenziali delle chiavi
- Se l'insieme di credenziali delle chiavi è stato eliminato per errore, è necessario ripetere la configurazione dall'inizio


## <a name="missing-key"></a>Chiave mancante 
Messaggio di errore: "404 ServerKeyNotFound - La chiave server richiesta non è stata trovata nella sottoscrizione corrente".
"409 ServerKeyDoesNotExists - La chiave server non esiste".

Rilevamento: come identificare l'URI della chiave e l'insieme di credenziali delle chiavi
- Identificare l'URI della chiave aggiunta per il server SQL logico usando i cmdlet della sezione Insieme di credenziali delle chiavi mancante precedente per restituire l'elenco delle chiavi.

Mitigazione: verificare che la protezione Transparent Data Encryption sia presente in Azure Key Vault
- Identificare l'insieme di credenziali delle chiavi e accedervi nel portale di Azure
- Assicurarsi che la chiave identificata dall'URI della chiave sia presente

## <a name="missing-permissions"></a>Autorizzazioni mancanti 
Messaggio di errore: "401 AzureKeyVaultMissingPermissions - Nel server mancano le autorizzazioni obbligatorie per Azure Key Vault".

Rilevamento: come identificare l'URI della chiave e l'insieme di credenziali delle chiavi
- Identificare l'insieme di credenziali delle chiavi usato dal server SQL logico usando i cmdlet della sezione Insieme di credenziali delle chiavi mancante precedente.

Mitigazione: verificare che il server SQL logico abbia le autorizzazioni per l'insieme di credenziali delle chiavi e le autorizzazioni corrette per accedere alla chiave
- Nel portale di Azure accedere all'insieme di credenziali delle chiavi, passare a Criteri di accesso e individuare l'APPID di SQL Server:  
  - Se l'APPID non è presente, aggiungerlo facendo clic sul pulsante Aggiungi nuovo. 
  - Se l'APPID è presente, verificare che abbia le autorizzazioni seguenti: Ottieni chiave, Esegui il wrapping della chiave e Annulla il wrapping della chiave.
