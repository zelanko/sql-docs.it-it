---
title: Replica di disponibilità non unita in join | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp4joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c1143efc4d5a695dd00766d1f78132f7e69adc46
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62815288"
---
# <a name="availability-replica-is-not-joined"></a>Replica di disponibilità non unita in join
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criterio**|Stato di join della replica di disponibilità|  
|**Problema**|La replica di disponibilità non è unita in join.|  
|**Categoria**|**Avviso**|  
|**Facet**|replica di disponibilità|  
  
## <a name="description"></a>Descrizione  
 Tramite questi criteri viene controllato lo stato del join della replica di disponibilità. Lo stato dei criteri non è integro quando la replica di disponibilità viene aggiunta al gruppo di disponibilità, ma non ne viene creato il join correttamente. Altrimenti, sono in uno stato integro.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili nella pagina relativa alla situazione in cui [la replica di disponibilità non è unita in join](https://go.microsoft.com/fwlink/p/?LinkId=220859) su Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 La replica secondaria non è unita in join al gruppo di disponibilità. Affinché una replica di disponibilità venga correttamente unita in join al gruppo di disponibilità, lo stato del join deve essere Istanza autonoma unita in join (1) o Cluster di failover unito in join (2).  
  
## <a name="possible-solution"></a>Possibile soluzione  
 Utilizzare Transact-SQL, PowerShell o SQL Server Management Studio per creare un join della replica secondaria al gruppo di disponibilità. Per altre informazioni sul join delle repliche secondarie ai gruppi di disponibilità, vedere [Creare un join di una replica secondaria a un gruppo di disponibilità (SQL Server)](https://msdn.microsoft.com/library/ff878473\(en-us,SQL.110\).aspx).  
  
## <a name="see-also"></a>Vedi anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
