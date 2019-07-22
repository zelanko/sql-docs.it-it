---
title: Visualizzare comandi replicati e altre informazioni nel database di distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_browsereplcmds
- transactional replication, monitoring
- distribution databases [SQL Server replication], viewing replicated commands
- viewing replicated commands
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8e4fc71168a424fa31675e616846f24f6f4af616
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111028"
---
# <a name="view-replicated-commands-and-information-in-distribution-database"></a>Visualizzare comandi replicati e altre informazioni nel database di distribuzione
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Durante l'utilizzo della replica transazionale, i comandi della transazione vengono archiviati nel database di distribuzione finché non vengono propagati a tutti i Sottoscrittori dall'agente di distribuzione o un agente di distribuzione nel Sottoscrittore non esegue il pull delle modifiche. È possibile visualizzare tali comandi in sospeso nel database di distribuzione a livello di programmazione, utilizzando le stored procedure di replica. Per altre informazioni, vedere [Stored procedure per la replica &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>Per visualizzare comandi replicati da tutte le pubblicazioni transazionali nel database di distribuzione  
  
1.  Nel database di distribuzione del server di distribuzione eseguire [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md).  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>Per visualizzare comandi replicati nel database di distribuzione da un articolo specifico o da un database specifico pubblicato tramite la replica transazionale  
  
1.  (Facoltativo) Nel database di pubblicazione del server di pubblicazione eseguire [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md). Specificare **@publication** e **@article** . Tenere presente il valore di **article id** nel set di risultati.  
  
2.  Nel database di distribuzione del server di distribuzione eseguire [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md). (Facoltativo) Specificare l'ID dell'articolo indicato nel passaggio 2 per **@article_id** . (Facoltativo) Specificare l'ID del database di pubblicazione per **@publisher_database_id** . Tale valore può essere ottenuto dalla colonna **database_id** nella vista del catalogo [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare la replica a livello di programmazione](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
