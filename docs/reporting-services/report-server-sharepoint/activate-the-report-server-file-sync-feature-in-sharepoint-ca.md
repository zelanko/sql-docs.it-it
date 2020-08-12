---
title: Attivare la funzionalità Sincronizzazione file server di report in SharePoint | Microsoft Docs
description: La funzionalità Sincronizzazione file server di report di Reporting Services prevede l'utilizzo di gestori di eventi di SharePoint per sincronizzare il catalogo del server di report con gli elementi nelle raccolte documenti.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: f5a0b7b6e50e07573c57882339e5fc3c7dd3cb39
ms.sourcegitcommit: 66a0672e47415dbd5cfd8d19075102c8c3973e70
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83767406"
---
# <a name="activate-the-report-server-file-sync-feature-in-sharepoint"></a>Attivare la funzionalità Sincronizzazione file server di report in SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

La funzionalità Sincronizzazione file server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] prevede l'utilizzo di gestori di eventi di SharePoint per sincronizzare il catalogo del server di report con gli elementi nelle raccolte documenti. Questa funzionalità è utile quando gli utenti caricano di frequente elementi di report pubblicati direttamente nelle raccolte documenti di SharePoint. Se la funzionalità di sincronizzazione file non è attivata, il contenuto viene comunque sincronizzato, ma meno frequentemente.

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.
  
 La funzionalità di sincronizzazione file può essere attivata in Amministrazione sito di SharePoint dopo aver installato il componente aggiuntivo [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] per prodotti SharePoint.  
  
 Tale caratteristica può essere attivata e disattivata manualmente per il sito ma non a livello di raccolta siti.  
  
## <a name="prerequisites"></a>Prerequisiti

 È necessario installare il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint. Se il componente aggiuntivo per SharePoint non è installato, la caratteristica di sincronizzazione file non verrà visualizzata nell'elenco delle caratteristiche.  
  
 Per verificare l'installazione, visualizzare l'elenco delle applicazioni installate nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] Pannello di controllo **di**Windows. Se il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è installato, seguire le indicazioni fornite in questo argomento per attivare la caratteristica di sincronizzazione file del server di report.  
  
### <a name="to-activate-or-deactivate-the-reporting-services-file-sync-feature-on-a-site"></a>Per attivare o disattivare la funzionalità di sincronizzazione file di Reporting Services in un sito
  
1.  Nella pagina principale del sito scegliere **Impostazioni sito** dal menu **Azioni sito**.  
  
2.  In **Azioni sito** fare clic su **Gestisci caratteristiche sito**.  
  
3.  Trovare **Sincronizzazione file server di report** nell'elenco.  
  
4.  Fare clic su **Attiva**.  

> [!NOTE]
> Per disattivare la funzionalità di sincronizzazione file del server di report, è possibile seguire la stessa procedura facendo però clic su **Disattiva**.

## <a name="see-also"></a>Vedere anche

 [Risoluzione dei problemi relativi alle parti del report (Generatore report e SSRS)](https://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [Attivare le funzionalità di integrazione per Power View e server di report in SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
 [Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Installare o disinstallare il componente aggiuntivo Reporting Services per SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
