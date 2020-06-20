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
ms.openlocfilehash: 44bf9789e98c29f89644a6cd1a191d4b8fa7eef7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062405"
---
# <a name="microsoft-sharepoint-2007-is-installed-upgrade-advisor"></a>Microsoft SharePoint è installato (Upgrade Advisor)
  È stata rilevata una versione non supportata di un prodotto o una tecnologia SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità SharePoint di.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrizione  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]non viene eseguito l'aggiornamento o l'installazione in SharePoint 2007. L'aggiornamento viene bloccato.  
  
## <a name="corrective-action"></a>Azione correttiva  
 Per procedere con l'aggiornamento, è necessario disinstallare SharePoint 2007 o passare da SharePoint 2007 a un prodotto SharePoint 2010. Dopo aver aggiornato l'installazione di SharePoint, eseguire nuovamente Upgrade Advisor per confermare che non sono presenti altri errori di aggiornamento.  
  
 Non è possibile eseguire direttamente l'aggiornamento da SharePoint 2007 a SharePoint 2013. Tuttavia, è possibile eseguire la connessione a un database "doppio hop" per eseguire l'aggiornamento da Office SharePoint Server 2007 a SharePoint Server 2010 e quindi da SharePoint Server 2010 a SharePoint Server 2013.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento Reporting Services &#40;preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
