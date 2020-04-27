---
title: Alcune repliche di disponibilità non presentano un ruolo integro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp6allroleshealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 7ec5b337-7201-4a66-a541-7560f8b18784
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 50518e78585b7e56f62411edc539d0f9ac3db9e9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62788185"
---
# <a name="some-availability-replicas-do-not-have-a-healthy-role"></a>Alcune repliche di disponibilità non dispongono di un ruolo integro
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criteri**|Stato del ruolo delle repliche di disponibilità|  
|**Problema**|Alcune repliche di disponibilità non presentano un ruolo integro.|  
|**Categoria**|**Warning**|  
|**Facet**|gruppo di disponibilità|  
  
## <a name="description"></a>Descrizione  
 Questi criteri consentono di eseguire il rollup dello stato di connessione di tutte le repliche di disponibilità e di verificare l'eventuale esistenza di repliche di disponibilità che non presentano un ruolo integro. I criteri sono in uno stato non integro quando una replica di disponibilità non è né primaria né secondaria. Altrimenti, sono in uno stato integro.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili nella pagina relativa ad [alcune repliche di disponibilità che non presentano un ruolo integro](https://go.microsoft.com/fwlink/p/?LinkId=220854) su Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 Nel gruppo di disponibilità è presente almeno una replica di disponibilità il cui ruolo attuale non è primario né secondario.  
  
## <a name="possible-solution"></a>Possibile soluzione  
 Utilizzare lo stato dei criteri della replica di disponibilità per trovare quella il cui ruolo non è primario o secondario e risolvere il problema.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
