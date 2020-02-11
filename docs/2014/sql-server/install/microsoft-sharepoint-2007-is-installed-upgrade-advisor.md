---
title: Microsoft SharePoint 2007 è installato (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6f1da295-d9b7-4948-99d3-ebd3587337c6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 84672ddf6a9b2912f3d53eef8d40727369376ba5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952095"
---
# <a name="microsoft-sharepoint-2007-is-installed-upgrade-advisor"></a>Microsoft SharePoint è installato (Upgrade Advisor)
  È stata rilevata una versione non supportata di un prodotto o una tecnologia SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità SharePoint di.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non viene eseguito l'aggiornamento o l'installazione in SharePoint 2007. L'aggiornamento viene bloccato.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Per procedere con l'aggiornamento, è necessario disinstallare SharePoint 2007 o passare da SharePoint 2007 a un prodotto SharePoint 2010. Dopo aver aggiornato l'installazione di SharePoint, eseguire nuovamente Upgrade Advisor per confermare che non sono presenti altri errori di aggiornamento.  
  
 Non è possibile eseguire direttamente l'aggiornamento da SharePoint 2007 a SharePoint 2013. Tuttavia, è possibile eseguire la connessione a un database "doppio hop" per eseguire l'aggiornamento da Office SharePoint Server 2007 a SharePoint Server 2010 e quindi da SharePoint Server 2010 a SharePoint Server 2013.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento Reporting Services &#40;preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
