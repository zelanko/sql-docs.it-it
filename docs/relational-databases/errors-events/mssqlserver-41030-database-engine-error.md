---
title: MSSQLSERVER_41030 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41030 (Database Engine error)
ms.assetid: c85341ae-0fbf-42ae-9275-4cfe678238f0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c5a9ef8027571650265292f298a8a0c2835241b6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68043486"
---
# <a name="mssqlserver_41030"></a>MSSQLSERVER_41030
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
[Abilitare e disabilitare la funzionalità Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
[Windows Server Failover Clustering &#40;WSFC&#41; con SQL Server](~/sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
