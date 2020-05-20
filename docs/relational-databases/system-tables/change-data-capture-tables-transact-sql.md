---
title: Tabelle Change Data Capture (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a4372d0b-50ca-4e58-80f6-2ed3cb52a84a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e98c770db0f1fc9c89275fc973a2bdee8ee4508f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82825941"
---
# <a name="change-data-capture-tables-transact-sql"></a>Tabelle Change Data Capture (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  L'acquisizione dei dati delle modifiche consente il rilevamento delle modifiche apportate alle tabelle, così che le modifiche DML e DDL apportate alle tabelle possono essere caricate in modo incrementale in un data warehouse. Negli argomenti di questa sezione vengono descritte le tabelle di sistema in cui sono archiviate le informazioni utilizzate dalle operazioni di acquisizione dei dati delle modifiche.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [cdc.<capture_instance>_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
 Restituisce una riga per ogni modifica apportata a una colonna acquisita nella tabella di origine associata.  
  
 [cdc.captured_columns](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
 Restituisce una riga per ogni colonna registrata in un'istanza di acquisizione.  
  
 [cdc.change_tables](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
 Restituisce una riga per ogni tabella delle modifiche del database.  
  
 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)  
 Restituisce una riga per ogni modifica DDL (Data Definition Language) apportata a tabelle abilitate per l'acquisizione dei dati delle modifiche.  
  
 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)  
 Restituisce una riga per ogni transazione per la quale sono presenti righe in una tabella delle modifiche. Questa tabella viene utilizzata per eseguire il mapping tra valori di commit di numero di sequenza del file di log (LSN) e l'ora in cui è stato eseguito il commit della transazione.  
  
 [cdc.index_columns](../../relational-databases/system-tables/cdc-index-columns-transact-sql.md)  
 Restituisce una riga per ogni colonna dell'indice associata a una tabella delle modifiche.  
  
 [dbo. cdc_jobs &#40;&#41;Transact-SQL](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
 Restituisce i parametri di configurazione per i processi dell'agente di acquisizione dei dati delle modifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure Change Data Capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Funzioni Change Data Capture &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)  
  
  
