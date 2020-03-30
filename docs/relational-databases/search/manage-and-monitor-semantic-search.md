---
title: Gestire e monitorare la ricerca semantica | Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], managing
- semantic search [SQL Server], monitoring
ms.assetid: eb5c3b29-da70-42aa-aa97-7d35a3f1eb98
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: c5e5c8256c117ebd3fbb57b5a7c291b539c5a428
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68132247"
---
# <a name="manage-and-monitor-semantic-search"></a>Gestire e monitorare la ricerca semantica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Vengono illustrati il processo di indicizzazione semantica e le attività correlate alla gestione e al monitoraggio degli indici.  
  
##  <a name="check-the-status-of-semantic-indexing"></a><a name="HowToMonitorStatus"></a> Verificare lo stato dell'indicizzazione semantica  
### <a name="is-the-first-phase-of-semantic-indexing-complete"></a>Verifica del completamento della prima fase dell'indicizzazione semantica
 Eseguire una query sulla DMV [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md) e verificare lo **stato** e le colonne **status_description**.  
  
 La prima fase dell'indicizzazione include il popolamento dell'indice di parole chiave full-text e dell'indice di frasi chiave semantico, nonché l'estrazione dei dati di somiglianza dei documenti.  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_index_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="is-the-second-phase-of-semantic-indexing-complete"></a>Verifica del completamento della seconda fase dell'indicizzazione semantica
 Eseguire una query sulla DMV [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md) e verificare lo **stato** e le colonne **status_description**.  
  
 La seconda fase dell'indicizzazione include il popolamento dell'indice di somiglianza dei documenti semantico.  
  
```wql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_fts_semantic_similarity_population WHERE table_id = OBJECT_ID('table_name')  
GO  
```  
  
##  <a name="check-the-size-of-the-semantic-indexes"></a><a name="HowToCheckSize"></a> Verificare le dimensioni degli indici semantici  
### <a name="what-is-the-logical-size-of-a-semantic-key-phrase-index-or-a-semantic-document-similarity-index"></a>Individuazione della dimensione logica di un indice di frasi chiave semantico o di un indice di somiglianza dei documenti semantico
 Eseguire una query sulla DMV [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md).  
  
 La dimensione logica viene visualizzata in numero di pagine di indice.  
  
```sql  
USE database_name  
GO  
  
SELECT * FROM sys.dm_db_fts_index_physical_stats WHERE object_id = OBJECT_ID('table_name')  
GO  
```  
  
### <a name="what-is-the-total-size-of-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>Individuazione delle dimensioni totali degli indici full-text e semantici per un catalogo full-text  
 Eseguire una query sulla proprietà **IndexSize** della funzione per i metadati [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'IndexSize')  
GO  
```  
  
### <a name="how-many-items-are-indexed-in-the-full-text-and-semantic-indexes-for-a-full-text-catalog"></a>Individuazione del numero di elementi indicizzati negli indici full-text e semantico per un catalogo full-text  
 Eseguire una query sulla proprietà **ItemCount** della funzione per i metadati [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).  
  
```sql  
SELECT FULLTEXTCATALOGPROPERTY('catalog_name', 'ItemCount')  
GO  
```  
  
##  <a name="force-the-population-of-the-semantic-indexes"></a><a name="HowToForcePopulation"></a> Forzare il popolamento degli indici semantici  
 È possibile forzare il popolamento degli indici full-text e semantici utilizzando la clausola START/STOP/PAUSE o RESUME POPULATION con la stessa sintassi e lo stesso comportamento descritti per gli indici full-text. Per altre informazioni, vedere [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md) e [Popolamento degli indici full-texts](../../relational-databases/search/populate-full-text-indexes.md).  
  
 Poiché l'indicizzazione semantica dipende dall'indicizzazione full-text, gli indici semantici vengono popolati solo al popolamento degli indici full-text associati.  
  
 **Esempio: Avviare un popolamento completo di indici full-text e semantici**  
  
 Nell'esempio seguente viene avviato il popolamento completo degli indici semantici e full-text mediante la modifica di un indice full-text esistente nella tabella **Production.Document** del database di esempio AdventureWorks2012.  
  
```vb  
USE AdventureWorks2012  
GO  
  
ALTER FULLTEXT INDEX ON Production.Document  
    START FULL POPULATION  
GO  
```  
  
##  <a name="disable-or-re-enable-semantic-indexing"></a><a name="HowToDisableIndexing"></a> Disabilitare o riabilitare l'indicizzazione semantica  
 È possibile abilitare o disabilitare l'indicizzazione full-text o semantica utilizzando la clausola ENABLE/DISABLE con la stessa sintassi e lo stesso comportamento descritti per gli indici full-text. Per altre informazioni, vedere [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
 Quando l'indicizzazione semantica è disabilitata e sospesa, le query sui dati semantici continuano a funzionare correttamente e a restituire dati precedentemente indicizzati. Questo comportamento non è coerente con quello della ricerca full-text.  
  
```sql  
-- To disable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name DISABLE  
GO  
  
-- To re-enable semantic indexing on a table  
USE database_name  
GO  
  
ALTER FULLTEXT INDEX ON table_name ENABLE  
GO  
```  
  
##  <a name="about-the-phases-of-semantic-indexing"></a><a name="SemanticIndexing"></a> Fasi di indicizzazione semantica  
 Tramite la ricerca semantica vengono indicizzati due tipi di dati per ogni colonna in cui è abilitata:  
  
1.  **Frasi chiave**  
  
2.  **Somiglianza dei documenti**  
  
 L'indicizzazione semantica viene eseguita in due fasi, insieme all'indicizzazione full-text:  
  
1.  **Fase 1**. L'indice delle parole chiave full-text e l'indice delle frasi chiave semantico vengono popolati in parallelo. In questa fase vengono anche estratti i dati necessari per indicizzare la somiglianza dei documenti.  
  
2.  **Fase 2**. Viene quindi popolato l'indice di somiglianza dei documenti semantico. Questo indice dipende da entrambi gli indici popolati nella fase precedente.  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="issue-semantic-indexes-are-not-populated"></a><a name="ProblemNotPopulated"></a> Problema: gli indici semantici non vengono popolati  
### <a name="are-the-associated-full-text-indexes-populated"></a>Verificare se gli indici full-text associati sono stati popolati.  
 Poiché l'indicizzazione semantica dipende dall'indicizzazione full-text, gli indici semantici vengono popolati solo al popolamento degli indici full-text associati.  
  
### <a name="are-full-text-search-and-semantic-search-properly-installed-and-configured"></a>Verificare se la ricerca full-text e la ricerca semantica sono state installate e configurate correttamente.  
 Per altre informazioni, vedere [Installazione e configurazione della ricerca semantica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
### <a name="is-the-fdhost-service-not-available-or-is-there-another-condition-that-would-cause-full-text-indexing-to-fail"></a>Controllare se il servizio FDHOST è disponibile o se si è verificata un'altra condizione che provoca la mancata esecuzione dell'indicizzazione full-text.  
 Per altre informazioni, vedere [Risoluzione dei problemi nell'indicizzazione full-text](../../relational-databases/search/troubleshoot-full-text-indexing.md).  
  
  
