---
title: Funzionalità di raccolta siti di Reporting Services | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e13654a38738c84095cc284a24fb723aa2b05327
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580493"
---
# <a name="reporting-services-site-collection-features"></a>Funzionalità di raccolta siti di Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

La modalità SharePoint di Reporting Services offre tre funzionalità di raccolta siti SharePoint. Le funzionalità supportano l'ambiente generale di report della modalità SharePoint di Reporting Services, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], una funzionalità del componente aggiuntivo SQL Server 2016 Reporting Services, e le operazioni di gestione per Reporting Services in Amministrazione centrale SharePoint.

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.
  
## <a name="site-collection-features"></a>Funzionalità di raccolta siti

 Nella tabella seguente vengono descritte le funzionalità di raccolta siti di Reporting Services.  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|**Funzionalità Amministrazione centrale del server di report**|Consente di abilitare le funzionalità per gestire l'integrazione con un server di report di Reporting Services. Questa funzionalità viene installata e utilizzata solo nella raccolta siti di Amministrazione centrale SharePoint.<br /><br /> La funzionalità di integrazione del server di report viene attivata automaticamente nella raccolta siti di Amministrazione centrale SharePoint dopo aver installato il componente aggiuntivo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] per prodotti SharePoint. In alcune situazioni è necessario attivare la funzionalità manualmente. Per attivare la funzionalità del server di report usare le pagine di Reporting Services nella pagina Impostazioni sito di Amministrazione centrale SharePoint.<br /><br /> Con la versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Reporting Services e successive del componente aggiuntivo per prodotti SharePoint, la funzionalità di integrazione del server di report viene attivata per tutte le raccolte siti esistenti al momento dell'installazione del componente aggiuntivo. La funzionalità risulta inoltre attivata automaticamente per le nuove raccolte siti.|  
|**Funzionalità di integrazione con il server di report**|Consente di generare report avanzati tramite [!INCLUDE[msCoName](../../includes/msconame-md.md)] Reporting Services<br /><br /> Questa funzionalità è attiva per impostazione predefinita.|  
|**Funzionalità di integrazione di Power View**|Consente l'esplorazione dei dati interattiva e la presentazione visiva su cartelle di lavoro di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e database tabulari di Analysis Services.<br /><br /> L'accesso alla funzionalità può essere eseguito dai menu di scelta rapida delle origini dati seguenti:<br /><br /> **rdlx**<br /><br /> **rsds**<br /><br /> File di connessione con estensione**bism**<br /><br /> <br /><br /> Se [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] non è visualizzato nei menu di scelta rapida, verificare che la **Funzionalità di integrazione Power View** sia attivata.<br /><br /> Questa funzionalità è disattivata per impostazione predefinita.|  

## <a name="next-steps"></a>Passaggi successivi

[Attivare le funzionalità di integrazione per Power View e server di report in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Funzionalità e impostazioni del sito di Reporting Services &#40;modalità SharePoint&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[Attivare la funzionalità Sincronizzazione file server di report in Amministrazione centrale SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
