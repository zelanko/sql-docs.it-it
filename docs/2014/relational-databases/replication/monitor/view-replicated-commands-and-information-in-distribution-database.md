---
title: Visualizzare comandi replicati e altre informazioni nel database di distribuzione (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 86ced6fd281da2e47ddaa31cab7fa977767b98d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74164959"
---
# <a name="view-replicated-commands-and-other-information-in-the-distribution-database-replication-transact-sql-programming"></a>Visualizzare comandi replicati e altre informazioni nel database di distribuzione (programmazione Transact-SQL della replica)
  Durante l'utilizzo della replica transazionale, i comandi della transazione vengono archiviati nel database di distribuzione finché non vengono propagati a tutti i Sottoscrittori dall'agente di distribuzione o un agente di distribuzione nel Sottoscrittore non esegue il pull delle modifiche. È possibile visualizzare tali comandi in sospeso nel database di distribuzione a livello di programmazione, utilizzando le stored procedure di replica. Per altre informazioni, vedere [Stored procedure per la replica &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql).  
  
### <a name="to-view-replicated-commands-from-all-transactional-publications-in-the-distribution-database"></a>Per visualizzare comandi replicati da tutte le pubblicazioni transazionali nel database di distribuzione  
  
1.  Nel database di distribuzione del server di distribuzione eseguire [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql).  
  
### <a name="to-view-replicated-commands-in-the-distribution-database-from-a-specific-article-or-from-a-specific-database-published-using-transactional-replication"></a>Per visualizzare comandi replicati nel database di distribuzione da un articolo specifico o da un database specifico pubblicato tramite la replica transazionale  
  
1.  (Facoltativo) Nel database di pubblicazione del server di pubblicazione eseguire [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql). Specificare ** \@pubblicazioni** e ** \@articoli**. Tenere presente il valore di **article id** nel set di risultati.  
  
2.  Nel database di distribuzione del server di distribuzione eseguire [sp_browsereplcmds](/sql/relational-databases/system-stored-procedures/sp-browsemergesnapshotfolder-transact-sql). Opzionale Specificare l'ID articolo del passaggio 2 per ** \@article_id**. Opzionale Specificare l'ID del database di pubblicazione per ** \@publisher_database_id**, che può essere ottenuto dalla colonna **database_id** nella vista del catalogo [sys. databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare la replica a livello di programmazione](../monitoring-replication.md)  
  
  
