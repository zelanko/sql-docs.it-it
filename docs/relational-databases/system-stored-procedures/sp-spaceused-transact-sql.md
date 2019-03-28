---
title: sp_spaceused (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_spaceused_TSQL
- sp_spaceused
dev_langs:
- TSQL
helpviewer_keywords:
- sp_spaceused
ms.assetid: c6253b48-29f5-4371-bfcd-3ef404060621
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 61cd3c5c4ba15d42c1b1fe261703cfbb67b3e24f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538553"
---
# <a name="spspaceused-transact-sql"></a>sp_spaceused (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Visualizza il numero di righe, lo spazio su disco riservato e lo spazio su disco utilizzato per una tabella, una vista indicizzata o una coda di [!INCLUDE[ssSB](../../includes/sssb-md.md)] nel database corrente oppure visualizza lo spazio su disco riservato e utilizzato dall'intero database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_spaceused [[ @objname = ] 'objname' ]   
[, [ @updateusage = ] 'updateusage' ]  
[, [ @mode = ] 'mode' ]  
[, [ @oneresultset = ] oneresultset ]  
[, [ @include_total_xtp_storage = ] include_total_xtp_storage ]
```  
  
## <a name="arguments"></a>Argomenti  

Per la [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] e [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)], `sp_spaceused` deve specificare i parametri denominati (ad esempio `sp_spaceused (@objname= N'Table1');` invece di basarsi al momento la posizione ordinale dei parametri. 

`[ @objname = ] 'objname'`
   
 Nome completo o non qualificato della tabella, della vista indicizzata o della coda per cui si desidera ottenere informazioni sull'utilizzo dello spazio. Le virgolette sono necessarie solo se viene specificato un nome di oggetto completo. Se viene specificato un nome di oggetto completo, ovvero contenente un nome di database, il nome del database deve essere quello del database corrente.  
Se *objname* non viene specificato, vengono restituiti risultati per l'intero database.  
*objname* viene **nvarchar(776)**, con un valore predefinito è NULL.  
> [!NOTE]  
> [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] e [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)] supportano solo gli oggetti di database e tabella.
  
`[ @updateusage = ] 'updateusage'` Indica di che eseguire DBCC UPDATEUSAGE per aggiornare le informazioni sull'utilizzo di spazio. Quando *objname* non è specificato, l'istruzione viene eseguita sull'intero database; in caso contrario, l'istruzione viene eseguita *objname*. I possibili valori sono **true** oppure **false**. *UPDATEUSAGE* viene **varchar (5)**, il valore predefinito è **false**.  
  
`[ @mode = ] 'mode'` Indica l'ambito dei risultati. Per una tabella estesa o il database, il *modalità* parametro consente di includere o escludere la parte remota dell'oggetto. Per ulteriori informazioni, vedere [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
 Il *modalità* argomento può avere i valori seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|ALL|Restituisce le statistiche di archiviazione dell'oggetto o database tra cui la parte locale sia la parte remota.|  
|LOCAL_ONLY|Restituisce le statistiche di archiviazione di solo la parte locale del database o oggetto. Se l'oggetto o il database non è abilitata per l'estensione, restituisce le stesse statistiche come quando @mode = ALL.|  
|REMOTE_ONLY|Restituisce le statistiche di archiviazione di solo la parte remota dell'oggetto o database. Questa opzione genera un errore quando viene soddisfatta una delle condizioni seguenti:<br /><br /> La tabella non è abilitata per l'estensione.<br /><br /> La tabella è abilitata per l'estensione, ma è non stata mai abilitata la migrazione dei dati. In questo caso, la tabella remota non ancora disponibile uno schema.<br /><br /> L'utente ha rilasciato manualmente alla tabella remota.<br /><br /> Il provisioning dell'archivio dati remoto ha restituito uno stato di esito positivo, ma in realtà non è riuscita.|  
  
 *modalità* viene **varchar (11)**, il valore predefinito è **al '**.  
  
`[ @oneresultset = ] oneresultset` Indica se restituire un singolo set di risultati. Il *oneresultset* argomento può avere i valori seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0|Quando *@objname* è null o non specificato, vengono restituiti due set di risultati. Due set di risultati è il comportamento predefinito.|  
|1|Quando *@objname* = null o viene omesso, viene restituito un singolo set di risultati.|  
  
 *oneresultset* viene **bit**, il valore predefinito è **0**.  

`[ @include_total_xtp_storage] 'include_total_xtp_storage'`
**Si applica a:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)], [!INCLUDE[sssds-md](../../includes/sssds-md.md)].  
  
 Quando @oneresultset= 1, il parametro @include_total_xtp_storage determina se il singolo set di risultati include le colonne per l'archiviazione MEMORY_OPTIMIZED_DATA. Il valore predefinito è 0, vale a dire, per impostazione predefinita (se il parametro viene omesso) le colonne XTP non sono inclusi nel set di risultati.  

## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Se *objname* viene omesso e il valore di *oneresultset* è 0, i set di risultati seguente vengono restituiti per fornire informazioni sulle dimensioni di database corrente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome del database corrente.|  
|**database_size**|**varchar(18)**|Dimensioni del database corrente, espresse in megabyte. **database_size** include file di dati e di log.|  
|**spazio non allocato**|**varchar(18)**|Spazio nel database non riservato per i relativi oggetti.|  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|Quantità totale di spazio allocato per gli oggetti del database.|  
|**data**|**varchar(18)**|Quantità totale di spazio utilizzato per i dati.|  
|**index_size**|**varchar(18)**|Quantità totale di spazio utilizzato per gli indici.|  
|**unused**|**varchar(18)**|Quantità totale di spazio riservato per gli oggetti del database ma non ancora utilizzato.|  
  
 Se *objname* viene omesso e il valore di *oneresultset* è 1, per offrire informazioni sulle dimensioni di database corrente viene restituito il seguente set di risultati singolo.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome del database corrente.|  
|**database_size**|**varchar(18)**|Dimensioni del database corrente, espresse in megabyte. **database_size** include file di dati e di log.|  
|**spazio non allocato**|**varchar(18)**|Spazio nel database non riservato per i relativi oggetti.|  
|**reserved**|**varchar(18)**|Quantità totale di spazio allocato per gli oggetti del database.|  
|**data**|**varchar(18)**|Quantità totale di spazio utilizzato per i dati.|  
|**index_size**|**varchar(18)**|Quantità totale di spazio utilizzato per gli indici.|  
|**unused**|**varchar(18)**|Quantità totale di spazio riservato per gli oggetti del database ma non ancora utilizzato.|  
  
 Se *objname* viene specificato, il set di risultati seguente viene restituito per l'oggetto specificato.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|Nome dell'oggetto per cui sono state richieste informazioni sull'utilizzo dello spazio.<br /><br /> Il nome dello schema dell'oggetto non viene restituito. Se è necessario il nome dello schema, usare il [DM db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) oppure [db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) viste a gestione dinamica per ottenere informazioni sulle dimensioni equivalenti.|  
|**rows**|**char(20)**|Numero di righe esistenti nella tabella. Se l'oggetto specificato è una coda di [!INCLUDE[ssSB](../../includes/sssb-md.md)], in questa colonna viene indicato il numero di messaggi presenti nella coda.|  
|**reserved**|**varchar(18)**|Quantità totale di spazio riservato per *objname*.|  
|**data**|**varchar(18)**|Quantità totale di spazio utilizzato dai dati *objname*.|  
|**index_size**|**varchar(18)**|Quantità totale di spazio utilizzato dagli indici nel *objname*.|  
|**unused**|**varchar(18)**|Quantità totale di spazio riservato *objname* ma non ancora utilizzato.|  
 
Questa è la modalità predefinita, quando viene specificato alcun parametro. I set di risultati seguente vengono restituiti che riporta informazioni sulle dimensioni di database su disco. 

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome del database corrente.|  
|**database_size**|**varchar(18)**|Dimensioni del database corrente, espresse in megabyte. **database_size** include file di dati e di log. Se il database ha un filegroup MEMORY_OPTIMIZED_DATA, ciò include la dimensione totale su disco di tutti i file di checkpoint nel filegroup.|  
|**spazio non allocato**|**varchar(18)**|Spazio nel database non riservato per i relativi oggetti. Se il database ha un filegroup MEMORY_OPTIMIZED_DATA, ciò include la dimensione totale su disco dei file di checkpoint con stato PRECREATED nel filegroup.|  

Spazio utilizzato dalle tabelle nel database: (questo set di risultati non riflette le tabelle ottimizzate per la memoria, come non vi è alcun contabilità per tabella di utilizzo del disco) 

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|Quantità totale di spazio allocato per gli oggetti del database.|  
|**data**|**varchar(18)**|Quantità totale di spazio utilizzato per i dati.|  
|**index_size**|**varchar(18)**|Quantità totale di spazio utilizzato per gli indici.|  
|**unused**|**varchar(18)**|Quantità totale di spazio riservato per gli oggetti del database ma non ancora utilizzato.|

Il set di risultati seguente viene restituito **solo se** il database ha un filegroup MEMORY_OPTIMIZED_DATA con almeno un contenitore: 

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**xtp_precreated**|**varchar(18)**|Dimensioni totali dei file di checkpoint con stato PRECREATED, espressa in KB. Conteggi per lo spazio non allocato del database nel suo complesso. [, Ad esempio, se è presente 600.000 KB di checkpoint precreati, questa colonna contiene 600000 ' KB']|  
|**xtp_used**|**varchar(18)**|Dimensioni totali dei file di checkpoint con gli stati UNDER CONSTRUCTION, ACTIVE e destinazione di tipo MERGE, in KB. Questo è lo spazio su disco usato attivamente per i dati nelle tabelle ottimizzate per la memoria.|  
|**xtp_pending_truncation**|**varchar(18)**|Dimensioni totali dei file di checkpoint con stato WAITING_FOR_LOG_TRUNCATION, espressa in KB. Questo è lo spazio su disco usato per i file di checkpoint in attesa di pulizia, una volta che si verifica il troncamento del log.|

Se *objname* viene omesso, il valore di oneresultset è 1, e *include_total_xtp_storage* è 1, per offrire informazioni sulle dimensioni di database corrente viene restituito il seguente set di risultati singolo. Se `include_total_xtp_storage` è 0 (impostazione predefinita), le ultime tre colonne sono stati omessi. 

|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nome del database corrente.|  
|**database_size**|**varchar(18)**|Dimensioni del database corrente, espresse in megabyte. **database_size** include file di dati e di log. Se il database ha un filegroup MEMORY_OPTIMIZED_DATA, ciò include la dimensione totale su disco di tutti i file di checkpoint nel filegroup.|
|**spazio non allocato**|**varchar(18)**|Spazio nel database non riservato per i relativi oggetti. Se il database ha un filegroup MEMORY_OPTIMIZED_DATA, ciò include la dimensione totale su disco dei file di checkpoint con stato PRECREATED nel filegroup.|  
|**reserved**|**varchar(18)**|Quantità totale di spazio allocato per gli oggetti del database.|  
|**data**|**varchar(18)**|Quantità totale di spazio utilizzato per i dati.|  
|**index_size**|**varchar(18)**|Quantità totale di spazio utilizzato per gli indici.|  
|**unused**|**varchar(18)**|Quantità totale di spazio riservato per gli oggetti del database ma non ancora utilizzato.|
|**xtp_precreated**|**varchar(18)**|Dimensioni totali dei file di checkpoint con stato PRECREATED, espressa in KB. Ciò viene conteggiato lo spazio non allocato del database nel suo complesso. Restituisce NULL se il database non dispone di un filegroup memory_optimized_data con almeno un contenitore. *Questa colonna è disponibile solo se incluse @include_total_xtp_storage= 1*.| 
|**xtp_used**|**varchar(18)**|Dimensioni totali dei file di checkpoint con gli stati UNDER CONSTRUCTION, ACTIVE e destinazione di tipo MERGE, in KB. Questo è lo spazio su disco usato attivamente per i dati nelle tabelle ottimizzate per la memoria. Restituisce NULL se il database non dispone di un filegroup memory_optimized_data con almeno un contenitore. *Questa colonna è disponibile solo se incluse @include_total_xtp_storage= 1*.| 
|**xtp_pending_truncation**|**varchar(18)**|Dimensioni totali dei file di checkpoint con stato WAITING_FOR_LOG_TRUNCATION, espressa in KB. Questo è lo spazio su disco usato per i file di checkpoint in attesa di pulizia, una volta che si verifica il troncamento del log. Restituisce NULL se il database non dispone di un filegroup memory_optimized_data con almeno un contenitore. Questa colonna è disponibile solo se incluse `@include_total_xtp_storage=1`.|

## <a name="remarks"></a>Note  
 **database_size** sia sempre maggiore rispetto alla somma **riservato** + **spazio non allocato** perché include le dimensioni dei file di log, ma **riservato**e **unallocated_space** prendere in considerazione solo le pagine di dati.  
  
 Le pagine che vengono utilizzate per indici XML e indici full-text vengono incluse nei **index_size** per entrambi gli insiemi di risultati. Quando *objname* è specificato, le pagine per gli indici XML e indici full-text per l'oggetto vengono conteggiate anche nel totale **riservato** e **index_size** risultati.  
  
 Se l'utilizzo dello spazio viene calcolato per un database o un oggetto che ha un indice spaziale, le colonne della dimensione dello spazio, ad esempio **database_size**, **riservato**, e **index_size**, includere le dimensioni dell'indice spaziale.  
  
 Quando *updateusage* è specificato, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] analizzati i dati delle pagine del database e apporta le correzioni necessarie le **Sys. allocation_units** e **Sys. Partitions** viste riguardanti lo spazio di archiviazione usato da ogni tabella del catalogo. In alcune situazioni, ad esempio dopo l'eliminazione di un indice, le informazioni sullo spazio restituite per la tabella non sono aggiornate. *UPDATEUSAGE* può richiedere alcuni minuti per l'esecuzione nel database o tabelle di grandi dimensioni. Uso *updateusage* solo quando si sospetta che vengano restituiti valori non corretti e quando il processo non avrà effetti negativi su altri utenti o i processi nel database. Se lo si preferisce, è possibile eseguire l'istruzione DBCC UPDATEUSAGE separatamente.  
  
> [!NOTE]  
>  In caso di eliminazione o ricompilazione di indici di grandi dimensioni oppure di eliminazione o troncamento di tabelle di grandi dimensioni, in [!INCLUDE[ssDE](../../includes/ssde-md.md)] le deallocazioni di pagine effettive e i relativi blocchi associati vengono posticipati fino all'esecuzione del commit della transazione. Le operazioni di eliminazione posticipate non rendono immediatamente disponibile lo spazio allocato. Di conseguenza, i valori restituiti da **sp_spaceused** immediatamente dopo l'eliminazione o troncamento di un oggetto di grandi dimensioni potrebbe non riflettere lo spazio disco effettivamente disponibile.  
  
## <a name="permissions"></a>Permissions  
 L'autorizzazione per eseguire **sp_spaceused** è concessa al ruolo **public** . Solo i membri del ruolo predefinito del database **db_owner** possono specificare il parametro **@updateusage** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-displaying-disk-space-information-about-a-table"></a>A. Visualizzazione di informazioni relative allo spazio su disco per una tabella  
 Nell'esempio seguente vengono visualizzate informazioni relative allo spazio su disco per la tabella `Vendor` e i relativi indici.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
### <a name="b-displaying-updated-space-information-about-a-database"></a>B. Visualizzazione di informazioni sullo spazio aggiornate per un database  
 Nell'esempio seguente viene riepilogato lo spazio utilizzato nel database corrente e viene utilizzato il parametro facoltativo `@updateusage` per garantire la restituzione di valori aggiornati.  
  
```sql  
USE AdventureWorks008R2;  
GO  
EXEC sp_spaceused @updateusage = N'TRUE';  
GO  
```  
  
### <a name="c-displaying-space-usage-information-about-the-remote-table-associated-with-a-stretch-enabled-table"></a>C. Visualizzazione di informazioni sull'utilizzo dello spazio per la tabella remota associata a una tabella abilitata per l'estensione  
 Nell'esempio seguente vengono riepilogate lo spazio utilizzato dalla tabella remota associata a una tabella abilitata per l'estensione usando il **@mode** argomento per specificare la destinazione remota. Per ulteriori informazioni, vedere [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
```sql  
USE StretchedAdventureWorks2016  
GO  
EXEC sp_spaceused N'Purchasing.Vendor', @mode = 'REMOTE_ONLY'  
```  
  
### <a name="d-displaying-space-usage-information-for-a-database-in-a-single-result-set"></a>D. Visualizzazione di informazioni sull'utilizzo dello spazio per un database in un singolo risultato impostato  
 Nell'esempio seguente riepiloga l'utilizzo dello spazio per il database corrente in un unico set di risultati.  
  
```sql  
USE AdventureWorks2016  
GO  
EXEC sp_spaceused @oneresultset = 1  
```  

### <a name="e-displaying-space-usage-information-for-a-database-with-at-least-one-memoryoptimized-file-group-in-a-single-result-set"></a>E. Visualizzazione di informazioni sull'utilizzo dello spazio per un database con almeno un gruppo di file MEMORY_OPTIMIZED in un unico set di risultati 
 Nell'esempio seguente riepiloga l'utilizzo dello spazio per il database corrente con almeno un gruppo di file MEMORY_OPTIMIZED in un unico set di risultati.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused @updateusage = 'FALSE', @mode = 'ALL', @oneresultset = '1', @include_total_xtp_storage = '1';
GO
``` 

### <a name="f-displaying-space-usage-information-for-a-memoryoptimized-table-object-in-a-database"></a>F. Visualizzazione di informazioni sull'utilizzo dello spazio per un oggetto tabella MEMORY_OPTIMIZED in un database.
 Nell'esempio seguente riepiloga l'utilizzo dello spazio per un oggetto tabella MEMORY_OPTIMIZED nel database corrente con almeno un gruppo di file MEMORY_OPTIMIZED.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused
@objname = N'VehicleTemparatures',
@updateusage = 'FALSE',
@mode = 'ALL',
@oneresultset = '0',
@include_total_xtp_storage = '1';
GO
```  

## <a name="see-also"></a>Vedere anche  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC UPDATEUSAGE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
