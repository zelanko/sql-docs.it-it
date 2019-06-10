---
title: Il database di disponibilità è sospeso per un gruppo di disponibilità
description: Informazioni su come identificare i possibili motivi per cui un database all'interno di un gruppo di disponibilità Always On può essere sospeso.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.drp1notsuspended.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 6baee70f-848c-4e86-b20d-78875c0f82cb
author: MashaMSFT
ms.author: mathoma
manager: jroth
ms.openlocfilehash: 4760bd036c4946ee8fe0b924043ab6188c009576
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66789415"
---
# <a name="availability-database-is-suspended-for-an-availability-group"></a>Il database di disponibilità è sospeso per un gruppo di disponibilità
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criteri**|Stato di sospensione del database di disponibilità|  
|**Problema**|Database di disponibilità sospeso.|  
|**Category**|**Avviso**|  
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
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
