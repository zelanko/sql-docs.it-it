---
title: Proprietà database (pagina Opzioni) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.options.f1
ms.assetid: a3447987-5507-4630-ac35-58821b72354d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a4420aaf7b11eccecf0b04bb67a55386215f1fc9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62917087"
---
# <a name="database-properties-options-page"></a>Proprietà database (pagina Opzioni)
  Utilizzare questa pagina per visualizzare o modificare le opzioni per il database selezionato. Per ulteriori informazioni sulle opzioni disponibili in questa pagina, vedere [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
## <a name="page-header"></a>Intestazione di pagina  
 **Regole di confronto**  
 È possibile specificare le regole di confronto del database selezionandole nell'elenco. Per altre informazioni, vedere [Set or Change the Database Collation](../collations/set-or-change-the-database-collation.md).  
  
 **Modello di recupero**  
 È possibile specificare uno dei modelli di recupero del database seguenti: **Con registrazione completa**, **Con registrazione minima delle operazioni bulk**o **Con registrazione minima**. Per altre informazioni sui modelli di recupero, vedere [Modelli di recupero &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md).  
  
 **Livello di compatibilità**  
 È possibile specificare la versione più recente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supportata dal database. I valori possibili sono  **SQL Server 2014 (120)**,  **SQL Server 2012 (110)** e **SQL Server 2008 (100)**. Quando un database di SQL Server 2005 viene aggiornato a SQL Server 2014, il livello di compatibilità del database viene modificato da 90 a 100.  Il livello di compatibilità 90 non è supportato in SQL Server 2014. Per altre informazioni, vedere [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
 **Tipo di contenimento**  
 È possibile specificare nessuno o parziale per determinare se si tratta di un database indipendente. Per altre informazioni sui database indipendenti, vedere [Contained Databases](contained-databases.md). La proprietà del server **Abilita database indipendenti** deve essere impostata su **TRUE** prima che un database possa essere configurato come indipendente.  
  
> [!IMPORTANT]  
>  L'abilitazione dei delegati di database parzialmente indipendenti controlla l'accesso all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i proprietari del database. Per altre informazioni, vedere [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md).  
  
## <a name="automatic"></a>Automatico  
 **Chiusura automatica**  
 Specifica se il database viene chiuso correttamente e se le risorse corrispondenti vengono liberate dopo la disconnessione dell'ultimo utente. I valori possibili sono `True` e `False`. Se `True`, il database viene chiuso correttamente e le relative risorse vengono rilasciate dopo la disconnessione dell'ultimo utente.  
  
 Creazione automatica statistiche incrementali  
 Specificare se utilizzare l'opzione incrementale nella creazione di statistiche per partizione. Per informazioni sulle statistiche incrementali, vedere [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Creazione automatica statistiche**  
 Indica se il database crea automaticamente le statistiche di ottimizzazione mancanti. I valori possibili sono `True` e `False`. Se `True`, le statistiche mancanti necessarie per l'ottimizzazione di una query vengono compilate automaticamente durante la fase di ottimizzazione. Per altre informazioni, vedere [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Compattazione automatica**  
 Indica se i file di database sono disponibili per la compattazione periodica. I valori possibili sono `True` e `False`. Per altre informazioni, vedere [Shrink a Database](shrink-a-database.md).  
  
 **Aggiornamento automatico statistiche**  
 Indica se il database aggiorna automaticamente le statistiche di ottimizzazione non aggiornate. I valori possibili sono `True` e `False`. Se `True`, tutte le statistiche non aggiornate necessarie per l'ottimizzazione di una query vengono compilate automaticamente durante la fase di ottimizzazione. Per altre informazioni, vedere [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
 **Aggiornamento automatico asincrono statistiche**  
 Se `True`, le query che avviano un aggiornamento automatico delle statistiche non aggiornate non attenderanno l'aggiornamento delle statistiche prima della compilazione. Le query successive utilizzeranno le statistiche aggiornate, non appena disponibili.  
  
 Se `False`, le query che avviano un aggiornamento automatico delle statistiche non aggiornate, restano in attesa fino a quando non è possibile utilizzare le statistiche aggiornate nel piano di ottimizzazione delle query.  
  
 L'impostazione di questa `True` opzione su non ha alcun effetto a meno che anche l'opzione `True` **aggiornamento automatico statistiche** non sia impostata su.  
  
## <a name="containment"></a>Containment  
 Nei database indipendenti alcune impostazioni che in genere sono configurate a livello di server possono essere configurate a livello di database.  
  
 **LCID lingua full-text predefinita**  
 Specifica una lingua predefinita per le colonne con indicizzazione full-text. L'analisi linguistica dei dati con indicizzazione full-text dipende dalla lingua dei dati. Il valore predefinito per questa opzione corrisponde alla lingua impostata per il server. Per la lingua corrispondente all'impostazione visualizzata, vedere [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql).  
  
 **Lingua predefinita**  
 Lingua predefinita per tutti i nuovi utenti del database indipendente, salvo altrimenti specificato.  
  
 **Trigger annidati abilitati**  
 Consente l'attivazione di trigger da altri trigger. I trigger possono essere nidificati fino a un massimo di 32 livelli. Per altre informazioni, vedere la sezione relativa ai trigger annidati in [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql).  
  
 **Trasforma parole non significative**  
 Evita la visualizzazione di un messaggio di errore qualora, a causa di parole non significative, un'operazione booleana su una query full-text restituisca zero righe. Per altre informazioni, vedere [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md).  
  
 **Cambio data per anno a due cifre**  
 Indica il numero più alto che può essere immesso come anno a due cifre. L'anno indicato e i 99 anni precedenti possono essere immessi con due cifre. Tutti gli altri anni devono essere immessi con quattro cifre.  
  
 Ad esempio, l'impostazione predefinita 2049 indica che la data '14/03/49' verrà interpretata come 14 marzo 2049, mentre la data '14/03/50' verrà interpretata come 14 marzo 1950. Per altre informazioni, vedere [Configurare l'opzione di configurazione del server two-digit year cutoff](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).  
  
## <a name="cursor"></a>Cursore  
 **Chiusura cursori dopo commit abilitata**  
 Specifica se i cursori vengono chiusi dopo l'esecuzione del commit della transazione di apertura del cursore. I valori possibili sono `True` e `False`. Se `True`, tutti i cursori che risultano aperti quando viene eseguito il commit o il rollback di un transazione vengono chiusi. Se `False`, quando viene eseguito il commit della transazione tali cursori rimangono aperti. Se `False`, il rollback di una transazione comporta la chiusura di tutti i cursori, a eccezione di quelli definiti come INSENSITIVE o STATIC. Per altre informazioni, vedere [SET CURSOR_CLOSE_ON_COMMIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-cursor-close-on-commit-transact-sql).  
  
 **Cursore predefinito**  
 Indica il comportamento del cursore predefinito. Se `True`, le dichiarazioni dei cursori sono LOCAL per impostazione predefinita. Se `False`, [!INCLUDE[tsql](../../includes/tsql-md.md)] per impostazione predefinita i cursori sono globali.  
  
## <a name="filestream"></a>FILESTREAM  
 **Nome di directory FILESTREAM**  
 Specifica il nome di directory per i dati FILESTREAM associati al database selezionato.  
  
 **Accesso FILESTREAM non in transazioni**  
 È possibile specificare una delle opzioni seguenti per l'accesso non transazionale tramite il file system a dati FILESTREAM archiviati in tabelle FileTable: **OFF**, **READ_ONLY**o **FULL**. Se FILESTREAM non è abilitato nel server, questo valore viene impostato su OFF ed è disabilitato. Per altre informazioni, vedere [FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md).  
  
## <a name="miscellaneous"></a>Varie  
 **NULL ANSI predefinito**  
 Consente l'uso di valori Null per ogni colonna o tipo di dati definito dall'utente non indicato in modo esplicito come `NOT NULL`, lo stato predefinito, durante un'istruzione `CREATE TABLE` o `ALTER TABLE`. Per altre informazioni, vedere [SET ANSI_NULL_DFLT_ON &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-on-transact-sql) e [SET ANSI_NULL_DFLT_OFF &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-null-dflt-off-transact-sql).  
  
 **NULL ANSI abilitati**  
 Indica il comportamento degli operatori di confronto Uguale a (`=`) e Diverso da (`<>`) quando vengono utilizzati con valori Null. I valori possibili `True` sono (on) `False` e (off). Se `True`, tutti i confronti con un valore Null restituiscono UNKNOWN. Se `False`, i confronti di valori non Unicode con un valore null restituiscono `True` se entrambi i valori sono null. Per altre informazioni, vedere [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql).  
  
 **Riempimento ANSI abilitato**  
 Indica se il riempimento ANSI è attivato o disattivato. I valori consentiti sono `True` ( `False` on) e (off). Per altre informazioni, vedere [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql).  
  
 **Avvisi ANSI abilitati**  
 Indica il comportamento dello standard ISO per diverse condizioni di errore. Quando `True`viene generato un messaggio di avviso se sono presenti valori null nelle funzioni di aggregazione, ad esempio Sum, AVG, Max, min, STDEV, STDEVP, var, VARP o count. Se `False`, non viene emesso alcun avviso. Per altre informazioni, vedere [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql).  
  
 **Interruzione per errori aritmetici abilitata**  
 Indica se l'opzione del database relativa all'interruzione aritmetica è abilitata o disabilitata. I valori possibili sono `True` e `False`. Se `True`, un errore di overflow o di divisione per zero comporta l'interruzione della query o del batch. Se l'errore si verifica in una transazione, viene eseguito il rollback della transazione. Se `False`, viene visualizzato un avviso, ma l'esecuzione della query, del batch o della transazione prosegue come se non si fosse verificato alcun errore. Per altre informazioni, vedere [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql).  
  
 **Risultato Null per concatenazione di valori Null**  
 Indica il comportamento in caso di valori Null concatenati. Quando il valore della proprietà `True`è `string` , + null restituisce null. Se `False`, il risultato è `string`. Per altre informazioni, vedere [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql).  
  
 **Concatenamento della proprietà tra database abilitato**  
 Questo valore di sola lettura indica se è abilitato il concatenamento della proprietà tra database. Se `True`, il database può essere l'origine o la destinazione di una catena di proprietà tra database. Utilizzare l'istruzione ALTER DATABASE per impostare questa proprietà.  
  
 **Ottimizzazione di correlazione data abilitata**  
 Quando `True`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene le statistiche di correlazione tra due tabelle qualsiasi del database collegate da un vincolo FOREIGN KEY e con `datetime` colonne.  
  
 Se `False`, le statistiche sulla correlazione non vengono mantenute.  
  
 **Interruzione per perdita di precisione numerica**  
 Indica la modalità di gestione degli errori di arrotondamento utilizzata dal database. I valori possibili sono `True` e `False`. Se `True`, viene generato un errore se si verifica una perdita di precisione in un'espressione. Se `False`, le perdite di precisione non generano messaggi di errore e il risultato viene arrotondato alla precisione della colonna o della variabile che archivia il risultato. Per altre informazioni, vedere [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql).  
  
 **Parametrizzazione**  
 Se **SIMPLE**, le query vengono parametrizzate in base al comportamento predefinito del database. Quando è **Forced**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parametrizza tutte le query nel database.  
  
 **Identificatori delimitati abilitati**  
 Indica se le parole chiave di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere utilizzate come identificatori (nome di variabile o oggetto) se racchiusi tra virgolette. I valori possibili sono `True` e `False`. Per altre informazioni, vedere [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).  
  
 **Trigger ricorsivi abilitati**  
 Indica se i trigger possono essere attivati da altri trigger. I valori possibili sono `True` e `False`. Quando è impostato `True`su, Abilita l'attivazione ricorsiva dei trigger. Quando è impostato `False`su, viene impedita solo la ricorsione diretta. Per disabilitare la ricorsione indiretta, impostare l'opzione del server nested triggers su 0 utilizzando sp_configure. Per altre informazioni, vedere [Creazione di trigger annidati](../triggers/create-nested-triggers.md).  
  
 `Trustworthy`  
 Quando viene `True`visualizzata, questa opzione di sola lettura indica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che consente l'accesso alle risorse esterne al database in un contesto di rappresentazione definito all'interno del database. I contesti di rappresentazione possono essere definiti all'interno del database mediante l'istruzione utente EXECUTE AS o la clausola EXECUTE AS sui moduli di database.  
  
 Per ottenere l'accesso, il proprietario del database deve anche disporre dell'autorizzazione AUTHENTICATE SERVER a livello del server.  
  
 Questa proprietà consente inoltre la creazione e l'esecuzione di assembly di accesso esterni e non sicuri all'interno del database. Oltre a impostare questa proprietà su `True`, il proprietario del database deve disporre dell'autorizzazione EXTERNAL ACCESS ASSEMBLY o UNSAFE ASSEMBLY a livello di server.  
  
 Per impostazione predefinita, questa proprietà è impostata su `False`tutti i database utente e tutti i database di sistema, ad eccezione di **msdb**. Il valore non può essere modificato per i database **Model** e **tempdb** .  
  
 TRUSTWORTHY è impostata su `False` ogniqualvolta un database è collegato al server.  
  
 La modalità consigliata per l'accesso alle risorse esterne al database in un contesto di rappresentazione consiste nell'utilizzo di certificati e firme al posto dell'opzione `Trustworthy`.  
  
 Per impostare questa proprietà, utilizzare l'istruzione ALTER DATABASE.  
  
 **Formato di archiviazione vardecimal abilitato**  
 Questa opzione è di sola lettura a partire [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] da e versioni successive, tutti i database sono abilitati per il formato di archiviazione vardecimal. Questa opzione usa [sp_db_vardecimal_storage_format](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql).  
  
## <a name="recovery"></a>Ripristino  
 **Verifica pagina**  
 Indica l'opzione utilizzata per individuare e segnalare le transazioni di I/O incomplete causate da errori di I/O su disco. I valori possibili sono **None**, **TornPageDetection**e **Checksum**. Per altre informazioni, vedere [Gestione della tabella suspect_pages &#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md).  
  
 **Tempo di recupero di riferimento (secondi)**  
 Specifica il limite massimo di tempo, in secondi, necessario per recuperare il database specificato in caso di un arresto anomalo del sistema. Per altre informazioni, vedere [Checkpoint di database &#40;SQL Server&#41;](../logs/database-checkpoints-sql-server.md).  
  
## <a name="state"></a>State  
 **Database di sola lettura**  
 Indica se il database è di sola lettura. I valori possibili sono `True` e `False`. Se `True`, gli utenti possono solo leggere i dati nel database. Gli utenti non sono in grado di modificare i dati o gli oggetti di database. È tuttavia possibile eliminare il database utilizzando l'istruzione DROP DATABASE. Il database non può essere in uso quando si specifica un nuovo valore per l'opzione **Database di sola lettura** . L'unica eccezione riguarda il database master e prevede che solo l'amministratore di sistema possa utilizzare il database master durante l'impostazione di questa opzione.  
  
 **Stato database**  
 Indica lo stato corrente del database. Non è modificabile. Per ulteriori informazioni su **Stato database**, vedere [Database States](database-states.md).  
  
 **Limitazione dell'accesso**  
 Indica gli utenti autorizzati ad accedere al database. I valori possibili sono:  
  
-   **Più di uno**  
  
     Rappresenta lo stato normale per un database di produzione e consente l'accesso simultaneo di più utenti al database.  
  
-   **Single**  
  
     Questa impostazione viene utilizzata per operazioni di manutenzione e consente l'accesso al database di un solo utente alla volta.  
  
-   **Restricted**  
  
     Solo i membri del ruolo db_owner, dbcreator o sysadmin possono utilizzare il database.  
  
 **Crittografia abilitata**  
 Se `True`, il database è abilitato per la crittografia del database. Per la crittografia è necessaria una chiave di crittografia del database. Per altre informazioni sulla crittografia trasparente del database, vedere [Transparent Data Encryption &#40;TDE&#41;](../security/encryption/transparent-data-encryption.md).  
  
## <a name="see-also"></a>Vedi anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
  
