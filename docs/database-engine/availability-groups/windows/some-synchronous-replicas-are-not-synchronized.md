---
title: Alcune repliche sincrone non sono sincronizzate
description: Descrive alcune possibili cause e soluzioni per i casi in cui una replica sincrona non è sincronizzata per un gruppo di disponibilità Always On.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.agp5synchronized.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: e58ed56e-4c30-42e6-a9fc-a8c401620e02
author: cawrites
ms.author: chadam
ms.openlocfilehash: a8e5fc7b3aa708acc3542082ece0d980c938eb34
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583842"
---
# <a name="some-synchronous-replicas-are-not-synchronized"></a>Alcune repliche sincrone non sono sincronizzate
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criteri**|Stato di sincronizzazione dei dati delle repliche sincrone|  
|**Problema**|Alcune repliche sincrone non sono sincronizzate.|  
|**Categoria**|**Warning**|  
|**Facet**|gruppo di disponibilità|  
  
## <a name="description"></a>Descrizione  
 Questi criteri consentono di eseguire il rollup dello stato di sincronizzazione dei dati di tutte le repliche di disponibilità e di verificare tutte le repliche di disponibilità che non sono nello stato di sincronizzazione previsto. I criteri sono in uno stato non integro se una replica asincrona è in uno stato NON IN SINCRONIZZAZIONE e una replica sincrona è in uno stato NON SINCRONIZZATO. Altrimenti, i criteri sono in uno stato integro.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili nella pagina relativa ad [alcune repliche sincrone non sono sincronizzate](https://go.microsoft.com/fwlink/p/?LinkId=220853) su Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 In questo gruppo di disponibilità, almeno una replica sincrona non è attualmente sincronizzata. Lo stato di sincronizzazione della replica può essere SINCRONIZZAZIONE IN CORSO o NON IN SINCRONIZZAZIONE.  
  
## <a name="possible-solution"></a>Possibile soluzione  
 Utilizzare lo stato dei criteri della replica di disponibilità per trovare quella con lo stato di sincronizzazione non corretto e risolvere il problema.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il dashboard Always On &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
