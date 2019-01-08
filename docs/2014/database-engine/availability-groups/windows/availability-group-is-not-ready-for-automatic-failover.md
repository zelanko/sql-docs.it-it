---
title: Il gruppo di disponibilità non è pronto per il failover automatico | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp3autofailover.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 28261014-342c-442a-bd89-6d04b8d4e8b7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9a7bdca770bccaac50da1ac6a7688eabd335e20
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353749"
---
# <a name="availability-group-is-not-ready-for-automatic-failover"></a>Il gruppo di disponibilità non è pronto per il failover automatico
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criteri**|Conformità del gruppo di disponibilità al failover automatico|  
|**Problema**|Il gruppo di disponibilità non è pronto per il failover automatico.|  
|**Categoria**|**Critico**|  
|**Facet**|gruppo di disponibilità|  
  
## <a name="description"></a>Descrizione  
 Con questi criteri è possibile verificare che nel gruppo di disponibilità sia disponibile almeno una replica secondaria pronta per il failover. I criteri si trovano in uno stato non integro e viene generato un avviso quando il failover della replica primaria è automatico, ma nessuna delle repliche secondarie nel gruppo di disponibilità è pronta per il failover.  
  
 I criteri sono in uno stato integro quando almeno una replica secondaria è pronta per il failover automatico.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili nella pagina relativa alla situazione in cui il [gruppo di disponibilità non è pronto per il failover automatico](https://go.microsoft.com/fwlink/p/?LinkId=220851) su Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 Il gruppo di disponibilità non è pronto per il failover automatico. La replica primaria viene configurata per il failover automatico; tuttavia, la replica secondaria non è pronta per il failover automatico. La replica secondaria configurata per il failover automatico potrebbe non essere disponibile o il relativo stato della sincronizzazione dei dati è attualmente NON SINCRONIZZATO.  
  
## <a name="possible-solutions"></a>Possibili soluzioni  
 Di seguito sono riportate le possibili soluzioni a questo problema:  
  
-   Verificare che almeno una replica secondaria venga configurata come failover automatico. Se non è disponibile alcuna replica secondaria configurata come failover automatico, aggiornare la configurazione di una replica secondaria affinché rappresenti la destinazione del failover automatico con commit sincrono.  
  
-   Utilizzare i criteri per verificare che i dati siano in uno stato di sincronizzazione e che la destinazione del failover automatico sia SINCRONIZZATO, quindi risolvere il problema della replica di disponibilità.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
