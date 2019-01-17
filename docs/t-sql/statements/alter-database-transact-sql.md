---
title: ALTER DATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-current||=azuresqldb-mi-current||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9eb95a89fa8539eede53a154f7e7087a3f31f71b
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135321"
---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE (Transact-SQL)

Consente di modificare alcune opzioni di configurazione di un database. 

Questo articolo fornisce la sintassi, gli argomenti, la sezione Osservazioni, le autorizzazioni ed esempi per qualsiasi prodotto SQL scelto.

Per altre informazioni sulle convenzioni di sintassi, vedere [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="click-a-product"></a>Fare clic su un prodotto.

Nella riga seguente fare clic su qualsiasi nome di prodotto. Viene visualizzato contenuto diverso in questa pagina Web, appropriato per il prodotto su cui si fa clic.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]  
> ||||||  
> |---|---|---|---|---|  
> |**_\* SQL Server \*_** &nbsp;|[Database SQL<br />server logico](alter-database-transact-sql.md?view=azuresqldb-current)|[Database SQL<br />Istanza gestita](alter-database-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-database-transact-sql.md?view=azure-sqldw-latest)|[Parallel<br />Data Warehouse](alter-database-transact-sql.md?view=aps-pdw-2016)|  

&nbsp;

## <a name="sql-server"></a>SQL Server

## <a name="overview"></a>Panoramica

In SQL Server, questa istruzione consente di modificare un database oppure i file e i filegroup associati al database. Consente di aggiungere o rimuovere file e filegroup in un database, modificare gli attributi di un database oppure dei relativi file e filegroup, modificare le regole di confronto e impostare le opzioni del database. Non è possibile modificare snapshot di database. Per la modifica delle opzioni di database associate alla replica, usare [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  

A causa della lunghezza, la sintassi di ALTER DATABASE è separata in più articoli.  

ALTER DATABASE  
L'articolo corrente fornisce la sintassi e le informazioni correlate per la modifica del nome e delle regole di confronto di un database.  
  
[Opzioni file e filegroup ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
Fornisce la sintassi e le informazioni correlate per l'aggiunta e la rimozione di file e filegroup da un database e per la modifica degli attributi di file e filegroup.  
  
[Opzioni ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
Fornisce la sintassi e le informazioni correlate per la modifica degli attributi di un database utilizzando le opzioni SET di ALTER DATABASE.  
  
[Mirroring del database ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)  
Include la sintassi e le informazioni correlate per le opzioni SET di ALTER DATABASE relative al mirroring del database.  
  
[ALTER DATABASE SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)  
Specifica la sintassi e le informazioni correlate per le opzioni [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] di ALTER DATABASE per la configurazione di un database secondario in una replica secondaria di un gruppo di disponibilità AlwaysOn.  
  
[Livello di compatibilità di ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
Include la sintassi e le informazioni correlate per le opzioni SET di ALTER DATABASE relative ai livelli di compatibilità del database.  
  
## <a name="syntax"></a>Sintassi  
  
```
-- SQL Server Syntax  
ALTER DATABASE { database_name  | CURRENT }  
{  
    MODIFY NAME = new_database_name   
  | COLLATE collation_name  
  | <file_and_filegroup_options>  
  | SET <option_spec> [ ,...n ] [ WITH <termination> ] 
  | SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 | 90 }   
  
}  
[;]  
  
<file_and_filegroup_options>::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  
  
<option_spec>::=  
  <auto_option> ::=
  <change_tracking_option> ::=  
  <cursor_option> ::=
  <database_mirroring_option> ::=
  <date_correlation_optimization_option> ::=  
  <db_encryption_option> ::=  
  <db_state_option> ::=  
  <db_update_option> ::=  
  <db_user_access_option> ::=  <delayed_durability_option> ::=  <external_access_option> ::=  
  <FILESTREAM_options> ::=  
  <HADR_options> ::=
  <parameterization_option> ::=  
  <query_store_options> ::=  
  <recovery_option> ::=
  <service_broker_option> ::=  
  <snapshot_option> ::=  
  <sql_option> ::=   
  <termination> ::=  
 
<compatibility_level>
   { 140 | 130 | 120 | 110 | 100 | 90 }   
```  
  
## <a name="arguments"></a>Argomenti  
*database_name*  
Nome del database da modificare.  
  
> [!NOTE]  
>  Questa opzione non è disponibile in un database indipendente.  
  
CURRENT  
**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Specifica che il database corrente in uso deve essere modificato.  
  
MODIFY NAME = **=**_new_database_name_  
Rinomina il database con il nome specificato come *new_database_name*.  
  
COLLATE *collation_name*  
Specifica le regole di confronto per il database. In *collation_name* è possibile usare nomi di regole di confronto di Windows o SQL. Se omesso, al database vengono assegnate le regole di confronto dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]
> Le regole di confronto non possono essere modificate dopo la creazione del database in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
Quando si creano database con regole di confronto diverse da quelle predefinite, i dati nel database rispettano sempre le regole di confronto specificate. Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quando si crea un database indipendente, le informazioni del catalogo interno vengono mantenute usando le regole di confronto predefinite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ovvero **Latin1_General_100_CI_AS_WS_KS_SC**.  
  
Per altre informazioni sui nomi di regole di confronto Windows e SQL, vedere [COLLATE](~/t-sql/statements/collations.md).  
  
**\<delayed_durability_option> ::=**  
**Si applica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Per altre informazioni, vedere [Opzioni di ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md) e [Controllo della durabilità delle transazioni](../../relational-databases/logs/control-transaction-durability.md).  
  
**\<file_and_filegroup_options>::=**  
Per altre informazioni, vedere [Opzioni per file e filegroup ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="remarks"></a>Remarks  
Per rimuovere un database usare [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
  
Per ridurre le dimensioni di un database, usare [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
L'istruzione ALTER DATABASE deve essere eseguita in modalità autocommit (modalità predefinita di gestione delle transazioni) e non è consentita in una transazione esplicita o implicita.  
  
Lo stato di un file di database, ad esempio online o offline, viene mantenuto indipendentemente dallo stato del database. Per altre informazioni, vedere [Stati del file](../../relational-databases/databases/file-states.md). Lo stato dei file all'interno di un filegroup determina la disponibilità dell'intero filegroup. Un filegroup è disponibile se tutti i file in esso inclusi sono online. Se un filegroup è offline, qualsiasi tentativo di accesso al filegroup tramite un'istruzione SQL avrà esito negativo e verrà generato un errore. Per la compilazione di piani delle query per istruzioni SELECT, Query Optimizer evita gli indici non cluster e le viste indicizzate presenti in filegroup offline. Ciò consente la corretta esecuzione di tali istruzioni. Se tuttavia il filegroup offline contiene l'indice cluster o heap della tabella di destinazione, l'istruzione SELECT avrà esito negativo, così come tutte le istruzioni INSERT, UPDATE o DELETE che implicano la modifica di una tabella tramite un indice incluso in un filegroup offline.  
  
Quando un database è nello stato RESTORING, la maggior parte delle istruzioni ALTER DATABASE avrà esito negativo. Un'alternativa consiste nell'impostare le opzioni di mirroring del database. Lo stato RESTORING può essere impostato durante un'operazione di ripristino attiva o quando un'operazione di ripristino di un database o di un file di log ha esito negativo a causa di un file di backup danneggiato.  
  
La cache dei piani per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene cancellata quando si imposta una delle opzioni seguenti.  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY|PAGE_VERIFY|  
  
La cancellazione della cache dei piani comporta la ricompilazione di tutti i piani di esecuzione successivi e può causare un peggioramento improvviso e temporaneo delle prestazioni di esecuzione delle query. Il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene il messaggio informativo seguente per ogni archivio cache cancellato nella cache dei piani: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha rilevato %d occorrenza/e di scaricamento dell'archivio cache '%s' (parte della cache dei piani) a causa di operazioni di manutenzione o riconfigurazione del database". Questo messaggio viene registrato ogni cinque minuti per tutta la durata dello scaricamento della cache.  
  
La cache delle procedure viene inoltre scaricata negli scenari seguenti:  
  
- L'opzione AUTO_CLOSE di un database è impostata su ON. Se il database non viene utilizzato da alcuna connessione utente, neanche come riferimento, tramite l'attività in background viene effettuato il tentativo di chiusura e di arresto automatici del database.  
- Vengono eseguite diverse query su un database contenente opzioni predefinite. Successivamente, il database viene eliminato.  
- Viene eliminato uno snapshot del database per un database di origine.  
- Viene ricompilato correttamente il log delle transazioni per un database.  
- Viene ripristinato un backup del database.  
- Viene scollegato un database.  
  
## <a name="changing-the-database-collation"></a>Modifica delle regole di confronto del database  
Prima di applicare regole di confronto diverse a un database, verificare che siano soddisfatte le condizioni seguenti:  
  
- Nessun altro utente sta utilizzando il database.  
- Nessun oggetto associato a schema dipende dalle regole di confronto del database.  
  
  Se il database contiene gli oggetti seguenti che dipendono dalle regole di confronto del database, l'istruzione ALTER DATABASE*database_name*COLLATE avrà esito negativo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituirà un messaggio di errore per ogni oggetto che blocca l'azione ALTER:  
  
  - Funzioni definite dall'utente e viste create con SCHEMABINDING.  
  
  - Colonne calcolate.  
  
  - Vincoli CHECK.  
  
  - Funzioni con valori di tabella che restituiscono tabelle contenenti colonne di tipo carattere con regole di confronto ereditate dalle regole di confronto predefinite del database.  
  
    Le informazioni sulle dipendenze per le entità non associate a schemi vengono aggiornate automaticamente quando vengono modificate le regole di confronto del database.  
  
La modifica delle regole di confronto del database non comporta la creazione di duplicati per i nomi di sistema degli oggetti di database. Se la modifica delle regole di confronto genera nomi duplicati, gli spazi dei nomi seguenti potrebbero impedire tale modifica:  
  
- Nomi di oggetti, quali stored procedure, tabelle, trigger e viste.  
- Nomi di schemi.  
- Entità, come gruppi, ruoli o utenti.  
- Nomi di tipi di dati scalari, come i tipi di dati di sistema e definiti dall'utente.  
- Nomi di cataloghi full-text.  
- Nomi di colonne o parametri in un oggetto.  
- Nomi di indici in una tabella.  
  
Se vengono generati nomi duplicati in seguito all'applicazione delle nuove regole di confronto, l'azione di modifica avrà esito negativo e in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà visualizzato un messaggio di errore che indica lo spazio dei nomi in cui è stato identificato il duplicato.  
  
## <a name="viewing-database-information"></a>Visualizzazione delle informazioni sui database  
Per restituire informazioni su database, file e filegroup, è possibile usare viste del catalogo, funzioni di sistema e stored procedure di sistema.  
  
## <a name="permissions"></a>Permissions  
È richiesta l'autorizzazione ALTER per il database.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-changing-the-name-of-a-database"></a>A. Modifica del nome di un database  
Nell'esempio seguente il nome del database `AdventureWorks2012` viene modificato in `Northwind`.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
### <a name="b-changing-the-collation-of-a-database"></a>b. Modifica delle regole di confronto del database  
Nell'esempio seguente viene creato un database denominato `testdb` con le regole di confronto `SQL_Latin1_General_CP1_CI_A`S, quindi vengono modificate le regole di confronto del database `testdb` in `COLLATE French_CI_AI`.  
  
**Si applica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
USE master;  
GO  
  
CREATE DATABASE testdb  
COLLATE SQL_Latin1_General_CP1_CI_AS ;  
GO  
  
ALTER DATABASE testDB  
COLLATE French_CI_AI ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
- [CREATE DATABASE](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
- [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
- [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
- [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
- [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
- [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
- [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
- [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
- [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
- [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
- [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
- [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
- [Database di sistema.](../../relational-databases/databases/system-databases.md)  

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]  
> ||||||  
> |---|---|---|---|---|  
> |[SQL Server](alter-database-transact-sql.md?view=sql-server-2016)|**_\* Database SQL<br />server logico \*_** &nbsp;|[Database SQL<br />Istanza gestita](alter-database-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-database-transact-sql.md?view=azure-sqldw-latest)|[Parallel<br />Data Warehouse](alter-database-transact-sql.md?view=aps-pdw-2016)|  

&nbsp;

## <a name="azure-sql-database-logical-server"></a>Server logico di database SQL di Azure

## <a name="overview"></a>Panoramica

Nel database SQL di Azure usare questa istruzione per modificare un database in un server logico. Usare questa istruzione per modificare il nome di un database, modificare l'obiettivo di servizio e l'edizione del database, creare un join con o rimuovere il database da un pool elastico, impostare le opzioni di database, aggiungere o rimuovere il database come database secondario in una relazione di replica geografica e impostare il livello di compatibilità del database.

A causa della lunghezza, la sintassi di ALTER DATABASE è separata in più articoli.  

ALTER DATABASE  
L'articolo corrente fornisce la sintassi e le informazioni correlate per la modifica del nome e delle regole di confronto di un database.  
  
[Opzioni ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md?&tabs=sqldbls)  
Fornisce la sintassi e le informazioni correlate per la modifica degli attributi di un database utilizzando le opzioni SET di ALTER DATABASE.  
  
[Livello di compatibilità di ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?&tabs=sqldbls)  
Include la sintassi e le informazioni correlate per le opzioni SET di ALTER DATABASE relative ai livelli di compatibilità del database.  

## <a name="syntax"></a>Sintassi 

```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name | CURRENT }  
{  
    MODIFY NAME = new_database_name  
  | MODIFY ( <edition_options> [, ... n] ) 
  | SET { <option_spec> [ ,... n ] WITH <termination>} 
  | SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }   
  | ADD SECONDARY ON SERVER <partner_server_name>  
    [WITH ( <add-secondary-option>::= [, ... n] ) ]  
  | REMOVE SECONDARY ON SERVER <partner_server_name>  
  | FAILOVER  
  | FORCE_FAILOVER_ALLOW_DATA_LOSS  
}  
[;] 

<edition_options> ::= 
{  

  MAXSIZE = { 100 MB | 250 MB | 500 MB | 1 ... 1024 ... 4096 GB }  
  | EDITION = { 'basic' | 'standard' | 'premium' | 'GeneralPurpose' | 'BusinessCritical' 'Hyperscale'} 
  | SERVICE_OBJECTIVE = 
       {  <service-objective>
       | { ELASTIC_POOL (name = <elastic_pool_name>) } 
       } 
}  

<add-secondary-option> ::=  
   {  
      ALLOW_CONNECTIONS = { ALL | NO }  
     | SERVICE_OBJECTIVE = 
       {  <service-objective> 
       | { ELASTIC_POOL ( name = <elastic_pool_name>) } 
       } 
   }  

<service-objective> ::=  { 'S0' | 'S1' | 'S2' | 'S3'| 'S4'| 'S6'| 'S7'| 'S9'| 'S12' |
       | 'P1' | 'P2' | 'P4'| 'P6' | 'P11'  | 'P15'
      | 'GP_GEN4_1' | 'GP_GEN4_2' | 'GP_GEN4_4' | 'GP_GEN4_8' | 'GP_GEN4_16' | 'GP_GEN4_24' |
      | 'BC_GEN4_1' | 'BC_GEN4_2' | 'BC_GEN4_4' | 'BC_GEN4_8' | 'BC_GEN4_16' | 'BC_GEN4_24' |
      | 'HS_GEN4_1' | 'HS_GEN4_2' | 'HS_GEN4_4' | 'HS_GEN4_8' | 'HS_GEN4_16' | 'HS_GEN4_24' |
      | 'GP_GEN5_2' | 'GP_GEN5_4' | 'GP_GEN5_8' | 'GP_GEN5_16' | 'GP_GEN5_24' | 'GP_GEN5_32' | 'GP_GEN5_48' | 'GP_GEN5_80' |
      | 'BC_GEN5_2' | 'BC_GEN5_4' | 'BC_GEN5_8' | 'BC_GEN5_16' | 'BC_GEN5_24' | 'BC_GEN5_32' | 'BC_GEN5_48' | 'BC_GEN5_80' |
      | 'HS_GEN5_2' | 'HS_GEN5_4' | 'HS_GEN5_8' | 'HS_GEN5_16' | 'HS_GEN5_24' | 'HS_GEN5_32' | 'HS_GEN5_48' | 'HS_GEN5_80' |
      }

<option_spec> ::= 
{  
    <auto_option> 
  | <change_tracking_option> 
  | <cursor_option> 
  | <db_encryption_option>  
  | <db_update_option> 
  | <db_user_access_option> 
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option> 
  | <target_recovery_time_option> 
  | <termination>  
  | <temporal_history_retention>  
}  
```
  
## <a name="arguments"></a>Argomenti  

*database_name*  

Nome del database da modificare.  
  
CURRENT  

Specifica che il database corrente in uso deve essere modificato.  
  
MODIFY NAME = **=**_new_database_name_  

Rinomina il database con il nome specificato come *new_database_name*. Nell'esempio seguente il nome di un database `db1` viene modificato in `db2`:   

```sql  
ALTER DATABASE db1  
    MODIFY Name = db2 ;  
```    

MODIFY (EDITION **=** ['basic' | 'standard' | 'premium' |'GeneralPurpose' | 'BusinessCritical' | 'Hyperscale'])    

Modifica il livello di servizio del database. 

Nell'esempio seguente l'edizione viene modificata in `premium`:
  
```sql  
ALTER DATABASE current 
    MODIFY (EDITION = 'premium');
``` 

La modifica di EDITION ha esito negativo se la proprietà MAXSIZE per il database è impostata su un valore non compreso nell'intervallo valido supportato da questa edizione.  

MODIFY (MAXSIZE **=** [100 MB | 500 MB | 1 | 1024...4096] GB)  

Specifica le dimensioni massime del database. Le dimensioni massime devono essere conformi al set valido di valori per la proprietà EDITION del database. La modifica delle dimensioni massime del database può causare la modifica del valore di EDITION del database. 

> [!NOTE]
> L'argomento **MAXSIZE** non è applicabile ai singoli database nel livello di servizio Hyperscale. I database di livello Hyperscale possono crescere in base alle necessità, fino a 100 TB. Il servizio database SQL aggiunge automaticamente l'archiviazione: non è necessaria impostare le dimensioni massime.

**Modello basato su DTU**

|**MAXSIZE**|**Base**|**S0-S2**|**S3-S12**|**P1-P6**|**P11-P15**|  
|-----------------|---------------|------------------|-----------------|-----------------|-----------------|-----------------|  
|100 MB|√|√|√|√|√|  
|250 MB|√|√|√|√|√|  
|500 MB|√|√|√|√|√|  
|1 GB|√|√|√|√|√|  
|2 GB|√ (P)|√|√|√|√|  
|5 GB|N/D|√|√|√|√|  
|10 GB|N/D|√|√|√|√|  
|20 GB|N/D|√|√|√|√|  
|30 GB|N/D|√|√|√|√|  
|40 GB|N/D|√|√|√|√|  
|50 GB|N/D|√|√|√|√|  
|100 GB|N/D|√|√|√|√|  
|150 GB|N/D|√|√|√|√|  
|200 GB|N/D|√|√|√|√|  
|250 GB|N/D|√ (P)|√ (P)|√|√|  
|300 GB|N/D|√|√|√|√|  
|400 GB|N/D|√|√|√|√|  
|500 GB|N/D|√|√|√ (P)|√|  
|750 GB|N/D|√|√|√|√|  
|1024 GB|N/D|√|√|√|√ (P)|  
|Da 1024 GB fino a 4096 GB con incrementi di 256 GB*|N/D|N/D|N/D|N/D|√|√|  
  
\* P11 e P15 consentono un valore massimo di MAXSIZE pari a 4 TB. Le dimensioni predefinite sono 1024 GB.  P11 e P15 possono usare fino a 4 TB di spazio di archiviazione incluso senza addebiti aggiuntivi. Nel livello Premium, MAXSIZE maggiore di 1 TB è attualmente disponibile nelle aree seguenti: Stati Uniti orientali 2, Stati Uniti occidentali, US Gov Virginia, Europa occidentale, Germania centrale, Asia sud-orientale, Giappone orientale, Australia orientale, Canada centrale e Canada orientale. Per altri dettagli relativi ai limiti delle risorse per il modello basato su DTU, vedere [DTU-based resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) (Limiti delle risorse basate su DTU).  

Il valore MAXSIZE per il modello basato su DTU, se specificato, deve essere un valore valido presente nella tabella precedente per il livello di servizio specificato.
 
**Modello basato su vCore**

**Livello di servizio Utilizzo generico: piattaforma di calcolo generazione 4**
|MAXSIZE|GP_Gen4_1|GP_Gen4_2|GP_Gen4_4|GP_Gen4_8|GP_Gen4_16|GP4_24|
|:--- | --: |--: |--: |--: |--: |--:|
|Dimensioni massime dei dati (GB)|1024|1024|1536|3072|4096|4096|

**Livello di servizio Utilizzo generico: piattaforma di calcolo generazione 5**
|MAXSIZE|GP_Gen5_2|GP_Gen5_4|GP_Gen5_8|GP_Gen5_16|GP_Gen5_24|GP_Gen5_32|GP_Gen5_48|GP_Gen5_80|
|:----- | ------: |-------: |-------: |--------: |--------: |---------:|--------: |---------: |
|Dimensioni massime dei dati (GB)|1024|1024|1536|3072|4096|4096|4096|4096|


**Livello di servizio Business critical: piattaforma di calcolo generazione 4**
|Livello di prestazioni|BC_Gen4_1|BC_Gen4_2|BC_Gen4_4|BC_Gen4_8|BC_Gen4_16|
|:--- | --: |--: |--: |--: |--: |--: |
|Dimensioni massime dei dati (GB)|1024|1024|1024|1024|1024|1024|

**Livello di servizio Business critical: piattaforma di calcolo generazione 5**
|MAXSIZE|BC_Gen5_2|BC_Gen5_4|BC_Gen5_8|BC_Gen5_16|BC_Gen5_24|BC_Gen5_32|BC_Gen5_48|BC_Gen5_80|
|:----- | ------: |-------: |-------: |--------: |--------: |---------:|--------: |---------: |
|Dimensioni massime dei dati (GB)|1024|1024|1024|1024|2048|4096|4096|4096|

Se non viene impostato alcun `MAXSIZE`valore quando viene usato il modello vCore, il valore predefinito è 32 GB. Per altri dettagli relativi ai limiti delle risorse per il modello basato su vCore, vedere [Limiti delle risorse basati su vCore](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits).
  
Le seguenti regole vengono applicate agli argomenti MAXSIZE ed EDITION:  
  
- Se il valore di EDITION è specificato e il valore di MAXSIZE viene omesso, viene utilizzato il valore predefinito dell'edizione. Ad esempio, se EDITION è impostato su Standard e MAXSIZE non è specificato, il valore di MAXSIZE viene automaticamente impostato su 500 MB.  
  
- Se né MAXSIZE né EDITION sono specificati, EDITION viene impostato su Standard (S0) e MAXSIZE viene impostato su 250 GB.  

MODIFY (SERVICE_OBJECTIVE = \<service-objective>)  

Specifica il livello di prestazioni. Nell'esempio seguente l'obiettivo di servizio di un database Premium viene modificato in `P6`:
 
```sql  
ALTER DATABASE current 
    MODIFY (SERVICE_OBJECTIVE = 'P6');
```  

Specifica il livello di prestazioni. I valori disponibili per l'obiettivo di servizio sono: `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`,    `GP_Gen5_8`,    `GP_Gen5_16`,   `GP_Gen5_24`,   `GP_Gen5_32`,   `GP_Gen5_48`,   `GP_Gen5_80`, `BC_Gen5_2`,  `BC_Gen5_4`,    `BC_Gen5_8`,    `BC_Gen5_16`,   `BC_Gen5_24`,   `BC_Gen5_32`,   `BC_Gen5_48`,   `BC_Gen5_80`, `HS_GEN4_1` `HS_GEN4_2` `HS_GEN4_4` `HS_GEN4_8` `HS_GEN4_16`, `HS_GEN4_24`, `HS_Gen5_2`,  `HS_Gen5_4`,    `HS_Gen5_8`,    `HS_Gen5_16`,   `HS_Gen5_24`,   `HS_Gen5_32`,   `HS_Gen5_48`,   `HS_Gen5_80`.  

Per le descrizioni degli obiettivi di servizio e altre informazioni su dimensioni, edizioni e combinazioni di obiettivi di servizio, vedere [Azure SQL Database Service Tiers and Performance Levels](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) (Livelli di servizio e livelli di prestazioni del database SQL di Azure), [DTU-based resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) (Limiti delle risorse basate su DTU) e [vCore-based resource limits](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits) (Limiti delle risorse basate su vCore). Il supporto per gli obiettivi di servizio PRS è stato rimosso. In caso di domande, usare l'alias di posta elettronica seguente: premium-rs@microsoft.com. 
  
MODIFY (SERVICE_OBJECTIVE = ELASTIC\_POOL (name = \<elastic_pool_name>)  

Per aggiungere un database esistente a un pool elastico, impostare SERVICE_OBJECTIVE del database su ELASTIC_POOL e specificare il nome del pool elastico. È anche possibile usare questa opzione per modificare il database in un pool elastico all'interno dello stesso server. Per altre informazioni, vedere [Creare e gestire un pool elastico in un database SQL](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/). Per rimuovere un database da un pool elastico, usare ALTER DATABASE per impostare SERVICE_OBJECTIVE su un livello di prestazioni di un unico database.  

> [!NOTE]
> I database con livello di servizio Hyperscale non possono essere aggiunti a un pool elastico.

ADD SECONDARY ON SERVER \<partner_server_name>  

Crea un database secondario con replica geografica usando lo stesso nome in un server partner e trasformando il database locale in un database con replica geografica. Avvia la replica asincrona dei dati dal database primario nel nuovo database secondario. Se esiste già un database con lo stesso nome nel database secondario, il comando non riesce. Il comando viene eseguito nel database master sul server che ospita il database locale, il quale diventa il database primario.  

> [!IMPORTANT]
> Il livello di servizio Hyperscale non supporta attualmente la replica geografica.
  
WITH ALLOW_CONNECTIONS { **ALL** | NO }  

Se non si specifica ALLOW_CONNECTION, il valore ALL viene impostato per impostazione predefinita. Se viene impostato ALL, il database è di sola lettura e consente a tutti gli account che hanno le autorizzazioni necessarie di connettersi.  
  
WITH SERVICE_OBJECTIVE {  `S0`, `S1`, `S2`, `S3`, `S4`, `S6`, `S7`, `S9`, `S12`, `P1`, `P2`, `P4`, `P6`, `P11`, `P15`, `GP_GEN4_1`, `GP_GEN4_2`, `GP_GEN4_4`, `GP_GEN4_8`, `GP_GEN4_16`, `GP_GEN4_24`, `BC_GEN4_1` `BC_GEN4_2` `BC_GEN4_4` `BC_GEN4_8` `BC_GEN4_16`, `BC_GEN4_24`, `GP_Gen5_2`, `GP_Gen5_4`,    `GP_Gen5_8`,    `GP_Gen5_16`,   `GP_Gen5_24`,   `GP_Gen5_32`,   `GP_Gen5_48`,   `GP_Gen5_80`, `BC_Gen5_2`,  `BC_Gen5_4`,    `BC_Gen5_8`,    `BC_Gen5_16`,   `BC_Gen5_24`,   `BC_Gen5_32`,   `BC_Gen5_48`,   `BC_Gen5_80` }  

Se non si specifica SERVICE_OBJECTIVE, il database secondario viene creato allo stesso livello di servizio del database primario. Se si specifica SERVICE_OBJECTIVE, il database secondario viene creato al livello specificato. Questa opzione supporta la creazione di database secondari con replica geografica con livelli di servizio meno costosi. Il valore SERVICE_OBJECTIVE specificato deve rientrare nella stessa edizione dell'origine. Ad esempio, non è possibile specificare S0 se l'edizione è Premium.  
  
ELASTIC_POOL (name = \<elastic_pool_name>)  

Se non si specifica ELASTIC_POOL, il database secondario non viene creato in un pool elastico. Se si specifica ELASTIC_POOL, il database secondario viene creato nel pool specificato.  
  
> [!IMPORTANT]  
>  Chi esegue il comando ADD SECONDARY deve avere il ruolo DBManager nel server primario, db_owner membership nel database locale e DBManager nel server secondario.  
  
REMOVE SECONDARY ON SERVER  \<partner_server_name>  

Rimuove il database secondario con replica geografica nel server specificato. Il comando viene eseguito nel database master sul server che ospita il database primario.  
  
> [!IMPORTANT]  
>  Chi esegue il comando REMOVE SECONDARY deve avere il ruolo DBManager nel server primario.  
  
FAILOVER  

Alza di livello il database secondario nella relazione con replica geografica in cui il comando viene eseguito perché il database diventi primario e abbassa di livello il database corrente perché diventi il nuovo database secondario. Durante questo processo, la modalità di replica geografica passa temporaneamente dalla modalità asincrona alla modalità sincrona. Durante il processo di failover:  
  
1.  Il database primario non accetta più nuove transazioni.  
  
2.  Tutte le transazioni in sospeso vengono scaricate nel database secondario.  
  
3.  Il database secondario diventa il database primario e la replica geografica asincrona viene avviata con il database primario precedente e il nuovo database secondario.  
  
Questa sequenza impedisce la perdita di dati. I due database non sono disponibili generalmente per un periodo di tempo compreso tra 0 e 25 secondi, il tempo necessario per lo scambio dei ruoli. L'operazione totale non richiederà più di un minuto circa. Se il database primario non è disponibile quando viene eseguito questo comando, il comando ha esito negativo e genera un messaggio di errore indicando che il database primario non è disponibile. Se il processo di failover non viene completato e sembra bloccato, è possibile usare il comando per forzare il failover e accettare la perdita di dati. Se è necessario recuperare i dati persi, chiamare la metodologia DevOps (CSS).  
  
> [!IMPORTANT]  
>  Chi esegue il comando FAILOVER deve avere il ruolo DBManager sia nel server primario sia nel server secondario.  
  
FORCE_FAILOVER_ALLOW_DATA_LOSS  

Alza di livello il database secondario nella relazione con replica geografica in cui il comando viene eseguito perché il database diventi primario e abbassa di livello il database corrente perché diventi il nuovo database secondario. Usare questo comando solo quando il database primario corrente non è più disponibile. È progettato per essere usato solo in caso di ripristino di emergenza, quando la disponibilità di ripristino è critica e la perdita di dati è accettabile.  
  
Durante un failover forzato:  
  
1. Il database secondario specificato diventa immediatamente il database primario e inizia ad accettare nuove transazioni.  
  
2. Quando il database primario originale si riconnette al nuovo database primario, viene eseguito un backup incrementale nel database primario originale e il database primario originale diventa un nuovo database secondario.  
  
3. Per ripristinare i dati da questo backup incrementale nel database primario precedente, è necessario usare la metodologia DevOps/CSS.  
  
4. Se esistono altri database secondari, vengono riconfigurati automaticamente per diventare i database secondari del nuovo database primario. Questo processo è asincrono. Fino al suo completamento, è possibile assistere a un ritardo. Quando la riconfigurazione è completa, i database secondari continuano a essere database secondari del database primario precedente.  
  
> [!IMPORTANT]  
>  Chi esegue il comando FORCE_FAILOVER_ALLOW_DATA_LOSS deve avere il ruolo DBManager sia nel server primario sia nel server secondario.  
  
## <a name="remarks"></a>Remarks  

Per rimuovere un database usare [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
Per ridurre le dimensioni di un database, usare [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
L'istruzione ALTER DATABASE deve essere eseguita in modalità autocommit (modalità predefinita di gestione delle transazioni) e non è consentita in una transazione esplicita o implicita.  
  
La cancellazione della cache dei piani comporta la ricompilazione di tutti i piani di esecuzione successivi e può causare un peggioramento improvviso e temporaneo delle prestazioni di esecuzione delle query. Il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene il messaggio informativo seguente per ogni archivio cache cancellato nella cache dei piani: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha rilevato %d occorrenza/e di scaricamento dell'archivio cache '%s' (parte della cache dei piani) a causa di operazioni di manutenzione o riconfigurazione del database". Questo messaggio viene registrato ogni cinque minuti per tutta la durata dello scaricamento della cache.  
  
La cache delle procedure viene inoltre scaricata nello scenario seguente: Vengono eseguite diverse query su un database contenente opzioni predefinite. Successivamente, il database viene eliminato.    
  
## <a name="viewing-database-information"></a>Visualizzazione delle informazioni sui database  

Per restituire informazioni su database, file e filegroup, è possibile usare viste del catalogo, funzioni di sistema e stored procedure di sistema.  
  
## <a name="permissions"></a>Permissions  

Solo l'account di accesso dell'entità a livello di server (creato dal processo di provisioning) o i membri del ruolo del database `dbmanager` possono modificare un database.  
  
> [!IMPORTANT]  
>  Il proprietario del database può modificare il database solo se è un membro del ruolo `dbmanager`.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-check-the-edition-options-and-change-them"></a>A. Controllare le opzioni di edizione e modificarle:

```sql
SELECT Edition = DATABASEPROPERTYEX('db1', 'EDITION'),
        ServiceObjective = DATABASEPROPERTYEX('db1', 'ServiceObjective'),
        MaxSizeInBytes =  DATABASEPROPERTYEX('db1', 'MaxSizeInBytes');

ALTER DATABASE [db1] MODIFY (EDITION = 'Premium', MAXSIZE = 1024 GB, SERVICE_OBJECTIVE = 'P15');
```

### <a name="b-moving-a-database-to-a-different-elastic-pool"></a>b. Spostare un database in un pool elastico diverso  

Sposta un database esistente in un pool denominato pool1:  
  
```sql  
ALTER DATABASE db1   
MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL ( name = pool1 ) ) ;  
```  
  
### <a name="c-add-a-geo-replication-secondary"></a>C. Aggiungere un database secondario con replica geografica  

Crea un database secondario leggibile denominato db1 nel server `secondaryserver` di db1 nel server locale.  
  
```sql  
ALTER DATABASE db1   
ADD SECONDARY ON SERVER secondaryserver   
WITH ( ALLOW_CONNECTIONS = ALL )  
```  
  
### <a name="d-remove-a-geo-replication-secondary"></a>D. Rimuovere un database secondario con replica geografica  
 
Rimuove il database secondario db1 nel server `secondaryserver`.  
  
```sql  
ALTER DATABASE db1   
REMOVE SECONDARY ON SERVER testsecondaryserver   
```  
  
### <a name="e-failover-to-a-geo-replication-secondary"></a>E. Eseguire il failover di un database secondario con replica geografica  

Alza di livello un database secondario db1 nel server `secondaryserver` perché diventi il nuovo database primario quando viene eseguito nel server `secondaryserver`.  
  
```sql  
ALTER DATABASE db1 FAILOVER  
```  
  
## <a name="see-also"></a>Vedere anche
  
[CREATE DATABASE (Database SQL di Azure)](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqldbls)   
 [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
 [Database di sistema.](../../relational-databases/databases/system-databases.md)  

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]  
> ||||||  
> |---|---|---|---|---|  
> |[SQL Server](alter-database-transact-sql.md?view=sql-server-2016)|[Database SQL<br />server logico](alter-database-transact-sql.md?view=azuresqldb-current)|**_\* Database SQL<br />Istanza gestita \*_** &nbsp;|[SQL Data<br />Warehouse](alter-database-transact-sql.md?view=azure-sqldw-latest)|[Parallel<br />Data Warehouse](alter-database-transact-sql.md?view=aps-pdw-2016)|  

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Istanza gestita di database SQL di Azure

## <a name="overview"></a>Panoramica

Nell'Istanza gestita di database SQL di Azure usare questa istruzione per impostare le opzioni di database.

A causa della lunghezza, la sintassi di ALTER DATABASE è separata in più articoli.  

ALTER DATABASE  
L'articolo corrente fornisce la sintassi e informazioni correlate per impostare le opzioni di file e filegroup, le opzioni di database e il livello di compatibilità del database.  
  
[Opzioni per file e filegroup ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md?&tabs=sqldbmi) Fornisce la sintassi e le informazioni correlate per l'aggiunta e la rimozione di file e filegroup da un database e per la modifica degli attributi di file e filegroup.  
  
[Opzioni ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md?&tabs=sqldbmi) Fornisce la sintassi e le informazioni correlate per la modifica degli attributi di un database utilizzando le opzioni SET di ALTER DATABASE.  
  
[Livello di compatibilità ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md?&tabs=sqldbmi) Include la sintassi e le informazioni correlate per le opzioni SET di ALTER DATABASE relative ai livelli di compatibilità del database.  

## <a name="syntax"></a>Sintassi 

```  
-- Azure SQL Database Syntax  
ALTER DATABASE { database_name | CURRENT }  
{  
    <file_and_filegroup_options>  
  | SET <option_spec> [ ,...n ]  
  | SET COMPATIBILITY_LEVEL = { 140 | 130 | 120 | 110 | 100 }   
}  
[;] 

<file_and_filegroup_options>::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  

<option_spec> ::= 
{  
    <auto_option> 
  | <change_tracking_option> 
  | <cursor_option> 
  | <db_encryption_option>  
  | <db_update_option> 
  | <db_user_access_option> 
  | <delayed_durability_option>  
  | <parameterization_option>  
  | <query_store_options>  
  | <snapshot_option>  
  | <sql_option> 
  | <target_recovery_time_option> 
  | <temporal_history_retention>  
}  

```
  
## <a name="arguments"></a>Argomenti  

*database_name*  

Nome del database da modificare.  
  
CURRENT  

Specifica che il database corrente in uso deve essere modificato.  
  
## <a name="remarks"></a>Remarks  

Per rimuovere un database usare [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
Per ridurre le dimensioni di un database, usare [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
L'istruzione ALTER DATABASE deve essere eseguita in modalità autocommit (modalità predefinita di gestione delle transazioni) e non è consentita in una transazione esplicita o implicita.  
  
La cancellazione della cache dei piani comporta la ricompilazione di tutti i piani di esecuzione successivi e può causare un peggioramento improvviso e temporaneo delle prestazioni di esecuzione delle query. Il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene il messaggio informativo seguente per ogni archivio cache cancellato nella cache dei piani: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha rilevato %d occorrenza/e di scaricamento dell'archivio cache '%s' (parte della cache dei piani) a causa di operazioni di manutenzione o riconfigurazione del database". Questo messaggio viene registrato ogni cinque minuti per tutta la durata dello scaricamento della cache.  
  
La cache delle procedure viene inoltre scaricata nello scenario seguente: Vengono eseguite diverse query su un database contenente opzioni predefinite. Successivamente, il database viene eliminato.    
  
## <a name="viewing-database-information"></a>Visualizzazione delle informazioni sui database  

Per restituire informazioni su database, file e filegroup, è possibile usare viste del catalogo, funzioni di sistema e stored procedure di sistema.  
  
## <a name="permissions"></a>Permissions  

Solo l'account di accesso dell'entità a livello di server (creato dal processo di provisioning) o i membri del ruolo del database `dbmanager` possono modificare un database.  
  
> [!IMPORTANT]  
>  Il proprietario del database può modificare il database solo se è un membro del ruolo `dbmanager`.  
  
## <a name="examples"></a>Esempi
Gli esempi seguenti mostrano come impostare l'ottimizzazione automatica e come aggiungere un file in un'istanza gestita.

```sql
ALTER DATABASE WideWorldImporters
    SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON)

ALTER DATABASE WideWorldImporters
    ADD FILE (NAME = 'data_17')
```

## <a name="see-also"></a>Vedere anche
  
[CREATE DATABASE (Database SQL di Azure)](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqldbmi)   
[DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md)   
[DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md)   
[SET TRANSACTION ISOLATION LEVEL](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
[EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
[sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
[sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
[sys.database_mirroring_witnesses](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)  [sys.data_spaces](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
[sys.filegroups](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
[Database di sistema.](../../relational-databases/databases/system-databases.md)  

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]  
> ||||||  
> |---|---|---|---|---|  
> |[SQL Server](alter-database-transact-sql.md?view=sql-server-2016)|[Database SQL<br />server logico](alter-database-transact-sql.md?view=azuresqldb-current)|[Database SQL<br />Istanza gestita](alter-database-transact-sql.md?view=azuresqldb-mi-current)|**_\* SQL Data<br />Warehouse \*_** &nbsp;|[Parallel<br />Data Warehouse](alter-database-transact-sql.md?view=aps-pdw-2016)|  

&nbsp;

## <a name="azure-sql-data-warehouse"></a>Azure SQL Data Warehouse

## <a name="overview"></a>Panoramica

Modifica il nome, la dimensione massima o l'obiettivo di servizio per un database.

## <a name="syntax"></a>Sintassi  
  
```  
ALTER DATABASE database_name  

  MODIFY NAME = new_database_name  
| MODIFY ( <edition_option> [, ... n] )  
  
<edition_option> ::=   
      MAXSIZE = { 
            250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 
          | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 
          | 92160 | 102400 | 153600 | 204800 | 245760 
      } GB  
      | SERVICE_OBJECTIVE = { 
            'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' 
          | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' 
          | 'DW3000' | 'DW6000' | 'DW1000c' | 'DW1500c' | 'DW2000c' 
          | 'DW2500c' | 'DW3000c' | 'DW5000c' | 'DW6000c' | 'DW7500c' 
          | 'DW10000c' | 'DW15000c' | 'DW30000c'
      }  
```  
  
## <a name="arguments"></a>Argomenti  
*database_name*  
Specifica il nome del database da modificare.  

MODIFY NAME = *new_database_name*  
Rinomina il database con il nome specificato come *new_database_name*.  
  
MAXSIZE  
Il valore predefinito è 245.760 GB (240 TB).  

**Si applica a:** livello di prestazioni Ottimizzato per l'elasticità

Dimensioni massime consentite per il database. Le dimensioni del database non possono superare il valore di MAXSIZE. 

**Si applica a:** livello di prestazioni Ottimizzato per il calcolo

Dimensioni massime consentite per i dati rowstore nel database. Le dimensioni dei dati archiviati nelle tabelle rowstore, nel deltastore di un indice columnstore o in un indice non cluster in un indice columnstore cluster non possono superare MAXSIZE.  I dati compressi in formato columnstore non hanno un limite di dimensioni e non sono limitati dal valore MAXSIZE. 
  
SERVICE_OBJECTIVE  
Specifica il livello di prestazioni. Per altre informazioni sugli obiettivi di servizio per [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], vedere [Livelli di prestazioni](https://azure.microsoft.com/documentation/articles/performance-tiers/).  
  
## <a name="permissions"></a>Permissions  
Richiede le autorizzazioni seguenti:  
  
- Accesso principale di livello server (creato dal processo di provisioning) oppure  
- Membro del ruolo del database `dbmanager`.  
  
Il proprietario del database può modificare il database solo se è un membro del ruolo `dbmanager`.  
  
## <a name="general-remarks"></a>Osservazioni generali  
Poiché il database corrente deve essere un database diverso da quello in fase di modifica, **ALTER deve essere eseguito durante la connessione al database master**.  
  
SQL Data Warehouse è impostato su COMPATIBILITY_LEVEL 130 e non può essere modificato. Per altri dettagli, vedere [Improved Query Performance with Compatibility Level 130 in Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/) (Prestazioni di query migliorate con Compatibility Level 130 nel database SQL di Azure).
  
Per ridurre le dimensioni di un database, usare [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
Per eseguire ALTER DATABASE, il database deve essere online e non può essere in pausa.  
  
L'istruzione ALTER DATABASE deve essere eseguita in modalità autocommit, ovvero la modalità di gestione delle transazioni predefinita. Questa opzione è specificata nelle impostazioni di connessione.  
  
L'istruzione ALTER DATABASE non può essere parte di una transazione definita dall'utente.

Le regole di confronto del database non possono essere modificate.  
  
## <a name="examples"></a>Esempi  
Prima di eseguire questi esempi, verificare che il database da modificare non sia il database corrente. Poiché il database corrente deve essere un database diverso da quello in fase di modifica, **ALTER deve essere eseguito durante la connessione al database master**.  

### <a name="a-change-the-name-of-the-database"></a>A. Modificare il nome del database  

```sql  
ALTER DATABASE AdventureWorks2012  
MODIFY NAME = Northwind;  
```  
  
### <a name="b-change-max-size-for-the-database"></a>b. Modificare la dimensione massima del database  
  
```sql  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB );  
```  
  
### <a name="c-change-the-performance-level"></a>C. Modificare il livello di prestazioni  
  
```sql  
ALTER DATABASE dw1 MODIFY ( SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
### <a name="d-change-the-max-size-and-the-performance-level"></a>D. Modificare la dimensione massima e il livello di prestazioni  
  
```sql  
ALTER DATABASE dw1 MODIFY ( MAXSIZE=10240 GB, SERVICE_OBJECTIVE= 'DW1200' );  
```  
  
## <a name="see-also"></a>Vedere anche  
[CREATE DATABASE (Azure SQL Data Warehouse)](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqldw.md)
[Elenco degli articoli di riferimento di SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-reference/) 
 
::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]  
> ||||||  
> |---|---|---|---|---|  
> |[SQL Server](alter-database-transact-sql.md?view=sql-server-2016)|[Database SQL<br />server logico](alter-database-transact-sql.md?view=azuresqldb-current)|[Database SQL<br />Istanza gestita](alter-database-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](alter-database-transact-sql.md?view=azure-sqldw-latest)|**_\* Parallel<br />Data Warehouse \*_** &nbsp;|  

&nbsp;

## <a name="parallel-data-warehouse"></a>Parallel Data Warehouse

## <a name="overview"></a>Panoramica

Modifica le opzioni relative alle dimensioni massime del database per le tabelle replicate, le tabelle distribuite e il log delle transazioni in Parallel Data Warehouse. Usare questa istruzione per gestire le allocazioni dello spazio su disco per un database man mano che le sue dimensioni aumentano o diminuiscono. L'articolo descrive anche la sintassi correlata all'impostazione di opzioni di database in Parallel Data Warehouse.

## <a name="syntax"></a>Sintassi  
  
```  
-- Parallel Data Warehouse  
ALTER DATABASE database_name    
    SET ( <set_database_options>   | <db_encryption_option> )  
[;]  
  
<set_database_options> ::=   
{  
    AUTOGROW = { ON | OFF }  
    | REPLICATED_SIZE = size [GB]  
    | DISTRIBUTED_SIZE = size [GB]  
    | LOG_SIZE = size [GB]
    | SET AUTO_CREATE_STATISTICS { ON | OFF }
    | SET AUTO_UPDATE_STATISTICS { ON | OFF } 
    | SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF }
}  
  
<db_encryption_option> ::=  
    ENCRYPTION { ON | OFF }  
```  
  
## <a name="arguments"></a>Argomenti  
*database_name*  
Nome del database da modificare. Per visualizzare un elenco di database nell'appliance, usare [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
AUTOGROW = { ON | OFF }  
Aggiorna l'opzione AUTOGROW. Quando l'opzione AUTOGROW è impostata su ON, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] aumenta automaticamente lo spazio allocato per le tabelle replicate, le tabelle distribuite e il log delle transazioni in modo da poter supportare l'aumento in termini di requisiti di archiviazione. Quando l'opzione AUTOGROW è impostata su OFF, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] restituisce un errore se le tabelle replicate, le tabelle distribuite o il log delle transazioni superano l'impostazione di dimensioni massime.  
  
REPLICATED_SIZE = *size* [GB]  
Specifica in gigabyte le nuove dimensioni massime per ogni nodo di calcolo per l'archiviazione di tutte le tabelle replicate nel database da modificare. Per pianificare lo spazio di archiviazione dell'appliance, è necessario moltiplicare il valore in REPLICATED_SIZE per il numero di nodi di calcolo nell'appliance.  
  
DISTRIBUTED_SIZE = *size* [GB]  
Specifica in gigabyte le nuove dimensioni massime per ogni database per l'archiviazione di tutte le tabelle distribuite nel database da modificare. Le dimensioni vengono distribuite su tutti i nodi di calcolo nell'appliance.  
  
LOG_SIZE = *size* [GB]  
Specifica in gigabyte le nuove dimensioni massime per ogni database per l'archiviazione dei log delle transazioni nel database da modificare. Le dimensioni vengono distribuite su tutti i nodi di calcolo nell'appliance.  
  
ENCRYPTION { ON | OFF }  
Imposta il database per l'utilizzo della crittografia (ON) o no (OFF). È possibile configurare la crittografica per [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] solo quando l'opzione [sp_pdw_database_encryption](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md) è stata impostata su **1**. Prima di configurare la tecnologia Transparent Data Encryption, è necessario creare una chiave di crittografia del database. Per altre informazioni sulla crittografia del database, vedere [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  

SET AUTO_CREATE_STATISTICS { ON | OFF } Quando l'opzione per la creazione automatica delle statistiche, AUTO_CREATE_STATISTICS, è impostata su ON, Query Optimizer crea le statistiche necessarie per colonne singole nel predicato di query, per migliorare le stime della cardinalità per il piano di query. Queste statistiche di colonna singola vengono create in colonne che ancora non dispongono di un istogramma in un oggetto statistiche esistente.

Il valore predefinito è ON per i nuovi database creati dopo l'aggiornamento ad AU7. Il valore predefinito è OFF per i database creati prima dell'aggiornamento. 

Per altre informazioni sulle statistiche, vedere [Statistiche](../../relational-databases/statistics/statistics.md)

SET AUTO_UPDATE_STATISTICS { ON | OFF } Quando l'opzione per l'aggiornamento automatico delle statistiche, AUTO_UPDATE_STATISTICS, è impostata su ON, Query Optimizer determina se le statistiche possano non essere aggiornate, quindi ne esegue l'aggiornamento qualora vengano usate da una query. Le statistiche diventano obsolete in seguito a operazioni di inserimento, aggiornamento, eliminazione o unione che modificano la distribuzione dei dati nella tabella o nella vista indicizzata. Query Optimizer determina che le statistiche potrebbero non essere aggiornate contando il numero di modifiche apportate ai dati dopo l'ultimo aggiornamento delle statistiche e confrontando il numero di modifiche con una soglia basata sul numero di righe nella tabella o nella vista indicizzata.

Il valore predefinito è ON per i nuovi database creati dopo l'aggiornamento ad AU7. Il valore predefinito è OFF per i database creati prima dell'aggiornamento. 

Per altre informazioni sulle statistiche, vedere [Statistiche](../../relational-databases/statistics/statistics.md).


SET AUTO_UPDATE_STATISTICS_ASYNC { ON | OFF } L'opzione relativa all'aggiornamento asincrono delle statistiche, AUTO_UPDATE_STATISTICS_ASYNC, determina se Query Optimizer debba usare gli aggiornamenti sincroni o asincroni delle statistiche. L'opzione AUTO_UPDATE_STATISTICS_ASYNC si applica a oggetti statistiche creati per indici, colonne singole nei predicati di query e statistiche create con l'istruzione CREATE STATISTICS.

Il valore predefinito è ON per i nuovi database creati dopo l'aggiornamento ad AU7. Il valore predefinito è OFF per i database creati prima dell'aggiornamento. 

Per altre informazioni sulle statistiche, vedere [Statistiche](/sql/relational-databases/statistics/statistics).

## <a name="permissions"></a>Permissions  
È necessaria l'autorizzazione ALTER per il database.  
  
## <a name="error-messages"></a>messaggi di errore
Se le statistiche automatiche sono disabilitate e si tenta di modificare le impostazioni delle statistiche, PDW visualizza l'errore "Questa opzione non è supportata in PDW". L'amministratore di sistema può abilitare le statistiche automatiche abilitando l'opzione [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) della funzionalità.

## <a name="general-remarks"></a>Osservazioni generali  
I valori di REPLICATED_SIZE DISTRIBUTED_SIZE e LOG_SIZE possono essere maggiore, uguali o minori dei valori correnti per il database.  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
Le operazioni di incremento e riduzione sono approssimative. Le dimensioni effettive ottenute possono variare rispetto ai parametri delle dimensioni.  
  
[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] non esegue l'istruzione ALTER DATABASE come operazione atomica. Se l'istruzione viene interrotta durante l'esecuzione, le modifiche già apportate vengono mantenute.  

Le impostazioni delle statistiche funzionano solo se l'amministratore ha abilitato le statistiche automatiche.  Per abilitare o disabilitare le statistiche automatiche, l'amministratore deve usare l'opzione [AutoStatsEnabled](../../analytics-platform-system/appliance-feature-switch.md) della funzionalità. 
  
## <a name="locking-behavior"></a>Comportamento di blocco  
Consente di acquisire un blocco condiviso per l'oggetto DATABASE. Non è possibile modificare un database che un altro utente sta usando in modalità di lettura o scrittura. Sono incluse le sessioni che hanno rilasciato un'istruzione [USE](../language-elements/use-transact-sql.md) nel database.  
  
## <a name="performance"></a>restazioni  
Per compattare un database possono essere necessari molto tempo e numerose risorse di sistema, a seconda delle dimensioni dei dati effettivi all'interno del database e del livello di frammentazione del disco. Ad esempio, la compattazione di un database può richiedere fino a diverse ore di lavoro.  
  
## <a name="determining-encryption-progress"></a>Definizione dello stato di avanzamento della crittografia  
Usare la query seguente per determinare lo stato di avanzamento della tecnologia Transparent Data Encryption sotto forma di percentuale:  
  
```sql  
WITH  
database_dek AS (  
    SELECT ISNULL(db_map.database_id, dek.database_id) AS database_id,  
        dek.encryption_state, dek.percent_complete,  
        dek.key_algorithm, dek.key_length, dek.encryptor_thumbprint,  
        type  
    FROM sys.dm_pdw_nodes_database_encryption_keys AS dek  
    INNER JOIN sys.pdw_nodes_pdw_physical_databases AS node_db_map  
        ON dek.database_id = node_db_map.database_id   
        AND dek.pdw_node_id = node_db_map.pdw_node_id  
    LEFT JOIN sys.pdw_database_mappings AS db_map  
        ON node_db_map .physical_name = db_map.physical_name  
    INNER JOIN sys.dm_pdw_nodes nodes  
        ON nodes.pdw_node_id = dek.pdw_node_id  
    WHERE dek.encryptor_thumbprint <> 0x  
),  
dek_percent_complete AS (  
    SELECT database_dek.database_id, AVG(database_dek.percent_complete) AS percent_complete  
    FROM database_dek  
    WHERE type = 'COMPUTE'  
    GROUP BY database_dek.database_id  
)  
SELECT DB_NAME( database_dek.database_id ) AS name,  
    database_dek.database_id,  
    ISNULL(  
       (SELECT TOP 1 dek_encryption_state.encryption_state  
        FROM database_dek AS dek_encryption_state  
        WHERE dek_encryption_state.database_id = database_dek.database_id  
        ORDER BY (CASE encryption_state  
            WHEN 3 THEN -1  
            ELSE encryption_state  
            END) DESC), 0)  
        AS encryption_state,  
dek_percent_complete.percent_complete,  
database_dek.key_algorithm, database_dek.key_length, database_dek.encryptor_thumbprint  
FROM database_dek  
INNER JOIN dek_percent_complete   
    ON dek_percent_complete.database_id = database_dek.database_id  
WHERE type = 'CONTROL';  
```  
  
Per un esempio completo che illustra tutti i passaggi di implementazione della tecnologia TDE, vedere [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-altering-the-autogrow-setting"></a>A. Modifica dell'impostazione AUTOGROW  
Impostare l'opzione AUTOGROW su ON per il database `CustomerSales`.  
  
```sql  
ALTER DATABASE CustomerSales  
    SET ( AUTOGROW = ON );  
```  
  
### <a name="b-altering-the-maximum-storage-for-replicated-tables"></a>b. Modifica dell'archiviazione massima per le tabelle replicate  
Nell'esempio seguente il limite di archiviazione delle tabelle replicate viene impostato su 1 GB per il database `CustomerSales`. È il limite di archiviazione per ogni nodo di calcolo.  
  
```sql  
ALTER DATABASE CustomerSales  
    SET ( REPLICATED_SIZE = 1 GB );  
```  
  
### <a name="c-altering-the-maximum-storage-for-distributed-tables"></a>C. Modifica dell'archiviazione massima per le tabelle distribuite  
 Nell'esempio seguente il limite di archiviazione delle tabelle distribuite viene impostato su 1000 GB (1 TB) per il database `CustomerSales`. È il limite di archiviazione combinato dell'appliance per tutti i nodi di calcolo, non il limite di archiviazione per ogni nodo di calcolo.  
  
```sql  
ALTER DATABASE CustomerSales  
    SET ( DISTRIBUTED_SIZE = 1000 GB );  
```  
  
### <a name="d-altering-the-maximum-storage-for-the-transaction-log"></a>D. Modifica dell'archiviazione massima per il log delle transazioni  
 Nell'esempio seguente il database `CustomerSales` viene aggiornato perché le dimensioni massime del log delle transazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siano di 10 GB per l'applicazione.  
  
```sql  
ALTER DATABASE CustomerSales  
    SET ( LOG_SIZE = 10 GB );  
```  

### <a name="e-check-for-current-statistics-values"></a>E. Controllo dei valori correnti delle statistiche

La query seguente restituisce i valori correnti delle statistiche per tutti i database. Il valore 1 indica che la funzionalità è attivata e 0 indica che la funzionalità è disattivata.

```sql
SELECT NAME,
    is_auto_create_stats_on,
    is_auto_update_stats_on,
    is_auto_update_stats_async_on
FROM sys.databases;
```
### <a name="f-enable-auto-create-and-auto-update-stats-for-a-database"></a>F. Abilitazione della creazione e dell'aggiornamento automatici delle statistiche per un database
Usare l'istruzione seguente per abilitare la creazione e l'aggiornamento automatici delle statistiche in modo asincrono per il database CustomerSales.  L'istruzione crea e aggiorna le statistiche di colonna singola necessarie per creare piani di query di qualità elevata.

```sql
ALTER DATABASE CustomerSales
    SET AUTO_CREATE_STATISTICS ON;
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS ON; 
ALTER DATABASE CustomerSales
    SET AUTO_UPDATE_STATISTICS_ASYNC ON;
```
  
## <a name="see-also"></a>Vedere anche  
 [CREATE DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlpdw)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  

::: moniker-end
