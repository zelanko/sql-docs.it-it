---
title: Restrizioni del modello di programmazione dell'integrazione CLR Documenti Microsoft
description: SQL ServerSQL Server esegue controlli del codice sugli oggetti di database gestiti quando vengono registrati per la prima volta tramite CREATE ASSEMBLY e in fase di esecuzione.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
author: rothja
ms.author: jroth
ms.openlocfilehash: 83b73909cf1844796640a83910ee609eadd7dba4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488539"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restrizioni relative al modello di programmazione dell'integrazione con CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Quando si compila una stored procedure gestita o un altro [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oggetto di database gestito, è necessario considerare alcuni controlli del codice eseguiti da tale stored procedure. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Esegue controlli sull'assembly del codice gestito quando viene registrato per la prima volta nel database, utilizzando l'istruzione **CREATE ASSEMBLY** e anche in fase di esecuzione. Il controllo del codice gestito viene effettuato anche in fase di esecuzione in quanto è possibile che in un assembly siano presenti percorsi di codice mai raggiunti in questa fase.  Tale controllo offre quindi la flessibilità necessaria per registrare soprattutto assembly di terze parti, in modo da evitare che un assembly venga bloccato in presenza di codice considerato poco sicuro, progettato per essere eseguito in un ambiente client, ma mai nel CLR hosted. I requisiti che il codice gestito deve soddisfare dipendono dal fatto che l'assembly sia registrato come **SAFE**, **EXTERNAL_ACCESS**o **UNSAFE**, **SAFE** è il più rigoroso e sono elencati di seguito.  
  
 Oltre alle restrizioni inserite negli assembly del codice gestito, vengono concesse anche delle autorizzazioni di sicurezza da accesso di codice. Common Language Runtime (CLR) supporta un modello di sicurezza definito sicurezza dall'accesso di codice per il codice gestito che prevede che le autorizzazioni vengano concesse agli assembly in base all'identità del codice. **Gli**assembly SAFE , **EXTERNAL_ACCESS**e **UNSAFE** dispongono di autorizzazioni CAS diverse. Per ulteriori informazioni, vedere [Sicurezza dall'accesso di codice dell'integrazione CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Controlli CREATE ASSEMBLY  
 Quando viene eseguita l'istruzione **CREATE ASSEMBLY,** vengono eseguiti i controlli seguenti per ogni livello di sicurezza.  Se un controllo ha esito negativo, **CREATE ASSEMBLY** avrà esito negativo con un messaggio di errore.  
  
### <a name="global-any-security-level"></a>Globale (qualsiasi livello di sicurezza)  
 Tutti gli assembly a cui si fa riferimento devono soddisfare uno o più dei criteri seguenti:  
  
-   L'assembly è già registrato nel database.  
  
-   L'assembly è uno degli assembly supportati. Per ulteriori informazioni, vedere [Librerie .NET Framework supportate](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
-   Si utilizza **CREATE ASSEMBLY FROM**_\<percorso>_ e tutti gli assembly a cui si fa riferimento e le relative dipendenze sono disponibili nel * \<percorso>*.  
  
-   Si utilizza **CREATE ASSEMBLY FROM**_\<byte ...>_ e tutti i riferimenti vengono specificati tramite byte separati da spazi.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Tutti **gli assembly EXTERNAL_ACCESS** devono soddisfare i seguenti criteri:  
  
-   I campi statici non vengono utilizzati per archiviare informazioni. Sono consentiti campi statici di sola lettura.  
  
-   Il test di PEVerify viene superato. Lo strumento PEVerify (peverify.exe) che verifica che il codice MSIL e i metadati associati soddisfino i requisiti di indipendenza dai tipi, viene fornito insieme a .NET Framework SDK.  
  
-   La sincronizzazione, ad esempio con la classe **SynchronizationAttribute,** non viene utilizzata.  
  
-   I metodi del finalizzatore non vengono utilizzati.  
  
 Negli assembly **di EXTERNAL_ACCESS** non sono consentiti gli attributi personalizzati seguenti:  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   Tutte le condizioni di assemblaggio **EXTERNAL_ACCESS** vengono controllate.  
  
## <a name="runtime-checks"></a>Controlli runtime  
 In fase di esecuzione l'assembly del codice viene esaminato per verificare la presenza delle condizioni riportate di seguito. Se ne viene riscontrata una, non verrà consentita l'esecuzione del codice gestito e sarà generata un'eccezione.  
  
### <a name="unsafe"></a>UNSAFE  
 Il caricamento di un assembly in modo esplicito chiamando il metodo **System.Reflection.Assembly.Load()** da una matrice di byte o in modo implicito tramite l'utilizzo dello spazio dei nomi **Reflection.Emit** non è consentito.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Tutte le condizioni **UNSAFE** sono controllate.  
  
 Tutti i tipi e i metodi annotati con i valori dell'attributo di protezione host riportati di seguito dell'elenco supportato di assembly non sono consentiti.  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Synchronization  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 Per ulteriori informazioni sugli HPA e su un elenco di tipi e membri non consentiti negli assembly supportati, vedere [Attributi di protezione host e programmazione dell'integrazione CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Tutte le condizioni **EXTERNAL_ACCESS** sono controllate.  
  
## <a name="see-also"></a>Vedere anche  
 [Librerie .NET Framework supportate](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [Sicurezza dall'accesso di codice dell'integrazione CLRCLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Host Protection Attributes and CLR Integration Programming](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Creazione di un assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
