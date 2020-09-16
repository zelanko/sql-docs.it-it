---
description: Ospitare un database del server di report in un cluster di failover di SQL Server
title: Ospitare un database del server di report in un cluster di failover di SQL Server | Microsoft Docs
ms.date: 03/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 7bd5f019-2857-452f-a023-cc3b9e93aec4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1bceb380b1c21f717ba6e20fd6a41c78cc393dba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492670"
---
# <a name="host-a-report-server-database-in-a-sql-server-failover-cluster"></a>Ospitare un database del server di report in un cluster di failover di SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre supporto per il clustering di failover, per consentire l'utilizzo di più dischi per una o più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il clustering di failover è supportato solo per il database del server di report e non è possibile eseguire il servizio Windows ReportServer o il servizio Web come parte di un cluster di failover.  
  
 Per ospitare un database del server di report in un cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario che il cluster sia già installato e configurato. È quindi possibile selezionare il cluster di failover come nome del server quando si crea il database del server di report nella pagina Impostazione database dello strumento Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Sebbene il servizio Windows ReportServer non possa essere eseguito come parte di un cluster di failover, è possibile installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un computer in cui è installato un cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il server di report viene eseguito indipendentemente dal cluster di failover. Se si installa un server di report in un computer che fa parte di un'istanza di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , non è necessario utilizzare il cluster di failover per il database del server di report, ma, per ospitare il database, è possibile utilizzare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diversa.  
  
## <a name="see-also"></a>Vedere anche  
 [Database del server di report &#40;modalità nativa SSRS&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Creare un database del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
  
