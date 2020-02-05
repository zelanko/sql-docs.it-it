---
title: La replica di disponibilità non è unita in join a un gruppo di disponibilità
description: Informazioni su come identificare i possibili motivi per cui una replica di disponibilità non è unita in join a un gruppo di disponibilità Always On.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp4joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 9c0d10b1-9e12-430c-83b9-ca2bd0a3afc4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: da14149b9518a14fa4b7a50072ba35c0b8dcefe2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "67991374"
---
# <a name="availability-replica-is-not-joined-to-an-always-on-availability-group"></a>La replica di disponibilità non è unita in join a un gruppo di disponibilità Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criteri**|Stato di join della replica di disponibilità|  
|**Problema**|La replica di disponibilità non è unita in join.|  
|**Categoria**|**Warning**|  
|**Facet**|replica di disponibilità|  
  
## <a name="description"></a>Descrizione  
 Tramite questi criteri viene controllato lo stato del join della replica di disponibilità. Lo stato dei criteri non è integro quando la replica di disponibilità viene aggiunta al gruppo di disponibilità, ma non ne viene creato il join correttamente. Altrimenti, sono in uno stato integro.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili nella pagina relativa alla situazione in cui [la replica di disponibilità non è unita in join](https://go.microsoft.com/fwlink/p/?LinkId=220859) su Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 La replica secondaria non è unita in join al gruppo di disponibilità. Affinché una replica di disponibilità venga correttamente unita in join al gruppo di disponibilità, lo stato del join deve essere Istanza autonoma unita in join (1) o Cluster di failover unito in join (2).  
  
## <a name="possible-solution"></a>Possibile soluzione  
 Utilizzare Transact-SQL, PowerShell o SQL Server Management Studio per creare un join della replica secondaria al gruppo di disponibilità. Per altre informazioni sul join delle repliche secondarie ai gruppi di disponibilità, vedere [Creare un join di una replica secondaria a un gruppo di disponibilità (SQL Server)](https://msdn.microsoft.com/library/ff878473\(SQL.110\).aspx).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il dashboard Always On &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
