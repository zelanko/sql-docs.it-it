---
title: Tipi e membri non consentiti in System. Data. dll | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4233bc1ddd98d6fe678d9d37f1acd7a4b66b687e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874363"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>Tipi e membri non consentiti in System.Data.dll
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la programmazione Common Language Integration (CLR) non consente l'utilizzo di un tipo o di un membro che `HostProtectionAttribute` dispone di un `System.Security.Permissions.HostProtectionResource` oggetto che specifica un'enumerazione `ExternalProcessMgmt`con `ExternalThreading`un `MayLeakOnAbort`valore `SecurityInfrastructure`, `SelfAffectingProcessMgmnt`, `SelfAffectingThreading`,,, `Synchronization`, **SharedState**, o `UI`. Nella tabella seguente sono elencati i membri e i tipi dell'assembly System.Data.dll i cui valori degli attributi di protezione host non sono consentiti.  
  
> [!NOTE]  
>  Questo elenco è stato generato dagli assembly supportati. Per ulteriori informazioni, vedere [supported .NET Framework libraries](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo o membro|Valori dell'attributo di protezione host|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState, Synchronization|  
|System.Xml.XmlDataDocument|Synchronization|  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi di protezione host e programmazione dell'integrazione con CLR](host-protection-attributes-and-clr-integration-programming.md)   
 [Tipi e membri non consentiti in Microsoft. VisualBasic. dll](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipi e membri non consentiti in mscorlib. dll](disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipi e membri non consentiti in System. dll](disallowed-types-and-members-in-system-dll.md)   
 [Tipi e membri non consentiti in System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
  
  
