---
title: Stored procedure estese (Transact-SQL)
titleSuffix: SQL Server Stretch Database
ms.custom: seo-dt-2019
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
ms.openlocfilehash: d82b6cb9049bf5a41cfb987a55bb6d5a7147c9bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74119268"
---
# <a name="stretch-database-extended-stored-procedures-transact-sql"></a>Stretch Database stored procedure estese (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

 In questa sezione vengono descritte le stored procedure estese correlate a Stretch Database.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[sys. sp_rda_deauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md) Rimuove la connessione autenticata tra un database locale abilitato per l'estensione e il database di Azure remoto.

[sys. sp_rda_get_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md) Ottiene il numero di ore di dati migrati che SQL Server conserva in una tabella di staging per garantire un ripristino completo del database di Azure remoto, se è necessario un ripristino.
  
 [sys. sp_rda_reauthorize_db](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) Ripristina la connessione autenticata tra un database locale abilitato per l'estensione e il database remoto.
  
 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)  
 Riconcilia l'ID batch archiviato nella tabella SQL Server abilitata per l'estensione per i dati migrati più di recente con l'ID batch archiviato nella tabella remota di Azure. 
 
[sys. sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md) Consente di riconciliare le colonne della tabella remota di Azure con le colonne nella tabella SQL Server abilitata per l'estensione.
 
 [sys. sp_rda_reconcile_indexes](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-indexes-transact-sql.md) Accoda un'attività dello schema per riconciliare gli indici nella tabella remota.
 
 [sys. sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) Specifica se le query eseguite sul database corrente abilitato per l'estensione e sulle relative tabelle restituiscono dati locali e remoti (impostazione predefinita) o solo dati locali.
 
 [sys. sp_rda_set_rpo_duration](../../relational-databases/system-stored-procedures/sys-sp-rda-set-rpo-duration-transact-sql.md) Imposta il numero di ore di dati migrati che SQL Server conserva in una tabella di staging per garantire un ripristino completo del database di Azure remoto, se è necessario un ripristino.
 
 [sys. sp_rda_test_connection](../../relational-databases/system-stored-procedures/sys-sp-rda-test-connection-transact-sql.md) Verifica la connessione da SQL Server al server Azure remoto e segnala problemi che possono impedire la migrazione dei dati.
 
## <a name="see-also"></a>Vedere anche  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
