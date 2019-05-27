---
title: Aggiornamento dati PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: ac8358a3-ee71-44c7-8ee6-ac7afe3ebaa4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4ab42604fabaa188a74858038e35a8b90a105df8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071215"
---
# <a name="powerpivot-data-refresh"></a>Aggiornamento dei dati PowerPivot
  Dopo avere creato una cartella di lavoro che contiene dati PowerPivot, è possibile aggiornare periodicamente i dati rieseguendo una query o un comando per ottenere informazioni aggiornate dalle origini utilizzate in origine per creare la cartella di lavoro. Questo processo, denominato `data refresh`, consente di aggiornare i dati su richiesta in [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] o come operazione pianificata eseguita come processo di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in un server applicazioni in una farm di SharePoint. Per altre informazioni, vedere:  
  
-   [Aggiornamento dati PowerPivot con SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md)  
  
-   [Configurare PowerPivot Account di aggiornamento dati automatico &#40;PowerPivot per SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)  
  
-   [Configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
-   [Pianificare un aggiornamento di dati &#40;PowerPivot per SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)  
  
-   [Visualizzare la cronologia aggiornamento dati &#40;PowerPivot per SharePoint&#41;](view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
> [!NOTE]
>  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e SharePoint Server 2013 Excel Services viene utilizzata un'architettura diversa per i modelli di dati PowerPivot. Nell'architettura supportata da SharePoint 2013 viene utilizzato Excel Services come componente principale per caricare modelli di dati PowerPivot. L'architettura di aggiornamento dati utilizzata in precedenza era basata su un server con in esecuzione il servizio di sistema di PowerPivot e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità SharePoint per caricare i modelli di dati. Per ulteriori informazioni, vedere quanto segue:  
> 
>  -   [Aggiornamento dati PowerPivot con SharePoint 2013](power-pivot-data-refresh-with-sharepoint-2013.md)  
> -   [Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato &#40;SharePoint 2013&#41;](../instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
