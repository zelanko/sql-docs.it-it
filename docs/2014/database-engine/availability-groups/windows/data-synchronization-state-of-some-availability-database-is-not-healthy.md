---
title: Lo stato di sincronizzazione dei dati di alcuni database di disponibilità non è integro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.agdashboard.drp3datasynchealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 89f95d15-33c6-4768-bccd-9dbf8c4f49a9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d128d38a1123e89b45dc3fdcaa0343aa5fd3d5b5
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936867"
---
# <a name="data-synchronization-state-of-some-availability-database-is-not-healthy"></a>Lo stato della sincronizzazione dei dati di alcuni database disponibili non è integro
    
## <a name="introduction"></a>Introduzione  
  
|||  
|-|-|  
|**Nome criterio**|Stato di sincronizzazione dei dati delle repliche di disponibilità|  
|**Problema**|Lo stato di sincronizzazione dei dati di alcuni database di disponibilità non è integro.|  
|**Categoria**|**Avviso**|  
|**Facet**|replica di disponibilità|  
  
## <a name="description"></a>Description  
 Questi criteri consentono di controllare lo stato di sincronizzazione dei dati del database di disponibilità, anche noto come "replica di database". I criteri sono in uno stato non integro se lo stato di sincronizzazione dei dati è NON IN SINCRONIZZAZIONE o lo stato per la replica del database con commit sincrono è NON SINCRONIZZATO.  
  
> [!NOTE]  
>  Per questa versione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], le informazioni sulle possibili cause e le soluzioni sono disponibili in [Lo stato della sincronizzazione dei dati del database di disponibilità non è integro](https://go.microsoft.com/fwlink/p/?LinkId=220863) su Wiki di TechNet.  
  
## <a name="possible-causes"></a>Possibili cause  
 Almeno un database di disponibilità in questa replica di disponibilità si trova in uno stato di sincronizzazione dei dati non integro. Se si tratta di una replica di disponibilità con commit asincrono, tutti i database di disponibilità devono trovarsi nello stato SINCRONIZZAZIONE IN CORSO. Se invece si tratta di una replica di disponibilità con commit sincrono, tutti i database di disponibilità devono trovarsi nello stato SINCRONIZZATO. Il problema può essere causato da uno dei motivi seguenti:  
  
-   La replica di disponibilità potrebbe essere disconnessa.  
  
-   Lo spostamento di dati potrebbe essere sospeso.  
  
-   Il database potrebbe non essere accessibile.  
  
-   Potrebbe verificarsi un problema di ritardo temporaneo dovuto alla latenza di rete o al carico nella replica primaria o secondaria.  
  
## <a name="possible-solution"></a>Possibile soluzione  
 Risolvere tutti i problemi di connessione o di spostamento di dati sospesi. Verificare gli eventi relativi a questo problema utilizzando SQL Server Management Studio e trovare l'errore di database. Seguire le procedure per la risoluzione dei problemi per l'errore specifico.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Usare il Dashboard Always On &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
