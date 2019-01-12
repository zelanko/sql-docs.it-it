---
title: Restrizioni relative al modello di programmazione dell'integrazione CLR | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d9d42017e3dfd6016d8b4a42c6953905e804200f
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54136021"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restrizioni relative al modello di programmazione dell'integrazione con CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando si compila una stored procedure gestita o un altro oggetto di database gestito, in alcuni controlli del codice eseguiti da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che devono essere presi in considerazione. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue controlli sull'assembly del codice gestito durante la registrazione prima di tutto nel database, usando il **CREATE ASSEMBLY** istruzione e anche in fase di esecuzione. Il controllo del codice gestito viene effettuato anche in fase di esecuzione in quanto è possibile che in un assembly siano presenti percorsi di codice mai raggiunti in questa fase.  Tale controllo offre quindi la flessibilità necessaria per registrare soprattutto assembly di terze parti, in modo da evitare che un assembly venga bloccato in presenza di codice considerato poco sicuro, progettato per essere eseguito in un ambiente client, ma mai nel CLR hosted. Il codice gestito deve soddisfare i requisiti dipendono dal fatto che l'assembly viene registrato come **sicura**, **EXTERNAL_ACCESS**, o **UNSAFE**, **SAFE** il più rigoroso e sono elencate di seguito.  
  
 Oltre alle restrizioni inserite negli assembly del codice gestito, vengono concesse anche delle autorizzazioni di sicurezza da accesso di codice. Common Language Runtime (CLR) supporta un modello di sicurezza definito sicurezza dall'accesso di codice per il codice gestito che prevede che le autorizzazioni vengano concesse agli assembly in base all'identità del codice. **-SAFE**, **EXTERNAL_ACCESS**, e **UNSAFE** assembly autorizzazioni diverse a seconda le autorità di certificazione. Per altre informazioni, vedere [CLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Controlli CREATE ASSEMBLY  
 Quando la **CREATE ASSEMBLY** istruzione viene eseguita, vengono eseguiti i controlli seguenti per ogni livello di sicurezza.  Se un controllo ha esito negativo **CREATE ASSEMBLY** avrà esito negativo con un messaggio di errore.  
  
### <a name="global-any-security-level"></a>Globale (qualsiasi livello di sicurezza)  
 Tutti gli assembly a cui si fa riferimento devono soddisfare uno o più dei criteri seguenti:  
  
-   L'assembly è già registrato nel database.  
  
-   L'assembly è uno degli assembly supportati. Per altre informazioni, vedere [librerie di .NET Framework supportate](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
-   Si usa **CREATE ASSEMBLY dal**_\<location >,_ e tutti gli assembly di riferimento e le relative dipendenze sono disponibili in *\<percorso >*.  
  
-   Si usa **CREATE ASSEMBLY dal**_\<... Byte >,_ e tutti i riferimenti vengono specificati tramite lo spazio separati byte.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Tutti i **EXTERNAL_ACCESS** gli assembly devono soddisfare i criteri seguenti:  
  
-   I campi statici non vengono utilizzati per archiviare informazioni. Sono consentiti campi statici di sola lettura.  
  
-   Il test di PEVerify viene superato. Lo strumento PEVerify (peverify.exe) che verifica che il codice MSIL e i metadati associati soddisfino i requisiti di indipendenza dai tipi, viene fornito insieme a .NET Framework SDK.  
  
-   La sincronizzazione, ad esempio con il **SynchronizationAttribute** classe, non viene utilizzata.  
  
-   I metodi del finalizzatore non vengono utilizzati.  
  
 Gli attributi personalizzati seguenti non sono consentiti negli **EXTERNAL_ACCESS** assembly:  
  
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
  
-   Tutti i **EXTERNAL_ACCESS** vengono verificate le condizioni dell'assembly.  
  
## <a name="runtime-checks"></a>Controlli runtime  
 In fase di esecuzione l'assembly del codice viene esaminato per verificare la presenza delle condizioni riportate di seguito. Se ne viene riscontrata una, non verrà consentita l'esecuzione del codice gestito e sarà generata un'eccezione.  
  
### <a name="unsafe"></a>UNSAFE  
 Il caricamento di un assembly da entrambe in modo esplicito chiamando il **System.Reflection.Assembly.Load()** metodo da una matrice di byte o in modo implicito tramite l'utilizzo di **Reflection. Emit** dello spazio dei nomi-non è consentito.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Tutti i **UNSAFE** le condizioni vengono controllate.  
  
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
  
 Per altre informazioni su attributi di protezione host e un elenco di tipi non consentiti e membri nell'assembly supportati, vedere [attributi di protezione Host e programmazione di integrazione CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Tutti i **EXTERNAL_ACCESS** le condizioni vengono controllate.  
  
## <a name="see-also"></a>Vedere anche  
 [Librerie .NET Framework supportate](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [Sicurezza dall'accesso di codice integrazione CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Attributi di protezione host e programmazione dell'integrazione con CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Creazione di un assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
