---
title: Sicurezza dall'accesso di codice integrazione di Common Language Runtime | Microsoft Docs
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
ms.openlocfilehash: f49968392dd813b48f43e5e63586fd0c6bec71d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118522"
---
# <a name="clr-integration-code-access-security"></a>Sicurezza da accesso di codice dell'integrazione con CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Common Language Runtime (CLR) supporta un modello di sicurezza definito sicurezza dall'accesso di codice per il codice gestito che prevede che le autorizzazioni vengano concesse agli assembly in base all'identità del codice. Per ulteriori informazioni, vedere la sezione relativa alla sicurezza da accesso di codice in .NET Framework SDK (Software Development Kit).  
  
 I criteri di sicurezza che determinano le autorizzazioni concesse agli assembly vengono definiti in tre punti diversi:  
  
-   Criteri del computer: Si tratta del criterio attivo per tutto il codice gestito in esecuzione sul computer in cui [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è installato.  
  
-   Criteri utente: Si tratta di criteri attivi per codice gestito ospitato da un processo. Per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], i criteri utente sono specifici dell'account di Windows su cui è in esecuzione il servizio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Criteri host: Si tratta di criteri impostati dall'host di CLR (in questo caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) che è attiva per il codice gestito in esecuzione in tale host.  
  
 Il meccanismo di sicurezza da accesso di codice supportato da CLR si basa sul presupposto che il runtime possa ospitare codice completamente o parzialmente attendibile. Le risorse che sono protette dalla sicurezza dall'accesso di codice CLR in genere vengono eseguito il wrapping da interfacce di programmazione dell'applicazione gestita che richiedono l'autorizzazione corrispondente prima di consentire l'accesso alla risorsa. La richiesta di autorizzazione viene soddisfatta solo se tutti i chiamanti a livello di assembly nello stack di chiamate dispongono dell'autorizzazione corrispondente per la risorsa.  
  
 Il set di autorizzazioni della sicurezza dell'accesso di codice concesse al codice gestito durante l'esecuzione all'interno di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] rappresenta l'intersezione del set di autorizzazioni concesse dai tre livelli di criteri sopra descritti. Anche se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede un set di autorizzazioni a un assembly caricato in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il set di autorizzazioni effettivo concesso al codice utente potrebbe essere limitato ulteriormente dai criteri utente e a livello di computer.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Set di autorizzazioni a livello di criteri host di SQL Server  
 Il set di autorizzazioni della sicurezza da accesso di codice concesso agli assembly al livello di criteri host di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è determinato dal set di autorizzazioni specificato durante la creazione dell'assembly. Sono disponibili tre set di autorizzazioni: **-SAFE**, **EXTERNAL_ACCESS** e **UNSAFE** (specificata tramite la **PERMISSION_SET** opzione di [CREATE ASSEMBLY &#40; Transact-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] offre criteri di sicurezza a livello host per CLR, quando ospita tale ambiente. Questo livello di criteri aggiuntivo è sottostante ai due livelli sempre attivi e viene impostato per ogni dominio applicazione creato da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Non è indicato per il dominio applicazione predefinito che sarebbe attivo quando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crea un'istanza di CLR.  
  
 I criteri a livello host di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono una combinazione dei criteri fissi di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per gli assembly di sistema e dei criteri specificati dall'utente per gli assembly utente.  
  
 I criteri fissi per gli assembly CLR e gli assembly di sistema di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concedono loro l'attendibilità totale.  
  
 La parte dei criteri host di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] specificata dall'utente è basata su uno dei tre bucket di autorizzazione specificati per ogni assembly dal relativo proprietario. Per ulteriori informazioni sulle autorizzazioni di sicurezza elencate in basso, vedere .NET Framework SDK.  
  
### <a name="safe"></a>SAFE  
 È consentito solo il calcolo interno e l'accesso locale ai dati. **SAFE** è il set di autorizzazioni più restrittivo. Il codice eseguito da un assembly con **sicuro** autorizzazioni non possono accedere alle risorse di sistema esterne, ad esempio file, rete, le variabili di ambiente o il Registro di sistema.  
  
 **SAFE** gli assembly hanno le autorizzazioni e i valori seguenti:  
  
|Autorizzazioni|Valori/Descrizione|  
|----------------|-----------------------------|  
|**SecurityPermission**|**Esecuzione:** Autorizzazione per eseguire codice gestito.|  
|**SqlClientPermission**|**Connessione di contesto = true**, **connessione di contesto = yes**: Solo la connessione di contesto può essere utilizzata e la stringa di connessione può specificare solo un valore di "connessione di contesto = true" o "connessione di contesto = yes".<br /><br /> **AllowBlankPassword = false:**  Le password vuote non sono consentite.|  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Gli assembly EXTERNAL_ACCESS dispongono delle stesse autorizzazioni **sicuro** assembly, con la possibilità aggiuntiva di accedere alle risorse di sistema esterne, ad esempio file, reti, variabili di ambiente e Registro di sistema.  
  
 **EXTERNAL_ACCESS** gli assembly hanno anche le autorizzazioni e i valori seguenti:  
  
|Autorizzazioni|Valori/Descrizione|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**Senza restrizioni:** Sono consentite transazioni distribuite.|  
|**DNSPermission**|**Senza restrizioni:** Autorizzazione per richiedere informazioni da server dei nomi di dominio.|  
|**EnvironmentPermission**|**Senza restrizioni:** Accesso completo alle variabili di ambiente di sistema e degli utenti è consentito.|  
|**EventLogPermission**|**Amministrazione:** Sono consentite le azioni seguenti: creazione di un'origine eventi, leggere i log esistenti, l'eliminazione di origini eventi o log, rispondere alle immissioni, cancellare un log eventi, in ascolto degli eventi e l'accesso a una raccolta di tutti i registri eventi.|  
|**FileIOPermission**|**Senza restrizioni:** Accesso completo ai file e cartelle è consentito.|  
|**KeyContainerPermission**|**Senza restrizioni:** Accesso completo ai contenitori di chiavi è consentito.|  
|**NetworkInformationPermission**|**Accesso:** Esecuzione del ping è consentita.|  
|**RegistryPermission**|Concede diritti di lettura a **HKEY_CLASSES_ROOT**, **HKEY_LOCAL_MACHINE**, **HKEY_CURRENT_USER**, **HKEY_CURRENT_CONFIG**e  **HKEY_USERS.**|  
|**SecurityPermission**|**Asserzione:** Capacità di asserire che tutti i chiamanti del codice dispongono dell'autorizzazione necessaria per l'operazione.<br /><br /> **ControlPrincipal:** Possibilità di modificare l'oggetto principal.<br /><br /> **Esecuzione:** Autorizzazione per eseguire codice gestito.<br /><br /> **SerializationFormatter:** Possibilità di fornire servizi di serializzazione.|  
|**SmtpPermission**|**Accesso:** Sono consentite le connessioni in uscita alla porta 25 dell'host SMTP.|  
|**SocketPermission**|**Connessione:** Sono consentite le connessioni in uscita (tutte le porte, tutti i protocolli) su un indirizzo di trasporto.|  
|**SqlClientPermission**|**Senza restrizioni:** Accesso completo all'origine dati è consentito.|  
|**StorePermission**|**Senza restrizioni:** Accesso completo agli archivi certificati X.509 è consentito.|  
|**WebPermission**|**Connessione:** Sono consentite le connessioni in uscita per le risorse web.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE concede agli assembly libero accesso a risorse interne ed esterne a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Codice eseguito all'interno un **UNSAFE** assembly può anche chiamare codice non gestito.  
  
 **UNSAFE** gli assembly vengono assegnati **FullTrust**.  
  
> [!IMPORTANT]  
>  **-SAFE** è l'impostazione di autorizzazioni consigliata per gli assembly che eseguono attività di gestione di calcolo e i dati senza accedere alle risorse esterne [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **EXTERNAL_ACCESS** è consigliato per gli assembly che accedono alle risorse esterne [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **EXTERNAL_ACCESS** gli assembly per impostazione predefinita vengono eseguiti come il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] account del servizio. È possibile **EXTERNAL_ACCESS** codice per rappresentare in modo esplicito di contesto di sicurezza di autenticazione di Windows del chiamante. Poiché il valore predefinito è l'esecuzione come le [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] account del servizio, l'autorizzazione per eseguire **EXTERNAL_ACCESS** deve solo essere assegnati agli account di accesso affidabili per essere eseguiti come account del servizio. Dal punto di vista della sicurezza, **EXTERNAL_ACCESS** e **UNSAFE** gli assembly sono identici. Tuttavia **EXTERNAL_ACCESS** assembly forniscono vari meccanismi di affidabilità ed efficienza che non sono nello **UNSAFE** assembly. Che specifica **UNSAFE** , il codice assembly può eseguire operazioni non valide sulle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] spazio di processo e pertanto può compromettere l'affidabilità e la scalabilità del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per altre informazioni sulla creazione di assembly CLR in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [la gestione degli assembly dell'integrazione CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Accesso a risorse esterne  
 Se un tipo definito dall'utente (UDT), stored procedure o altro tipo di assembly del costrutto è registrato con il **sicuro** del set di autorizzazioni, quindi l'esecuzione nel costrutto di codice gestito è in grado di accedere a risorse esterne. Tuttavia, se il **EXTERNAL_ACCESS** o **UNSAFE** vengono specificati i set di autorizzazioni e codice gestito tenta di accedere alle risorse esterne, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] applica le regole seguenti:  
  
|Se|Allora|  
|--------|----------|  
|Il contesto di esecuzione corrisponde a un account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|I tentativi di accesso a risorse esterne vengono negati e viene generata un'eccezione di sicurezza.|  
|Il contesto di esecuzione corrisponde a un account di accesso di Windows e rappresenta il chiamante originale.|L'accesso alla risorsa esterna viene effettuato nel contesto di sicurezza dell'account di servizio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|Il chiamante non è il chiamante originale.|L'accesso viene negato e viene generata un'eccezione di sicurezza.|  
|Il contesto di esecuzione corrisponde a un account di accesso di Windows e rappresenta il chiamante originale, mentre il chiamante è stato rappresentato.|L'accesso verrà effettuato nel contesto di sicurezza del chiamante e non in quello dell'account del servizio.|  
  
## <a name="permission-set-summary"></a>Riepilogo dei set di autorizzazioni  
 Il grafico seguente sono riepilogate le restrizioni e autorizzazioni concesse per il **sicura**, **EXTERNAL_ACCESS**, e **UNSAFE** set di autorizzazioni.  
  
|||||  
|-|-|-|-|  
||**SAFE**|**EXTERNAL_ACCESS**|**UNSAFE**|  
|**Autorizzazioni di sicurezza di accesso di codice**|Sola esecuzione|Esecuzione più accesso a risorse esterne|Senza restrizioni (incluso P/Invoke)|  
|**Restrizioni del modello di programmazione**|Yes|Yes|Nessuna restrizione|  
|**Requisito di verificabilità**|Yes|Sì|No|  
|**Accesso ai dati locali**|Yes|Yes|Yes|  
|**Possibilità di chiamare codice nativo**|No|No|Yes|  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza dell'integrazione CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Attributi di protezione host e programmazione dell'integrazione con CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restrizioni relative al modello programmazione CLR Integration](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Ambiente CLR](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
