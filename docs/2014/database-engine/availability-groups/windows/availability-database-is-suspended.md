---
title: Il database di disponibilità è sospeso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.drp1notsuspended.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 21d788db62fe39b86eb801c028450c16cf845845
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62815766"
---
# <a name="availability-database-is-suspended"></a>Il database di disponibilità è sospeso
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criterio**|Stato di sospensione del database di disponibilità|  
|**Problema**|Database di disponibilità sospeso.|  
|**Categoria**|**Avviso**|  
|**Facet**|Database di disponibilità|  
  
## <a name="description"></a>Descrizione  
 Questi criteri consentono di controllare lo stato di spostamento dei dati del database secondario, anche noto come "replica di database secondaria". I criteri sono in uno stato non integro se questo spostamento è sospeso. Altrimenti, sono in uno stato integro.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili in [Il database di disponibilità è sospeso](https://go.microsoft.com/fwlink/p/?LinkId=220860) in TechNet Wiki.  
  
## <a name="possible-causes"></a>Possibili cause  
 È probabile che la sincronizzazione dei dati in questo database di disponibilità sia stata sospesa per i motivi seguenti:  
  
-   È probabile che la sincronizzazione dei dati sia sospesa a causa di un errore.  
  
-   È probabile che l'amministratore del database abbia sospeso la sincronizzazione dei dati per scopi di manutenzione.  
  
## <a name="possible-solution"></a>Possibile soluzione  
 Riprendere la sincronizzazione dei dati. Se il problema persistente, controllare il gruppo di disponibilità nel Registro eventi, quindi diagnosticare il motivo per il quale lo spostamento dei dati è stato sospeso.  
  
## <a name="see-also"></a>Vedi anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
