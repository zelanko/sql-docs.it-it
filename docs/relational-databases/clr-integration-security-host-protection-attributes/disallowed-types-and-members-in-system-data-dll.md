---
description: Tipi e membri non consentiti in System.Data.dll
title: Tipi e membri non consentiti in System.Data.dll | Microsoft Docs
descriptions: SQL Server CLR programming disallows a type or member with some values for the HostProtectionResource enum. This article lists System.Data.dll disallowed values.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
ms.openlocfilehash: 02c659d599491a61a42784a09d0e68a25b44c73a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429023"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>Tipi e membri non consentiti in System.Data.dll
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la programmazione Common Language Integration (CLR) non consente l'utilizzo di un tipo o di un membro con **HostProtectionAttribute** che specifica un'enumerazione **System. Security. Permissions. HostProtectionResource** con il valore **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **Synchronization**o **UI**. Nella tabella seguente sono elencati i membri e i tipi dell'assembly System.Data.dll i cui valori degli attributi di protezione host non sono consentiti.  
  
> [!NOTE]  
>  Questo elenco è stato generato dagli assembly supportati. Per ulteriori informazioni, vedere [supported .NET Framework libraries](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo o membro|Valori dell'attributo di protezione host|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState, Synchronization|  
|System.Xml.XmlDataDocument|Sincronizzazione|  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi di protezione host e programmazione dell'integrazione con CLR](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Tipi e membri non consentiti in Microsoft.VisualBasic.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipi e membri non consentiti in mscorlib.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipi e membri non consentiti in System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [Tipi e membri non consentiti in System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
