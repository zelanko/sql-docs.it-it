---
title: Attributi di protezione host clr (Common Language Runtime)
description: CLR fornisce un meccanismo per annotare le API gestite in .NET Framework con attributi quali SharedState, Synchronization e ExternalProcessMgmt.
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
author: rothja
ms.author: jroth
ms.openlocfilehash: 2aeaeb5d4eb06d6d632a59300225d01cc4376369
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488056"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Attributi di protezione host e programmazione dell'integrazione con CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Common Language Runtime (CLR) fornisce un meccanismo di annotazione delle API gestite che fanno parte di .NET Framework con determinati attributi che possono interessare un host di CLR, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Di seguito sono riportati alcuni esempi di attributi di protezione host:  
  
-   **SharedState**, che indica se l'API espone la possibilità di creare o gestire lo stato condiviso, ad esempio i campi di classe statici.  
  
-   **Sincronizzazione**, che indica se l'API espone la possibilità di eseguire la sincronizzazione tra i thread.  
  
-   **ExternalProcessMgmt**, che indica se l'API espone un modo per controllare il processo host.  
  
 Sulla base di tali attributi, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specifica un elenco di attributi di protezione host non consentiti nell'ambiente host attraverso la sicurezza da accesso di codice. I requisiti CAS sono specificati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da uno dei tre set di autorizzazioni: **SAFE**, **EXTERNAL_ACCESS**o **UNSAFE**. Uno di questi tre livelli di sicurezza viene specificato quando l'assembly viene registrato nel server, utilizzando l'istruzione **CREATE ASSEMBLY.** Il codice in esecuzione all'interno dei set di autorizzazioni **SAFE** o **EXTERNAL_ACCESS** deve evitare determinati tipi o membri a cui è applicato l'attributo **System.Security.Permissions.HostProtectionAttribute.** Per ulteriori informazioni, vedere [Restrizioni relative alla creazione di un assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md) e al modello di [programmazione dell'integrazione CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 **HostProtectionAttribute** non è un'autorizzazione di sicurezza tanto quanto un modo per migliorare l'affidabilità, in quanto identifica costrutti di codice specifici, tipi o metodi, che l'host potrebbe non consentire. L'utilizzo di **HostProtectionAttribute** impone un modello di programmazione che consente di proteggere la stabilità dell'host.  
  
## <a name="host-protection-attributes"></a>Attributi di protezione host  
 Gli attributi di protezione host identificano i tipi o i membri non inclusi nel modello di programmazione host e rappresentano i livelli di pericolo per l'affidabilità, riportati di seguito in ordine crescente di gravità:  
  
-   Sono altrimenti innocui.  
  
-   Possono determinare la destabilizzazione del codice utente gestito dal server.  
  
-   Possono determinare la destabilizzazione del processo del server stesso.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]non è possibile utilizzare un tipo o un membro che dispone di un **HostProtectionAttribute** che specifica **un'enumerazione System.Security.Permissions.HostProtectionResource** con valore **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **Synchronization**o **UI**. In questo modo si impedisce agli assembly di chiamare membri che attivano la condivisione dello stato, eseguono la sincronizzazione, possono determinare una perdita di risorse al termine del processo o compromettere l'integrità del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipi e membri non consentiti  
 Negli argomenti seguenti vengono identificati i tipi e i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]membri i cui valori **HostProtectionResource** non sono consentiti da .  
  
> [!NOTE]  
>  Gli elenchi presenti in questi argomenti sono stati generati dagli assembly supportati.  Per ulteriori informazioni, vedere [Librerie .NET Framework supportate](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Tipi e membri non consentiti in Microsoft.VisualBasic.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Vengono elencati i tipi e i membri di Microsoft.VisualBasic.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
 [Tipi e membri non consentiti in mscorlib.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 Elenca i tipi e i membri in mscorlib.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
 [Tipi e membri non consentiti in System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 Elenca i tipi e i membri in System.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
 [Tipi e membri non consentiti in System.Data.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 Elenca i tipi e i membri in System.Data.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
 [Tipi e membri non consentiti in System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 Elenca i tipi e i membri in System.Core.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza dall'accesso di codice dell'integrazione CLRCLR Integration Code Access Security](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrizioni del modello di programmazione dell'integrazione CLRCLR Integration Programming Model Restrictions](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Creazione di un assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
