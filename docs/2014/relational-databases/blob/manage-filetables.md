---
title: Gestire tabelle FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], security
- FileTables [SQL Server], managing access
ms.assetid: 93af982c-b4fe-4be0-8268-11f86dae27e1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e8522cde5be0ccc34f858ce6bff945433af11ac
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537603"
---
# <a name="manage-filetables"></a>Gestione di tabelle FileTable
  Vengono descritte attività amministrative comuni per la gestione di tabelle FileTable.  
  
##  <a name="HowToEnumerate"></a> Come si fa: Procedura: recuperare un elenco di tabelle FileTable e di oggetti correlati  
 Per ottenere un elenco di tabelle FileTable, eseguire una query su una delle viste del catalogo riportate di seguito:  
  
-   [sys.filetables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)  
  
-   [sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql) (verificare il valore della colonna **is_filetable**).  
  
```sql  
SELECT * FROM sys.filetables;  
GO  
  
SELECT * FROM sys.tables WHERE is_filetable = 1;  
GO  
```  
  
 Per ottenere un elenco degli oggetti definiti dal sistema creati quando sono state create le tabelle FileTable associate, eseguire una query sulla vista del catalogo [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql).  
  
```sql  
SELECT object_id, OBJECT_NAME(object_id) AS 'Object Name'  
    FROM sys.filetable_system_defined_objects  
    WHERE object_id = filetable_object_id;  
GO  
```  
  
##  <a name="BasicsDisabling"></a> Disabilitare e riabilitare l'accesso non transazionale a livello di database  
 Per acquisire l'accesso esclusivo necessario per determinate attività di amministrazione, può essere necessario disabilitare temporaneamente l'accesso non transazionale.  
  
 **Comportamento dell'istruzione ALTER DATABASE in caso di modifica del livello di accesso non transazionale**  
  
-   Quando si imposta l'accesso non transazionale su READ_ONLY o OFF, il comando ALTER DATABASE non restituisce il controllo all'utente finché sono presenti handle di file aperti che creano conflitti con l'operazione richiesta. Gli handle di file che creano conflitti con questa operazione includono gli elementi seguenti:  
  
    -   Quando l'accesso viene impostato su **NESSUNO**, tutti gli handle di file aperti.  
  
    -   Quando l'accesso viene impostato su **READ_ONLY**, tutti gli handle di file aperti per l'accesso in scrittura.  
  
     Per informazioni sulla terminazione degli handle di file aperti, vedere [Terminazione di handle di file aperti associati a una tabella FileTable](#BasicsKilling) in questo argomento.  
  
     Se il comando ALTER DATABASE è annullato o termina con un timeout, il livello di accesso transazionale non viene modificato.  
  
-   Se viene chiamata l'istruzione ALTER DATABASE con una clausola WITH \<terminazione> (ROLLBACK AFTER integer [ SECONDS ] | ROLLBACK IMMEDIATE | NO_WAIT), vengono terminati tutti gli handle di file non transazionali aperti.  
  
> [!WARNING]  
>  La terminazione di handle di file aperti può causare la perdita dei dati non salvati da parte degli utenti. Questo comportamento è coerente con quello del file system stesso.  
  
 **Effetti della disabilitazione dell'accesso non transazionale**  
  
 La modifica del livello dell'accesso non transazionale a livello del database comporta gli effetti seguenti sulle directory FileTable all'interno della directory a livello di database:  
  
-   Quando l'accesso viene impostato su **NESSUNO**, tutte le directory FileTable e il relativo contenuto non sono più accessibili o visibili.  
  
-   Quando l'accesso viene impostato su **READ_ONLY**, anche tutte le directory FileTable e il relativo contenuto sono in sola lettura.  
  
 La disabilitazione di FILESTREAM a livello di istanza comporta gli effetti seguenti sulle directory a livello di database nell'istanza e la tabella FileTable all'interno di esse:  
  
-   Nessuna delle directory a livello di database nell'istanza è visibile se FILESTREAM è disabilitato a livello di istanza.  
  
###  <a name="HowToDisable"></a> Come si fa: Disabilitare e riabilitare l'accesso non transazionale a livello di database.  
 Per altre informazioni, vedere [Opzioni ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 **Per disabilitare l'accesso non transazionale completo**  
 Chiamare l'istruzione **ALTER DATABASE** e usare SET per impostare il valore di **NON_TRANSACTED_ACCESS** su **READ_ONLY** o **OFF**.  
  
```sql  
-- Disable write access.  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = READ_ONLY );  
GO  
  
-- Disable non-transactional access.  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = OFF );  
GO  
```  
  
 **Per riabilitare l'accesso non transazionale completo**  
 Chiamare l'istruzione **ALTER DATABASE** e usare SET per impostare il valore di **NON_TRANSACTED_ACCESS** su **FULL**.  
  
```sql  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL );  
GO  
```  
  
###  <a name="visible"></a> Come si fa: Assicurare la visibilità delle tabelle FileTables in un Database  
 Una directory a livello di database e le directory FileTable in essa contenute sono visibili se si verificano tutte le condizioni seguenti:  
  
1.  FILESTREAM è abilitato a livello di istanza.  
  
2.  L'accesso non transazionale è abilitato a livello di database.  
  
3.  Una directory valida è stata specificata al livello di database.  
  
##  <a name="BasicsEnabling"></a> Disabilitare e riabilitare lo spazio dei nomi FileTable a livello di tabella  
 Disabilitando lo spazio dei nomi della tabella FileTable vengono disabilitati tutti i vincoli e i trigger definiti dal sistema creati con la tabella FileTable. Ciò è utile nei casi in cui una tabella FileTable deve essere riorganizzata su larga scala utilizzando operazioni [!INCLUDE[tsql](../../includes/tsql-md.md)] , ma si desidera evitare le spese correlate all'applicazione di semantica della tabella FileTable. Queste operazioni possono, tuttavia, lasciare la tabella FileTable in uno stato non coerente e impedire l'operazione di abilitazione dello spazio dei nomi di Filetable.  
  
 La disabilitazione di uno spazio dei nomi FileTable comporta i risultati riportati di seguito:  
  
-   Le colonne e i dati della tabella FileTable non vengono eliminati fisicamente dalla tabella.  
  
-   La directory FileTable, i file e le directory in essa contenute vengono rimossi dal file system e non sono disponibili per l'accesso I/O al file.  
  
-   Le colonne della tabella FileTable definite dal sistema non possono essere eliminate e ricreate, diversamente si comportano come colonne ordinarie per le operazioni DML.  
  
-   Gli handle di file aperti impediscono la disabilitazione dei vincoli FileTable, poiché questa operazione richiede un blocco dello schema sulla tabella.  
  
-   L'applicazione di tutta la semantica FileTable, incluso i vincoli e i trigger definiti dal sistema, si arresta dopo la disabilitazione dello spazio dei nomi FileTable.  
  
 La riabilitazione di uno spazio dei nomi FileTable comporta i risultati riportati di seguito:  
  
-   Viene verificata la coerenza della tabella FileTable. Quando vengono individuate incoerenze, viene generato un errore e FileTable rimane disabilitata; in caso contrario la tabella FileTable viene riabilitata.  
  
-   L'applicazione della semantica FileTable, incluso i vincoli e i trigger definiti dal sistema, viene ripristinata.  
  
-   La directory FileTable, i file e le directory in essa contenute diventano visibili nel file system e disponibili per l'accesso I/O al file.  
  
###  <a name="HowToEnableNS"></a> Come si fa: Disabilitare e riabilitare lo spazio dei nomi FileTable a livello di tabella  
 Chiamare l'istruzione ALTER TABLE con l'opzione **{ ENABLE | DISABLE } FILETABLE_NAMESPACE** .  
  
 **Per disabilitare lo spazio dei nomi FileTable**  
 ```sql  
ALTER TABLE filetable_name  
    DISABLE FILETABLE_NAMESPACE;  
GO  
```  
  
 **Per riabilitare lo spazio dei nomi FileTable**  
 ```sql  
ALTER TABLE filetable_name  
    ENABLE FILETABLE_NAMESPACE;  
GO  
```  
  
##  <a name="BasicsKilling"></a> Terminazione di handle di file aperti associati a una tabella FileTable  
 Gli handle aperti per i file archiviati in una tabella FileTable possono impedire l'accesso esclusivo necessario per determinate attività di amministrazione. Per consentire attività urgenti, può essere necessario terminare gli handle di file aperti associati a una o più tabelle FileTable.  
  
> [!WARNING]  
>  La terminazione di handle di file aperti può causare la perdita dei dati non salvati da parte degli utenti. Questo comportamento è coerente con quello del file system stesso.  
  
###  <a name="HowToListOpen"></a> Come si fa: Ottenere un elenco di handle di File aperti associati a una tabella FileTable  
 Eseguire una query sulla vista del catalogo [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql).  
  
```sql  
SELECT * FROM sys.dm_filestream_non_transacted_handles;  
GO  
```  
  
###  <a name="HowToKill"></a> Come si fa: Terminare gli handle di file aperti associati a una tabella FileTable  
 Chiamare la stored procedure [sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles) con gli argomenti appropriati per terminare tutti gli handle di file aperti nel database o nella tabella FileTable o per terminare un handle specifico.  
  
```  
USE database_name;  
  
-- Kill all open handles in all the filetables in the database.  
EXEC sp_kill_filestream_non_transacted_handles;  
GO  
  
-- Kill all open handles in a single filetable.  
EXEC sp_kill_filestream_non_transacted_handles @table_name = 'filetable_name';  
GO  
  
-- Kill a single handle.  
EXEC sp_kill_filestream_non_transacted_handles @handle_id = integer_handle_id;  
GO  
```  
  
###  <a name="HowToIdentifyLocks"></a> Come si fa: Identificare i blocchi utilizzati da tabelle Filetable  
 La maggior parte dei blocchi applicati da tabelle FileTable corrisponde a file aperti dalle applicazioni.  
  
 **Identificazione di file aperti e blocchi associati**  
 Aggiungere il campo **request_owner_id** nella vista a gestione dinamica [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql) con il campo **fcb_id** in [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql). In alcuni casi, il blocco non corrisponde a un solo handle di file aperto.  
  
```sql  
SELECT opened_file_name  
    FROM sys.dm_filestream_non_transacted_handles  
    WHERE fcb_id IN  
        ( SELECT request_owner_id FROM sys.dm_tran_locks );  
GO  
```  
  
##  <a name="BasicsSecurity"></a> Sicurezza delle tabelle FileTable  
 I file e le directory archiviati nelle tabelle FileTable sono protetti solo dalla sicurezza di SQL. La sicurezza basata sulla tabella e sulla colonna è applicata per l'accesso al file system nonché per l'accesso a [!INCLUDE[tsql](../../includes/tsql-md.md)] . Le API di sicurezza del file system di Windows e le impostazioni ACL non sono supportate.  
  
 Alle tabelle File Table vengono applicate anche le autorizzazioni di sicurezza e accesso applicabili a filegroup e contenitori FILESTREAM, in quanto i dati dei file vengono archiviati come colonna FILESTREAM nella tabella FileTable.  
  
 **Sicurezza delle tabelle FileTable e accesso Transact-SQL**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] L'accesso ai dati nelle tabelle FileTable è protetto con la stessa modalità di qualsiasi altra tabella. Per ogni operazione di accesso o modifica dei dati, vengono effettuati controlli di sicurezza appropriati a livello di tabella e colonna.  
  
 **Sicurezza delle tabelle FileTable e accesso al file system**  
 Per aprire un handle per una directory o un file archiviato nella tabella FileTable tramite API del file system, saranno necessarie autorizzazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] appropriate per l'intera riga nella tabella FileTable (ovvero autorizzazioni a livello di tabella). Se l'utente non dispone dell'autorizzazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] appropriata per una qualsiasi colonna nella tabella FileTable, l'accesso al file system viene negato.  
  
##  <a name="OtherBackup"></a> Backup e tabelle FileTable  
 Quando si utilizza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire il backup di una tabella FileTable, viene eseguito il backup dei dati FILESTREAM con i dati strutturati nel database. Se non si desidera eseguire il backup dei dati FILESTREAM con i dati relazionali, è possibile utilizzare un backup parziale per escludere i filegroup FILESTREAM.  
  
 **Consistenza transazionale dei backup di FileTable**  
  
 Molti strumenti e operazioni di amministrazione, quali backup, backup del log e replica transazionale, leggono dati coerenti a livello di transazione tramite la lettura dei log delle transazioni. A questo punto, leggono tutti i dati FILESTREAM aggiornati come parte di una transazione. Quando l'accesso non transazionale non è abilitato a livello di database, questi strumenti e operazioni funzionano con coerenza transazionale completa.  
  
 Quando invece è abilitato l'accesso non transazionale completo, una tabella FileTable potrebbe contenere dati aggiornati più recentemente (tramite un aggiornamento non transazionale) rispetto alla transazione letta dallo strumento o dal processo dal log delle transazioni. Ciò significa che un'operazione di ripristino temporizzata di una transazione specifica può contenere dati FILESTREAM più recenti di tale transazione. Si tratta del comportamento previsto quando nelle tabelle FileTable sono consentiti gli aggiornamenti non transazionali.  
  
##  <a name="Monitor"></a> SQL Server Profiler e tabelle FileTable  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Il profiler può acquisire le operazioni di Windows File Open e File Close nell'output di traccia per i file archiviati in una tabella FileTable.  
  
##  <a name="OtherAuditing"></a> Controllo e tabelle FileTable  
 È possibile controllare una tabella FileTable proprio come qualsiasi altra tabella. I modelli di accesso Win32, tuttavia, non sono operazioni basate su set. Una singola azione nel file system si traduce in più operazioni DML Transact-SQL. L'apertura di un file in Microsoft Word, ad esempio, si traduce in più operazioni di apertura/chiusura/creazione/ridenominazione/eliminazione e nelle attività DML Transact-SQL corrispondenti. Ciò comporta record di controllo dettagliati in cui è difficile correlare i record tra azioni del file system e i record di controllo DML Transact-SQL corrispondenti.  
  
##  <a name="OtherDBCC"></a> DBCC e tabelle FileTable  
 È possibile utilizzare DBCC CHECKCONSTRAINTS per convalidare i vincoli su una tabella FileTable, inclusi i vincoli definiti dal sistema.  
  
## <a name="see-also"></a>Vedere anche  
 [Compatibilità di FileTable con altre funzionalità di SQL Server](filetable-compatibility-with-other-sql-server-features.md)   
 [DDL FileTable, funzioni, stored Procedure e viste](../views/views.md)  
  
  
