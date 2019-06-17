---
title: Le proprietà di sicurezza | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], properties
- SecurityPackageList property
- BuiltinAdminsAreServerAdmins property
- DisableClientImpersonation property
- ErrorMessageMode property
- RequiredProtectionLevel property
- ServiceAccountIsServerAdmin property
- RequireClientAuthentication property
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9316827245adfbcf64bd798869f570dc5f0af14c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068912"
---
# <a name="security-properties"></a>Proprietà di sicurezza
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta le proprietà di sicurezza del server elencate nella tabella seguente. Per altre informazioni sulle proprietà aggiuntive del server e sulla relativa impostazione, vedere [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Si applica a:** Modalità server multidimensionale e tabulare  
  
## <a name="properties"></a>Proprietà  
 `RequireClientAuthentication`  
 Proprietà booleana che indica se è necessaria l'autenticazione client.  
  
 Il valore predefinito della proprietà è True, che indica che l'autenticazione client è necessaria.  
  
 `SecurityPackageList`  
 Proprietà stringa che contiene un elenco delimitato da virgole di pacchetti SSPI utilizzati dal server per l'autenticazione client.  
  
 `DisableClientImpersonation`  
 Proprietà booleana che indica se la rappresentazione client, ad esempio dalle stored procedure, è disabilitata.  
  
 Il valore predefinito della proprietà è False, che indica che la rappresentazione client è abilitata.  
  
 `BuiltinAdminsAreServerAdmins`  
 Proprietà booleana che indica se i membri del gruppo Administrators nel computer locale sono amministratori di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 `ServiceAccountIsServerAdmin`  
 Proprietà booleana che indica se l'account del servizio è un amministratore del server.  
  
 Il valore predefinito della proprietà è True, che indica che l'account del servizio è un amministratore del server.  
  
 `ErrorMessageMode`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `DataProtection\ RequiredProtectionLevel`  
 Proprietà a valore integer a 32 bit con segno che definisce il livello di protezione richiesto per tutte le richieste client. Questa proprietà può assumere uno dei valori elencati nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*0*|Nessun livello di protezione, è consentito l'utilizzo di testo non crittografato.|  
|*1*|Valore predefinito. È necessaria la crittografia, non è consentito l'utilizzo di testo non crittografato.|  
|*2*|Sono ammesse le richieste in testo non crittografato ma solo con firme, livello di protezione più debole rispetto alla crittografia.|  
  
 `AdministrativeDataProtection\ RequiredProtectionLevel`  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà del Server in Analysis Services](server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
