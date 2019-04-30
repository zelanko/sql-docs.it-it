---
title: Microsoft SQL Server SharePoint servizio condiviso Reporting Services è installato Side-by-Side (Upgrade Advisor) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 93bbc8ca6c2a67ec2ec224db51c780a38534c098
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267906"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>Il servizio Shared SharePoint di Microsoft SQL Server Reporting Services è installato in modalità affiancata (Upgrade Advisor)
  Preparazione aggiornamento ha rilevato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servizio condiviso di SharePoint viene installato affiancata a una versione precedente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 Preparazione aggiornamento ha rilevato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servizio condiviso SharePoint viene installata affiancata a una versione precedente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che non si basa sull'architettura del servizio SharePoint shared. Poiché nel computer sono installate side-by-side la tecnologia precedente e la nuova tecnologia SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], l'aggiornamento viene bloccato.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Per procedere con l'aggiornamento, è necessario disinstallare una delle installazioni esistenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Dopo aver rimosso una delle installazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], eseguire nuovamente Upgrade Advisor per confermare che non sono presenti altri errori di aggiornamento.  
  
  
