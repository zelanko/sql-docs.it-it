---
title: Statistiche per tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e47a8c6f5b0da31aea9168bbbc56bd9b28afb96
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530833"
---
# <a name="statistics-for-memory-optimized-tables"></a>Statistiche per tabelle con ottimizzazione per la memoria
  In Query Optimizer vengono utilizzate le statistiche sulle colonne per creare piani di query che consentono di migliorare le prestazioni di esecuzione delle query. Le statistiche vengono raccolte dalle tabelle del database e archiviate nei metadati del database.  
  
 Le statistiche vengono create automaticamente, ma possono essere create anche manualmente. Ad esempio, le statistiche vengono create automaticamente per le colonne chiave dell'indice alla creazione dell'indice. Per altre informazioni sulla creazione di statistiche, vedere [Statistiche](../statistics/statistics.md).  
  
 I dati della tabella in genere cambiano nel corso del tempo quando le righe vengono inserite, aggiornate ed eliminate. Ciò significa che le statistiche devono essere periodicamente aggiornate. Per impostazione predefinita, le statistiche sulle tabelle basate su disco vengono aggiornate automaticamente quando l'utilità di ottimizzazione determina che potrebbero non essere aggiornate.  
  
 Le statistiche sulle tabelle ottimizzate per la memoria non vengono aggiornate per impostazione predefinita. È necessario quindi aggiornarle manualmente. Uso [UPDATE STATISTICS &#40;Transact-SQL&#41; ](/sql/t-sql/statements/update-statistics-transact-sql) per le singole colonne, indici o tabelle. Uso [sp_updatestats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) per aggiornare le statistiche per tutti gli utenti e le tabelle interne nel database.  
  
 Quando si usa [CREATE STATISTICS &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-statistics-transact-sql) oppure [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql), è necessario specificare `NORECOMPUTE` per disabilitare le statistiche automatiche aggiornamento per le tabelle ottimizzate per la memoria. Per le tabelle basate su disco [sp_updatestats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) Aggiorna le statistiche solo se la tabella è stata modificata dall'ultima [sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql). Per le tabelle ottimizzate per la memoria [sp_updatestats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) genera sempre statistiche aggiornate. [sp_updatestats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) è uno strumento utile per le tabelle ottimizzate per la memoria; in caso contrario, è necessario sapere quali tabelle presentano modifiche significative in modo che è possibile aggiornare le statistiche singolarmente.  
  
 Le statistiche possono essere generate eseguendo il campionamento dei dati oppure un'analisi completa. Le statistiche campionate utilizzano solo un campione di dati della tabella per stimare la distribuzione dei dati. Le statistiche fullscan eseguono l'analisi dell'intera tabella per determinare la distribuzione dei dati. Le statistiche fullscan sono in genere più accurate, ma richiedono tempi di calcolo più lunghi. Le statistiche campionate possono essere raccolte più velocemente.  
  
 Le tabelle basate su disco utilizzano per impostazione predefinita le statistiche campionate. Le tabelle con ottimizzazione per la memoria supportano solo statistiche fullscan. Quando si usa [CREATE STATISTICS &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-statistics-transact-sql) oppure [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql), è necessario specificare il `FULLSCAN` opzione ottimizzate per la memoria tabelle.  
  
 Considerazioni aggiuntive per le statistiche delle tabelle ottimizzate per la memoria:  
  
-   Gli indici delle tabelle ottimizzate per la memoria vengono creati con la tabella. Le statistiche delle colonne chiave dell'indice vengono create quando la tabella è vuota. Pertanto, queste statistiche devono essere aggiornate dopo che i dati vengono caricati nella tabella.  
  
-   Per le stored procedure compilate in modo nativo, i piani di esecuzione delle query nella procedura vengono ottimizzati quando la procedura viene compilata. Questa operazione viene eseguita solo quando la procedura viene creata e il server viene riavviato, non quando le statistiche vengono aggiornate. Pertanto, le tabelle devono contenere un set rappresentativo di dati e le statistiche devono essere aggiornate prima che le procedure vengano create. Le stored procedure compilate in modo nativo vengono ricompilate se il database viene portato offline e poi online o se il server viene riavviato.  
  
## <a name="guidelines-for-statistics-when-deploying-memory-optimized-tables"></a>Linee guida per le statistiche durante la distribuzione delle tabelle con ottimizzazione per la memoria  
 Per garantire che le statistiche in Query Optimizer risultino aggiornate durante la creazione dei piani di query, distribuire le tabelle ottimizzate per la memoria utilizzando i seguenti cinque passaggi:  
  
1.  Creare tabelle e indici. Gli indici sono specificati inline nelle istruzioni `CREATE TABLE`.  
  
2.  Caricare i dati nelle tabelle.  
  
3.  Aggiornare le statistiche delle tabelle.  
  
4.  Creare stored procedure che accedono alle tabelle.  
  
5.  Eseguire il carico di lavoro che può contenere una combinazione di stored procedure [!INCLUDE[tsql](../../../includes/tsql-md.md)] compilate in modo nativo e interpretate nonché i batch ad hoc.  
  
 La creazione delle stored procedure compilate in modo nativo dopo il caricamento dei dati e l'aggiornamento delle statistiche garantisce la presenza delle statistiche disponibili per le tabelle ottimizzate per la memoria in Query Optimizer. In questo modo si ottengono piani di query efficienti quando la procedura viene compilata.  
  
## <a name="guidelines-for-maintaining-statistics-on-memory-optimized-tables"></a>Linee guida per la gestione delle statistiche delle tabelle con ottimizzazione per la memoria  
 Per mantenere le statistiche aggiornate, aggiornare regolarmente le statistiche delle tabelle ottimizzate per la memoria.  
  
 Se i dati vengono modificati di frequente, è necessario aggiornare spesso le statistiche. Ad esempio, aggiornare le statistiche delle tabelle dopo un aggiornamento batch. Dopo l'aggiornamento delle statistiche, eliminare e ricreare le stored procedure compilate in modo nativo perché possano utilizzare le statistiche aggiornate.  
  
 .  
  
 Non aggiornare le statistiche durante i picchi di carico di lavoro.  
  
 Per aggiornare le statistiche:  
  
-   Uso [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] al [creare un piano di manutenzione](../maintenance-plans/create-a-maintenance-plan.md) con un [attività Aggiorna statistiche](../maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
-   In alternativa, aggiornare le statistiche tramite uno script [!INCLUDE[tsql](../../../includes/tsql-md.md)], come illustrato di seguito.  
  
 Per aggiornare le statistiche per una singola tabella con ottimizzazione per la memoria (*myschema*. *MyTable*), eseguire lo script seguente:  
  
```  
UPDATE STATISTICS myschema.Mytable WITH FULLSCAN, NORECOMPUTE  
```  
  
 Per aggiornare le statistiche per tutte le tabelle ottimizzate per la memoria nel database corrente, eseguire lo script seguente:  
  
```sql  
DECLARE @sql NVARCHAR(MAX) = N''  
  
SELECT @sql += N'  
   UPDATE STATISTICS ' + quotename(schema_name(schema_id)) + N'.' + quotename(name) + N' WITH FULLSCAN, NORECOMPUTE'  
FROM sys.tables WHERE is_memory_optimized=1  
  
EXEC sp_executesql @sql  
```  
  
 Per aggiornare le statistiche per tutte le tabelle nel database, eseguire [sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql).  
  
 Nell'esempio seguente viene indicato quando è stato effettuato l'ultimo aggiornamento delle statistiche sulle tabelle ottimizzate per la memoria. Queste informazioni sono utili per stabilire se è necessario aggiornare le statistiche.  
  
```sql  
select t.object_id, t.name, sp.last_updated as 'stats_last_updated'  
from sys.tables t join sys.stats s on t.object_id=s.object_id cross apply sys.dm_db_stats_properties(t.object_id, s.stats_id) sp  
where t.is_memory_optimized=1  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle con ottimizzazione per la memoria](memory-optimized-tables.md)  
  
  
