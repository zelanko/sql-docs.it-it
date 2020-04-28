---
title: Attributi di protezione host CLR (Common Language Runtime)
description: CLR fornisce un meccanismo per annotare le API gestite nel .NET Framework con attributi quali SharedState, Synchronization e ExternalProcessMgmt.
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488056"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Attributi di protezione host e programmazione dell'integrazione con CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Common Language Runtime (CLR) fornisce un meccanismo di annotazione delle API gestite che fanno parte di .NET Framework con determinati attributi che possono interessare un host di CLR, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Di seguito sono riportati alcuni esempi di attributi di protezione host:  
  
-   **SharedState**, che indica se l'API espone la possibilità di creare o gestire lo stato condiviso (ad esempio, i campi di classe statici).  
  
-   **Sincronizzazione**, che indica se l'API espone la possibilità di eseguire la sincronizzazione tra thread.  
  
-   **ExternalProcessMgmt**, che indica se l'API espone un modo per controllare il processo host.  
  
 Sulla base di tali attributi, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specifica un elenco di attributi di protezione host non consentiti nell'ambiente host attraverso la sicurezza da accesso di codice. I requisiti CAS sono specificati da uno dei tre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di autorizzazioni: **Safe**, **EXTERNAL_ACCESS**o **unsafe**. Uno di questi tre livelli di sicurezza viene specificato quando l'assembly viene registrato nel server usando l'istruzione **create assembly** . Il codice eseguito nei set di autorizzazioni **Safe** o **EXTERNAL_ACCESS** deve evitare alcuni tipi o membri con l'attributo **System. Security. Permissions. HostProtectionAttribute** applicato. Per ulteriori informazioni, vedere [creazione di un assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md) e [restrizioni del modello di programmazione dell'integrazione CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 **HostProtectionAttribute** non è un'autorizzazione di sicurezza per migliorare l'affidabilità, perché identifica costrutti di codice specifici, ovvero tipi o metodi, che l'host potrebbe non consentire. L'utilizzo di **HostProtectionAttribute** impone un modello di programmazione che consente di proteggere la stabilità dell'host.  
  
## <a name="host-protection-attributes"></a>Attributi di protezione host  
 Gli attributi di protezione host identificano i tipi o i membri non inclusi nel modello di programmazione host e rappresentano i livelli di pericolo per l'affidabilità, riportati di seguito in ordine crescente di gravità:  
  
-   Sono altrimenti innocui.  
  
-   Possono determinare la destabilizzazione del codice utente gestito dal server.  
  
-   Possono determinare la destabilizzazione del processo del server stesso.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]non consente l'utilizzo di un tipo o di un membro che dispone di un **HostProtectionAttribute** che specifica un'enumerazione **System. Security. Permissions. HostProtectionResource** con il valore **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **Synchronization**o **UI**. In questo modo si impedisce agli assembly di chiamare membri che attivano la condivisione dello stato, eseguono la sincronizzazione, possono determinare una perdita di risorse al termine del processo o compromettere l'integrità del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipi e membri non consentiti  
 Gli argomenti seguenti identificano i tipi e i membri i cui valori **HostProtectionResource** non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sono consentiti da.  
  
> [!NOTE]  
>  Gli elenchi presenti in questi argomenti sono stati generati dagli assembly supportati.  Per ulteriori informazioni, vedere [supported .NET Framework libraries](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
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
 [Sicurezza dall'accesso di codice per l'integrazione con CLR](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrizioni del modello di programmazione dell'integrazione con CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Creazione di un assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
