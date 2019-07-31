---
title: DBCC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC
- DBCC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactional consistency
- Database Console Command statements
- status information [SQL Server], DBCC statements
- snapshots [SQL Server database snapshots], DBCC statements
- emergency database state [SQL Server]
- TABLOCK
- internal database snapshots [SQL Server]
- reporting DBCC statement progress
- logical consistency of data [SQL Server]
- DBCC statements
- validation statements [SQL Server]
- miscellaneous statements [SQL Server]
- statements [SQL Server], DBCC statements
- DBCC commands [SQL Server]
- result sets [SQL Server], DBCC statements
- maintenance statements [SQL Server]
- physical consistency of data [SQL Server]
- current DBCC statement status
- progress reporting [DBCC statements]
- informational statements [SQL Server]
ms.assetid: c6da8c04-5b6b-459a-9f76-110c92ca8b29
author: pmasl
ms.author: umajay
ms.openlocfilehash: 22b7963d17039e029ac88ae6f9bc4c2bd9005275
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040523"
---
# <a name="dbcc-transact-sql"></a>DBCC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Il linguaggio di programmazione [!INCLUDE[tsql](../../includes/tsql-md.md)] include istruzioni DBCC che fungono da comandi DBCC (Database Console Command) per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Le istruzioni DBCC sono suddivise nelle categorie seguenti.
  
|Categoria|Attività svolte|  
|---|---|
|Manutenzione|Attività di manutenzione di un database, un indice o un filegroup.|  
|Varie|Attività varie, ad esempio l'attivazione di flag di traccia o la rimozione di una DLL dalla memoria.|  
|Istruzioni informative|Attività mirate alla raccolta e alla visualizzazione di vari tipi di informazioni.|  
|Convalida|Operazioni di convalida di un database, una tabella, un indice, un catalogo, un filegroup o dell'allocazione delle pagine del database.|  
  
I comandi DBCC accettano parametri di input e restituiscono valori. Tutti i parametri dei comandi DBCC accettano valori letterali sia Unicode che DBCS.
  
## <a name="dbcc-internal-database-snapshot-usage"></a>Utilizzo dello snapshot interno del database DBCC  
I comandi DBCC seguenti possono essere eseguiti su uno snapshot interno di sola lettura del database creato da [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Ciò consente di evitare problemi di blocco e concorrenza durante l'esecuzione di questi comandi. Per altre informazioni, vedere [Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).
- DBCC CHECKALLOC
- DBCC CHECKCATALOG
- DBCC CHECKDB
- DBCC CHECKFILEGROUP
- DBCC CHECKTABLE

Quando si esegue uno di questi comandi DBCC, [!INCLUDE[ssDE](../../includes/ssde-md.md)] crea uno snapshot del database con uno stato consistente dal punto di vista transazionale. Il comando DBCC esegue quindi i controlli in base a questo snapshot. Al termine dell'esecuzione del comando DBCC, lo snapshot viene eliminato.
  
Talvolta lo snapshot interno del database non è necessario oppure non può essere creato. In tali casi, il comando DBCC viene eseguito sul database effettivo. Se il database è online, il comando DBCC attiva il blocco a livello di tabella per garantire la consistenza degli oggetti controllati, come se fosse stata specificata l'opzione WITH TABLOCK.
  
Lo snapshot interno del database non viene creato quando il comando DBCC viene eseguito:
-   Sul database **master** e l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in modalità utente singolo.  
-   Su un database diverso da **master** per cui è stata attivata la modalità utente singolo tramite l'istruzione ALTER DATABASE.  
-   Su un database di sola lettura.  
-   Su un database impostato in modalità di emergenza utilizzando l'istruzione ALTER DATABASE.  
-   Su **tempdb**. In tal caso, lo snapshot del database non può essere creato a causa di restrizioni interne.  
-   Con l'opzione WITH TABLOCK. In tal caso, DBCC soddisfa la richiesta evitando di creare uno snapshot del database.  
  
I comandi DBCC utilizzano blocchi a livello di tabella anziché snapshot interni del database quando vengono eseguiti sugli elementi seguenti:
-   Un filegroup di sola lettura  
-   Un file system FAT  
-   Un volume che non supporta "flussi denominati"  
-   Un volume che non supporta "flussi alternativi"  
  
> [!NOTE]  
>  Per tentare di eseguire DBCC CHECKALLOC, oppure la parte equivalente di DBCC CHECKDB, con l'opzione WITH TABLOCK è necessario acquisire un blocco esclusivo a livello di database. Questo blocco non può essere impostato per **tempdb** o **master** e probabilmente ha esito negativo per tutti gli altri database.  
  
> [!NOTE]  
>  L'esecuzione dell'istruzione DBCC CHECKDB sul database **master** ha esito negativo se non è possibile creare uno snapshot interno del database.  
  
## <a name="progress-reporting-for-dbcc-commands"></a>Report di stato per i comandi DBCC  
La vista del catalogo **sys.dm_exec_requests** contiene informazioni riguardanti lo stato e la fase di esecuzione corrente dei comandi DBCC CHECKDB, CHECKFILEGROUP e CHECKTABLE. La colonna **percent_complete** indica la percentuale di completamento del comando, mentre la colonna **command** indica la fase corrente dell'esecuzione del comando.
  
L'unità di riferimento dello stato dipende dalla fase di esecuzione corrente del comando DBCC. In alcune fasi lo stato viene segnalato per ogni pagina del database e in altre per ogni correzione del database o dell'allocazione. Nella tabella seguente viene descritta ogni fase di esecuzione e viene specificato il livello di granularità in base a cui viene segnalato lo stato del comando.
  
|Fase di esecuzione|Descrizione|Granularità del report di stato|  
|---------------------|-----------------|------------------------------------|  
|DBCC TABLE CHECK|Durante questa fase viene controllata la consistenza logica e fisica degli oggetti del database.|Lo stato viene segnalato a livello di pagina del database.<br /><br /> Il valore del report di stato viene aggiornato ogni 1000 pagine del database controllate.|  
|DBCC TABLE REPAIR|Se viene specificata l'opzione REPAIR_FAST, REPAIR_REBUILD o REPAIR_ALLOW_DATA_LOSS ed è necessario correggere alcuni errori relativi agli oggetti, durante questa fase vengono implementate correzioni nel database.|Lo stato viene segnalato a livello di singola correzione.<br /><br /> Il contatore viene aggiornato ogni volta che viene completata una correzione.|  
|DBCC ALLOC CHECK|Durante questa fase vengono controllate le strutture di allocazione del database.<br /><br /> Nota: il comando DBCC CHECKALLOC esegue gli stessi controlli.|Lo stato non viene segnalato.|  
|DBCC ALLOC REPAIR|Se viene specificata l'opzione REPAIR_FAST, REPAIR_REBUILD o REPAIR_ALLOW_DATA_LOSS ed è necessario correggere alcuni errori di allocazione, durante questa fase vengono implementate correzioni nel database.|Lo stato non viene segnalato.|  
|DBCC SYS CHECK|Durante questa fase vengono controllate le tabelle di sistema del database.|Lo stato viene segnalato a livello di pagina del database.<br /><br /> Il valore del report di stato viene aggiornato ogni 1000 pagine del database controllate.|  
|DBCC SYS REPAIR|Se viene specificata l'opzione REPAIR_FAST, REPAIR_REBUILD o REPAIR_ALLOW_DATA_LOSS ed è necessario correggere alcuni errori relativi alle tabelle di sistema, durante questa fase vengono implementate correzioni nel database.|Lo stato viene segnalato a livello di singola correzione.<br /><br /> Il contatore viene aggiornato ogni volta che viene completata una correzione.|  
|DBCC SSB CHECK|Durante questa fase vengono controllati gli oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker.<br /><br /> Nota: questa fase non viene completata quando viene eseguito il comando DBCC CHECKTABLE.|Lo stato non viene segnalato.|  
|DBCC CHECKCATALOG|Durante questa fase viene controllata la consistenza dei cataloghi del database.<br /><br /> Nota: questa fase non viene completata quando viene eseguito il comando DBCC CHECKTABLE.|Lo stato non viene segnalato.|  
|DBCC IVIEW CHECK|Durante questa fase viene controllata la consistenza logica di tutte le viste indicizzate presenti nel database.|Lo stato viene segnalato a livello di singola vista del database controllata.|  
  
## <a name="informational-statements"></a>Istruzioni informative  
  
|||  
|-|-|  
|[DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)|[DBCC SHOWCONTIG](../../t-sql/database-console-commands/dbcc-showcontig-transact-sql.md)|  
|[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)|[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)|  
|[DBCC OUTPUTBUFFER](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)|[DBCC TRACESTATUS](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)|  
|[DBCC PROCCACHE](../../t-sql/database-console-commands/dbcc-proccache-transact-sql.md)|[DBCC USEROPTIONS](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)|  
|[DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)||  
  
## <a name="validation-statements"></a>Istruzioni di convalida  
  
|||  
|-|-|  
|[DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)|[DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)|  
|[DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)|[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)|  
|[DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)|[DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)|  
|[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)||  
  
## <a name="maintenance-statements"></a>Istruzioni di manutenzione  
  
|||  
|-|-|  
|[DBCC CLEANTABLE](../../t-sql/database-console-commands/dbcc-cleantable-transact-sql.md)|[DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)|  
|[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)|[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)|  
|[DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)|[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)|  
|[DBCC FREEPROCCACHE](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)|[DBCC UPDATEUSAGE](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)|  
  
## <a name="miscellaneous-statements"></a>Istruzioni varie  
  
|||  
|-|-|  
|[DBCC dllname (FREE)](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)|[DBCC HELP](../../t-sql/database-console-commands/dbcc-help-transact-sql.md)|  
|[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)|[DBCC TRACEOFF](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)|  
|[DBCC FREESESSIONCACHE](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)|[DBCC TRACEON](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)|  
|[DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)|[DBCC CLONEDATABASE](../../t-sql/database-console-commands/dbcc-clonedatabase-transact-sql.md) <br /><br /> **Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] da SP2 fino a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
  
