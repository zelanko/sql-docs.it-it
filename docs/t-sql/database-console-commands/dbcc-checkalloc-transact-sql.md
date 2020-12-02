---
description: DBCC CHECKALLOC (Transact-SQL)
title: DBCC CHECKALLOC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKALLOC_TSQL
- DBCC CHECKALLOC
- DBCC_CHECKALLOC_TSQL
- CHECKALLOC
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKALLOC statement
- checking database space allocation
- database space allocation [SQL Server]
- consistency [SQL Server], disk space allocations
- space allocation [SQL Server]
- allocation checks
- disk space [SQL Server], allocation consistency checks
- space allocation [SQL Server], checking
ms.assetid: bc1218eb-ffff-44ce-8122-6e4fa7d68a79
author: pmasl
ms.author: umajay
ms.openlocfilehash: b4631e88e76aeb9657327d9dbe4d6300b36b70df
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128606"
---
# <a name="dbcc-checkalloc-transact-sql"></a>DBCC CHECKALLOC (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Controlla la consistenza delle strutture di allocazione dello spazio su disco per il database specificato.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DBCC CHECKALLOC   
[  
    ( database_name | database_id | 0   
      [ , NOINDEX   
      | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]  
    )  
    [ WITH   
        {   
          [ ALL_ERRORMSGS ]  
          [ , NO_INFOMSGS ]   
          [ , TABLOCK ]   
          [ , ESTIMATEONLY ]   
        }  
    ]  
]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *database_name* | *database_id* | 0   
 Nome o ID del database per cui si vuole controllare l'allocazione e l'uso delle pagine.
Se questo argomento viene omesso oppure se viene specificato il valore 0, viene utilizzato il database corrente.
I nomi di database devono essere conformi alle regole per gli [identificatori](../../relational-databases/databases/database-identifiers.md).

 NOINDEX  
 Specifica che il controllo degli indici non cluster di tabelle utente non è necessario.<br>NOINDEX è disponibile solo per compatibilità con le versioni precedenti e non ha alcun effetto su DBCC CHECKALLOC.

 REPAIR_ALLOW_DATA_LOSS \| REPAIR_FAST \| REPAIR_REBUILD  
 Specifica che DBCC CHECKALLOC corregge gli errori rilevati. *database_name* deve essere in modalità utente singolo.

 REPAIR_ALLOW_DATA_LOSS  
 Tenta di correggere tutti gli errori rilevati. Le operazioni di correzione possono comportare la perdita di dati. REPAIR_ALLOW_DATA_LOSS è l'unica opzione che consente di correggere errori di allocazione.

 REPAIR_FAST  
 La sintassi è stata mantenuta solo a scopo di compatibilità con le versioni precedenti. Non vengono eseguite correzioni.

 REPAIR_REBUILD  
 Non applicabile.  
 Utilizzare le opzioni REPAIR solo come ultima risorsa. Per correggere gli errori, è consigliabile eseguire un ripristino da un backup. Le operazioni di correzione non tengono conto degli eventuali vincoli esistenti per le tabelle o tra le tabelle. Se la tabella specificata è interessata da uno o più vincoli, è consigliabile eseguire DBCC CHECKCONSTRAINTS dopo l'operazione di correzione. Se è necessario utilizzare REPAIR, eseguire DBCC CHECKDB senza opzioni di correzione per individuare il livello di correzione da applicare. Se si utilizza il livello REPAIR_ALLOW_DATA_LOSS, è consigliabile eseguire il backup del database prima di utilizzare DBCC CHECKDB con questa opzione.

 WITH  
 Consente di specificare opzioni.

 ALL_ERRORMSGS  
 Visualizza tutti i messaggi di errore. Tutti i messaggi di errore vengono visualizzati per impostazione predefinita. La specifica o l'omissione di questa opzione non ha alcun effetto.

 NO_INFOMSGS  
 Disattiva tutti i messaggi informativi e il report relativo allo spazio utilizzato.

 TABLOCK  
 Richiede l'acquisizione di un blocco esclusivo del database per l'esecuzione del comando DBCC.

 ESTIMATEONLY  
 Visualizza la quantità stimata di spazio in tempdb necessaria per l'esecuzione di DBCC CHECKALLOC quando vengono specificate tutte le altre opzioni.
  
## <a name="remarks"></a>Osservazioni  
DBCC CHECKALLOC controlla l'allocazione di tutte le pagine nel database, indipendentemente dal tipo di pagina o dal tipo di oggetto a cui la pagina appartiene. Questa istruzione convalida inoltre le varie strutture interne utilizzate per tenere traccia delle pagine e delle relative relazioni.
Se NO_INFOMSGS viene omesso, DBCC CHECKALLOC raccoglie informazioni relative all'utilizzo dello spazio per tutti gli oggetti del database. Queste informazioni vengono aggiunte a tutti gli errori rilevati.
  
> [!NOTE]  
> La funzionalità di DBCC CHECKALLOC è inclusa in [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) e [DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md). Non è pertanto necessario eseguire DBCC CHECKALLOC separatamente rispetto a queste istruzioni.   I dati di FILESTREAM non vengono controllati da DBCC CHECKALLOC. Tramite FILESTREAM vengono archiviati oggetti binari di grandi dimensioni (BLOB) nel file system.  
  
## <a name="internal-database-snapshot"></a>Snapshot di database interno  
DBCC CHECKALLOC utilizza uno snapshot interno del database per indicare la consistenza transazionale necessaria per l'esecuzione di questi controlli. Se non è possibile creare uno snapshot o si specifica TABLOCK, DBCC CHECKALLOC tenta di acquisire un blocco esclusivo (X) sul database per ottenere la consistenza necessaria.
  
> [!NOTE]  
> L'esecuzione di DBCC CHECKALLOC in tempdb non comporta alcun controllo. Questo funzionamento dipende dal fatto che per motivi di prestazioni gli snapshot di database non sono disponibili in tempdb. Ciò significa che non è possibile ottenere la consistenza delle transazioni necessaria. Arrestare e avviare il servizio MSSQLSERVER per risolvere gli eventuali problemi di allocazione di tempdb. Il database tempdb viene quindi eliminato e ricreato.  
  
## <a name="understanding-dbcc-error-messages"></a>Informazioni sui messaggi di errore DBCC  
Dopo il completamento del comando DBCC CHECKALLOC, nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene scritto un messaggio. Se il comando DBCC viene eseguito correttamente, il messaggio indica il completamento corretto e la durata dell'esecuzione del comando. Se il comando DBCC viene arrestato prima del completamento del controllo a causa di un errore, il messaggio indica che il comando è stato terminato e specifica un valore di stato e la durata dell'esecuzione del comando. Nella tabella seguente sono elencati e descritti i valori di stato che possono essere inclusi nel messaggio.
  
|State|Descrizione|  
|---|---|  
|0|È stato generato l'errore numero 8930. Indica che il comando DBCC è stato terminato a causa di un danneggiamento dei metadati.|  
|1|È stato generato l'errore numero 8967. Si è verificato un errore DBCC interno.|  
|2|Si è verificato un errore durante un ripristino di database in modalità di emergenza.|  
|3|Indica che il comando DBCC è stato terminato a causa di un danneggiamento dei metadati.|  
|4|È stata rilevata una violazione di accesso o asserzione.|  
|5|il comando DBCC è stato terminato da un errore sconosciuto.|  
  
## <a name="error-reporting"></a>Segnalazione errori  
Quando un comando DBCC CHECKALLOC rileva un errore di danneggiamento, viene creato un piccolo file di dump denominato SQLDUMP *nnnn*.txt nella directory LOG di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se le funzionalità di segnalazione degli errori e di raccolta di dati relativi all'utilizzo delle funzionalità sono abilitate per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il file verrà inoltrato automaticamente a [!INCLUDE[msCoName](../../includes/msconame-md.md)]. I dati raccolti consentono di migliorare la funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
Il file di dump contiene i risultati dell'esecuzione del comando DBCC CHECKALLOC e l'output di dati diagnostici supplementari. Il file dispone di elenchi di controllo di accesso discrezionale (DACL) limitati. L'accesso è limitato all'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e ai membri del ruolo sysadmin. Per impostazione predefinita il ruolo sysadmin contiene tutti i membri del gruppo BUILTIN\Administrators di Windows e del gruppo dell'amministratore locale. Se il processo di raccolta dei dati non ha esito positivo, l'esecuzione del comando DBCC viene completata comunque.
  
## <a name="resolving-errors"></a>Risoluzione degli errori  
Se DBCC CHECKALLOC segnala la presenza di errori, è consigliabile ripristinare il database dal backup anziché eseguire un'operazione di correzione. Se non esiste un backup, l'operazione di correzione può consentire di risolvere i problemi segnalati, ma può comportare l'eliminazione di alcune pagine e, di conseguenza, di alcuni dati.
Un'operazione di correzione può essere eseguita durante una transazione utente in modo da consentire il rollback delle modifiche. Se si esegue il rollback delle modifiche, il database conterrà ancora gli errori e dovrà essere ripristinato da un backup. Al termine delle correzioni, eseguire il backup del database.
  
## <a name="result-sets"></a>Set di risultati  
Nelle tabelle seguenti vengono descritte le informazioni restituite da DBCC CHECKALLOC.
  
|Elemento|Descrizione|  
|---|---|  
|FirstIAM|Solo per uso interno.|  
|Radice|Solo per uso interno.|  
|Dpages|Conteggio delle pagine di dati.|  
|Pages used|Pagine allocate.|  
|Dedicated extents|Extent allocati all'oggetto.<br /><br /> Se si utilizzano pagine di allocazione miste, è possibile che alcune pagine allocate siano prive di extent.|  
  
DBCC CHECKALLOC fornisce inoltre per ogni indice e partizione di ogni file un riepilogo dell'allocazione, in cui viene descritta la distribuzione dei dati.
  
|Elemento|Descrizione|  
|---|---|  
|Reserved pages|Pagine allocate all'indice e pagine non utilizzate negli extent allocati.|  
|Used pages|Pagine allocate e utilizzate dall'indice.|  
|Partition ID|Solo per uso interno.|  
|Alloc unit ID|Solo per uso interno.|  
|Dati In-row|Pagine contenenti dati di indice o di heap.|  
|Dati LOB|Pagine contenenti dati **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **text**, **ntext**, **xml** e **image**.|  
|Dati Row-overflow|Pagine contenenti dati di colonne a lunghezza variabile spostati all'esterno di righe.|  
  
DBCC CHECKALLOC restituisce il set di risultati seguente (i valori possono variare), tranne quando viene specificata la parola chiave ESTIMATEONLY o NO_INFOMSGS.
  
```
DBCC results for 'master'.  
***************************************************************  
Table sysobjects                Object ID 1.  
Index ID 1         FirstIAM (1:11)   Root (1:12)    Dpages 22.  
    Index ID 1. 24 pages used in 5 dedicated extents.  
Index ID 2         FirstIAM (1:1368)   Root (1:1362)    Dpages 10.  
    Index ID 2. 12 pages used in 2 dedicated extents.  
Index ID 3         FirstIAM (1:1392)   Root (1:1408)    Dpages 4.  
    Index ID 3. 6 pages used in 0 dedicated extents.  
Total number of extents is 7.  
***************************************************************  
'...'  
***************************************************************  
Table spt_server_info                Object ID 1938105945.  
Index ID 1         FirstIAM (1:520)   Root (1:508)    Dpages 1.  
    Index ID 1. 3 pages used in 0 dedicated extents.  
Total number of extents is 0.  
***************************************************************  
Processed 52 entries in sysindexes for database ID 1.  
File 1. Number of extents = 210, used pages = 1126, reserved pages = 1280.  
           File 1 (number of mixed extents = 73, mixed pages = 184).  
    Object ID 1, Index ID 0, data extents 5, pages 24, mixed extent pages 9.  
'...'  
    Object ID 1938105945, Index ID 0, data extents 0, pages 3, mixed extent pages 3.  
Total number of extents = 210, used pages = 1126, reserved pages = 1280 in this database.  
       (number of mixed extents = 73, mixed pages = 184) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC results for 'master'.  
***************************************************************  
Table sys.sysrowsetcolumns                Object ID 4.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). FirstIAM (1:98). Root (1:94). Dpages 7.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). 9 pages used in 1 dedicated extents.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). FirstIAM (0:0). Root (0:0). Dpages 0.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). 0 pages used in 0 dedicated extents.  
Total number of extents is 1.  
...  
***************************************************************  
Processed 201 entries in system catalog for database ID 1.  
File 1. Number of extents = 44, used pages = 300, reserved pages = 345.  
           File 1 (number of mixed extents = 29, mixed pages = 225).  
    Object ID 4, index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 5, index ID 1, partition ID 327680, alloc unit ID 327680 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 7, index ID 1, partition ID 458752, alloc unit ID 458752 (type In-row data), data extents 0, pages 5, mixed extent pages 5.  
    Object ID 8, index ID 0, partition ID 524288, alloc unit ID 524288 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 13, index ID 1, partition ID 851968, alloc unit ID 851968 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 15, index ID 1, partition ID 983040, alloc unit ID 983040 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 26, index ID 1, partition ID 281474978414592, alloc unit ID 1703937 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 1, partition ID 281474978480128, alloc unit ID 1769473 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 2, partition ID 562949955190784, alloc unit ID 1769474 (type In-row data), index extents 0, pages 3, mixed extent pages 3.  
...  
    Object ID 1179151246, index ID 1, partition ID 72057594038845440, alloc unit ID 13435136 (type In-row data), data extents 2, pages 18, mixed extent pages 8.  
    Object ID 1179151246, index ID 2, partition ID 72057594038910976, alloc unit ID 13566208 (type In-row data), index extents 1, pages 16, mixed extent pages 8.  
    Object ID 1911677858, index ID 0, partition ID 72057594039631872, alloc unit ID 15073536 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
Total number of extents = 41, used pages = 289, reserved pages = 323 in this database.  
       (number of mixed extents = 27, mixed pages = 211) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Quando si specifica ESTIMATEONLY, viene restituito il set di risultati seguente.
  
```
Estimated TEMPDB space needed for CHECKALLOC (KB)   
-------------------------------------------------   
34  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Autorizzazioni  
È richiesta l'appartenenza al ruolo predefinito del server sysadmin o al ruolo predefinito del database db_owner.
  
## <a name="examples"></a>Esempi  
Nell'esempio seguente viene eseguito `DBCC CHECKALLOC` per il database corrente e per il database `AdventureWorks2012`.
  
```sql  
-- Check the current database.  
DBCC CHECKALLOC;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKALLOC (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

