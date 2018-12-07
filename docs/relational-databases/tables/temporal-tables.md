---
title: Tabelle temporali | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: e442303d-4de1-494e-94e4-4f66c29b5fb9
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 967605ee7a4857347b4f1f7ca8ffc62ea0451d91
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403646"
---
# <a name="temporal-tables"></a>Tabelle temporali
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In SQL Server 2016 è stato introdotto il supporto per le tabelle temporali con controllo delle versioni del sistema come una funzionalità di database, che offre un supporto predefinito per la gestione delle informazioni sui dati archiviati nella tabella in qualsiasi momento anziché solo sui dati che risultano corretti nel momento attuale. Questa funzionalità di database è stata introdotta in SQL ANSI 2011.  
  
 **Avvio rapido**  
  
-   **Guida introduttiva:**  
  
    -   [Introduzione alle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)  
  
    -   [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)  
  
    -   [Scenari di utilizzo delle tabelle temporali](../../relational-databases/tables/temporal-table-usage-scenarios.md)  
  
    -   [Introduzione alle tabelle temporali nel database SQL Azure](https://azure.microsoft.com/documentation/articles/sql-database-temporal-tables/)  
  
-   **Esempi:**  
  
    -   [Creazione di una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)  
  
    -   [Utilizzo di una tabella temporale con controllo delle versioni di sistema e ottimizzazione per la memoria](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)  
  
    -   [Modifica dei dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)  
  
    -   [Query sui dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
    -   **Download del database di esempio Adventure Works:** per iniziare a usare le tabelle temporali, scaricare il [database AdventureWorks per SQL Server 2016 CTP3](https://www.microsoft.com/download/details.aspx?id=49502), che contiene esempi di script, e seguire le istruzioni nella cartella 'Temporal'  
  
-   **Sintassi:**  
  
    -   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
    -   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
    -   [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
-   **Video:** per una discussione di 20 minuti sulle tabelle temporali, vedere [Tabelle temporali in SQL Server 2016](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).  
  
## <a name="what-is-a-system-versioned-temporal-table"></a>Che cos'è una tabella temporale con controllo delle versioni di sistema?  
 Una tabella temporale con controllo delle versioni di sistema è un tipo di tabella utente progettato per mantenere una cronologia completa delle modifiche dei dati e semplificare l'analisi temporizzata. Questo tipo di tabella temporale è definito tabella temporale con controllo delle versioni di sistema perché il periodo di validità per ogni riga viene gestito dal sistema, ad esempio, il motore di database.  
  
 Ogni tabella temporale ha due colonne definite in modo esplicito, ciascuna con un tipo di dati **datetime2** . Queste colonne sono note come colonne periodo. Le colonne periodo vengono usate esclusivamente dal sistema per registrare il periodo di validità per ciascuna riga ogni volta che una riga viene modificata.  
  
 Oltre alle colonne periodo, una tabella temporale contiene anche un riferimento a un'altra tabella con schema con mirroring. Il sistema usa questa tabella per archiviare automaticamente la versione precedente della riga ogni volta che una riga della tabella temporale viene aggiornata o eliminata. Questa tabella aggiuntiva è detta tabella di cronologia, mentre la tabella principale che contiene le versioni attuali (effettive) delle righe è definita tabella corrente o semplicemente tabella temporale. Durante la creazione di una tabella temporale gli utenti possono specificare una tabella di cronologia esistente (deve essere conforme allo schema) oppure consentire al sistema di creare una tabella di cronologia predefinita.  
  
## <a name="why-temporal"></a>Perché temporale?  
 Le origini dati reali sono dinamiche e quasi sempre le decisioni aziendali si basano su approfondimenti che gli analisti ricavano dall'evoluzione dei dati. Alcuni casi d'uso delle tabelle temporali:  
  
-   Controllo di tutte le modifiche dei dati ed esecuzione di analisi forensi, se necessario  
  
-   Ricostruzione dello stato dei dati in qualsiasi momento trascorso  
  
-   Calcolo delle tendenze nel tempo  
  
-   Gestione di una dimensione a modifica lenta per le applicazioni di supporto decisionale  
  
-   Recupero da modifiche accidentali dei dati ed errori delle applicazioni  
  
## <a name="how-does-temporal-work"></a>Come funziona una tabella temporale?  
 Il controllo delle versioni di sistema per una tabella viene implementato come una coppia di tabelle, una tabella corrente e una tabella di cronologia. All'interno di ogni tabella vengono usate due colonne **datetime2** aggiuntive per definire il periodo di validità per ogni riga:  
  
-   Colonna di inizio periodo: il sistema registra l'ora di inizio per la riga in questa colonna, in genere indicata come colonna **SysStartTime** .  
  
-   Colonna di fine periodo: il sistema registra l'ora di fine per la riga in questa colonna, in genere indicata come colonna **SysEndTime** .  
  
 La tabella corrente contiene il valore corrente per ogni riga. La tabella di cronologia contiene ogni valore precedente per ogni riga, se presente, e l'ora di inizio e di fine del relativo periodo di validità.  
  
 ![Temporal-HowWorks](../../relational-databases/tables/media/temporal-howworks.PNG "Temporal-HowWorks")  
  
 L'esempio seguente illustra uno scenario con informazioni su Employee in un ipotetico database delle risorse umane:  
  
```  
CREATE TABLE dbo.Employee   
(    
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED   
  , [Name] nvarchar(100) NOT NULL  
  , [Position] varchar(100) NOT NULL   
  , [Department] varchar(100) NOT NULL  
  , [Address] nvarchar(1024) NOT NULL  
  , [AnnualSalary] decimal (10,2) NOT NULL  
  , [ValidFrom] datetime2 (2) GENERATED ALWAYS AS ROW START  
  , [ValidTo] datetime2 (2) GENERATED ALWAYS AS ROW END  
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)  
 )    
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));  
```  
  
 **INSERIMENTI:** su **INSERT**il sistema imposta il valore per la colonna **SysStartTime** sull'ora di inizio della transazione corrente (fuso orario UTC) in base al clock di sistema e assegna come valore per la colonna **SysEndTime** il valore massimo di 31-12-9999. In questo modo la riga viene contrassegnata come aperta.  
  
 **AGGIORNAMENTI:** su **UPDATE**il sistema archivia il valore precedente della riga nella tabella di cronologia e imposta il valore per la colonna **SysEndTime** sull'ora di inizio della transazione corrente (fuso orario UTC) in base al clock di sistema. In questo modo la riga viene contrassegnata come chiusa, con un periodo registrato in cui risultava valida. Nella tabella corrente la riga viene aggiornata con il nuovo valore e il sistema imposta il valore per la colonna **SysStartTime** sull'ora di inizio della transazione (fuso orario UTC) in base al clock di sistema. Il valore per la riga aggiornata nella tabella corrente per la colonna **SysEndTime** rimane il valore massimo di 31-12-9999.  
  
 **ELIMINAZIONI:** su **DELETE**il sistema archivia il valore precedente della riga nella tabella di cronologia e imposta il valore per la colonna **SysEndTime** sull'ora di inizio della transazione corrente (fuso orario UTC) in base al clock di sistema. In questo modo la riga viene contrassegnata come chiusa, con un periodo registrato in cui la riga precedente risultava valida. Nella tabella corrente la riga viene rimossa. Le query della tabella corrente non restituiscono questa riga. Solo le query che gestiscono i dati di cronologia restituiscono dati per i quali viene chiusa una riga.  
  
 **UNIONE:** su **MERGE**l'operazione si comporta esattamente come se fossero eseguite fino a tre istruzioni ( **INSERT**, **UPDATE**e/o **DELETE**), in base alle azioni specificate nell'istruzione **MERGE** .  
  
> [!IMPORTANT]  
>  I tempi registrati nelle colonne datetime2 del sistema sono basati sull'ora di inizio della transazione stessa. Ad esempio, tutte le righe inserite all'interno di una singola transazione avranno la stessa ora UTC registrata nella colonna corrispondente all'inizio del periodo **SYSTEM_TIME** .  
  
## <a name="how-do-i-query-temporal-data"></a>Come si esegue una query sui dati temporali?  
 La clausola **FROM**_\<tabella\>_ dell'istruzione **SELECT** usa una nuova clausola **FOR SYSTEM_TIME** con cinque sottoclausole specifiche per i dati temporali per eseguire query sui dati nelle tabelle correnti e di cronologia. La nuova sintassi dell'istruzione **SELECT** è supportata direttamente su una singola tabella, propagata attraverso diversi join e viste su più tabelle temporali.  
  
 ![Temporal-Querying](../../relational-databases/tables/media/temporal-querying.PNG "Temporal-Querying")  
  
 La query seguente esegue la ricerca di versioni delle righe della riga Employee con EmployeeID = 1000 attive almeno per una parte del periodo compreso tra il 1° gennaio 2014 e il 1° gennaio 2015, incluso il limite superiore:  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME    
        BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'   
            WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
> [!NOTE]  
>  **FOR SYSTEM_TIME** esclude le righe che hanno un periodo di validità con durata pari a zero (**SysStartTime** = **SysEndTime**).  
> Tali righe verranno generate se si eseguono più aggiornamenti sulla stessa chiave primaria nell'ambito della stessa transazione.  
> In questo caso, la query temporale rileva solo le versioni di riga precedenti alle transazioni e quelle che sono diventate effettive dopo le transazioni.  
> Se è necessario includere le righe nell'analisi, eseguire la query direttamente nella tabella di cronologia.  
  
 Nella tabella seguente il valore SysStartTime della colonna delle righe risultanti rappresenta il valore presente nella colonna **SysStartTime** della tabella su cui si esegue la query e **SysEndTime** rappresenta il valore presente nella colonna **SysEndTime** della tabella su cui si esegue la query. Per la sintassi completa e per esempi, vedere [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md) e [Query sui dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md).  
  
|Espressione|Righe risultanti|Descrizione|  
|----------------|---------------------|-----------------|  
|**AS OF**<date_time>|SysStartTime \<= date_time AND SysEndTime > date_time|Restituisce una tabella con una singola riga contenente i valori che erano effettivi (correnti) in un momento specificato nel passato. Internamente, viene eseguita un'unione tra la tabella temporale e la relativa tabella di cronologia e i risultati vengono filtrati in modo da restituire i valori nella riga che era valida nel momento specificato dal parametro *<date_time>*. Il valore per una riga viene considerato valido se il valore *system_start_time_column_name* è minore o uguale al valore del parametro *<date_time>* e il valore *system_end_time_column_name* è maggiore del valore del parametro *<date_time>*.|  
|**FROM**<start_date_time>**TO**<end_date_time>|SysStartTime < end_date_time AND SysEndTime > start_date_time|Restituisce una tabella con i valori per tutte le versioni di riga che erano attive nell'intervallo di tempo specificato, indipendentemente dal fatto che abbiano iniziato a essere attive prima del valore del parametro *<start_date_time>* per l'argomento FROM o non siano più state attive dopo il valore del parametro *<end_date_time>* per l'argomento TO. Internamente, viene eseguita un'unione tra la tabella temporale e la relativa tabella di cronologia e i risultati vengono filtrati in modo da restituire i valori per tutte le versioni di riga che erano attive in qualsiasi momento durante l'intervallo di tempo specificato. Le righe che non sono più state attive esattamente in corrispondenza del limite inferiore definito dall'endpoint FROM non sono incluse e le righe diventate attive esattamente in corrispondenza del limite superiore definito dall'endpoint TO non sono incluse.|  
|**BETWEEN**<start_date_time>**AND**<end_date_time>|SysStartTime \<= end_date_time AND SysEndTime > start_date_time|Come sopra per la descrizione di **FOR SYSTEM_TIME FROM** <start_date_time>**TO** <end_date_time>, tranne per il fatto che la tabella delle righe restituite include le righe diventate attive in corrispondenza del limite superiore definito dall'endpoint <end_date_time>.|  
|**CONTAINED IN** (<start_date_time> , <end_date_time>)|SysStartTime >= start_date_time AND SysEndTime \<= end_date_time|Restituisce una tabella con i valori per tutte le versioni di riga che sono state aperte e chiuse nell'intervallo di tempo specificato, definito dai due valori datetime per l'argomento CONTAINED IN. Sono incluse le righe diventate attive esattamente in corrispondenza del limite inferiore o che non sono più state attive esattamente in corrispondenza del limite superiore.|  
|**ALL**|Tutte le righe|Restituisce l'unione di righe che appartengono alla tabella corrente e a quella di cronologia.|  
  
> [!NOTE]  
>  Facoltativamente, è possibile scegliere di nascondere le colonne periodo in modo tale che le query che non fanno riferimento in modo esplicito alle colonne periodo non le restituiscano (scenario **SELECT \* FROM**_\<tabella\>_). Per restituire una colonna nascosta, basta fare riferimento in modo esplicito alla colonna nella query. Allo stesso modo, le istruzioni **INSERT** e **BULK INSERT** continueranno come se le nuove colonne periodo non fossero presenti (e i valori delle colonne saranno popolati automaticamente). Per altre informazioni sull'uso della clausola **HIDDEN** , vedere [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) e [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Scenari di utilizzo delle tabelle temporali](../../relational-databases/tables/temporal-table-usage-scenarios.md)   
 [Considerazioni e limitazioni delle tabelle temporali](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Gestire la conservazione dei dati cronologici nelle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Partizionamento con le tabelle temporali](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Verifiche di coerenza del sistema della tabella temporale](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Sicurezza di una tabella temporale](../../relational-databases/tables/temporal-table-security.md)   
 [Funzioni e viste per i metadati delle tabelle temporali](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
