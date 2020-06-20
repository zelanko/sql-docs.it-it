---
title: Configurazione di Analysis Services-provisioning dell'account | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services configuration
- account provisioning
ms.assetid: 169b1af2-6fe2-467f-8ca4-919f24c620ce
author: heidisteen
ms.author: heidist
ms.openlocfilehash: 109b5d9ddddf2b78c0bb8947cfa876d233f804ea
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85042705"
---
# <a name="analysis-services-configuration---account-provisioning"></a>Configurazione di Analysis Services - Provisioning account
  Utilizzare questa pagina per impostare la modalità server e per concedere le autorizzazioni amministrative a utenti o servizi che richiedono l'accesso illimitato ad [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Durante l'installazione non viene aggiunto automaticamente il gruppo locale BUILTIN\Administrators di Windows al ruolo di amministratore del server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dell'istanza che viene installata. Se si desidera aggiungere il gruppo Administrators locale al ruolo di amministratore del server, è necessario specificare in modo esplicito tale gruppo.  
  
 Se si installa [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], accertarsi di concedere le autorizzazioni amministrative agli amministratori di farm SharePoint o agli amministratori di servizi responsabili di una distribuzione server di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in una farm [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]. Per ulteriori informazioni sui [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] requisiti di installazione e account del servizio, vedere [Install SQL Server BI features with SharePoint &#40;PowerPivot and Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md).  
  
## <a name="options"></a>Opzioni  
 **Modalità server** : specifica il tipo di database di Analysis Services che è possibile distribuire nel server. Le modalità del server vengono determinate durante l'installazione e non possono essere modificate successivamente. Le modalità si escludono a vicenda, ovvero saranno necessarie due istanze di Analysis Services, ciascuna configurata per una modalità diversa, in modo da supportare sia la soluzione OLAP classico che quella per il modello tabulare.  
  
 **Specifica amministratori**: è necessario specificare almeno un amministratore del server per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli utenti o i gruppi specificati diventeranno membri del ruolo di amministratore del server dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che viene installata e devono essere account utente di dominio Windows nello stesso dominio del computer in cui viene installato il software.  
  
> [!NOTE]  
>  Controllo account utente è una caratteristica di sicurezza di Windows che richiede a un amministratore di approvare in modo specifico azioni o applicazioni amministrative prima di poterle eseguire. Poiché Controllo account utente è attivato per impostazione predefinita, verrà richiesto di consentire operazioni specifiche che necessitano di privilegi elevati. È possibile configurare Controllo account utente per modificare il comportamento predefinito oppure è possibile personalizzarlo per programmi specifici. Per ulteriori informazioni sulla configurazione del controllo dell'account utente e dell'UAC, vedere [Guida dettagliata al controllo dell'account utente e al](https://go.microsoft.com/fwlink/?linkid=196350) [controllo dell'account utente (Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351).  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli account del servizio &#40;Analysis Services&#41;](../../../2014/analysis-services/instances/configure-service-accounts-analysis-services.md)   
 [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
