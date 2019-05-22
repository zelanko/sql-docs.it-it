---
title: Stretch Database (Transact-SQL) le Stored procedure estese | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Stretch Database, stored procedures
ms.assetid: bda29952-4b8b-4295-ab78-f24dcb0b03c6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5acbd4a14de04df412d71fb4ec8fd7d40e8fb7a8
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65979980"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database (Transact-SQL) le Stored procedure estese
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 In questa sezione vengono descritte le stored procedure estese associate a Stretch Database.  
  
## <a name="in-this-section"></a>In questa sezione  
[Sys. sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) rimuove la connessione autenticata tra un database locale abilitato per l'estensione e il database di Azure remoto.

[sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) Ottiene il numero di ore di dati migrati che SQL Server viene mantenuto in una tabella di staging al fine di garantire un ripristino completo del database di Azure remoto, se è necessario un ripristino.
  
 [Sys. sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) consente di ripristinare la connessione autenticata tra un database locale abilitato per l'estensione e il database remoto.
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 Risolve le differenze tra l'ID batch archiviato nella tabella abilitata per l'estensione SQL Server per i dati migrati più di recente con l'ID batch archiviato nella tabella di Azure remota. 
 
[sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) risolve le differenze tra le colonne nella tabella di Azure remota per le colonne nella tabella abilitata per l'estensione SQL Server.
 
 [Sys.sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) accoda un'attività di schema per riconciliare gli indici nella tabella remota.
 
 [sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) specifica se le query su database abilitati per l'estensione corrente e le relative tabelle restituiscono dati locali e remoti (predefinito) o solo i dati locali.
 
 [Sys. sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) imposta il numero di ore di dati migrati che SQL Server viene mantenuto in una tabella di staging al fine di garantire un ripristino completo del database di Azure remoto, se è necessario un ripristino.
 
 [Sys.sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) testa la connessione da SQL Server per il server Azure remoto e segnala i problemi che potrebbero impedire la migrazione dei dati.
 
## <a name="see-also"></a>Vedere anche  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
