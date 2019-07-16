---
title: Le proprietà di sicurezza di Analysis Services | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31191e266b017400b8b8aceb2eb912f9bebca3d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163469"
---
# <a name="security-properties"></a>Proprietà di sicurezza
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta le proprietà di sicurezza del server elencate nella tabella seguente. Per altre informazioni sulle proprietà aggiuntive del server e sulla relativa impostazione, vedere [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Si applica a:** Modalità server multidimensionale e tabulare  
  
## <a name="properties"></a>Proprietà  
 **RequireClientAuthentication**  
 Proprietà booleana che indica se è necessaria l'autenticazione client.  
  
 Il valore predefinito della proprietà è True, che indica che l'autenticazione client è necessaria.  
  
 **SecurityPackageList**  
 Proprietà stringa che contiene un elenco delimitato da virgole di pacchetti SSPI utilizzati dal server per l'autenticazione client.  
  
 **DisableClientImpersonation**  
 Proprietà booleana che indica se la rappresentazione client, ad esempio dalle stored procedure, è disabilitata.  
  
 Il valore predefinito della proprietà è False, che indica che la rappresentazione client è abilitata.  
  
 **BuiltinAdminsAreServerAdmins**  
 Proprietà booleana che indica se i membri del gruppo Administrators nel computer locale sono amministratori di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 **ServiceAccountIsServerAdmin**  
 Proprietà booleana che indica se l'account del servizio è un amministratore del server.  
  
 Il valore predefinito della proprietà è True, che indica che l'account del servizio è un amministratore del server.  
  
 **ErrorMessageMode**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataProtection\ RequiredProtectionLevel**  
 Proprietà a valore integer a 32 bit con segno che definisce il livello di protezione richiesto per tutte le richieste client. Questa proprietà può assumere uno dei valori elencati nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|*0*|Nessun livello di protezione, è consentito l'utilizzo di testo non crittografato.|  
|*1*|Valore predefinito. È necessaria la crittografia, non è consentito l'utilizzo di testo non crittografato.|  
|*2*|Sono ammesse le richieste in testo non crittografato ma solo con firme, livello di protezione più debole rispetto alla crittografia.|  
  
 **AdministrativeDataProtection\ RequiredProtectionLevel**  
 Proprietà avanzata che deve essere modificata solo sotto la supervisione del servizio di supporto tecnico [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinare la modalità server di un'istanza di Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
