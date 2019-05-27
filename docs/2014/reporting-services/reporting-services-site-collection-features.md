---
title: Caratteristiche raccolta siti di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e05ae162-a4b2-489d-9853-d6b09414e632
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9475ee323222b800a9c4b9a86e737fdd161e7a60
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66102755"
---
# <a name="reporting-services-site-collection-features"></a>Funzionalità della raccolta siti di Reporting Services
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] La modalità SharePoint fornisce tre funzionalità della raccolta siti di SharePoint. Le funzionalità supportano l'ambiente di report in modalità SharePoint di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] generale, [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], una funzionalità del componente aggiuntivo [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per [!INCLUDE[SPS2010](../includes/sps2010-md.md)] Enterprise Edition, e le operazioni di gestione per [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in Amministrazione centrale SharePoint.  
  
## <a name="site-collection-features"></a>Funzionalità della raccolta siti  
 Nella tabella seguente vengono descritte le funzionalità della raccolta siti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|**Funzionalità Amministrazione centrale del server di report**|Consente di abilitare le funzionalità per la gestione dell'integrazione con un server di report [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Questa funzionalità viene installata e utilizzata solo nella raccolta siti di Amministrazione centrale SharePoint.<br /><br /> La funzionalità di integrazione del server di report viene attivata automaticamente nella raccolta siti di Amministrazione centrale SharePoint dopo aver installato il componente aggiuntivo [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] per prodotti SharePoint. In alcune situazioni sarà necessario attivare manualmente la funzionalità. Per attivare la funzionalità del server di report, usare le pagine di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nella pagina Impostazioni del sito di Amministrazione centrale SharePoint.<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e versioni successive del componente aggiuntivo per prodotti SharePoint attiva la funzionalità di integrazione del server di report per tutte le raccolte siti esistenti al momento dell'installazione del componente aggiuntivo. La funzionalità risulterà inoltre attivata automaticamente per le nuove raccolte siti.|  
|**Funzionalità di integrazione con il server di report**|Consente la creazione di report avanzata tramite [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> Questa funzionalità è attiva per impostazione predefinita.|  
|**Funzionalità di integrazione di Power View**|Consente l'esplorazione dei dati interattiva e la presentazione visiva in base a cartelle di lavoro di PowerPivot e database tabulari di Analysis Services.<br /><br /> L'accesso alla funzionalità può essere eseguito dai menu di scelta rapida delle origini dati seguenti:<br /><br /> rdlx<br /><br /> rsds<br /><br /> file di connessione bism<br /><br /> <br /><br /> Se [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] non è visualizzato nei menu di scelta rapida, verificare che la **Funzionalità di integrazione Power View** sia attivata.<br /><br /> Questa funzionalità è disattivata per impostazione predefinita.|  
  
## <a name="see-also"></a>Vedere anche  
 [Attivare le funzionalità di integrazione per Power View e server di report in SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Funzionalità e impostazioni del sito di Reporting Services &#40;modalità SharePoint&#41;](../../2014/reporting-services/reporting-services-site-settings-and-site-features-sharepoint-mode.md)   
 [Attivare la funzionalità Sincronizzazione file server di report in Amministrazione centrale SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md)  
  
  
