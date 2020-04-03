---
title: Novità
description: Scopri le novità di Microsoft Analytics Platform System, un'appliance locale con scalabilità orizzontale che ospita MPP SQL Server Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: faf3bd1f487fb5c850759fdde3ddecd32bdd3b1f
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625544"
---
# <a name="whats-new-in-analytics-platform-system-a-scale-out-mpp-data-warehouse"></a>Novità di Analytics Platform System, un data warehouse MPP con scalabilità orizzontale
Scopri le novità degli aggiornamenti più recenti di Appliance per Microsoft Analytics Platform System (APS). APS è un'appliance locale con scalabilità orizzontale che ospita MPP SQL Server Parallel Data Warehouse. 

::: moniker range=">= aps-pdw-2016-au7 || = sqlallproducts-allversions"
<a name="h2-aps-cu7.6"></a>
## <a name="aps-cu76"></a>APS CU7.6
Data di rilascio - Aprile 2020

### <a name="rename-column"></a>Rename Column (Rinomina colonna)
Dopo l'aggiornamento a CU7.6, i clienti saranno in grado di rinominare una colonna di una tabella creata dall'utente. Per sintassi, esempi, limitazioni e altre informazioni, vedere [RENAME (Transact-SQL).](https://docs.microsoft.com/sql/t-sql/statements/rename-transact-sql)

### <a name="alter-view"></a>Modifica visualizzazione
I clienti saranno ora in grado di modificare le visualizzazioni. Per altre informazioni, vedere [ALTER VIEW (Transact-SQL).](https://docs.microsoft.com/sql/t-sql/statements/alter-view-transact-sql)

<a name="h2-aps-cu7.5"></a>
## <a name="aps-cu75"></a>APS CU7.5
Data di rilascio - Settembre 2019

### <a name="alter-external-data-source"></a>Modifica origine dati esterna
I clienti saranno in grado di modificare la definizione dell'origine dati esterna con l'aggiornamento CU7.5. I clienti con disponibilità elevata del nodo del nome Hadoop possono ora modificare l'origine dati per modificare gli argomenti quando si verifica un failover. Per APS, è possibile modificare solo LOCATION, RESOURCE_MANAGER_LOCATION e CREDENTIAL. Per ulteriori informazioni, vedere [Modificare l'origine dati esterna.](https://docs.microsoft.com/sql/t-sql/statements/alter-external-data-source-transact-sql?view=sql-server-2017)

### <a name="cdh-515-and-516-support-with-polybase"></a>Supporto per CDH 5.15 e 5.16 con PolyBase
PolyBase su APS con aggiornamento CU7.5 ora supporta le versioni CDH 5.15 e 5.16 della distribuzione Hadoop da Cloudera. Utilizzare l'opzione 6 per le versioni CDH 5.x. 

### <a name="try_convert-and-try_cast-support"></a>supporto Try_Convert e Try_Cast
CU7.5 APS supporta ora le funzioni [tsql TRY_CAST](https://docs.microsoft.com/sql/t-sql/functions/try-cast-transact-sql?view=sql-server-2017) e [TRY_CONVERT.](https://docs.microsoft.com/sql/t-sql/functions/try-convert-transact-sql?view=sql-server-2017) Entrambe queste funzioni restituiscono un valore convertito nel tipo di dati specificato se la conversione ha esito positivo; in caso contrario, restituisce null.

<a name="h2-aps-cu7.4"></a>
## <a name="aps-cu74"></a>APS CU7.4
Data di rilascio - Maggio 2019

### <a name="loading-large-rows-with-dwloader"></a>Caricamento di file di grandi dimensioni con dwloader
A partire da APS CU7.4, i clienti saranno in grado di utilizzare un nuovo dwloader per caricare righe in tabelle di dimensioni superiori a 32 KB (32.768 byte). Il nuovo dwloader supporta l'opzione -l che accetta un valore intero compreso tra 32768 e 33554432 (in byte) per caricare righe superiori a 32 KB. Utilizzare questa opzione solo durante il caricamento di righe di grandi dimensioni (maggiori di 32 KB) in quanto questa opzione allocherà più memoria sul client e sul server e potrebbe rallentare i carichi. È possibile scaricare il nuovo dwloader dal sito di [download](https://www.microsoft.com/download/details.aspx?id=57472).  

### <a name="hdp-30-and-31-support-with-polybase"></a>Supporto per HDP 3.0 e 3.1 con PolyBase
PolyBase su APS ora supporta HDP 3.0 e 3.1 con questo aggiornamento. Utilizzare l'opzione 7 per le versioni HDP 3.x. Per altre informazioni, vedere la pagina [Connettività PolyBase.For](https://docs.microsoft.com/sql/database-engine/configure-windows/polybase-connectivity-configuration-transact-sql) more information, see PolyBase connectivity page.

### <a name="utf16-file-support-with-polybase"></a>Supporto di file UTF16 con PolyBase
PolyBase supporta ora la lettura di file di testo delimitati con codifica UTF16 (LE). Vedere [Creare un formato di file esterno](https://docs.microsoft.com/sql/t-sql/statements/create-external-file-format-transact-sql) per i dettagli di installazione. 

<a name="h2-aps-cu7.3"></a>
## <a name="aps-cu73"></a>APS CU7.3
Data di rilascio - Dicembre 2018

### <a name="common-subexpression-elimination"></a>Eliminazione di sottoespressioni comuni
APS CU7.3 migliora le prestazioni delle query con l'eliminazione di sottoespressioni comuni in SQL Query Optimizer. Il miglioramento migliora le query in due modi. Il primo vantaggio è la possibilità di identificare ed eliminare tali espressioni consente di ridurre i tempi di compilazione SQL. Il secondo e più importante vantaggio è il fatto che le operazioni di spostamento dei dati per queste sottoespressioni ridondanti vengono eliminate, pertanto il tempo di esecuzione delle query diventa più veloce. Spiegazione dettagliata di questa funzione può essere trovato [qui](common-sub-expression-elimination.md).

### <a name="aps-informatica-connector-for-informatica-1020-published"></a>Connettore APS Informatica per Informatica 10.2.0 pubblicato
Abbiamo rilasciato una nuova versione di connettori Informatica per APS che funziona con Informatica versione 10.2.0 e 10.2.0 Hotfix 1. I nuovi connettori possono essere scaricati dal sito di [download.](https://www.microsoft.com/download/details.aspx?id=57472)

#### <a name="supported-versions"></a>Versioni supportate

| Versione APS | Informatica PowerCenter | Driver |
|:---|:---|:---|
| APS 2016 | 9.6.1 | SQL Server Native Client 11.x |
| APS 2016 e versioni successive | 10.2.0, 10.2.0 Hotfix 1 | SQL Server Native Client 11.x |

<a name="h2-aps-cu7.2"></a>
## <a name="aps-cu72"></a>APS CU7.2
Data di rilascio - Ottobre 2018

### <a name="support-for-tls-12"></a>Supporto per TLS 1.2
APS CU7.2 supporta TLS 1.2. La comunicazione tra computer client e aPS all'innodio può ora essere impostata per comunicare solo tramite TLS1.2. Strumenti come SSDT, SSIS e Dwloader installati nei computer client impostati per comunicare solo tramite TLS 1.2 possono ora connettersi a APS utilizzando TLS 1.2. Per impostazione predefinita, APS supporterà tutte le versioni TLS (1.0, 1.1 e 1.2) per la compatibilità con le versioni precedenti. Se si desidera impostare l'appliance APS per utilizzare rigorosamente TLS 1.2, è possibile farlo modificando le impostazioni del Registro di sistema. 

Per ulteriori informazioni, consultate [Configurazione di TLS1.2 su APS.](configure-tls12-aps.md)

### <a name="hadoop-encryption-zone-support-for-polybase"></a>Supporto della zona di crittografia Hadoop per PolyBase
PolyBase ora può comunicare con le zone di crittografia Hadoop. Vedere Le modifiche alla configurazione aPS necessarie per configurare la [sicurezza Hadoop](polybase-configure-hadoop-security.md#encryptionzone).

### <a name="insert-select-maxdop-options"></a>Inserisci-Seleziona le opzioni maxdop
È stata aggiunta [un'opzione](appliance-feature-switch.md) di funzionalità che consente di selezionare impostazioni maxdop maggiori di 1 per le operazioni di inserimento-selezione. È ora possibile impostare l'impostazione maxdop su 0, 1, 2 o 4. Il valore predefinito è 1.

> [!IMPORTANT]  
> L'aumento di maxdop può talvolta causare operazioni più lente o errori di deadlock. In questo caso, modificare l'impostazione su maxdop 1 e ripetere l'operazione.

### <a name="columnstore-index-health-dmv"></a>ColumnStore index health DMV
È possibile visualizzare le informazioni sull'integrità dell'indice columnstore utilizzando **dmv dm_pdw_nodes_db_column_store_row_group_physical_stats.** Utilizzare la visualizzazione seguente per determinare la frammentazione e decidere quando ricostruire o riorganizzare un indice columnstore.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[pdw_node_id]    = nt.[pdw_node_id]                                          
)
select *
from cte;
```

### <a name="polybase-date-range-increase-for-orc-and-parquet-files"></a>Aumento dell'intervallo di date PolyBase per i file ORC e Parquet
La lettura, l'importazione e l'esportazione di tipi di dati data utilizzando PolyBase ora supporta le date prima del 1970-01-01 e dopo il 2038-01-20 per i tipi di file ORC e Parquet.

### <a name="ssis-destination-adapter-for-sql-server-2017-as-target"></a>Scheda di destinazione SSIS per SQL Server 2017 come destinazioneSSIS destination adapter for SQL Server 2017 as target
Nuova scheda di destinazione APS SSIS che supporta SQL Server 2017COME destinazione di distribuzione può essere scaricata dal sito di [download.](https://www.microsoft.com/download/details.aspx?id=57472)

<a name="h2-aps-cu7.1"></a>
## <a name="aps-cu71"></a>APS CU7.1
Data di rilascio - Luglio 2018

### <a name="dbcc-commands-do-not-consume-concurrency-slots-behavior-change"></a>I comandi DBCC non utilizzano gli slot di concorrenza (modifica del comportamento)DBCC commands do not consume concurrency slots (behavior change)
APS supporta un sottoinsieme dei [comandi DBCC](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-transact-sql) T-SQL, ad esempio [DBCC DROPCLEANBUFFERS](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql). In precedenza, questi comandi avrebbero utilizzato uno [slot di concorrenza](https://docs.microsoft.com/sql/analytics-platform-system/workload-management?view=aps-pdw-2016-au7#concurrency-slots) riducendo il numero di carichi/query utente che poteva essere eseguito. I `DBCC` comandi vengono ora eseguiti in una coda locale che non utilizzano uno slot di concorrenza utente migliorando le prestazioni complessive di esecuzione delle query.

### <a name="replaces-some-metadata-calls-with-catalog-objects"></a>Sostituisce alcune chiamate ai metadati con gli oggetti del catalogo
L'uso di oggetti catalogo per le chiamate ai metadati invece di smo ha mostrato un miglioramento delle prestazioni in APS. A partire da CU7.1, alcune di queste chiamate ai metadati ora utilizzano oggetti catalogo per impostazione predefinita. Questo comportamento può essere disattivato in base [all'opzione di funzionalità](appliance-feature-switch.md) se i clienti che utilizzano query di metadati si verificano problemi.

### <a name="bug-fixes"></a>Correzioni di bug
È stato eseguito l'aggiornamento a SQL Server 2016 SP2 CU2 con APS CU7.1. L'aggiornamento consente di risolvere alcuni problemi descritti di seguito.

| Titolo | Descrizione |
|:---|:---|
| **Potenziale deadlock di tupla** |L'aggiornamento corregge una possibilità di lunga data di deadlock in una transazione distribuita e tupla mover thread in background. Dopo aver installato CU7.1, i clienti che hanno utilizzato TF634 per arrestare lo spostamento tra tetti come parametro di avvio di SQL Server o flag di traccia globale possono rimuoverlo in modo sicuro. | 
| **Una query di ritardo/lead non riesce** |Alcune query su tabelle CCI con funzioni di ritardo/lead annidate che errore sarebbero ora corrette con questo aggiornamento. | 


<a name="h2-aps-au7"></a>
## <a name="aps-au7"></a>APS AU7
Data di rilascio - Maggio 2018

APS 2016 è un prerequisito per l'aggiornamento a AU7. Di seguito sono riportate le nuove funzionalità di APS AU7:

### <a name="auto-create-and-auto-update-statistics"></a>Statistiche di creazione e aggiornamento automatico
APS AU7 crea e aggiorna automaticamente le statistiche, per impostazione predefinita. Per aggiornare le impostazioni delle statistiche, gli amministratori possono utilizzare una nuova voce di menu Cambio funzionalità in [Configuration Manager.](appliance-configuration.md#CMTasks) [L'opzione](appliance-feature-switch.md) di funzionalità controlla il comportamento di creazione automatica, aggiornamento automatico e aggiornamento asincrono delle statistiche. È inoltre possibile aggiornare le impostazioni delle statistiche con l'istruzione [ALTER DATABASE (Parallel Data Warehouse).](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)

### <a name="t-sql"></a>T-SQL
Select @var è ora supportato. Per altre informazioni, vedere [selezionare la variabile localeFor](/sql/t-sql/language-elements/select-local-variable-transact-sql) more information, see select local variable 

Gli hint per le query HASH e ORDER GROUP sono ora supportati. Per altre informazioni, vedere [Hints(Transact-SQL) - QueryFor more information, see Hints(Transact-SQL) - Query](/sql/t-sql/queries/hints-transact-sql-query)

### <a name="feature-switch"></a>Interruttore di funzione
APS AU7 introduce Feature Switch in [Configuration Manager](launch-the-configuration-manager.md). AutoStatsEnabled e DmsProcessStopMessageTimeoutInSeconds sono ora opzioni configurabili che possono essere modificate dagli amministratori.

### <a name="known-issues"></a>Problemi noti
Con il software APS AU7, viene fornito un aggiornamento del BIOS Intel che risolve un problema descritto come *attacchi di canale laterale*di esecuzione speculativa . Gli attacchi mirano a sfruttare ciò che vengono chiamati *Spectre e Meltdown vulnerabilità*. Anche se incluso in un pacchetto con APS, l'aggiornamento del BIOS viene installato manualmente e non come parte dell'installazione del software APS AU7.

Microsoft consiglia a tutti i clienti di installare il BIOS aggiornato. Microsoft ha misurato l'effetto di Kernel Virtual Address Shadowing (KVAS), Kernel Page Table Indirection (KPTI) e Indirect Branch Prediction mitigation (IBP) su vari carichi di lavoro SQL in vari ambienti. Le misurazioni hanno rilevato un degrado significativo su alcuni carichi di lavoro. In base ai risultati, è consigliabile testare l'effetto sulle prestazioni dell'abilitazione dell'aggiornamento del BIOS prima di distribuirli in un ambiente di produzione. Vedere Le linee guida di SQL Server [qui](https://support.microsoft.com/help/4073225/guidance-protect-sql-server-against-spectre-meltdown).

::: moniker-end
::: moniker range=">= aps-pdw-2016 || = sqlallproducts-allversions"
<a name="h2-aps-au6"></a>
## <a name="aps-2016"></a>APS 2016
In questa sezione sono descritte le nuove funzionalità per APS 2016-AU6.

### <a name="sql-server-2016"></a>SQL Server 2016

APS AU6 viene eseguito sulla versione più recente di SQL Server 2016 e usa il livello di compatibilità del database predefinito 130. SQL Server 2016 sql consente il supporto per nuove funzionalità, ad esempio:SQL Server 2016 enables support for new features such as:

- Indici secondari per gli indici columnstore cluster.
- Kerberos per PolyBase.

### <a name="t-sql"></a>T-SQL
APS AU6 supporta questi miglioramenti di compatibilità T-SQL.  Questi elementi del linguaggio aggiuntivi semplificano la migrazione da SQL ServerSQL Server e altre origini dati. 

- Le regole di confronto SQL a livello di colonna sono ora supportate, oltre alle regole di confronto di [Windows.Column-level SQL collations][] are now supported, in addition to Windows collations.
- [Gli indici non cluster negli indici columnstore cluster][] migliorano le prestazioni delle query che cercano valori specifici nell'indice columnstore cluster. 
- [SELECT...INTO][] 
- [sp_spaceused()][] visualizza lo spazio su disco utilizzato o riservato in una tabella o in un database.
- [Supporto tabelle estese][] è lo stesso di SQL Server 2016. Il limite precedente di 32 K per la dimensione della riga non esiste più. 

**Tipi di dati**

- [VARCHAR(MAX)][], [NVARCHAR(MAX)][] e [VARBINARY(MAX)][]. Questi tipi di dati LOB hanno una dimensione massima di 2 GB. Per caricare questi oggetti utilizzare [utilità bcp][]. PolyBase e dwloader non supportano attualmente questi tipi di dati. 
- [Sysname][]
- [Uniqueidentifier][]
- tipi di dati [NUMERIC][] e DECIMAL.

**Funzioni finestra**

- [ROWS o RANGE][] nella clausola OVER dell'istruzione SELECT.
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

**Funzioni di sicurezza**

- [CHECKSUM()][] e [BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

**Funzioni aggiuntive**

- [NUOVOID()][]
- [Funzione RAND()][]

### <a name="polybasehadoop-enhancements"></a>Miglioramenti PolyBase/Hadoop

- Compatibilità con Hortonworks HDP 2.4 e HDP 2.5
- Supporto Kerberos tramite credenziali con ambito database
- Supporto delle credenziali con BLOB di Archiviazione di AzureCredential support with Azure Storage Blobs

### <a name="install-and-upgrade-enhancements"></a>Miglioramenti dell'installazione e dell'aggiornamento

**Aggiornamenti dell'architettura aziendale** L'aggiornamento dell'appliance esistente ad APS AU6 consente di installare gli aggiornamenti del firmware e dei driver più recenti, che includono correzioni per la sicurezza. 

Un nuovo apparecchio HPE o DELL include tutti gli aggiornamenti più recenti più:

- Supporto del processore di ultima generazione (Broadwell)
- Aggiornamento ai DIMM DDR4
- Miglioramento della velocità effettiva di DIMM

**Integrazione**

- Il supporto del nome di dominio completo (FQDN, Fully Qualified Domain Name) consente di configurare un trust di dominio per l'appliance. 
- Per utilizzare FQDN, è necessario eseguire un aggiornamento completo e acconsentire esplicitamente durante l'aggiornamento. 

**Riduzione dei tempi di inattività** L'installazione o l'aggiornamento ad APS AU6 è più veloce e richiede meno tempi di inattività rispetto alle versioni precedenti. Per ridurre i tempi di inattività, l'installazione o l'aggiornamento: 

 - Semplifica l'applicazione degli aggiornamenti WSUS utilizzando un'immagine che contiene tutti gli aggiornamenti fino a giugno 2016
 - Applica gli aggiornamenti della sicurezza con gli aggiornamenti del driver e del firmware
 - Inserisce gli aggiornamenti rapidi più recenti e l'utilità di verifica dell'appliance (PAV) sull'appliance in modo che siano pronti per l'installazione senza che sia necessario scaricarli.

::: moniker-end

<!--
Link references to other articles in this same GitHub repo.

The link format that starts with '/sql/what-ever/my-artlcle' is not appropriate for common links within the same repo (as most of these link are).  The first couple links have been edited to show the proper syntax, but all other links in this article need to be similarly edited.
The proper formats have at least two big advantages.  One big advantage is that the proper formats enable the OPS Build system to detect broken links at Pull Request build time, instead of only later during run time.
-->
[database compatibility level 130]: ../t-sql/statements/alter-database-transact-sql-compatibility-level.md
[Regole di confronto SQL a livello di colonnaColumn-level SQL collations]: ~/relational-databases/collations/collation-and-unicode-support.md

[Indici non cluster negli indici columnstore cluster]:/sql/t-sql/statements/create-index-transact-sql
[VARCHAR (MAX)]:/sql/t-sql/data-types/char-and-varchar-transact-sql
[NVARCHAR(MAX)]:/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql
[VARBINARIO (MAX)]:/sql/t-sql/data-types/binary-and-varbinary-transact-sql
[Sysname]:/sql/relational-databases/system-catalog-views/sys-types-transact-sql
[SELECT...INTO]:/sql/t-sql/queries/select-into-clause-transact-sql
[sp_spaceused()]:/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql
[Tavoli ampi]:/sql/sql-server/maximum-capacity-specifications-for-sql-server
[BULK INSERT]:/sql/t-sql/statements/bulk-insert-transact-sql
[Utilità bcp]:/sql/tools/bcp-utility
[Uniqueidentifier]:/sql/t-sql/data-types/uniqueidentifier-transact-sql
[Numerico]:/sql/t-sql/data-types/decimal-and-numeric-transact-sql
[RIGHE o RANGE]:/sql/t-sql/queries/select-over-clause-transact-sql
[FIRST_VALUE]:/sql/t-sql/functions/first-value-transact-sql
[LAST_VALUE]:/sql/t-sql/functions/last-value-transact-sql
[CUME_DIST]:/sql/t-sql/functions/cume-dist-transact-sql
[PERCENT_RANK]:/sql/t-sql/functions/percent-rank-transact-sql
[CHECKSUM()]:/sql/t-sql/functions/checksum-transact-sql
[BINARY_CHECKSUM()]:/sql/t-sql/functions/binary-checksum-transact-sql
[HAS_PERMS_BY_NAME()]:/sql/t-sql/functions/has-perms-by-name-transact-sql
[NUOVOID()]:/sql/t-sql/functions/newid-transact-sql
[Funzione RAND()]:/sql/t-sql/functions/rand-transact-sql


  

  


