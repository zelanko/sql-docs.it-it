---
title: Sicurezza dall'accesso al codice dell'integrazione CLR Documenti Microsoft
description: Per l'integrazione CLR di SQL ServerSQL Server , CLR supporta la sicurezza dall'accesso di codice per il codice gestito, in cui le autorizzazioni vengono concesse agli assembly in base all'identità del codice.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
author: rothja
ms.author: jroth
ms.openlocfilehash: 912db3acb6f6dc21952e99da31a1484a9745ed0b
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488312"
---
# <a name="clr-integration-code-access-security"></a>Sicurezza da accesso di codice dell'integrazione con CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Common Language Runtime (CLR) supporta un modello di sicurezza definito sicurezza dall'accesso di codice per il codice gestito che prevede che le autorizzazioni vengano concesse agli assembly in base all'identità del codice. Per ulteriori informazioni, vedere la sezione relativa alla sicurezza da accesso di codice in .NET Framework SDK (Software Development Kit).  
  
 I criteri di sicurezza che determinano le autorizzazioni concesse agli assembly vengono definiti in tre punti diversi:  
  
-   Criteri del computer: criteri attivi per tutto il codice gestito in esecuzione sul computer nel quale viene installato [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Criteri utente: criteri attivi per il codice gestito ospitato da un processo. Per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], i criteri utente sono specifici dell'account di Windows su cui è in esecuzione il servizio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Criteri host: criteri impostati dall'host di CLR (in questo caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]), attivi per il codice gestito in esecuzione su quell'host.  
  
 Il meccanismo di sicurezza da accesso di codice supportato da CLR si basa sul presupposto che il runtime possa ospitare codice completamente o parzialmente attendibile. La protezione delle risorse mediante la sicurezza dell'accesso di codice di CRL in genere viene eseguita tramite wrapping di API gestite, che richiedono l'autorizzazione  corrispondente prima di consentire l'accesso alla risorsa. La richiesta di autorizzazione viene soddisfatta solo se tutti i chiamanti a livello di assembly nello stack di chiamate dispongono dell'autorizzazione corrispondente per la risorsa.  
  
 Il set di autorizzazioni della sicurezza dell'accesso di codice concesse al codice gestito durante l'esecuzione all'interno di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] rappresenta l'intersezione del set di autorizzazioni concesse dai tre livelli di criteri sopra descritti. Anche se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede un set di autorizzazioni a un assembly caricato in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il set di autorizzazioni effettivo concesso al codice utente potrebbe essere limitato ulteriormente dai criteri utente e a livello di computer.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Set di autorizzazioni a livello di criteri host di SQL Server  
 Il set di autorizzazioni della sicurezza da accesso di codice concesso agli assembly al livello di criteri host di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è determinato dal set di autorizzazioni specificato durante la creazione dell'assembly. Sono disponibili tre set di autorizzazioni: **SAFE**, **EXTERNAL_ACCESS** e **UNSAFE** (specificati utilizzando l'opzione **PERMISSION_SET** di CREATE ASSEMBLY [&#40;Transact-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] offre criteri di sicurezza a livello host per CLR, quando ospita tale ambiente. Questo livello di criteri aggiuntivo è sottostante ai due livelli sempre attivi e viene impostato per ogni dominio applicazione creato da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Non è indicato per il dominio applicazione predefinito che sarebbe attivo quando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crea un'istanza di CLR.  
  
 I criteri a livello host di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono una combinazione dei criteri fissi di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per gli assembly di sistema e dei criteri specificati dall'utente per gli assembly utente.  
  
 I criteri fissi per gli assembly CLR e gli assembly di sistema di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concedono loro l'attendibilità totale.  
  
 La parte dei criteri host di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] specificata dall'utente è basata su uno dei tre bucket di autorizzazione specificati per ogni assembly dal relativo proprietario. Per ulteriori informazioni sulle autorizzazioni di sicurezza elencate in basso, vedere .NET Framework SDK.  
  
### <a name="safe"></a>SAFE  
 È consentito solo il calcolo interno e l'accesso locale ai dati. **SAFE** è il set di autorizzazioni più restrittivo. Il codice eseguito da un assembly con autorizzazioni **SAFE** non può accedere a risorse di sistema esterne quali file, rete, variabili di ambiente o Registro di sistema.  
  
 **Gli** assembly SAFE dispongono delle autorizzazioni e dei valori seguenti:  
  
|Autorizzazione|Valori/Descrizione|  
|----------------|-----------------------------|  
|**Securitypermission**|**Esecuzione:** Autorizzazione all'esecuzione di codice gestito.|  
|**Sqlclientpermission**|Connessione di **contesto, ovvero true**, connessione di **contesto , sì**: è possibile utilizzare solo la connessione di contesto e la stringa di connessione può specificare solo un valore di "context connection" o "context connection-yes".<br /><br /> **AllowBlankPassword - false:**  Le password vuote non sono consentite.|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS assembly dispongono delle stesse autorizzazioni degli assembly **SAFE,** con la possibilità aggiuntiva di accedere a risorse di sistema esterne quali file, reti, variabili di ambiente e registro.  
  
 **EXTERNAL_ACCESS** assembly dispongono inoltre delle autorizzazioni e dei valori seguenti:  
  
|Autorizzazione|Valori/Descrizione|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**Senza restrizioni:** Le transazioni distribuite sono consentite.|  
|**Dnspermission**|**Senza restrizioni:** Autorizzazione a richiedere informazioni dai server dei nomi di dominio.|  
|**Environmentpermission**|**Senza restrizioni:** È consentito l'accesso completo alle variabili di ambiente di sistema e utente.|  
|**Eventlogpermission**|**Amministrare:** Sono consentite le azioni seguenti: creazione di un'origine eventi, lettura di log esistenti, eliminazione di origini eventi o registri, risposta alle voci, cancellazione di un registro eventi, ascolto di eventi e accesso a una raccolta di tutti i registri eventi.|  
|**Fileiopermission**|**Senza restrizioni:** È consentito l'accesso completo a file e cartelle.|  
|**KeyContainerPermission**|**Senza restrizioni:** È consentito l'accesso completo ai contenitori di chiavi.|  
|**Networkinformationpermission**|**Accesso:** Il ping è consentito.|  
|**Registrypermission**|Consente di **HKEY_CLASSES_ROOT**i diritti di lettura per HKEY_CLASSES_ROOT , **HKEY_LOCAL_MACHINE**, **HKEY_CURRENT_USER**, **HKEY_CURRENT_CONFIG**e **HKEY_USERS.**|  
|**Securitypermission**|**Asserzione:** Possibilità di affermare che tutti i chiamanti di questo codice dispongono dell'autorizzazione necessaria per l'operazione.<br /><br /> **ControlPrincipal:** Possibilità di manipolare l'oggetto principal.<br /><br /> **Esecuzione:** Autorizzazione all'esecuzione di codice gestito.<br /><br /> **SerializationFormatter:** Capacità di fornire servizi di serializzazione.|  
|**Smtppermission**|**Accesso:** Sono consentite le connessioni in uscita alla porta host SMTP 25.|  
|**Socketpermission**|**Connetti:** Sono consentite le connessioni in uscita (tutte le porte, tutti i protocolli) su un indirizzo di trasporto.|  
|**Sqlclientpermission**|**Senza restrizioni:** È consentito l'accesso completo all'origine dati.|  
|**Storepermission**|**Senza restrizioni:** È consentito l'accesso completo agli archivi certificati X.509.|  
|**Webpermission**|**Connetti:** Sono consentite le connessioni in uscita alle risorse Web.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE concede agli assembly libero accesso a risorse interne ed esterne a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il codice eseguito dall'interno di un assembly **UNSAFE** può anche chiamare codice non gestito.  
  
 Agli assembly **UNSAFE** viene assegnato **FullTrust**.  
  
> [!IMPORTANT]  
>  **SAFE** è l'impostazione di autorizzazione consigliata per gli [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]assembly che eseguono attività di calcolo e gestione dei dati senza accedere alle risorse all'esterno di . **EXTERNAL_ACCESS** è consigliato per gli [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]assembly che accedono a risorse esterne a . **EXTERNAL_ACCESS** assembly per impostazione predefinita vengono eseguiti come account del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio. È possibile che **EXTERNAL_ACCESS** codice impersonaino esplicitamente il contesto di sicurezza dell'autenticazione di Windows del chiamante. Poiché l'impostazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] predefinita prevede l'esecuzione come account del servizio, l'autorizzazione per eseguire **EXTERNAL_ACCESS** deve essere concessa solo agli account di accesso considerati attendibili per l'esecuzione come account del servizio. Dal punto di vista della sicurezza, **EXTERNAL_ACCESS** e **unSAFE** sono identici. Tuttavia, **gli** EXTERNAL_ACCESS assembly forniscono diverse protezioni di affidabilità e robustezza che non si trovano negli assembly **UNSAFE.** La specifica di **UNSAFE** consente al codice nell'assembly di eseguire operazioni non illegali sullo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]spazio di processo e, pertanto, può compromettere la robustezza e la scalabilità di . Per ulteriori informazioni sulla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]creazione di assembly CLR in , vedere Gestione degli assembly di [integrazione CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Accesso a risorse esterne  
 Se un tipo definito dall'utente (UDT), una stored procedure o un altro tipo di assembly del costrutto viene registrato con il set di autorizzazioni **SAFE,** il codice gestito in esecuzione nel costrutto non è in grado di accedere alle risorse esterne. Tuttavia, se vengono specificati i set di autorizzazioni **EXTERNAL_ACCESS** o **UNSAFE** e il codice gestito tenta di accedere alle risorse esterne, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] applica le regole seguenti:  
  
|Se|Risultato|  
|--------|----------|  
|Il contesto di esecuzione corrisponde a un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|I tentativi di accesso a risorse esterne vengono negati e viene generata un'eccezione di sicurezza.|  
|Il contesto di esecuzione corrisponde a un account di accesso di Windows e rappresenta il chiamante originale.|L'accesso alla risorsa esterna viene effettuato nel contesto di sicurezza dell'account di servizio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|Il chiamante non è il chiamante originale.|L'accesso viene negato e viene generata un'eccezione di sicurezza.|  
|Il contesto di esecuzione corrisponde a un account di accesso di Windows e rappresenta il chiamante originale, mentre il chiamante è stato rappresentato.|L'accesso verrà effettuato nel contesto di sicurezza del chiamante e non in quello dell'account del servizio.|  
  
## <a name="permission-set-summary"></a>Riepilogo dei set di autorizzazioni  
 Nel grafico seguente vengono riepilogate le restrizioni e le autorizzazioni concesse ai set di autorizzazioni **SAFE**, **EXTERNAL_ACCESS**e **UNSAFE.**  
  
|||||  
|-|-|-|-|  
||**SAFE**|**EXTERNAL_ACCESS**|**Pericoloso**|  
|**Autorizzazioni di sicurezza dall'accesso di codiceCode Access Security Permissions**|Sola esecuzione|Esecuzione più accesso a risorse esterne|Senza restrizioni (incluso P/Invoke)|  
|**Restrizioni del modello di programmazione**|Sì|Sì|Nessuna restrizione|  
|**Requisito di verificabilità**|Sì|Sì|No|  
|**Accesso ai dati locali**|Sì|Sì|Sì|  
|**Possibilità di chiamare il codice nativo**|No|No|Sì|  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza dell'integrazione CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Host Protection Attributes and CLR Integration Programming](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restrizioni del modello di programmazione dell'integrazione CLRCLR Integration Programming Model Restrictions](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Ambiente CLR](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
