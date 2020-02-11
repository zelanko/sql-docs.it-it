---
title: Attivare la funzionalità Sincronizzazione file del server di report in Amministrazione centrale SharePoint | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/06/2017
ms.openlocfilehash: 762cf7e67a9983c345b58d2afd1c47da93306bd0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67413140"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint-central-administration"></a>Attivare la funzionalità Sincronizzazione file server di report in Amministrazione centrale SharePoint

La funzionalità Sincronizzazione file server di report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] prevede l'utilizzo di gestori di eventi di SharePoint per sincronizzare il catalogo del server di report con gli elementi nelle raccolte documenti. Questa funzionalità è utile quando gli utenti caricano di frequente elementi di report pubblicati direttamente nelle raccolte documenti di SharePoint. Se la funzionalità di sincronizzazione file non è attivata, il contenuto verrà comunque sincronizzato ma non con la stessa frequenza.  
  
La funzionalità di sincronizzazione file può essere attivata in Amministrazione sito di SharePoint dopo aver installato il componente aggiuntivo [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] per prodotti SharePoint.  
  
Tale caratteristica può essere attivata e disattivata manualmente per il sito ma non a livello di raccolta siti.  
  
## <a name="prerequisites"></a>Prerequisites  
 È necessario installare il componente aggiuntivo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] per SharePoint. Se il componente aggiuntivo non è installato, la funzionalità di sincronizzazione file non sarà visibile nell'elenco delle funzionalità del sito.  
  
 Per verificare l'installazione, visualizzare l'elenco delle applicazioni installate nel [!INCLUDE[msCoName](../includes/msconame-md.md)] Pannello di controllo **di**Windows. Se il componente aggiuntivo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] è installato, seguire le indicazioni fornite in questo argomento per attivare la caratteristica di sincronizzazione file del server di report.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>Per attivare o disattivare la funzionalità di sincronizzazione file di Reporting Services in un sito  
  
1.  Dalla pagina principale del sito, fare clic sul menu **Azioni sito** e fare clic su **Impostazioni sito**.  
  
2.  In **Azioni sito**fare clic su **Gestisci caratteristiche sito**.  
  
3.  Trovare **Sincronizzazione file server di report** nell'elenco.  
  
4.  Fare clic su **Attiva**.  
  
> [!NOTE]  
>  Per disattivare la funzionalità di sincronizzazione file del server di report, è possibile seguire la stessa procedura facendo però clic su **Disattiva**.  
  
## <a name="see-also"></a>Vedere anche  
 [Risolvere i problemi relativi alle parti del report &#40;Generatore report e SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [Attivare le funzionalità di integrazione per Power View e server di report in SharePoint](activate-the-report-server-and-power-view-integration-features-in-sharepoint.md)   
 [Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
