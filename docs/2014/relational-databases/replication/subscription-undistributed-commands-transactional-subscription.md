---
title: Sottoscrizione, comandi non distribuiti (sottoscrizione transazionale, SQL Server 2005 e versioni successive) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a1f957c417c5c63766dfbffa923edd6935d1eb5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63151486"
---
# <a name="subscription-undistributed-commands-transactional-subscription-sql-server-2005-and-later"></a>Sottoscrizione, Comandi non distribuiti (sottoscrizione transazionale, SQL Server 2005 e versioni successive)
  La scheda **Comandi non distribuiti** visualizza informazioni sul numero di comandi nel database di distribuzione che non sono stati recapitati al Sottoscrittore selezionato e il tempo previsto per il recapito di tali comandi. Per informazioni sulla visualizzazione dei comandi nel database di distribuzione, vedere [sp_replshowcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql).  
  
## <a name="options"></a>Opzioni  
 **Numero di comandi nel database di distribuzione in attesa di essere applicati al Sottoscrittore**  
 Numero di comandi nel database di distribuzione che non sono stati recapitati al Sottoscrittore selezionato. Un comando è composto da un'istruzione DDL (Data Definition Language) o da un'istruzione DML (Data Manipulation Language) Transact-SQL.  
  
 **Tempo previsto per l'applicazione di questi comandi, sulla base delle prestazioni passate**  
 Tempo stimato per il recapito dei comandi al Sottoscrittore. Se questo valore è maggiore del tempo necessario per generare uno snapshot e applicarlo al Sottoscrittore, potrebbe risultare conveniente reinizializzare il Sottoscrittore. Per altre informazioni, vedere [Reinizializzare le sottoscrizioni](reinitialize-subscriptions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md)   
 [Monitorare le prestazioni con Monitoraggio replica](monitor/monitor-performance-with-replication-monitor.md)   
 [Monitoraggio della replica](monitoring-replication.md)  
  
  
