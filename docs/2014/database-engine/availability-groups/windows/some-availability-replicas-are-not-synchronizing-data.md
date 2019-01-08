---
title: Alcune repliche di disponibilità non stanno sincronizzando i dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.agp4synchronizing.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 3db6a569-e942-4321-a0dd-c4ab002087c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0fb7d422687d0bc956937b30bae261b28edb3931
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53351486"
---
# <a name="some-availability-replicas-are-not-synchronizing-data"></a>Alcune repliche di disponibilità non stanno sincronizzando i dati.
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criteri**|Stato di sincronizzazione dei dati delle repliche di disponibilità|  
|**Problema**|Alcune repliche di disponibilità non prevedono la sincronizzazione dei dati.|  
|**Categoria**|**Avviso**|  
|**Facet**|gruppo di disponibilità|  
  
## <a name="description"></a>Descrizione  
 Questi criteri consentono di eseguire il rollup dello stato di sincronizzazione dei dati di tutte le repliche di disponibilità nel gruppo di disponibilità e di verificare se la sincronizzazione di una qualsiasi replica di disponibilità non funzioni. I criteri si trovano in uno stato non integro se uno degli stati di sincronizzazione dei dati della replica di disponibilità è NON IN SINCRONIZZAZIONE.  
  
 Questi criteri sono in uno stato integro se nessuno degli stati di sincronizzazione dei dati della replica di disponibilità è NON IN SINCRONIZZAZIONE.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili in [Alcune repliche di disponibilità non stanno sincronizzando i dati](https://go.microsoft.com/fwlink/p/?LinkId=220852) nella Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 In questo gruppo di disponibilità, almeno una replica secondaria non si trova nello stato di sincronizzazione NON IN SINCRONIZZAZIONE e non riceve dati dalla replica primaria.  
  
## <a name="possible-solution"></a>Possibile soluzione  
 Utilizzare lo stato dei criteri della replica di disponibilità per trovare la replica di disponibilità con uno stato NON IN SINCRONIZZAZIONE e risolvere il relativo problema.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
