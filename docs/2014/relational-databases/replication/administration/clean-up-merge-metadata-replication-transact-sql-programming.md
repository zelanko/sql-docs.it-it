---
title: Eseguire la pulizia dei metadati di merge (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 384b5cc158600848dbca6528a4c8c39250a23908
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62629177"
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>Pulizia dei metadati di merge (programmazione Transact-SQL della replica)
  La rimozione dei metadati della replica di tipo merge viene eseguita periodicamente dall'agente di merge in base all'impostazione di memorizzazione per la pubblicazione. Nel server di pubblicazione e nel Sottoscrittore ciò avviene nelle tabelle di sistema [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql), [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql), [MSmerge_past_partition_mappings](/sql/relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql)e [MSmerge_current_partition_mappings](/sql/relational-databases/system-tables/msmerge-current-partition-mappings) . È inoltre possibile rimuovere i dati in tali tabelle a livello di programmazione utilizzando le stored procedure di replica.  
  
### <a name="to-manually-clean-up-merge-metadata"></a>Per pulire manualmente i metadati di merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_mergemetadataretentioncleanup](/sql/relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql).  
  
2.  Opzionale Si noti il numero di righe rimosse nel passaggio 1 dalle tabelle di sistema [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql)e [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql) , restituite rispettivamente **@num_genhistory_rows**nei **@num_contents_rows**parametri di **@num_tombstone_rows** output, e.  
  
3.  Ripetere i passaggi 1 e 2 nel Sottoscrittore per eseguire la pulizia dei metadati nel database di sottoscrizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Scadenza e disattivazione delle sottoscrizioni](../subscription-expiration-and-deactivation.md)  
  
  
