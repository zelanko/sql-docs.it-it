---
title: La replica di disponibilità è disconnessa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 51004cf91b039ccdd83eda91425b3aea0764d237
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937071"
---
# <a name="availability-replica-is-disconnected"></a>La replica di disponibilità è disconnessa
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criterio**|Stato di connessione della replica di disponibilità|  
|**Problema**|La replica di disponibilità è disconnessa.|  
|**Categoria**|**Critico**|  
|**Facet**|replica di disponibilità|  
  
## <a name="description"></a>Description  
 Tramite questi criteri è possibile controllare lo stato di connessione tra le repliche di disponibilità. I criteri sono in uno stato non integro quando lo stato di connessione della replica di disponibilità è DISCONNESSO. Altrimenti, sono in uno stato integro.  
  
> [!NOTE]  
>   Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili nella pagina relativa alla situazione in cui la [replica di disponibilità è disconnessa](https://go.microsoft.com/fwlink/p/?LinkId=220857) su Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 La replica secondaria non è connessa alla replica primaria. Lo stato è DISCONNESSO. Il problema può essere causato da uno dei motivi seguenti:  
  
-   La porta di connessione potrebbe essere in conflitto con un'altra applicazione.  
  
-   Il tipo o l'algoritmo di crittografia non è corrispondente.  
  
-   L'endpoint di connessione è stato eliminato o non è stato avviato.  
  
-   Il trasporto è disconnesso.  
  
## <a name="possible-solutions"></a>Possibili soluzioni  
 Di seguito sono riportate le possibili soluzioni a questo problema:  
  
-   Verificare la configurazione dell'endpoint del mirroring di database per le istanze della replica primaria e secondaria e aggiornare la configurazione non corrispondente.  
  
-   Controllare se la porta è in conflitto, e in questo caso, modificare il numero di porta.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
