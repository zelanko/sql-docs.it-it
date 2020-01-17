---
title: Comandi non distribuiti (Monitoraggio replica)
description: Informazioni sulla scheda "Comandi non distribuiti" di Monitoraggio replica in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.subscription.performance.f1
ms.assetid: 5451561e-0ce3-4bb5-844a-88cd15b0b371
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 09271bf91d561e86fdf6525ccd217bb000449044
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321402"
---
# <a name="subscription-undistributed-commands-transactional-subscription"></a>Sottoscrizione, Comandi non distribuiti (sottoscrizione transazionale)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La scheda **Comandi non distribuiti** visualizza informazioni sul numero di comandi nel database di distribuzione che non sono stati recapitati al Sottoscrittore selezionato e il tempo previsto per il recapito di tali comandi. Per informazioni sulla visualizzazione dei comandi nel database di distribuzione, vedere [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md).  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opzioni  
 **Numero di comandi nel database di distribuzione in attesa di essere applicati al Sottoscrittore**  
 Numero di comandi nel database di distribuzione che non sono stati recapitati al Sottoscrittore selezionato. Un comando è composto da un'istruzione DDL (Data Definition Language) o da un'istruzione DML (Data Manipulation Language) Transact-SQL.  
  
 **Tempo previsto per l'applicazione di questi comandi, sulla base delle prestazioni passate**  
 Tempo stimato per il recapito dei comandi al Sottoscrittore. Se questo valore è maggiore del tempo necessario per generare uno snapshot e applicarlo al Sottoscrittore, potrebbe risultare conveniente reinizializzare il Sottoscrittore. Per altre informazioni, vedere [Reinizializzare le sottoscrizioni](../../relational-databases/replication/reinitialize-subscriptions.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Avviare Monitoraggio replica](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Monitorare le prestazioni con Monitoraggio replica](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
