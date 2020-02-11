---
title: Microsoft SQL Server Reporting Services servizio SharePoint Shared è installato side-by-Side (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 529e07dc7beed8dc37741f6c9dab0b0b080d4898
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952687"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>Il servizio Shared SharePoint di Microsoft SQL Server Reporting Services è installato in modalità affiancata (Upgrade Advisor)
  È stato rilevato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che il servizio SharePoint Shared è installato side-by-side con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]una versione precedente di.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità SharePoint di.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 È stato rilevato [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che il servizio condiviso SharePoint è installato side-by-side con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] una versione precedente di che non si basa sull'architettura del servizio SharePoint Shared. Poiché nel computer sono installate side-by-side la tecnologia precedente e la nuova tecnologia SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], l'aggiornamento viene bloccato.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Per procedere con l'aggiornamento, è necessario disinstallare una delle installazioni esistenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Dopo aver rimosso una delle installazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], eseguire nuovamente Upgrade Advisor per confermare che non sono presenti altri errori di aggiornamento.  
  
  
