---
title: DBCC SHRINKDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- shrinking files
- shrinking databases
- DBCC SHRINKDATABASE statement
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
ms.assetid: fc976afd-1edb-4341-bf41-c4a42a69772b
author: pmasl
ms.author: umajay
monikerRange: = azuresqldb-current ||>= sql-server-2016 ||>= sql-server-linux-2017||=azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 38d542d84121b41311cd8aa64d4ec9747bfc2bf8
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279533"
---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE [sql-asdb-asa.md](../../includes/applies-to-version/sql-asdb-asa.md)]

Compatta le dimensioni dei file di dati e di log nel database specificato.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  

```syntaxsql
-- Azure Synapse Analytics (formerly SQL DW)

DBCC SHRINKDATABASE   
( database_name   
     [ , target_percent ]   
)  
[ WITH NO_INFOMSGS ]

```  

## <a name="arguments"></a>Argomenti  
_database\_name_ | _database\_id_ | 0  
Nome o ID del database da compattare. Il valore 0 specifica che si sta usando il database corrente.  
  
_target\_percent_  
Percentuale di spazio che si desidera rendere disponibile nel file del database dopo la compattazione.  
  
NOTRUNCATE  
Sposta le pagine assegnate dalla fine del file alle pagine non assegnate all'inizio del file. Questa azione compatta i dati all'interno del file. _target\_percent_ è facoltativo. Azure SQL Data Warehouse non supporta questa opzione. 
  
Lo spazio disponibile alla fine del file non viene restituito al sistema operativo e le dimensioni fisiche del file rimangono invariate. Di conseguenza, quando si specifica NOTRUNCATE il database viene visualizzato come non compattato.  
  
NOTRUNCATE è applicabile solo ai file di dati. NOTRUNCATE non ha effetti sul file di log.  
  
TRUNCATEONLY  
Restituisce al sistema operativo tutto lo spazio disponibile alla fine del file. Non sposta le pagine all'interno del file. Il file di dati viene compattato solo fino all'ultimo extent assegnato. _target\_percent_ viene ignorato se specificato con TRUNCATEONLY. Azure SQL Data Warehouse non supporta questa opzione.
  
TRUNCATEONLY interessa il file di log. Per troncare solo il file di dati, utilizzare DBCC SHRINKFILE.  
  
WITH NO_INFOMSGS  
Evita la visualizzazione di tutti i messaggi informativi con livello di gravità compreso tra 0 e 10.  
  
## <a name="result-sets"></a>Set di risultati  
Nella tabella seguente vengono descritte le colonne del set di risultati.
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**DbId**|Numero di identificazione del database del file che [!INCLUDE[ssDE](../../includes/ssde-md.md)] tenta di compattare.|  
|**FileId**|Numero di identificazione del file che [!INCLUDE[ssDE](../../includes/ssde-md.md)] tenta di compattare.|  
|**CurrentSize**|Numero di pagine da 8 KB attualmente occupate dal file.|  
|**MinimumSize**|Numero minimo di pagine da 8 KB che il file può occupare. Il valore corrisponde alle dimensioni minime o alle dimensioni originali di un file.|  
|**UsedPages**|Numero di pagine da 8 KB utilizzate dal file.|  
|**EstimatedPages**|Numero di pagine da 8 KB calcolato da [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Corrisponde alle possibili dimensioni finali del file compattato.|  
  
>[!NOTE]
> [!INCLUDE[ssDE](../../includes/ssde-md.md)] non visualizza alcuna riga per i file non compattati.  
  
## <a name="remarks"></a>Osservazioni  

>[!NOTE]
> L'esecuzione di questo comando non è consigliata poiché si tratta di un'operazione a elevato utilizzo di input/output che può portare il data warehouse offline. Inoltre, l'esecuzione di questo comando comporta costi per gli snapshot del data warehouse. 

Per compattare tutti i file di dati e di log per un database specifico, eseguire il comando DBCC SHRINKDATABASE. Per compattare un file di dati o di log alla volta per un database specifico, eseguire il comando [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md).
  
Per visualizzare la quantità corrente di spazio disponibile, ovvero non allocato, nel database, eseguire [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).
  
È possibile arrestare le istruzioni DBCC SHRINKDATABASE in qualsiasi momento, senza perdere il lavoro completato.
  
Non è possibile ridurre il database a dimensioni inferiori a quelle minime configurate. Le dimensioni minime vengono specificate al momento della creazione del database. In alternativa, le dimensioni minime possono essere le ultime dimensioni impostate esplicitamente tramite un'operazione di modifica delle dimensioni del file. Operazioni come DBCC SHRINKFILE o ALTER DATABASE sono esempi di operazioni di modifica delle dimensioni del file. 

Si supponga che un database venga creato con dimensioni pari a 10 MB. In seguito, tali dimensioni aumentano fino a 100 MB. Le dimensioni minime a cui è possibile compattare il database sono pari a 10 MB, anche se tutti i dati nel database sono stati eliminati.
  
Quando si esegue DBCC SHRINKDATABASE, specificare l'opzione NOTRUNCATE o l'opzione TRUNCATEONLY. In caso contrario, il risultato è lo stesso di quando si esegue un'operazione DBCC SHRINKDATABASE con NOTRUNCATE seguita da un'operazione DBCC SHRINKDATABASE con TRUNCATEONLY.
  
Non è necessario che il database compattato sia in modalità utente singolo. I database possono essere usati anche da altri utenti quando sono compattati e questo vale anche per i database di sistema.
  
Non è possibile compattare un database mentre ne viene eseguito il backup e non è possibile eseguire il backup di un database mentre è in corso un'operazione di compattazione.
  
## <a name="how-dbcc-shrinkdatabase-works"></a>Funzionamento di DBCC SHRINKDATABASE  
DBCC SHRINKDATABASE compatta i file di dati uno alla volta mentre i file di log vengono compattati come se fossero inclusi in un pool di log contigui. I file vengono compattati sempre a partire dalla fine.
  
Si supponga di avere un paio di file di log, un file di dati e un database denominato **mydb**. I file di dati e di log hanno una dimensione di 10 MB ciascuno e il file di dati contiene 6 MB di dati. Per ogni file, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcola le dimensioni di destinazione in base alle quali il file deve essere compattato. Quando DBCC SHRINKDATABASE è specificato con _target\_percent_, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcola le dimensioni di destinazione come _target\_percent_ dello spazio disponibile nel file dopo la compattazione. 

Ad esempio, se si specifica un valore _target\_percent_ di 25 per la compattazione di **mydb**, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] calcola le dimensioni di destinazione del file di dati come 8 MB, ovvero 6 MB di dati e 2 MB di spazio disponibile. Di conseguenza, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] sposta i dati degli ultimi 2 MB del file di dati nello spazio disponibile nei primi 8 MB del file di dati e quindi compatta il file.
  
Si supponga che il file di dati di **mydb** contenga 7 MB di dati. Specificando un valore _target\_percent_ pari a 30, il file di dati può essere compattato alla percentuale disponibile di 30. Tuttavia, specificando un valore _target\_percent_ di 40, il file di dati non viene compattato perché il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non compatta un file a dimensioni minori di quelle occupate attualmente dai dati. 

È possibile anche considerare il problema in un altro modo: il 40% di spazio disponibile desiderato + il 70% del file di dati completo (7 dei 10 MB) è maggiore del 100%. Con valori _target\_size_ superiori a 30 il file di dati non viene compattato. Non viene compattato perché la percentuale disponibile desiderata più la percentuale corrente occupata dal file di dati è superiore al 100%.
  
Per i file di log, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa _target\_percent_ per calcolare le dimensioni di destinazione dell'intero log. Per questa ragione _target\_percent_ è la quantità di spazio disponibile nel log dopo l'operazione di compattazione. Le dimensioni di destinazione per l'intero log vengono quindi convertite nelle dimensioni di destinazione per ogni file di log.
  
DBCC SHRINKDATABASE tenta di compattare immediatamente ogni file di log fisico fino alle dimensioni di destinazione specificate. Se i log virtuali non includano parti con dimensioni superiori alle dimensioni di destinazione del file di log, il file viene troncato e l'operazione DBCC SHRINKDATABASE termina senza messaggi. Se invece i log virtuali includono parti del log logico oltre le dimensioni di destinazione, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] libera la maggior quantità di spazio possibile e viene visualizzato un messaggio informativo in cui sono descritte le operazioni necessarie per estrarre le parti del log logico dai log virtuali alla fine del file. Dopo l'esecuzione di queste operazioni, è possibile usare DBCC SHRINKDATABASE per liberare lo spazio rimanente.
  
È possibile compattare un file di log solo entro il limite di un file di log virtuale. Ecco perché la compattazione di un file di log a dimensioni inferiori a quelle di un file di log virtuale può non essere possibile. Può non essere possibile anche se il file non viene usato. Le dimensioni del file di log virtuale vengono scelte in modo dinamico da [!INCLUDE[ssDE](../../includes/ssde-md.md)] durante la creazione o l'estensione dei file di log.
  
## <a name="best-practices"></a>Procedure consigliate  
Quando si pianifica la compattazione di un database, considerare le informazioni seguenti:
-   Un'operazione di compattazione è più efficace dopo l'esecuzione di un'operazione che crea spazio inutilizzato, ad esempio il troncamento o l'eliminazione di una tabella.
-   La maggior parte dei database richiede spazio disponibile per lo svolgimento delle normali attività quotidiane. È possibile che, nonostante le ripetute operazioni di compattazione di un database, questo continui ad aumentare di dimensioni. Questo aumento indica che lo spazio compattato è necessario per le normali operazioni. In questi casi è inutile compattare ripetutamente il database.  
-   L'operazione di compattazione generalmente aumenta la frammentazione degli indici del database. Questo è un altro motivo per evitare di compattare ripetutamente un database.  
-   Se non è necessario soddisfare esigenze specifiche, non impostare l'opzione di database AUTO_SHRINK su ON.  
  
## <a name="troubleshooting"></a>Risoluzione dei problemi  
È possibile che le operazioni di compattazione vengano bloccate da una transazione eseguita in un [livello di isolamento basato sul controllo della versione delle righe](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Ad esempio, si tenta di eseguire un'operazione DBCC SHRINK DATABASE mentre è in corso un'operazione di eliminazione di grandi dimensioni che usa un livello di isolamento basato sul controllo delle versioni delle righe. Quando si verifica questa situazione, l'operazione di compattazione attende fino al completamento dell'operazione di eliminazione prima di compattare i file. Mentre l'operazione di compattazione è in attesa, le operazioni DBCC SHRINKFILE e DBCC SHRINKDATABASE generano un messaggio informativo (5202 per SHRINKDATABASE e 5203 per SHRINKFILE). Questo messaggio viene generato nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ogni cinque minuti nella prima ora e in seguito una volta all'ora. Ad esempio, il log degli errori può contenere il messaggio di errore seguente:  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
Questo errore indica che le transazioni snapshot con timestamp precedenti a 109 bloccano l'operazione di compattazione. La transazione indicata è l'ultima transazione completata dall'operazione di compattazione. Il messaggio indica anche che la colonna **transaction_sequence_num** o **first_snapshot_sequence_num** nella DMV [sys.dm_tran_active_snapshot_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) contiene un valore 15. La colonna **transaction_sequence_num** o **first_snapshot_sequence_num** nella vista può contenere un numero minore rispetto all'ultima transazione completata da un'operazione di compattazione (109). In questo caso, l'operazione di compattazione attenderà il completamento delle transazioni.
  
Per risolvere il problema, è possibile eseguire una delle attività seguenti:
-   Terminare la transazione che blocca l'operazione di compattazione.  
-   Terminare l'operazione di compattazione. Il lavoro completato fino a quel momento viene mantenuto.  
-   Non eseguire alcuna operazione per consentire che l'operazione di compattazione venga rimandata fino al completamento della transazione di blocco.  
  
## <a name="permissions"></a>Autorizzazioni  
È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** o al ruolo predefinito del database **db_owner** .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>R. Compattazione di un database e impostazione di una percentuale di spazio disponibile  
Nell'esempio seguente vengono ridotte le dimensioni dei file di dati e di log nel database utente `UserDB` per ottenere il 10% di spazio disponibile nel database.  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. Troncamento di un database  
Nell'esempio seguente i file di dati e di log nel database di esempio `AdventureWorks` vengono compattati fino all'ultimo extent assegnato.  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
### <a name="c-shrinking-an-azure-synapse-analytics-database"></a>C. Compattazione di un database di Azure Synapse Analytics

```
DBCC SHRINKDATABASE (database_A);
DBCC SHRINKDATABASE (database_B, 10); 

```

## <a name="see-also"></a>Vedere anche  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[Compattare un database](../../relational-databases/databases/shrink-a-database.md)
  
  
