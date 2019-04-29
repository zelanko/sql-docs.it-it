---
title: Ospitare gli attributi di protezione e programmazione dell'integrazione con Common Language Runtime | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 68f1f114002ab0ef38c7565a523723a06958048d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874346"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Attributi di protezione host e programmazione dell'integrazione con CLR
  Common Language Runtime (CLR) fornisce un meccanismo di annotazione delle API gestite che fanno parte di .NET Framework con determinati attributi che possono interessare un host di CLR, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Di seguito sono riportati alcuni esempi di attributi di protezione host:  
  
-   `SharedState`, che indica se l'API espone la possibilità di creare o gestire uno stato condiviso, ad esempio campi classe statici.  
  
-   `Synchronization`, che indica se l'API espone la possibilità di eseguire la sincronizzazione tra thread.  
  
-   `ExternalProcessMgmt`, che indica se l'API espone una modalità per controllare il processo host.  
  
 Sulla base di tali attributi, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specifica un elenco di attributi di protezione host non consentiti nell'ambiente host attraverso la sicurezza da accesso di codice. I requisiti della protezione dall'accesso di codice sono specificati da uno dei tre set di autorizzazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: `SAFE`, `EXTERNAL_ACCESS` o `UNSAFE`. Uno dei tre livelli di sicurezza viene specificato quando l'assembly viene registrato nel server, mediante l'istruzione `CREATE ASSEMBLY`. Durante l'esecuzione di codice nell'ambito dei set di autorizzazioni `SAFE` o `EXTERNAL_ACCESS`, è necessario evitare alcuni tipi o membri a cui è applicato l'attributo `System.Security.Permissions.HostProtectionAttribute`. Per altre informazioni, vedere [creazione di un Assembly](../clr-integration/assemblies/creating-an-assembly.md) e [restrizioni del modello di programmazione integrazione CLR](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 `HostProtectionAttribute` rappresenta più una modalità per migliorare l'affidabilità che un'autorizzazione di sicurezza, in quanto identifica i costrutti di codice specifici, tipi o metodi, che possono essere disattivati dall'host. L'utilizzo di `HostProtectionAttribute` impone un modello di programmazione che consente di migliorare la stabilità dell'host.  
  
## <a name="host-protection-attributes"></a>Attributi di protezione host  
 Gli attributi di protezione host identificano i tipi o i membri non inclusi nel modello di programmazione host e rappresentano i livelli di pericolo per l'affidabilità, riportati di seguito in ordine crescente di gravità:  
  
-   Sono altrimenti innocui.  
  
-   Possono determinare la destabilizzazione del codice utente gestito dal server.  
  
-   Possono determinare la destabilizzazione del processo del server stesso.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente l'utilizzo di un tipo o membro che dispone di un `HostProtectionAttribute` che specifica una `System.Security.Permissions.HostProtectionResource` con un valore di enumerazione `ExternalProcessMgmt`, `ExternalThreading`, `MayLeakOnAbort`, `SecurityInfrastructure`, `SelfAffectingProcessMgmnt`, `SelfAffectingThreading`, `SharedState`, `Synchronization`, o `UI`. In questo modo si impedisce agli assembly di chiamare membri che attivano la condivisione dello stato, eseguono la sincronizzazione, possono determinare una perdita di risorse al termine del processo o compromettere l'integrità del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipi e membri non consentiti  
 Negli argomenti riportati di seguito vengono identificati tipi e membri i cui valori di `HostProtectionResource` non sono consentiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Gli elenchi presenti in questi argomenti sono stati generati dagli assembly supportati.  Per altre informazioni, vedere [librerie di .NET Framework supportate](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
## <a name="in-this-section"></a>In questa sezione  
 [Tipi e membri non consentiti in Microsoft.VisualBasic.dll](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Vengono elencati i tipi e i membri di Microsoft.VisualBasic.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
 [Tipi e membri non consentiti in mscorlib.dll](disallowed-types-and-members-in-mscorlib-dll.md)  
 Elenca i tipi e i membri in mscorlib.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
 [Tipi e membri non consentiti in System.dll](disallowed-types-and-members-in-system-dll.md)  
 Elenca i tipi e i membri in System.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
 [Tipi e membri non consentiti in System.Data.dll](disallowed-types-and-members-in-system-data-dll.md)  
 Elenca i tipi e i membri in System.Data.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
 [Tipi e membri non consentiti in System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
 Elenca i tipi e i membri in System.Core.dll, i cui valori degli attributi di protezione host non sono consentiti.  
  
## <a name="see-also"></a>Vedere anche  
 [Sicurezza dall'accesso di codice integrazione CLR](../clr-integration/security/clr-integration-code-access-security.md)   
 [Restrizioni relative al modello programmazione CLR Integration](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Creazione di un assembly](../clr-integration/assemblies/creating-an-assembly.md)  
  
  
