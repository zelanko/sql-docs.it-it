---
title: Oggetto Databases di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 668fe6a825be365aa605febaaea7aafdd71ddf7d
ms.sourcegitcommit: fa2f85b6deeceadc0f32aa7f5f4e2b6e4d99541c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/03/2019
ms.locfileid: "53997573"
---
# <a name="sql-server-databases-object"></a>SQL Server, oggetto di database
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L'oggetto **SQLServer:Database** in SQL Server include contatori per il monitoraggio delle operazioni di copia bulk, della velocità effettiva dei backup e del ripristino e delle attività del log delle transazioni. Eseguire il monitoraggio delle transazioni e del log delle transazioni per determinare la quantità di attività degli utenti eseguita nel database e lo spazio disponibile nel log delle transazioni. La quantità di attività degli utenti ha effetto sulle prestazioni del database e sulle dimensioni del log, sul blocco e sulla replica. Il monitoraggio dell'attività del log di basso livello per misurare l'attività degli utenti e l'utilizzo delle risorse può essere utile per identificare eventuali colli di bottiglia.  
  
 È possibile monitorare contemporaneamente più istanze dell'oggetto **Databases** che rappresentano i singoli database.  
  
 Questa tabella descrive i contatori **Databases** di SQL Server.  
  
|Contatori di database di SQL Server|Descrizione|  
|-----------------------------------|-----------------|  
|**Transazioni attive**|Numero di transazioni attive per il database.|  
|**Distanza media da fine log per richiesta pool di log**|Distanza media in byte dalla fine del log per ogni richiesta del pool di log, per le richieste effettuate nell'ultimo VLF.| 
|**Velocità effettiva di backup o ripristino/sec**|Velocità effettiva di lettura/scrittura delle operazioni di backup e ripristino di un database al secondo. Ad esempio, è possibile verificare come vengono modificate le prestazioni dell'operazione di backup del database quando vengono utilizzati più dispositivi di backup in parallelo o dispositivi più veloci. La velocità effettiva di un'operazione di backup o ripristino del database consente di determinare lo stato di avanzamento e le prestazioni delle operazioni di backup e di ripristino.|  
|**Righe copia bulk/sec**|Numero di righe al secondo di cui viene eseguita la copia bulk.|  
|**Velocità effettiva copia bulk/sec**|Quantità di copie bulk di dati eseguite al secondo (in kilobyte).|  
|**Voci della tabella di commit**|Dimensioni (conteggio righe) della parte in memoria della tabella di commit per il database. Per altre informazioni, vedere [sys.dm_tran_commit_table &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md).|  
|**Dimensioni file di dati (KB)**|Dimensioni cumulative in kilobyte di tutti i file di dati del database, inclusi eventuali incrementi automatici. Il monitoraggio di questo contatore consente, ad esempio, di determinare le dimensioni corrette di **tempdb**.|  
|**Byte/sec analisi logiche DBCC**|Numero di byte di analisi di lettura logica al secondo per comandi DBCC (Database Command Console).|  
|**Tempo di Commit gruppo/sec**|Tempo di blocco del gruppo (in microsecondi) al secondo.|
|**Byte/sec scaricamento log**|Numero totale di byte dei log scaricati.|  
|**Percentuale riscontri cache log**|Percentuale di letture della cache del log soddisfatte dalla cache.|  
|**Base percentuale riscontri cache log**|Solo per uso interno.| 
|**Letture cache log/sec**|Letture eseguire al secondo tramite la cache dello strumento di gestione del log.|  
|**Dimensioni file di log (KB)**|Dimensioni cumulative in kilobyte di tutti i file di log delle transazioni del database.|  
|**Spazio file di log utilizzato (KB)**|Spazio cumulativo utilizzato in tutti i file di log del database.|  
|**Tempo di attesa scaricamento log**|Tempo totale di attesa, espresso in millisecondi, per lo scaricamento del log. In un database secondario Always On questo valore indica il tempo di attesa prima che i record di log vengano salvati su disco.|  
|**Attese scaricamento log /sec**|Numero di operazioni di commit al secondo in attesa dello scaricamento del log.|  
|**Ora di scrittura scaricamento log (ms)**|Tempo in millisecondi necessario per eseguire scritture di scaricamenti log completati nell'ultimo secondo.|  
|**Scaricamenti log/sec**|Numero di scaricamenti del log al secondo.|  
|**Aumenti dimensioni log**|Numero totale di aumenti delle dimensioni del log delle transazioni del database.|  
|**Mancati riscontri cache del pool di log/sec**|Numero di richieste per il quale il blocco del log non è disponibile nel pool di log. Il *pool di log* è una cache in memoria del log delle transazioni. Questa cache viene utilizzata per ottimizzare la lettura del log per il recupero, la replica della transazione, il rollback e per [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].|  
|**Letture disco del pool di log/sec**|Numero di letture del disco che il pool di log ha emesso per recuperare i blocchi di log.|  
|**Eliminazioni hash pool di log/sec**|Frequenza delle eliminazioni di voci hash non elaborate dal pool di log.|
|**Inserimenti hash pool di log/sec**|Frequenza degli inserimenti di voci hash non elaborate nel pool di log.|
|**Voci hash pool di log non valide/sec**|Frequenza delle ricerche hash non riuscite perché non valide.|
|**Push di analisi del log del pool di log/sec**|Frequenza di push del blocco del log da parte delle analisi del log, derivanti dal disco o dalla memoria.|
|**Push writer di log del pool di log/sec**|Frequenza di push del blocco di log da parte del thread del writer di log.|
|**Push del pool di log con pool libero vuoto/sec**|Frequenza errori di push dei blocchi di log a causa di un pool libero vuoto.|
|**Push del pool di log con memoria insufficiente/sec**|Frequenza di errori di push dei blocchi di log a causa di memoria insufficiente.|
|**Push del pool di log senza buffer liberi/sec**|Frequenza di errori di push dei blocchi di log a causa della mancata disponibilità di un buffer.|
|**Richieste del pool di log protette da troncamento/sec**|Mancati riscontri nella cache del pool di log a causa della protezione del blocco richiesto da parte dell'LSN di troncamento.|
|**Base richieste del pool di log**|Solo per uso interno.| 
|**Richieste del pool di log nel VLF precedente/sec**|Richieste del pool di log non incluse nell'ultimo VLF del log.|  
|**Richieste del pool di log/sec**|Numero di richieste di blocco di log elaborate dal pool di log.|  
|**Dimensioni totali log attivo del pool di log**|Dimensioni totali log attivo corrente archiviato in Gestione buffer di cache condiviso in byte.|
|**Dimensioni totali pool condiviso del pool di log**|Utilizzo di memoria totale corrente di Gestione buffer di cache condiviso in byte.|
|**Compattazioni log**|Numero totale di compattazioni del log del database corrente.|  
|**Troncamenti log**|Numero di volte in cui il log delle transazioni è stato compattato.|  
|**Percentuale log utilizzata**|Percentuale di spazio del log utilizzata.|  
|**Transazioni replica in sospeso**|Numero di transazioni nel log delle transazioni del database di pubblicazione contrassegnate per la replica, ma non ancora recapitate al database di distribuzione.|  
|**Velocità transazioni replica**|Numero di transazioni al secondo lette dal log delle transazioni del database di pubblicazione e recapitate al database di distribuzione.|  
|**Byte/sec spostamento dati per compattazione**|Quantità di dati spostati al secondo tramite le operazioni di compattazione automatica o l'istruzione DBCC SHRINKDATABASE o DBCC SHRINKFILE.|  
|**Transazioni rilevate al secondo**|Numero di transazioni di cui è stato eseguito il commit nella tabella di commit per il database.|  
|**Transazioni/sec**|Numero di transazioni avviate al secondo per il database.<br /><br /> **Transazioni/sec** non conteggia le transazioni solo XTP (transazioni avviate da una stored procedure compilata in modo nativo).|  
|**Scrittura transazioni/sec**|Numero di transazioni che hanno scritto nel database e di cui è stato eseguito il commit nell'ultimo secondo.|  
|**Base di latenza DLC del controller XTP**|Solo per uso interno.| 
|**Latenza/recupero DLC del controller XTP**|Latenza media in microsecondi tra quando i blocchi di log arrivano nel consumer di log diretto e quando vengono recuperati dal controller XTP al secondo.|
|**Latenza di picco DLC del controller XTP**|Massima latenza registrata in microsecondi di un recupero dal consumer di log diretto da parte del controller XTP.|
|**Log del controller XTP elaborato/sec**|Quantità di byte di log elaborati dal thread del controller XTP al secondo.|
|**Memoria XTP utilizzata (KB)**|Quantità di memoria usata da XTP nel database.| 
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, replica di database](../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
  
