---
title: Costrutti Transact-SQL non supportati da OLTP in memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e3f8009c-319d-4d7b-8993-828e55ccde11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dda74f247f9899b9e0a23d43143a5031574d8c13
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541230"
---
# <a name="transact-sql-constructs-not-supported-by-in-memory-oltp"></a>Costrutti Transact-SQL non supportati da OLTP in memoria
  Le tabelle con ottimizzazione per la memoria e le stored procedure compilate in modo nativo non supportano la superficie di attacco totale di [!INCLUDE[tsql](../../includes/tsql-md.md)] utilizzata dalle tabelle basate su disco e dalle stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretate. Quando si tenta di usare una delle funzionalità non supportate, il server restituisce un errore.  
  
 Nel testo del messaggio di errore viene indicato il tipo di istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] (ad esempio funzionalità, operazione, opzione) e il nome della funzionalità o della parola chiave [!INCLUDE[tsql](../../includes/tsql-md.md)] . La maggior parte delle funzionalità non supportate restituirà l'errore 10794, con il testo del messaggio di errore che indica la funzionalità non supportata. Nelle tabelle seguenti vengono elencate le parole chiave e le funzionalità di [!INCLUDE[tsql](../../includes/tsql-md.md)] che possono essere incluse nel testo del messaggio di errore e l'azione correttiva per risolvere l'errore.  
  
 Per altre informazioni sulle funzionalità supportate con tabelle ottimizzate per la memoria e stored procedure compilate in modo nativo, vedere:  
  
-   [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](migration-issues-for-natively-compiled-stored-procedures.md)  
  
-   [Supporto di Transact-SQL per OLTP in memoria](transact-sql-support-for-in-memory-oltp.md)  
  
-   [Funzionalità di SQL Server supportate](unsupported-sql-server-features-for-in-memory-oltp.md)  
  
-   [Stored procedure compilate in modo nativo](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
## <a name="databases-that-use-in-memory-oltp"></a>Database che utilizzano OLTP in memoria  
 Nella tabella seguente vengono elencate le funzionalità e le parole chiave [!INCLUDE[tsql](../../includes/tsql-md.md)] che possono essere incluse nel testo del messaggio di un errore relativo a un database OLTP in memoria.  
  
|Tipo|nome|Soluzione|  
|----------|----------|----------------|  
|Opzione|AUTO_CLOSE|L'opzione di database AUTO_CLOSE=ON non è supportata con i database che contengono un filegroup MEMORY_OPTIMIZED_DATA.|  
|Opzione|ATTACH_REBUILD_LOG|L'opzione di database CREATE ATTACH_REBUILD_LOG non è supportata con i database contenenti un filegroup MEMORY_OPTIMIZED_DATA.|  
|Funzionalità|DATABASE SNAPSHOT|La creazione di snapshot del database non è supportata con i database che contengono un filegroup MEMORY_OPTIMIZED_DATA.|  
|Funzionalità|Replica che utilizza 'database snapshot' o 'database snapshot character' come sync_method|La replica che utilizza 'database snapshot' or 'database snapshot character' come sync_method non è supportata con i database che contengono un filegroup MEMORY_OPTIMIZED_DATA.|  
|Funzionalità|DBCC CHECKDB<br /><br /> DBCC CHECKTABLE|DBCC CHECKDB ignora le tabelle ottimizzate per la memoria nel database.<br /><br /> DBCC CHECKTABLE avrà esito negativo per le tabelle ottimizzate per la memoria.|  
  
## <a name="memory-optimized-tables"></a>Tabelle con ottimizzazione per la memoria  
 Nella tabella seguente vengono elencate le parole chiave e le funzionalità di [!INCLUDE[tsql](../../includes/tsql-md.md)] che possono essere incluse nel testo del messaggio di un errore che interessa una tabella ottimizzata per la memoria e l'azione correttiva per risolvere l'errore.  
  
|Tipo|nome|Soluzione|  
|----------|----------|----------------|  
|Funzionalità|ON|Le tabelle con ottimizzazione per la memoria non possono essere posizionate in uno schema di partizione o filegroup. Rimuovere la clausola ON dall'istruzione `CREATE TABLE`.|  
|Tipo di dati|*Nome del tipo di dati*|Il tipo di dati indicato non è supportato. Sostituirlo con un tipo di dati supportato. Per altre informazioni, vedere [Supported Data Types](supported-data-types-for-in-memory-oltp.md).|  
|Funzionalità|Colonne calcolate|Le colonne calcolate non sono supportate dalle tabelle ottimizzate per la memoria. Rimuovere le colonne calcolate dall'istruzione `CREATE TABLE`.|  
|Funzionalità|Replica|La replica non è supportata con le tabelle ottimizzate per la memoria.|  
|Funzionalità|FILESTREAM|L'archiviazione FILESTREAM non è supportata dalle colonne delle tabelle ottimizzate per la memoria. Rimuovere la parola chiave `FILESTREAM` dalla definizione della colonna.|  
|Funzionalità|SPARSE|Le colonne delle tabelle ottimizzate per la memoria non possono essere definite come SPARSE. Rimuovere la parola chiave `SPARSE` dalla definizione della colonna.|  
|Funzionalità|ROWGUIDCOL|L'opzione ROWGUIDCOL non è supportata dalle colonne delle tabelle ottimizzate per la memoria. Rimuovere la parola chiave `ROWGUIDCOL` dalla definizione della colonna.|  
|Funzionalità|FOREIGN KEY|I vincoli FOREIGN KEY non sono supportati dalle tabelle ottimizzate per la memoria. Rimuovere il vincolo dalla definizione della tabella.<br /><br /> Per informazioni su come sopperire alla mancanza di supporto per i vincoli, vedere [eseguire la migrazione verificare e Foreign Key Constraints](../../database-engine/migrating-check-and-foreign-key-constraints.md).|  
|Funzionalità|CHECK|I vincoli CHECK non sono supportati dalle tabelle ottimizzate per la memoria. Rimuovere il vincolo dalla definizione della tabella.<br /><br /> Per informazioni su come sopperire alla mancanza di supporto per i vincoli, vedere [eseguire la migrazione verificare e Foreign Key Constraints](../../database-engine/migrating-check-and-foreign-key-constraints.md).|  
|Funzionalità|UNIQUE|I vincoli UNIQUE non sono supportati dalle tabelle ottimizzate per la memoria. Rimuovere il vincolo dalla definizione della tabella.<br /><br /> Per informazioni su come sopperire alla mancanza di supporto per i vincoli, vedere [eseguire la migrazione verificare e Foreign Key Constraints](../../database-engine/migrating-check-and-foreign-key-constraints.md).|  
|Funzionalità|COLUMNSTORE|Gli indici COLUMNSTORE non sono supportati con le tabelle ottimizzate per la memoria. Specificare invece un indice NON CLUSTER o HASH NON CLUSTER.|  
|Funzionalità|indice cluster|Specificare un indice non cluster. Nel caso di un indice di chiave primaria assicurarsi di specificare `PRIMARY KEY NONCLUSTERED [HASH]`.|  
|Funzionalità|tabella codici non 1252|Le colonne delle tabelle ottimizzate per la memoria con tipi di dati `char` e `varchar` devono usare la tabella codici 1252. Utilizzare n(var)char anziché (var)char oppure regole di confronto con tabella codici 1252, ad esempio Latin1_General_BIN2. Per altre informazioni, vedere [Collations and Code Pages](../../database-engine/collations-and-code-pages.md).|  
|Funzionalità|DDL all'interno delle transazioni|Le tabelle con ottimizzazione per la memoria e le stored procedure compilate in modo nativo non possono essere create o eliminate nel contesto di una transazione utente. Non avviare una transazione e assicurarsi che l'impostazione della sessione IMPLICIT_TRANSACTIONS sia OFF prima di eseguire l'istruzione CREATE o DROP.|  
|Funzionalità|trigger DDL|Le tabelle con ottimizzazione per la memoria e le stored procedure compilate in modo nativo non possono essere create o eliminate se esiste un trigger di database o di server per l'operazione DDL. Rimuovere i trigger di database e di server da CREATE/DROP TABLE e CREATE/DROP PROCEDURE.|  
|Funzionalità|EVENT NOTIFICATION|Le tabelle con ottimizzazione per la memoria e le stored procedure compilate in modo nativo non possono essere create o eliminate se esiste una notifica degli eventi di database o di server per l'operazione DDL. Rimuovere le notifiche degli eventi di database e di server in CREATE TABLE o DROP TABLE e CREATE PROCEDURE o DROP PROCEDURE.|  
|Funzionalità|FileTable|Le tabelle con ottimizzazione per la memoria non possono essere create come tabelle di file. Rimuovere l'argomento `AS FileTable` dall'istruzione `CREATE TABLE`.|  
|Operazione|Aggiornamento di colonne chiave primaria|Le colonne chiave primaria delle tabelle ottimizzate per la memoria e dei tipi di tabella non possono essere aggiornate. Se la chiave primaria deve essere aggiornata, eliminare la vecchia riga e inserire una nuova riga con la chiave primaria aggiornata.|  
|Operazione|CREATE INDEX|Gli indici delle tabelle ottimizzate per la memoria devono essere specificati inline con l'istruzione `CREATE TABLE`. Per aggiungere un indice in una tabella ottimizzata per la memoria, eliminare e ricreare la tabella includendo la nuova specifica dell'indice.|  
|Operazione|ALTER TABLE|La modifica delle tabelle ottimizzate per la memoria non è supportata. Eliminare e ricreare la tabella utilizzando la definizione della tabella aggiornata.|  
|Operazione|CREATE FULLTEXT INDEX|Gli indici full-text non sono supportati dalle tabelle ottimizzate per la memoria.|  
|Operazione|modifica schema|Le tabelle con ottimizzazione per la memoria e le stored procedure compilate in modo nativo non supportano le modifiche dello schema, ad esempio `sp_rename`.<br /><br /> Se si tenta di apportare modifiche allo schema, ad esempio di rinominare una tabella, verrà generato l'errore 12320. Le operazioni che richiedono una modifica alla versione dello schema, ad esempio la ridenominazione, non sono supportate con le tabelle ottimizzate per la memoria.<br /><br /> Per modificare lo schema, eliminare e ricreare la tabella o la procedura utilizzando una definizione aggiornata.|  
|Operazione|CREATE TRIGGER|I trigger non sono supportati nelle tabelle ottimizzate per la memoria.|  
|Operazione|TRUNCATE TABLE|L'operazione TRUNCATE non è supportata dalle tabelle ottimizzate per la memoria. Per rimuovere tutte le righe da una tabella, eliminare tutte le righe usando `DELETE FROM` *tabella* oppure eliminare e ricreare la tabella.|  
|Operazione|ALTER AUTHORIZATION|La modifica del proprietario di una tabella ottimizzata per la memoria o di una stored procedure compilata in modo nativo non è supportata. Eliminare e ricreare la tabella o la stored procedure per modificare la proprietà.|  
|Operazione|ALTER SCHEMA|La modifica dello schema di una tabella ottimizzata per la memoria o di una stored procedure compilata in modo nativo esistente non è supportata. Eliminare e ricreare la tabella o la stored procedure per modificare lo schema.|  
|Operazione|DBCC CHECKTABLE|DBCC CHECKTABLE non è supportato con le tabelle ottimizzate per la memoria.|  
|Funzionalità|ANSI_PADDING OFF|L'opzione di sessione `ANSI_PADDING` deve essere impostata su ON durante la creazione delle tabelle ottimizzate per la memoria e delle stored procedure compilate in modo nativo. Eseguire `SET ANSI_PADDING ON` prima di eseguire l'istruzione CREATE.|  
|Opzione|DATA_COMPRESSION|La compressione dati non è supportata dalle tabelle ottimizzate per la memoria. Rimuovere l'opzione dalla definizione della tabella.|  
|Funzionalità|DTC|Non è possibile accedere alle tabelle con ottimizzazione per la memoria e alle stored procedure compilate in modo nativo da transazioni distribuite. Utilizzare le transazioni SQL.|  
|Funzionalità|MARS (Multiple Active Result Sets)|MARS (Multiple Active Result Set) non è supportato con le tabelle ottimizzate per la memoria. L'errore può inoltre indicare l'utilizzo di un server collegato. Il server collegato può usare MARS. I server collegati non sono supportati con le tabelle ottimizzate per la memoria. Connettersi direttamente al server e al database che ospita le tabelle ottimizzate per la memoria.|  
|Operazione|Tabelle con ottimizzazione per la memoria come destinazione di MERGE|Le tabelle con ottimizzazione per la memoria non possono essere la destinazione di un'operazione `MERGE`. Utilizzare l'istruzione `INSERT`, `UPDATE` o `DELETE`.|  
  
## <a name="indexes-on-memory-optimized-tables"></a>Indici in tabelle con ottimizzazione per la memoria  
 Nella tabella seguente vengono elencate le parole chiave e le funzionalità di [!INCLUDE[tsql](../../includes/tsql-md.md)] che possono essere inclusi nel testo del messaggio di un errore che interessa l'indice di una tabella ottimizzata per la memoria e l'azione correttiva per risolvere l'errore.  
  
|Tipo|nome|Soluzione|  
|----------|----------|----------------|  
|Funzionalità|Indice filtrato|Gli indici filtrati non sono supportati con le tabelle ottimizzate per la memoria. Omettere la clausola `WHERE` dalla specifica dell'indice.|  
|Funzionalità|UNIQUE|Gli indici univoci non sono supportati dalle tabelle ottimizzate per la memoria. Rimuovere l'argomento `UNIQUE` dalla specifica dell'indice.|  
|Funzionalità|Colonne che ammettono i valori Null|Tutte le colonne della chiave di un indice in una tabella ottimizzata per la memoria devono essere specificate come `NOT NULL`. Includere il vincolo `NOT NULL` per tutte le colonne delle chiavi di indice.|  
|Funzionalità|regole di confronto non BIN2|Tutte le colonne di caratteri della chiave di un indice ottimizzato per la memoria devono essere dichiarate utilizzando le regole di confronto BIN2. Utilizzare la clausola `COLLATE` per impostare le regole di confronto nella definizione di colonna. Per altre informazioni, vedere [Collations and Code Pages](../../database-engine/collations-and-code-pages.md).|  
|Funzionalità|included_columns|Non è necessario specificare le colonne incluse per le tabelle ottimizzate per la memoria. Tutte le colonne della tabella ottimizzata per la memoria vengono incluse in modo implicito in ogni indice ottimizzato per la memoria.|  
|Operazione|ALTER INDEX|La modifica degli indici nelle tabelle ottimizzate per la memoria non è supportata. In alternativa, eliminare la tabella e ricrearla utilizzando la specifica dell'indice aggiornata.|  
|Operazione|DROP INDEX|L'eliminazione degli indici nelle tabelle ottimizzate per la memoria non è supportata. In alternativa, eliminare la tabella e ricrearla con gli indici desiderati.|  
|Opzione dell'indice|*Opzione di indice*|L'opzione di indice indicata non è supportata con gli indici delle tabelle ottimizzate per la memoria. Rimuovere l'opzione dalla specifica dell'indice.|  
  
## <a name="nonclustered-hash-indexes"></a>Indici hash non cluster  
 Nella tabella seguente vengono elencate le parole chiave e le funzionalità di [!INCLUDE[tsql](../../includes/tsql-md.md)] che possono essere incluse nel testo del messaggio di un errore che interessa un indice hash non cluster e l'azione correttiva per risolvere l'errore.  
  
|Tipo|nome|Soluzione|  
|----------|----------|----------------|  
|Opzione|ASC/DESC|Gli indici hash non cluster non sono ordinati. Rimuovere le parole chiave `ASC` e `DESC` dalla specifica della chiave di indice.|  
  
## <a name="natively-compiled-stored-procedures"></a>stored procedure compilate in modo nativo  
 Nella tabella seguente vengono elencate le parole chiave e le funzionalità di [!INCLUDE[tsql](../../includes/tsql-md.md)] che possono essere incluse nel testo del messaggio di un errore che interessa le stored procedure compilate in modo nativo e l'azione correttiva per risolvere l'errore.  
  
|Tipo|Funzionalità|Soluzione|  
|----------|-------------|----------------|  
|Funzionalità|Variabili di tabella inline|I tipi di tabella non possono essere dichiarati inline con le dichiarazioni di variabili. I tipi di tabella devono essere dichiarati in modo esplicito utilizzando un'istruzione `CREATE TYPE`.|  
|Funzionalità|Cursori|I cursori non sono supportati nelle stored procedure compilate in modo nativo.<br /><br /> -Quando si esegue la procedura dal client, usare RPC anziché l'API cursore. Con ODBC, evitare l'istruzione `EXECUTE` di [!INCLUDE[tsql](../../includes/tsql-md.md)] e specificare direttamente il nome della procedura.<br /><br /> -Quando si esegue la procedura da un [!INCLUDE[tsql](../../includes/tsql-md.md)] batch o un'altra stored procedure, evitare di utilizzare un cursore con la stored procedure compilata in modo nativo.<br /><br /> -Quando si crea una stored procedure compilata in modo nativo, anziché utilizzare un cursore, usare la logica basata su set o un `WHILE` ciclo.|  
|Funzionalità|Valori predefiniti del parametro non costanti|Quando si utilizzano i valori predefiniti con i parametri nelle stored procedure compilate in modo nativo, i valori devono essere costanti. Rimuovere tutti i caratteri jolly dalle dichiarazioni di parametro.|  
|Funzionalità|EXTERNAL|Le stored procedure CLR non possono essere compilate in modo nativo. Rimuovere la clausola AS EXTERNAL o l'opzione NATIVE_COMPILATION dall'istruzione CREATE PROCEDURE.|  
|Funzionalità|Stored procedure numerate|Le stored procedure compilate in modo nativo non possono essere numerate. Rimuovere il `;` *numero* dal `CREATE PROCEDURE` istruzione.|  
|Funzionalità|INSERT di più righe... Istruzioni VALUES|Non è possibile inserire più righe utilizzando la stessa istruzione `INSERT` in una stored procedure compilata in modo nativo. Creare istruzioni `INSERT` per ogni riga.|  
|Funzionalità|Espressioni di tabella comuni|Le espressioni di tabella comuni (CTE) non sono supportate nelle stored procedure compilate in modo nativo. Riformulare la query.|  
|Funzionalità|Sottoquery|Le sottoquery (query annidata in un'altra query) non sono supportate. Riformulare la query.|  
|Funzionalità|COMPUTE|La clausola `COMPUTE` non è supportata. Rimuoverla dalla query.|  
|Funzionalità|SELECT INTO|La clausola `INTO` non è supportata con l'istruzione `SELECT`. Riscrivere la query come `INSERT INTO` *tabella*`SELECT`.|  
|Funzionalità|OUTPUT|La clausola `OUTPUT` non è supportata. Rimuoverla dalla query.|  
|Funzionalità|elenco delle colonne di inserimento incompleto|Nelle istruzioni `INSERT`, i valori devono essere specificati per tutte le colonne della tabella.|  
|Funzione|*Funzione*|La funzione predefinita non è supportata nelle stored procedure compilate in modo nativo. Rimuovere la funzione dalla stored procedure. Per altre informazioni sulle funzioni predefinite supportate, vedere [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Funzionalità|CASE|L'istruzione `CASE` non è supportata nelle query all'interno di stored procedure compilate in modo nativo. Creare query per ogni istruzione CASE. Per altre informazioni, vedere [implementazione di un'istruzione CASE](implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md).|  
|Funzionalità|funzioni definite dall'utente|Le funzioni definite dall'utente non possono essere utilizzate nelle stored procedure compilate in modo nativo. Rimuovere il riferimento alla funzione dalla definizione delle procedure.|  
|Funzionalità|aggregazioni definite dall'utente|Le funzioni di aggregazione definite dall'utente non possono essere utilizzate nelle stored procedure compilate in modo nativo. Rimuovere il riferimento alla funzione dalla procedura.|  
|Funzionalità|metadati in modalità browse|Nelle stored procedure compilate in modo nativo non è ancora previsto il supporto per i metadati in modalità browse. Accertarsi che l'opzione di sessione `NO_BROWSETABLE` sia impostata su OFF.|  
|Funzionalità|DELETE con clausola FROM|La clausola `FROM` non è supportata dalle istruzioni `DELETE` con un'origine della tabella nelle stored procedure compilate in modo nativo.<br /><br /> `DELETE` con la clausola `FROM` è supportata quando viene utilizzata per indicare la tabella da cui eseguire l'eliminazione.|  
|Funzionalità|UPDATE con clausola FROM|La clausola `FROM` non è supportata dalle istruzioni `UPDATE` nelle stored procedure compilate in modo nativo.|  
|Funzionalità|stored procedure temporanee|Le stored procedure temporanee non possono essere compilate in modo nativo. Creare una stored procedure compilata in modo nativo permanente o una stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] temporaneamente interpretata.|  
|Livello di isolamento|READ UNCOMMITTED|Il livello di isolamento READ UNCOMMITTED non è supportato dalle stored procedure compilate in modo nativo. Utilizzare un livello di isolamento supportato, ad esempio SNAPSHOT.|  
|Livello di isolamento|READ COMMITTED|Il livello di isolamento READ UNCOMMITTED non è supportato dalle stored procedure compilate in modo nativo. Utilizzare un livello di isolamento supportato, ad esempio SNAPSHOT.|  
|Funzionalità|tabelle temporanee|Le tabelle del tempdb non possono essere utilizzate nelle stored procedure compilate in modo nativo. In alternativa, usare una variabile di tabella o una tabella ottimizzata per la memoria con DURABILITY=SCHEMA_ONLY.|  
|Funzionalità|MARS|MARS (Multiple Active Result Sets) non è supportato con le stored procedure compilate in modo nativo. L'errore può inoltre indicare l'utilizzo di un server collegato. Il server collegato può usare MARS. I server collegati non sono supportati con le stored procedure compilate in modo nativo. Connettersi direttamente al server e al database che ospita le stored procedure compilate in modo nativo.|  
|Funzionalità|DTC|Non è possibile accedere alle tabelle con ottimizzazione per la memoria e alle stored procedure compilate in modo nativo da transazioni distribuite. Utilizzare le transazioni SQL.|  
|Funzionalità|regole di confronto non BIN2|Il confronto, l'ordinamento e altre operazioni delle stringhe di caratteri nelle stored procedure compilate in modo nativo richiedono l'utilizzo di regole di confronto BIN2. Utilizzare la clausola COLLATE oppure le colonne e le variabili con le regole di confronto appropriate. Per altre informazioni, vedere [Collations and Code Pages](../../database-engine/collations-and-code-pages.md).|  
|Funzionalità|Troncamento delle stringhe di caratteri con regole di confronto SC.|Le stringhe di caratteri con le regole di confronto `_SC` utilizzano la codifica UTF-16. La conversione di un valore n(var)char in un valore n(var)char con lunghezza ridotta comporta il troncamento. Ciò non è supportato per i valori UTF-16 delle stored procedure compilate in modo nativo. Evitare il troncamento delle stringhe UTF-16.|  
|Funzionalità|EXECUTE WITH RECOMPILE|L'opzione `WITH RECOMPILE` non è supportata dalle stored procedure compilate in modo nativo.|  
|Funzionalità|LEN e SUBSTRING con un argomento nelle regole di confronto SC|Le stringhe di caratteri con le regole di confronto _SC utilizzano la codifica UTF-16. Le funzioni predefinite LEN e SUBSTRING, quando utilizzate all'interno di stored procedure compilate in modo native, non supportano la codifica UTF-16. Utilizzare regole di confronto diverse o evitare di usare queste funzioni.|  
|Funzionalità|Esecuzione dalla connessione amministrativa dedicata.|Le stored procedure compilate in modo nativo non possono essere eseguite dalla connessione amministrativa dedicata. Utilizzare una connessione normale.|  
|Operazione|ALTER PROCEDURE|Le stored procedure compilate in modo nativo non possono essere modificate. Per modificare la definizione della procedura, eliminare e ricreare la stored procedure.|  
|Operazione|punto di salvataggio|Le stored procedure compilate in modo nativo non possono essere richiamate dalle transazioni che hanno un punto di salvataggio attivo. Rimuovere il punto di salvataggio dalla transazione.|  
|Operazione|ALTER AUTHORIZATION|La modifica del proprietario di una tabella ottimizzata per la memoria o di una stored procedure compilata in modo nativo non è supportata. Eliminare e ricreare la tabella o la stored procedure per modificare la proprietà.|  
|Operatore|OPENROWSET|Questo operatore non è supportato. Rimuovere `OPENROWSET` dalla stored procedure compilata in modo nativo.|  
|Operatore|OPENQUERY|Questo operatore non è supportato. Rimuovere `OPENQUERY` dalla stored procedure compilata in modo nativo.|  
|Operatore|OPENDATASOURCE|Questo operatore non è supportato. Rimuovere `OPENDATASOURCE` dalla stored procedure compilata in modo nativo.|  
|Operatore|OPENXML|Questo operatore non è supportato. Rimuovere `OPENXML` dalla stored procedure compilata in modo nativo.|  
|Operatore|CONTAINSTABLE|Questo operatore non è supportato. Rimuovere `CONTAINSTABLE` dalla stored procedure compilata in modo nativo.|  
|Operatore|FREETEXTTABLE|Questo operatore non è supportato. Rimuovere `FREETEXTTABLE` dalla stored procedure compilata in modo nativo.|  
|Funzionalità|funzioni con valori di tabella|Non è possibile fare riferimento alle funzioni con valori di tabella nelle stored procedure compilate in modo nativo. Una soluzione alternativa possibile per questa restrizione consiste nell'aggiungere la logica nelle funzioni con valori di tabella al corpo della procedura.|  
|Operatore|CHANGETABLE|Questo operatore non è supportato. Rimuovere `CHANGETABLE` dalla stored procedure compilata in modo nativo.|  
|Operatore|GOTO|Questo operatore non è supportato. Utilizzare altri costrutti procedurali come WHILE.|  
|Operatore|EXECUTE, INSERT EXEC|L'annidamento di stored procedure compilate in modo nativo non è supportato. Le operazioni necessarie possono essere specificate inline durante la definizione della stored procedure.|  
|Operatore|OFFSET|Questo operatore non è supportato. Rimuovere `OFFSET` dalla stored procedure compilata in modo nativo.|  
|Operatore|UNION|Questo operatore non è supportato. Rimuovere `UNION` dalla stored procedure compilata in modo nativo. La combinazione di più set di risultati in un unico set di risultati può essere effettuata utilizzando una variabile di tabella.|  
|Operatore|INTERSECT|Questo operatore non è supportato. Rimuovere `INTERSECT` dalla stored procedure compilata in modo nativo. In alcuni casi è possibile usare INNER JOIN per ottenere lo stesso risultato.|  
|Operatore|EXCEPT|Questo operatore non è supportato. Rimuovere `EXCEPT` dalla stored procedure compilata in modo nativo.|  
|Operatore|OUTER JOIN|Questo operatore non è supportato. Rimuovere `OUTER JOIN` dalla stored procedure compilata in modo nativo. Per altre informazioni, vedere [implementazione di un Outer Join](implementing-an-outer-join.md).|  
|Operatore|APPLY|Questo operatore non è supportato. Rimuovere `APPLY` dalla stored procedure compilata in modo nativo.|  
|Operatore|PIVOT|Questo operatore non è supportato. Rimuovere `PIVOT` dalla stored procedure compilata in modo nativo.|  
|Operatore|UNPIVOT|Questo operatore non è supportato. Rimuovere `UNPIVOT` dalla stored procedure compilata in modo nativo.|  
|Operatore|OR, IN|La disgiunzione (OR, IN) non è supportata nella clausola WHERE delle query nelle stored procedure compilate in modo nativo. Creare query per ciascun caso.|  
|Operatore|CONTAINS|Questo operatore non è supportato. Rimuovere `CONTAINS` dalla stored procedure compilata in modo nativo.|  
|Operatore|FREETEXT|Questo operatore non è supportato. Rimuovere `FREETEXT` dalla stored procedure compilata in modo nativo.|  
|Operatore|NOT|Questo operatore non è supportato. Rimuovere `NOT` dalla stored procedure compilata in modo nativo. In alcuni casi, `NOT` può essere sostituito dalla disuguaglianza. Ad esempio, `NOT a=b` può essere sostituito da `a!=b`.|  
|Operatore|TSEQUAL|Questo operatore non è supportato. Rimuovere `TSEQUAL` dalla stored procedure compilata in modo nativo.|  
|Operatore|LIKE|Questo operatore non è supportato. Rimuovere `LIKE` dalla stored procedure compilata in modo nativo.|  
|Operatore|NEXT VALUE FOR|Non è possibile fare riferimento alle sequenze all'interno di stored procedure compilate in modo nativo. Ottenere il valore utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretato, quindi passarlo alla stored procedure compilata in modo nativo. Per altre informazioni, vedere [Implementazione di IDENTITY in una tabella con ottimizzazione per la memoria](implementing-identity-in-a-memory-optimized-table.md).|  
|Opzione SET|*opzione*|Le opzioni SET non possono essere modificate all'interno di stored procedure compilate in modo nativo. Alcune opzioni possono essere impostate tramite l'istruzione BEGIN ATOMIC. Per altre informazioni, vedere la sezione relativa ai blocchi atonici in [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Operando|TABLESAMPLE|Questo operatore non è supportato. Rimuovere `TABLESAMPLE` dalla stored procedure compilata in modo nativo.|  
|Opzione|RECOMPILE|Le stored procedure compilate in modo nativo vengono compilate al momento della creazione. Per ricompilare una stored procedure compilata in modo nativo è necessario eliminarla e ricrearla. Rimuovere `RECOMPILE` dalla definizione della procedura.|  
|Opzione|ENCRYPTION|Questa opzione non è supportata. Rimuovere `ENCRYPTION` dalla definizione della procedura.|  
|Opzione|FOR REPLICATION|Le stored procedure compilate in modo nativo non possono essere create per la replica. Rimuovere `FOR REPLICATION` dalla definizione della procedura.|  
|Opzione|FOR XML|Questa opzione non è supportata. Rimuovere `FOR XML` dalla stored procedure compilata in modo nativo.|  
|Opzione|FOR BROWSE|Questa opzione non è supportata. Rimuovere `FOR BROWSE` dalla stored procedure compilata in modo nativo.|  
|Hint per il join|HASH, MERGE|Nelle stored procedure compilate in modo nativo sono supportati solo i join a cicli annidati. I join merge e hash non sono supportati. Rimuovere l'hint per il join.|  
|Hint per la query|*Hint per la query*|Questo hint per la query non è all'interno di stored procedure compilate in modo nativo. Per gli hint per la query supportati, vedere [Hint per la query &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query).|  
|Opzione|DISTINCT|Questa opzione non è supportata. Rimuovere `DISTINCT` dalla query nella stored procedure compilata in modo nativo.|  
|Opzione|PERCENT|Questa opzione non è supportata con le clausole `TOP`. Rimuovere `PERCENT` dalla query nella stored procedure compilata in modo nativo.|  
|Opzione|WITH TIES|Questa opzione non è supportata con le clausole `TOP`. Rimuovere `WITH TIES` dalla query nella stored procedure compilata in modo nativo.|  
|Funzione di aggregazione|*Funzione di aggregazione*|Questa clausola non è supportata. Per altre informazioni sulle funzioni di aggregazione delle stored procedure compilate in modo nativo, vedere [Natively Compiled Stored Procedures](../in-memory-oltp/natively-compiled-stored-procedures.md).|  
|Funzione di rango|*Funzione di rango*|Le funzioni di rango non sono supportate nelle stored procedure compilate in modo nativo. Rimuoverle dalla definizione della procedura.|  
|Funzione|*Funzione*|Questa funzione non è supportata. Rimuoverla dalla stored procedure compilata in modo nativo.|  
|.|*Istruzione*|Questa istruzione non è supportata. Rimuoverla dalla stored procedure compilata in modo nativo.|  
|Funzionalità|MIN e MAX utilizzati con stringhe binarie e di caratteri|Le funzioni di aggregazione `MIN` e `MAX` non possono essere utilizzate per i valori delle stringhe binarie e di caratteri all'interno di stored procedure compilate in modo nativo.|  
|Funzionalità|GROUP BY senza funzione di aggregazione|Nelle stored procedure compilate in modo nativo, se una query include una clausola `GROUP BY` deve usare anche una funzione di aggregazione nella clausola SELECT o HAVING. Aggiungere una funzione di aggregazione alla query.|  
|Funzionalità|GROUP BY ALL|ALL non può essere utilizzato con le clausole GROUP BY nelle stored procedure compilate in modo nativo. Rimuovere ALL dalla clausola GROUP BY.|  
|Funzionalità|GROUP BY ()|il raggruppamento da un elenco vuoto non è supportato. Rimuovere la clausola GROUP BY o includere colonne nell'elenco di raggruppamento.|  
|Funzionalità|ROLLUP|`ROLLUP` non può essere utilizzato con le clausole `GROUP BY` nelle stored procedure compilate in modo nativo. Rimuovere `ROLLUP` dalla definizione della procedura.|  
|Funzionalità|CUBE|`CUBE` non può essere utilizzato con le clausole `GROUP BY` nelle stored procedure compilate in modo nativo. Rimuovere `CUBE` dalla definizione della procedura.|  
|Funzionalità|GROUPING SETS|`GROUPING SETS` non può essere utilizzato con le clausole `GROUP BY` nelle stored procedure compilate in modo nativo. Rimuovere `GROUPING SETS` dalla definizione della procedura.|  
|Funzionalità|BEGIN TRANSACTION, COMMIT TRANSACTION e ROLLBACK TRANSACTION|Utilizzare i blocchi ATOMIC per controllare le transazioni e la gestione degli errori. Per altre informazioni, vedere [Atomic Blocks](atomic-blocks-in-native-procedures.md).|  
|Funzionalità|Dichiarazioni di variabili di tabelle inline.|Le variabili di tabella devono fare riferimento ai tipi di tabella ottimizzata per la memoria definiti in modo esplicito. È consigliabile creare un tipo di tabella ottimizzata per la memoria e usare tale tipo per la dichiarazione di variabili, anziché specificare il tipo inline.|  
|Funzionalità|sp_recompile|La ricompilazione di stored procedure compilate in modo nativo non è supportata. Eliminare e ricreare la stored procedure.|  
|Funzionalità|EXECUTE AS CALLER|La clausola `EXECUTE AS` è obbligatoria. Ma `EXECUTE AS CALLER` non è supportato. Uso `EXECUTE AS OWNER`, `EXECUTE AS` *utente*, o `EXECUTE AS SELF`.|  
|Funzionalità|Tabelle basate su disco|Non è possibile accedere alle tabelle basate su dico dalle stored procedure compilate in modo nativo. Rimuovere i riferimenti alle tabelle basate su disco dalle stored procedure compilate in modo nativo. In alternativa, eseguire la migrazione delle tabelle basate su disco alle tabelle con ottimizzazione per la memoria.|  
|Funzionalità|Visualizzazioni|Non è possibile accedere alle viste dalle stored procedure compilate in modo nativo. Anziché alle viste, fare riferimento alle tabelle di base sottostanti.|  
|Funzionalità|Funzioni con valori di tabella|Non è possibile accedere alle funzioni con valori di tabella dalle stored procedure compilate in modo nativo. Rimuovere i riferimenti alle funzioni con valori di tabella dalle stored procedure compilate in modo nativo.|  
  
## <a name="transactions-that-access-memory-optimized-tables"></a>Transazioni che accedono alle tabelle con ottimizzazione per la memoria  
 Nella tabella seguente vengono elencate le parole chiave e le funzionalità di [!INCLUDE[tsql](../../includes/tsql-md.md)] che possono essere incluse nel testo del messaggio di un errore che interessa le transazioni che accedono alle tabelle ottimizzate per la memoria e l'azione correttiva per risolvere l'errore.  
  
|Tipo|nome|Soluzione|  
|----------|----------|----------------|  
|Funzionalità|punto di salvataggio|La creazione di punti di salvataggio espliciti nelle transazioni che accedono alle tabelle ottimizzate per la memoria non è supportata.|  
|Funzionalità|transazione associata|Le sessioni associate non possono partecipare alle transazioni che accedono alle tabelle ottimizzate per la memoria. Non associare la sessione prima di eseguire la procedura.|  
|Funzionalità|DTC|Le transazioni che accedono alle tabelle ottimizzate per la memoria non possono essere transazioni distribuite.|  
  
## <a name="see-also"></a>Vedere anche  
 [Migrazione a OLTP in memoria](migrating-to-in-memory-oltp.md)  
  
  
