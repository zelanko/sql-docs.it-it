---
title: Progettazione di assembly | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- designing assemblies [SQL Server]
- assemblies [CLR integration], designing
ms.assetid: 9c07f706-6508-41aa-a4d7-56ce354f9061
author: rothja
ms.author: jroth
ms.openlocfilehash: 785ab80a529140a52ec18ef96ccaaeafd03698cd
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954256"
---
# <a name="designing-assemblies"></a>Progettazione di assembly
  In questo argomento vengono illustrati alcuni fattori da prendere in considerazione durante la progettazione degli assembly:  
  
-   Assemblaggio di assembly  
  
-   Gestione della sicurezza degli assembly  
  
-   Limitazioni relative agli assembly  
  
## <a name="packaging-assemblies"></a>Assemblaggio di assembly  
 Le classi e i metodi di un assembly possono contenere funzionalità per più di una routine o un tipo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Nella maggior parte dei casi è opportuno assemblare le funzionalità delle routine che eseguono funzioni correlate all'interno dello stesso assembly, in particolare se le routine condividono classi i cui metodi si chiamano a vicenda. Ad esempio, le classi che eseguono attività di gestione dell'immissione di dati per trigger CLR (Common Language Runtime) e stored procedure CLR possono essere assemblate nello stesso assembly. Il motivo di questa scelta è che è più probabile che i metodi di queste classi si chiamino l'un l'altro rispetto ai metodi di attività meno correlate.  
  
 Quando si assembla codice in assembly, è opportuno prendere in considerazione i fattori seguenti:  
  
-   I tipi CLR definiti dall'utente e gli indici che dipendono da funzioni CLR definite dall'utente possono provocare la presenza di dati persistenti nel database che dipende dall'assembly. Modificare il codice di un assembly risulta spesso più complesso quando nel database sono presenti dati persistenti che dipendono dall'assembly. È pertanto preferibile separare il codice sul quale si basano le dipendenze dei dati persistenti, ad esempio i tipi definiti dall'utente e gli indici che utilizzano funzioni definite dall'utente, dal codice che non contiene questo tipo di dipendenze. Per ulteriori informazioni, vedere [implementazione di assembly](assemblies-implementing.md) e [ALTER assembly &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql).  
  
-   Se una parte di codice gestito richiede un'autorizzazione di livello superiore, è opportuno inserirla in un assembly separato.  
  
## <a name="managing-assembly-security"></a>Gestione della sicurezza degli assembly  
 È possibile controllare l'accesso di un assembly alle risorse protette dalla sicurezza dall'accesso di codice .NET quando esegue codice gestito. A questo scopo, quando si crea o modifica l'assembly è necessario specificare uno dei tre set di autorizzazioni disponibili: SAFE, EXTERNAL_ACCESS oppure UNSAFE.  
  
### <a name="safe"></a>SAFE  
 SAFE è il set di autorizzazioni predefinito ed è il più restrittivo. Il codice eseguito da un assembly con autorizzazioni SAFE non può accedere a risorse di sistema esterne, ad esempio file, la rete, variabili di ambiente o il Registro di sistema. Il codice SAFE può accedere ai dati dei database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] locali o eseguire calcoli e logiche di business che non comportino l'accesso a risorse esterne ai database locali.  
  
 Nella maggior parte dei casi gli assembly eseguono attività di calcolo e gestione dei dati senza accedere a risorse esterne a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. È pertanto consigliabile applicare agli assembly il set di autorizzazioni SAFE.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS consente agli assembly di accedere a specifiche risorse di sistema esterne, ad esempio file, reti, servizi Web, variabili di ambiente e il Registro di sistema. Solo gli account di accesso di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con autorizzazioni EXTERNAL ACCESS possono creare assembly EXTERNAL_ACCESS.  
  
 Gli assembly SAFE ed EXTERNAL_ACCESS possono contenere solo codice effettivamente indipendente dai tipi. Ciò significa che questi assembly possono accedere alle classi solo tramite punti di accesso ben definiti, validi per la definizione del tipo. Non possono pertanto accedere arbitrariamente a buffer di memoria non di proprietà del codice. Non possono inoltre eseguire operazioni che possono influire in modo negativo sull'affidabilità del processo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
### <a name="unsafe"></a>UNSAFE  
 Il set di autorizzazioni UNSAFE concede agli assembly libero accesso alle risorse interne ed esterne a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il codice eseguito da un assembly UNSAFE può chiamare codice non gestito.  
  
 Specificando UNSAFE si consente inoltre al codice dell'assembly di eseguire operazioni considerate non indipendenti dai tipi da CLR Verifier. Tali operazioni potrebbero accedere ai buffer di memoria nello spazio di processo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in modo incontrollato. Gli assembly UNSAFE possono anche compromettere il sistema di sicurezza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o del CLR. Si consiglia di concedere le autorizzazioni UNSAFE solo ad assembly assolutamente attendibili, creati da sviluppatori o amministratori esperti. Solo i membri del ruolo predefinito del server **sysadmin** possono creare assembly UNSAFE.  
  
## <a name="restrictions-on-assemblies"></a>Limitazioni relative agli assembly  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono imposte restrizioni sul codice gestito negli assembly per garantirne l'affidabilità e la scalabilità. Alcune operazioni potenzialmente in grado di compromettere l'affidabilità del server non sono consentite negli assembly SAFE ed EXTERNAL_ACCESS.  
  
### <a name="disallowed-custom-attributes"></a>Attributi personalizzati non consentiti  
 Non è possibile annotare gli assembly con gli attributi personalizzati seguenti:  
  
```  
System.ContextStaticAttribute  
System.MTAThreadAttribute  
System.Runtime.CompilerServices.MethodImplAttribute  
System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
System.Runtime.Remoting.Contexts.ContextAttribute  
System.Runtime.Remoting.Contexts.SynchronizationAttribute  
System.Runtime.InteropServices.DllImportAttribute   
System.Security.Permissions.CodeAccessSecurityAttribute  
System.STAThreadAttribute  
System.ThreadStaticAttribute  
```  
  
 Non è inoltre possibile annotare gli assembly SAFE ed EXTERNAL_ACCESS con gli attributi personalizzati seguenti:  
  
```  
System.Security.SuppressUnmanagedCodeSecurityAttribute  
System.Security.UnverifiableCodeAttribute  
```  
  
### <a name="disallowed-net-framework-apis"></a>API .NET Framework non consentite  
 Le [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] API annotate con uno dei **HostProtectionAttributes** non consentiti non possono essere chiamate da assembly SAFE e EXTERNAL_ACCESS.  
  
```  
eSelfAffectingProcessMgmt  
eSelfAffectingThreading  
eSynchronization  
eSharedState   
eExternalProcessMgmt  
eExternalThreading  
eSecurityInfrastructure  
eMayLeakOnAbort  
eUI  
```  
  
### <a name="supported-net-framework-assemblies"></a>Assembly .NET Framework supportati  
 Gli assembly cui fa riferimento l'assembly personalizzato devono essere caricati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando CREATE ASSEMBLY. Gli assembly [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] seguenti sono già caricati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e, pertanto, possono essere utilizzati come riferimento dagli assembly personalizzati senza richiedere l'utilizzo di CREATE ASSEMBLY.  
  
```  
custommarshallers.dll  
Microsoft.visualbasic.dll  
Microsoft.visualc.dll  
mscorlib.dll  
system.data.dll  
System.Data.SqlXml.dll  
system.dll  
system.security.dll  
system.web.services.dll  
system.xml.dll  
System.Transactions  
System.Data.OracleClient  
System.Configuration  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Assembly &#40;motore di database&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Sicurezza per l'integrazione con CLR](security/clr-integration-security.md)  
  
  
