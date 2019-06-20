---
title: MSSQLSERVER_41030 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41030 (Database Engine error)
ms.assetid: c85341ae-0fbf-42ae-9275-4cfe678238f0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 015a01f849bb00dd0db4c2f060447d63a2f96bc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914073"
---
# <a name="mssqlserver41030"></a>MSSQLSERVER_41030
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|41030|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|OPEN_CLUSTER_SUB_KEY|  
|Testo del messaggio|Impossibile aprire la sottochiave del Registro di sistema WSFC (Windows Server Failover Clustering) '%.*ls', codice di errore %d.  La chiave padre è la chiave radice cluster.  È possibile che il servizio WSFC non sia in esecuzione o non sia accessibile nello stato corrente o che gli argomenti specificati non siano validi. Se il gruppo di disponibilità corrispondente è stato eliminato, l'errore è previsto. Per informazioni su questo codice di errore, vedere la sezione relativa ai codici di errore di sistema nella documentazione sullo sviluppo per Windows.|  
  
## <a name="explanation"></a>Spiegazione  
 Se un cluster WSFC viene eliminato, vengono rimosse tutte le chiavi del Registro di sistema correlate a [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
## <a name="user-action"></a>Azione dell'utente  
 Dopo aver creato di nuovo il cluster WSFC, disabilitare e quindi riabilitare AlwaysOn in ogni nodo del cluster in cui un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è abilitata per AlwaysOn. Per questa attività è possibile utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare e disabilitare gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)   
 [Windows Server Failover Clustering &#40;WSFC&#41; con SQL Server](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
