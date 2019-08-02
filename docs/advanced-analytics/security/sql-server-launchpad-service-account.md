---
title: Configurazione dell'account del servizio Launchpad di SQL Server
description: Come modificare l'account del servizio Launchpad di SQL Server usato per l'esecuzione di script esterni su SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a94ae0f82b407f8f254a31b33d4d9dcd97f24e77
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714939"
---
# <a name="sql-server-launchpad-service-configuration"></a>Configurazione del servizio Launchpad di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] È un servizio che gestisce ed esegue script esterni, in modo analogo al modo in cui il servizio di indicizzazione e query full-text avvia un host separato per l'elaborazione di query full-text.

Per ulteriori informazioni, vedere le sezioni Launchpad nell' [architettura di estendibilità in SQL Server Machine Learning Services](../../advanced-analytics/concepts/extensibility-framework.md#launchpad) e [Panoramica della sicurezza per il Framework di estendibilità in SQL Server Machine Learning Services](../../advanced-analytics/concepts/security.md#launchpad).

## <a name="account-permissions"></a>Autorizzazioni dell'account

Per impostazione predefinita, Launchpad di SQL Server è configurato per l'esecuzione in **NT Service\MSSQLLaunchpad**, di cui viene effettuato il provisioning con tutte le autorizzazioni necessarie per eseguire script esterni. La rimozione delle autorizzazioni da questo account può comportare la mancata avvio di Launchpad o l'accesso all'istanza SQL Server in cui devono essere eseguiti gli script esterni.

Se si modifica l'account del servizio, assicurarsi di utilizzare la [console Criteri di sicurezza locali](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings).

Le autorizzazioni necessarie per questo account sono elencate nella tabella seguente.

| Impostazione di criteri di gruppo | Nome costante |
|----------------------|---------------|
| [Modificare le quote di memoria per un processo](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [Ignora controllo incrociato](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [Accedi come servizio](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [Sostituire un token a livello di processo](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

Per altre informazioni sulle autorizzazioni necessarie per l'esecuzione di servizi di SQL Server, vedere [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>Proprietà di configurazione

In genere, non esiste alcun motivo per modificare la configurazione del servizio. Le proprietà che possono essere modificate includono l'account del servizio, il numero di processi esterni (20 per impostazione predefinita) o i criteri di reimpostazione della password per gli account di lavoro.

1. Aprire [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md).

2. In servizi SQL Server fare clic con il pulsante destro del mouse su Launchpad di SQL Server e scegliere **Proprietà**.
  + Per modificare l'account del servizio, fare clic sulla scheda **accesso** .
  + Per aumentare il numero di utenti, fare clic sulla scheda **Avanzate** e modificare il numero di contesti di **sicurezza**.

> [!Note]
> Nelle prime versioni di SQL Server 2016 R Services, è possibile modificare alcune proprietà del servizio modificando il [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] file di configurazione. Questo file non viene più utilizzato per la modifica delle configurazioni. Gestione configurazione SQL Server è l'approccio corretto per le modifiche alla configurazione del servizio, ad esempio l'account del servizio e il numero di utenti.

## <a name="debug-settings"></a>Impostazioni di debug

Alcune proprietà possono essere modificate solo tramite il file di configurazione della finestra di avvio, che può essere utile in casi limitati, ad esempio il debug. Il file di configurazione viene creato durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'installazione e per impostazione predefinita viene salvato come file di testo `<instance path>\binn\rlauncher.config`normale in.

Per poter apportare modifiche a questo file è necessario essere amministratore del computer su cui è eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si decide di modificare il file, si consiglia di crearne una copia di backup prima di salvare le modifiche.

Nella tabella seguente sono elencate le impostazioni avanzate [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]per, con i valori consentiti.

|**Nome impostazione**|**Tipo**|**Descrizione**|
|----|----|----|
|PULIZIA\_PROCESSO\_ALL'USCITA\_|Integer |Si tratta solo di un'impostazione interna. non modificare questo valore. </br></br>Specifica se la cartella di lavoro temporanea creata per ogni sessione del runtime esterno deve essere pulita dopo il completamento della sessione. L'impostazione è utile per il debug. </br></br>I valori supportati sono **0** (disabilitato) o **1** (abilitato). </br></br>Il valore predefinito è 1, che indica che i file di log sono rimossi all'uscita.|
|LIVELLO\_DI TRACCIA|Integer |Configura il livello di dettaglio della traccia di MSSQLLAUNCHPAD a scopo di debug. Ciò influiscono sui file di traccia nel percorso specificato dall'impostazione LOG_DIRECTORY. </br></br>I valori supportati sono: **1** (errore), **2** (prestazioni), **3** (avviso), **4** (informazioni). </br></br>Il valore predefinito è 1, che indica solo gli errori di output.|

Tutte le impostazioni assumono la forma di coppie chiave-valore e ogni impostazione si trova su una riga diversa. Ad esempio, per modificare il livello di traccia, è necessario aggiungere la `Default: TRACE_LEVEL=4`riga.

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>Applicazione di criteri password

Se l'organizzazione ha criteri che richiedono la modifica delle password a intervalli regolari, potrebbe essere necessario forzare il servizio Launchpad in modo da rigenerare le password crittografate gestite dal servizio per gli account di lavoro.

Per abilitare questa impostazione e forzare l'aggiornamento delle password, aprire il riquadro **Proprietà** per il servizio Launchpad in Gestione configurazione SQL Server, fare clic su **Avanzate** e modificare l'impostazione di **Reimposta password utenti esterni** scegliendo **Sì**. Quando si applica questa modifica, le password vengono rigenerate immediatamente per tutti gli account utente. Per eseguire uno script esterno dopo questa modifica, è necessario riavviare il servizio Launchpad, al momento della lettura delle password appena generate.

Per reimpostare le password a intervalli regolari, è possibile impostare questo flag manualmente o usare uno script.

## <a name="next-steps"></a>Passaggi successivi

+ [Framework di estendibilità](../concepts/extensibility-framework.md)
+ [Panoramica della sicurezza](../concepts/security.md)
