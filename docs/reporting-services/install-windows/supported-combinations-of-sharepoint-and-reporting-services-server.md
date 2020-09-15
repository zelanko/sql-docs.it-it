---
title: Combinazioni supportate di SharePoint e server Reporting Services | Microsoft Docs
description: Un server di report SQL Server Reporting Services installato in modalità SharePoint richiede una versione di SharePoint e il componente aggiuntivo SQL Server Reporting Services (rsSharePoint.msi) per prodotti SharePoint, da installare nei server SharePoint.
ms.date: 12/04/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.custom: seo-lt-2019, seo-mmd-2019
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: d5499ace3a3a0b0f1ba98b8ae1859b51d9867eeb
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2020
ms.locfileid: "87397090"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server"></a>Combinazioni supportate di SharePoint e server Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Un server di report SQL Server Reporting Services installato in modalità SharePoint richiede una versione di SharePoint e il componente aggiuntivo SQL Server Reporting Services (rsSharePoint.msi) per prodotti SharePoint, da installare nei server SharePoint. In questo argomento vengono riepilogate le combinazioni supportate.

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Combinazioni supportate di SharePoint e componenti Reporting Services

 Nella tabella seguente sono riepilogate le combinazioni supportate di server di report, componente aggiuntivo Reporting Services per prodotti SharePoint e prodotti SharePoint. Le combinazioni non elencate nella tabella seguente non sono supportate.

### <a name="supported-combinations"></a>Combinazioni supportate

|Number|Server di report|Componente aggiuntivo|Versione di SharePoint|
|-|-------------------|-------------|------------------------|
|1|SQL Server 2016|SQL Server 2016|SharePoint 2016|
|2|SQL Server 2016|SQL Server 2016|SharePoint 2013|
|3|SQL Server 2014|SQL Server 2014|SharePoint 2013|
|4|SQL Server 2014|SQL Server 2014|SharePoint 2010|
|5|SQL Server 2012 SP4|SQL Server 2014 e SQL Server 2012 SP4|SharePoint 2013|
|6|SQL Server 2012 SP3|SQL Server 2014 e SQL Server 2012 SP3|SharePoint 2013|
|7|SQL Server 2012 SP2|SQL Server 2014 e SQL Server 2012 SP2|SharePoint 2013|
|8|SQL Server 2012 SP1|SQL Server 2014 e SQL Server 2012 SP1|SharePoint 2013|
|9|SQL Server 2012 e SQL Server 2012 SP1*|SQL Server 2014|SharePoint 2010|
|10|SQL Server 2012|SQL Server 2012|SharePoint 2010|
|11|SQL Server 2008 R2|SQL Server 2014|SharePoint 2010|
|12|SQL Server 2008 R2|SQL Server 2012 e SQL Server 2012 SP1 o versione successiva|SharePoint 2010|
|13|SQL Server 2008 R2|SQL Server 2008 R2|SharePoint 2010|
|14|SQL Server 2008 R2|SQL Server 2008 SP2|SharePoint 2007|
|15|SQL Server 2008 SP2|SQL Server 2008 R2|SharePoint 2010|
|16|SQL Server 2008 SP2|SQL Server 2008 e SQL Server 2008 SP2|SharePoint 2007|

 *Eccezione: l'integrazione di Power View non è supportata.

 Per i collegamenti alle pagine di download del componente aggiuntivo, vedere [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  

 **Altre considerazioni:**

- Assicurarsi di aggiornare tutti i server SharePoint all'interno della farm. Sono inclusi i server front-end Web e i server applicazioni.

- Per il supporto di SharePoint 2016, inclusa l'integrazione di Power View, sono necessari il server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e la versione del componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] di SQL Server 2016 o versione successiva.

- Per il supporto di SharePoint 2013, inclusa l'integrazione di Power View, sono necessari il server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e la versione del componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] di SQL Server 2012 SP1 o versione successiva.

- Power View è stato introdotto in SQL Server 2012. L'integrazione di Power View con SharePoint 2010 richiede pertanto la versione SQL Server 2012 o successiva del componente aggiuntivo.

- Il componente aggiuntivo di SQL Server 2008 R2 non è supportato dai server di report SQL Server 2012 o versione successiva. Tramite il programma di installazione essenziale di SharePoint 2010 viene installato automaticamente il componente aggiuntivo di SQL Server 2008 R2. È necessario disinstallarlo prima di installare le versioni più recenti del componente aggiuntivo. L'aggiornamento sul posto del componente aggiuntivo non è supportato.

- **Aggiornamento:** non è possibile eseguire l'aggiornamento sul posto di SharePoint 2010 con il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a SharePoint 2013. SharePoint 2013 richiede la versione SQL Server 2012 SP1 o successiva del componente aggiuntivo e del server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per altre informazioni sull'aggiornamento, vedere [Eseguire l'aggiornamento e la migrazione di Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).

## <a name="next-steps"></a>Passaggi successivi

 [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-components-of-sql-server-2017.md)   
 [Requisiti hardware e software per l'installazione di SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
