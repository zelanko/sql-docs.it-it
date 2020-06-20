---
title: Oggetto Databases di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2f4f46bd388476934226e41d371c85fa13b94d23
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066091"
---
# <a name="sql-server-databases-object"></a>SQL Server, oggetto di database
  L'oggetto **SQLServer:Database** in SQL Server include contatori per il monitoraggio delle operazioni di copia bulk, della velocità effettiva dei backup e del ripristino e delle attività del log delle transazioni. Eseguire il monitoraggio delle transazioni e del log delle transazioni per determinare la quantità di attività degli utenti eseguita nel database e lo spazio disponibile nel log delle transazioni. La quantità di attività degli utenti ha effetto sulle prestazioni del database e sulle dimensioni del log, sul blocco e sulla replica. Il monitoraggio dell'attività del log di basso livello per misurare l'attività degli utenti e l'utilizzo delle risorse può essere utile per identificare eventuali colli di bottiglia.  
  
 È possibile monitorare contemporaneamente più istanze dell'oggetto **Databases** che rappresentano i singoli database.  
  
 Questa tabella descrive i contatori **Databases** di SQL Server.  
  
|Contatori di database di SQL Server|Descrizione|  
|-----------------------------------|-----------------|  
|**Transazioni attive**|Numero di transazioni attive per il database.|  
|**Velocità effettiva di backup o ripristino/sec**|Velocità effettiva di lettura/scrittura delle operazioni di backup e ripristino di un database al secondo. Ad esempio, è possibile verificare come vengono modificate le prestazioni dell'operazione di backup del database quando vengono utilizzati più dispositivi di backup in parallelo o dispositivi più veloci. La velocità effettiva di un'operazione di backup o ripristino del database consente di determinare lo stato di avanzamento e le prestazioni delle operazioni di backup e di ripristino.|  
|**Righe copia bulk/sec**|Numero di righe al secondo di cui viene eseguita la copia bulk.|  
|**Velocità effettiva copia bulk/sec**|Quantità di copie bulk di dati eseguite al secondo (in kilobyte).|  
|**Voci della tabella di commit**|Dimensioni della parte in memoria della tabella di commit per il database. Per altre informazioni, vedere [sys.dm_tran_commit_table &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table).|  
|**Dimensioni file di dati (KB)**|Dimensioni cumulative in kilobyte di tutti i file di dati del database, inclusi eventuali incrementi automatici. Il monitoraggio di questo contatore consente, ad esempio, di determinare le dimensioni corrette di **tempdb**.|  
|**Byte/sec analisi logiche DBCC**|Numero di byte di analisi di lettura logica al secondo per comandi DBCC (Database Command Console).|  
|**Percentuale riscontri cache log**|Percentuale di letture della cache del log soddisfatte dalla cache.|  
|**Letture cache log/sec**|Letture eseguire al secondo tramite la cache dello strumento di gestione del log.|  
|**Dimensioni file di log (KB)**|Dimensioni cumulative in kilobyte di tutti i file di log delle transazioni del database.|  
|**Spazio file di log utilizzato (KB)**|Spazio cumulativo utilizzato in tutti i file di log del database.|  
|**Tempo di attesa scaricamento log**|Tempo totale di attesa, espresso in millisecondi, per lo scaricamento del log. In un database secondario AlwaysOn, questo valore indica il tempo di attesa prima che i record di log vengano salvati su disco.|  
|**Attese scaricamento log /sec**|Numero di operazioni di commit al secondo in attesa dello scaricamento del log.|  
|**Ora di scrittura scaricamento log (ms)**|Tempo in millisecondi necessario per eseguire scritture di scaricamenti log completati nell'ultimo secondo.|  
|**Scaricamenti log/sec**|Numero di scaricamenti del log al secondo.|  
|**Aumenti dimensioni log**|Numero totale di aumenti delle dimensioni del log delle transazioni del database.|  
|**Compattazioni log**|Numero totale di compattazioni del log delle transazioni del database.|  
|**Mancati riscontri cache del pool di log/sec**|Numero di richieste per il quale il blocco del log non è disponibile nel pool di log. Il *pool di log* è una cache in memoria del log delle transazioni. Questa cache viene utilizzata per ottimizzare la lettura del log per il recupero, la replica della transazione, il rollback e per [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**Letture disco del pool di log/sec**|Numero di letture del disco che il pool di log ha emesso per recuperare i blocchi di log.|  
|**Richieste del pool di log/sec**|Numero di richieste di blocco di log elaborate dal pool di log.|  
|**Troncamenti log**|Numero di volte in cui il log delle transazioni è stato compattato.|  
|**Percentuale log utilizzata**|Percentuale di spazio del log utilizzata.|  
|**Repl. transazioni in sospeso**|Numero di transazioni nel log delle transazioni del database di pubblicazione contrassegnate per la replica, ma non ancora recapitate al database di distribuzione.|  
|**Velocità transazioni replica**|Numero di transazioni al secondo lette dal log delle transazioni del database di pubblicazione e recapitate al database di distribuzione.|  
|**Byte/sec spostamento dati per compattazione**|Quantità di dati spostati al secondo tramite le operazioni di compattazione automatica o l'istruzione DBCC SHRINKDATABASE o DBCC SHRINKFILE.|  
|**Transazioni rilevate al secondo**|Numero di transazioni di cui è stato eseguito il commit nella tabella di commit per il database.|  
|**Transazioni/sec**|Numero di transazioni avviate al secondo per il database.<br /><br /> **Transazioni/sec** non conteggia le transazioni solo XTP (transazioni avviate da una stored procedure compilata in modo nativo).|  
|**Transazioni di scrittura/sec**|Numero di transazioni che hanno scritto nel database e di cui è stato eseguito il commit nell'ultimo secondo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;monitoraggio di sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, replica di database](sql-server-database-replica.md)  
  
  
