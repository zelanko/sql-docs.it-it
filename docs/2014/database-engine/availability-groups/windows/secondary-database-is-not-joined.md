---
title: Un database secondario non è associato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.drp2joined.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 10817e5e-75fa-42dd-baa2-359bea3ad051
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 59c8c7e13faf5c3ed9874779c2f9b38faaf33791
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358943"
---
# <a name="secondary-database-is-not-joined"></a>Un database secondario non è associato
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criteri**|Stato di join del database di disponibilità|  
|**Problema**|Il database secondario non è unito in join.|  
|**Categoria**|**Avviso**|  
|**Facet**|Database di disponibilità|  
  
## <a name="description"></a>Descrizione  
 Questi criteri consentono di controllare lo stato di join del database secondario, anche noto come "replica di database secondaria". I criteri sono in uno stato non integro quando la replica del set di dati non è unita in join. Altrimenti, sono in uno stato integro.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]le informazioni sulle cause e sulle soluzioni possibili sono disponibili in [Secondary database is not joined](https://go.microsoft.com/fwlink/p/?LinkId=220862) (Database secondario non unito in join) in TechNet Wiki.  
  
## <a name="possible-causes"></a>Possibili cause  
 Questo database secondario non è unito in join al gruppo di disponibilità. La configurazione di questo database secondario è incompleta.  
  
## <a name="possible-solution"></a>Possibile soluzione  
 Utilizzare Transact-SQL, PowerShell o SQL Server Management Studio per creare un join della replica secondaria al gruppo di disponibilità. Per altre informazioni sul join delle repliche secondarie ai gruppi di disponibilità, vedere [Creare un join di una replica secondaria a un gruppo di disponibilità (SQL Server)](https://msdn.microsoft.com/en-sg/library/ff878473\(en-us,SQL.110\).aspx).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
