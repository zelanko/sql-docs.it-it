---
title: Analysis Services - configurazione di provisioning degli Account | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services configuration
- account provisioning
ms.assetid: 169b1af2-6fe2-467f-8ca4-919f24c620ce
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 095709115c15e770b8ad54678d4a359ab4b04ac8
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351826"
---
# <a name="analysis-services-configuration---account-provisioning"></a>Configurazione di Analysis Services - Provisioning account
  Utilizzare questa pagina per impostare la modalità server e per concedere le autorizzazioni amministrative a utenti o servizi che richiedono l'accesso illimitato ad [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Durante l'installazione non viene aggiunto automaticamente il gruppo locale BUILTIN\Administrators di Windows al ruolo di amministratore del server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dell'istanza che viene installata. Se si desidera aggiungere il gruppo Administrators locale al ruolo di amministratore del server, è necessario specificare in modo esplicito tale gruppo.  
  
 Se si installa [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], accertarsi di concedere le autorizzazioni amministrative agli amministratori di farm SharePoint o agli amministratori di servizi responsabili di una distribuzione server di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in una farm [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]. Per altre informazioni sulle [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] installazione e requisiti dell'account del servizio, vedere [installare le funzionalità di Business Intelligence di SQL Server con SharePoint &#40;PowerPivot e Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md).  
  
## <a name="options"></a>Opzioni  
 **Modalità server** : specifica il tipo di database di Analysis Services che è possibile distribuire nel server. Le modalità del server vengono determinate durante l'installazione e non possono essere modificate successivamente. Le modalità si escludono a vicenda, ovvero saranno necessarie due istanze di Analysis Services, ciascuna configurata per una modalità diversa, in modo da supportare sia la soluzione OLAP classico che quella per il modello tabulare.  
  
 **Specifica amministratori**: è necessario specificare almeno un amministratore del server per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli utenti o i gruppi specificati diventeranno membri del ruolo di amministratore del server dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che viene installata e devono essere account utente di dominio Windows nello stesso dominio del computer in cui viene installato il software.  
  
> [!NOTE]  
>  Controllo account utente è una caratteristica di sicurezza di Windows che richiede a un amministratore di approvare in modo specifico azioni o applicazioni amministrative prima di poterle eseguire. Poiché Controllo account utente è attivato per impostazione predefinita, verrà richiesto di consentire operazioni specifiche che necessitano di privilegi elevati. È possibile configurare Controllo account utente per modificare il comportamento predefinito oppure è possibile personalizzarlo per programmi specifici. Per altre informazioni sul controllo dell'account utente e sulla relativa configurazione, vedere [User Account Control Step by Step Guide](https://go.microsoft.com/fwlink/?linkid=196350) (Guida dettagliata sul controllo dell'account utente in Windows) e [User Account Control (Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351).  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli account del servizio &#40;Analysis Services&#41;](../../../2014/analysis-services/instances/configure-service-accounts-analysis-services.md)   
 [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
