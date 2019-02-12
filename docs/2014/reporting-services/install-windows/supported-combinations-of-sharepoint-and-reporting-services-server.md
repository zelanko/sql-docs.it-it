---
title: Combinazioni supportate di SharePoint e Server Reporting Services e componente aggiuntivo (SQL Server 2014) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: b4e1a516f10c15b8e84d80ff91de1aa9d66d8e1b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034102"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server-and-add-in-sql-server-2014"></a>Combinazioni supportate di SharePoint, server Reporting Services e componente aggiuntivo (SQL Server 2014)
  È possibile installare i server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint e integrarli con una distribuzione di SharePoint. Non tutte le funzionalità sono supportate in tutte le combinazioni di server di report, componente aggiuntivo di Reporting Services per SharePoint e prodotti SharePoint. In questo argomento vengono riepilogate le combinazioni supportate. In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] l'integrazione è il risultato della combinazione degli elementi seguenti:  
  
-   Una versione del server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurata per la modalità SharePoint.  
  
-   Un prodotto SharePoint  
  
-   Il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per prodotti SharePoint, da installare sui server SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 &#124; SharePoint 2010 &#124; SharePoint 2007|  
  
## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Combinazioni supportate di componenti SharePoint e Reporting Services  
 Nella tabella seguente sono riepilogate le combinazioni supportate di server di report, componente aggiuntivo Reporting Services per prodotti SharePoint e prodotti SharePoint. Le combinazioni non elencate nella tabella seguente non sono supportate.  
  
### <a name="supported-combinations"></a>Combinazioni supportate  
  
||Server di report|Componente aggiuntivo|Versione di SharePoint|Supportato|  
|-|-------------------|-------------|------------------------|---------------|  
|1|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2013|Yes|  
|2|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Yes|  
|3|[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2013|Yes|  
|4|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Yes<br /><br /> Exception: Integrazione di Power view non è supportato.|  
|5|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|SharePoint 2010|Yes|  
|6|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SharePoint 2010|Yes|  
|7|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)]|SharePoint 2010|Yes|  
|8|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|SharePoint 2010|Yes|  
|9|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|Yes|  
|10|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] R2|SharePoint 2010|Yes|  
|11|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2|SharePoint 2007|Yes|  
  
 Per ulteriori informazioni sul [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] le funzionalità e le modalità server di report, vedere [Server di Report di Reporting Services](../reporting-services-report-server.md).  
  
 **Note aggiuntive:**  
  
-   Per il supporto di SharePoint 2013, inclusa l'integrazione di Power View, sono necessari il server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e la versione del componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] di SQL Server 2012 SP1 o versione successiva.  
  
-   Power View è stato introdotto in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Pertanto, per l'integrazione di Power View con SharePoint 2010 è necessario [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o le versioni successive del componente aggiuntivo.  
  
-   Il componente aggiuntivo di SQL Server 2008 R2 non è supportato dai server di report SQL Server 2012 o versione successiva. Tramite il programma di installazione essenziale di SharePoint 2010 viene installato automaticamente il componente aggiuntivo di SQL Server 2008 R2. È necessario disinstallarlo prima di installare le versioni più recenti del componente aggiuntivo. L'aggiornamento sul posto del componente aggiuntivo non è supportato.  
  
-   **Eseguire l'aggiornamento:** SharePoint 2010 con il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aggiuntivo installato, non è possibile aggiornare sul posto a SharePoint 2013. Per SharePoint 2013 è necessario [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] o versioni successive del componente aggiuntivo e del server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni sull'aggiornamento, vedere [Eseguire l'aggiornamento e la migrazione di Reporting Services](upgrade-and-migrate-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Eseguire l'aggiornamento e la migrazione di Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
  
