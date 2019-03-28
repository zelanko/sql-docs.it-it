---
title: Costrutti è supportato nelle Stored procedure compilate in modo nativo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 05515013-28b5-4ccf-9a54-ae861448945b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4fd1a406848006739b83c1b8a0886d5c2d4bdfa
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527143"
---
# <a name="supported-constructs-in-natively-compiled-stored-procedures"></a>Costrutti supportati in stored procedure compilate in modo nativo
  In questo argomento contiene un elenco delle funzionalità supportate per le stored procedure compilate in modo nativo ([CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)):  
  
-   [Programmabilità nelle Stored procedure compilate in modo nativo](#pncsp)  
  
-   [Operatori supportati](#so)  
  
-   [Funzioni predefinite nelle Stored procedure compilate in modo nativo](#bfncsp)  
  
-   [Superficie di query nelle Stored procedure compilate in modo nativo](#qsancsp)  
  
-   [Controllo](#auditing)  
  
-   [Nella tabella, Query e gli hint di Join](#tqh)  
  
-   [Limitazioni relative all'ordinamento](#los)  
  
 Per informazioni sui tipi di dati supportati nelle stored procedure compilate in modo nativo, vedere [Supported Data Types](supported-data-types-for-in-memory-oltp.md).  
  
 Per informazioni complete sui costrutti non supportati e per informazioni su come sopperire ad alcune funzionalità non supportate nelle stored procedure compilate in modo nativo, vedere [Migration Issues for Natively Compiled Stored Procedures](migration-issues-for-natively-compiled-stored-procedures.md). Per altre informazioni su funzionalità non supportate, vedere [Costrutti Transact-SQL non supportati da OLTP in memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
##  <a name="pncsp"></a> Programmabilità nelle Stored procedure compilate in modo nativo  
 Sono supportati gli elementi seguenti:  
  
-   BEGIN ATOMIC (al livello esterno della stored procedure), LANGUAGE, ISOLATION LEVEL, DATEFORMAT e DATEFIRST.  
  
-   Dichiarazione di variabili come NULL o NOT NULL. Se una variabile viene dichiarata come NOT NULL, la dichiarazione deve avere un inizializzatore. Se la variabile non viene dichiarata come NOT NULL, un inizializzatore è facoltativo.  
  
-   IF e WHILE.  
  
-   INSERT/UPDATE/DELETE  
  
     Le sottoquery non sono supportate. Nella clausola WHERE o HAVING, AND e BETWEEN sono supportati; OR, NOT IN e IN non sono supportati.  
  
-   Tipi di tabella con ottimizzazione per la memoria e variabili di tabella.  
  
-   RETURN  
  
-   SELECT  
  
-   SET  
  
-   TRY/CATCH/THROW  
  
     Per ottimizzare le prestazioni, utilizzare un solo blocco TRY/CATCH per un'intera stored procedure compilata in modo nativo.  
  
##  <a name="so"></a> Operatori supportati  
 Di seguito vengono elencati gli operatori supportati.  
  
-   [Gli operatori di confronto &#40;Transact-SQL&#41; ](/sql/t-sql/language-elements/comparison-operators-transact-sql) (ad esempio, >, \<, > =, e < =) sono supportati nelle condizionali (IF, mentre).  
  
-   Operatori unari (+, -).  
  
-   Operatori binari (*, /, +, -, % (modulo)).  
  
     L'operatore di addizione (+) è supportato sia con i numeri che con le stringhe.  
  
-   Operatori logici (AND, OR, NOT). OR e NOT sono supportati nelle istruzioni IF e WHILE ma non nelle clausole WHERE o HAVING.  
  
-   Operatori bit per bit ~, &, | e ^  
  
##  <a name="bfncsp"></a> Funzioni predefinite nelle Stored procedure compilate in modo nativo  
 Le seguenti funzioni sono supportate nei vincoli predefiniti nelle tabelle ottimizzate per la memoria e nelle stored procedure compilate in modo nativo.  
  
-   Funzioni matematiche: ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, EXP, LOG, LOG10, PI, POWER, RADIANS, RAND, SIN, SQRT, SQUARE e TAN  
  
-   Funzioni di data: CURRENT_TIMESTAMP, DATEADD, DATEDIFF, DATEFROMPARTS, DATEPART, DATETIME2FROMPARTS, DATETIMEFROMPARTS, DAY, EOMONTH, GETDATE, GETUTCDATE, MONTH, SMALLDATETIMEFROMPARTS, SYSDATETIME, SYSUTCDATETIME e YEAR.  
  
-   Funzioni per i valori stringa: LEN, LTRIM, RTRIM e SUBSTRING  
  
-   Funzione di identità: SCOPE_IDENTITY  
  
-   Funzione NULL: ISNULL  
  
-   Funzioni di identificazione univoca: NEWID e NEWSEQUENTIALID  
  
-   Funzioni di errore: ERROR_LINE, ERROR_MESSAGE, ERROR_NUMBER, ERROR_PROCEDURE, ERROR_SEVERITY ed ERROR_STATE  
  
-   Conversioni: CAST e CONVERT. Le conversioni tra stringhe di caratteri Unicode e non Unicode (n(var)char e (var)char) non sono supportate.  
  
-   Funzioni di sistema: @@rowcount. Le istruzioni all'interno di stored procedure compilate in modo nativo aggiornano @@rowcount ed è possibile usare @@rowcount in una stored procedure compilata in modo nativo per determinare il numero di righe interessate dall'ultima istruzione eseguita all'interno della stored procedure. Tuttavia, @@rowcount viene reimpostato su 0 all'inizio e alla fine dell'esecuzione di una stored procedure compilata in modo nativo.  
  
##  <a name="qsancsp"></a> Superficie di query nelle Stored procedure compilate in modo nativo  
 Sono supportati gli elementi seguenti:  
  
-   BETWEEN  
  
-   Alias di nomi di colonna (utilizzando la sintassi AS o =).  
  
-   CROSS JOIN e INNER JOIN, supportati solo con query SELECT.  
  
-   Le espressioni sono supportate nell'elenco SELECT e [dove &#40;Transact-SQL&#41; ](/sql/t-sql/queries/where-transact-sql) clausola se si usa un operatore supportato. Vedere [Operatori supportati](#so) per l'elenco degli operatori attualmente supportati.  
  
-   Predicato del filtro IS [NOT] NULL  
  
-   DA \<tabella con ottimizzazione per la memoria >  
  
-   [GROUP BY &#40;Transact-SQL&#41; ](/sql/t-sql/queries/select-group-by-transact-sql) è supportato, con le funzioni di aggregazione AVG, COUNT, COUNT_BIG, MIN, MAX e SUM. MIN e MAX non sono supportate per i tipi nvarchar, char, varchar, varchar, varbinary e binary. [Clausola ORDER BY &#40;Transact-SQL&#41; ](/sql/t-sql/queries/select-order-by-clause-transact-sql) è supportato con [GROUP BY &#40;Transact-SQL&#41; ](/sql/t-sql/queries/select-group-by-transact-sql) se un'espressione nell'elenco ORDER BY appare in modo identico nell'elenco GROUP BY. Ad esempio, l'espressione GROUP BY a + b ORDER BY a + b è supportata, ma GROUP BY a, b ORDER BY a + b non lo è.  
  
-   HAVING, soggetto alle stesse limitazioni delle espressioni della clausola WHERE.  
  
-   INSERT VALUES (una riga per istruzione) e INSERT SELECT  
  
-   ORDER BY <sup>1</sup>  
  
-   Predicati che non fanno riferimento a una colonna  
  
-   SELECT, UPDATE e DELETE  
  
-   TOP <sup>1</sup>  
  
-   Assegnazione di variabile nell'elenco SELECT.  
  
-   POSIZIONE IN CUI... AND  
  
 <sup>1</sup> ORDER BY e TOP sono supportati nelle stored procedure compilate in modo nativo, con alcune restrizioni:  
  
-   `DISTINCT` non è supportata nella clausola `SELECT` o `ORDER BY`.  
  
-   `WITH TIES` o `PERCENT` non è supportata nella clausola `TOP`.  
  
-   `TOP` in combinazione con `ORDER BY` non supporta un valore superiore a 8.192 quando si utilizza una costante nella clausola `TOP`. Questo limite può risultare più basso nel caso in cui la query contenga funzioni di aggregazione o dei join. Ad esempio, con un join (due tabelle) il limite scende a 4.096 righe. Con due join (tre tabelle) il limite è 2.730 righe.  
  
     È possibile che si ottengano risultati maggiori di 8.192 archiviando il numero di righe in una variabile:  
  
    ```sql  
    DECLARE @v INT = 9000  
    SELECT TOP (@v) ... FROM ... ORDER BY ...  
    ```  
  
 Tuttavia, una costante nella clausola `TOP` assicura prestazioni migliori rispetto a una variabile.  
  
 Queste limitazioni non si applicano all'accesso [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretato nelle tabelle ottimizzate per la memoria.  
  
##  <a name="auditing"></a> Controllo  
 Il controllo a livello di routine è supportato nelle stored procedure compilate in modo nativo. Il controllo a livello di istruzione non è supportato.  
  
 Per ulteriori informazioni sul controllo, vedere [Creazione di un controllo del server e di una specifica del controllo del database](../security/auditing/create-a-server-audit-and-database-audit-specification.md)  
  
##  <a name="tqh"></a> Nella tabella, Query e gli hint di Join  
 Sono supportati gli elementi seguenti:  
  
-   Gli hint INDEX, FORCESCAN e FORCESEEK, nella sintassi di hint di tabella o nella [clausola OPTION &#40;Transact-SQL&#41;](/sql/t-sql/queries/option-clause-transact-sql) della query.  
  
-   FORCE ORDER  
  
-   INNER LOOP JOIN  
  
-   OPTIMIZE FOR  
  
 Per altre informazioni, vedere [hint per la &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql).  
  
##  <a name="los"></a> Limitazioni relative all'ordinamento  
 È possibile ordinare più di 8.000 righe in una query che usa [TOP &#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) e una clausola [ORDER BY Clause &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql). Tuttavia, senza la [ clausola ORDER BY &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql), [TOP &#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) può ordinare fino a 8.000 righe, meno se sono presenti join.  
  
 Se la query usa sia l'operatore [TOP &#40;Transact-SQL&#41;](/sql/t-sql/queries/top-transact-sql) che una [clausola ORDER BY &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql), è possibile specificare fino a 8192 righe per l'operatore TOP. Se si specificano più di 8192 righe viene visualizzato il messaggio di errore: **Messaggio 41398, livello 16, stato 1, procedura  *\<NomeProcedura >*, riga  *\<lineNumber >* l'operatore TOP può restituire un massimo di 8192 righe.  *\<numero >* è stato richiesto.**  
  
 Se non si dispone di una clausola TOP, è possibile ordinare qualsiasi numero di righe con ORDER BY.  
  
 Se non si utilizza una clausola ORDER BY, è possibile utilizzare qualsiasi valore intero con l'operatore TOP.  
  
 Esempio con TOP N = 8192: compila  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8192 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 Esempio con TOP N > 8192: non riesce a compilare.  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    SELECT TOP 8193 ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 Il limite di 8192 righe si applica solo a `TOP N``N` dove  è una costante, come negli esempi precedenti.  Se è necessario un valore `N` maggiore di 8192 è possibile assegnare il valore a una variabile e utilizzare tale variabile con `TOP`.  
  
 Esempio di utilizzo di una variabile: compila  
  
```sql  
CREATE PROCEDURE testTop  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
  AS  
  BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
    DECLARE @v int = 8193   
    SELECT TOP (@v) ShoppingCartId, CreatedDate, TotalPrice FROM dbo.ShoppingCart  
    ORDER BY ShoppingCartId DESC  
  END;  
GO  
```  
  
 **Limitazioni per le righe restituite:** In due casi è possibile che il numero di righe che possono essere restituite dall'operatore TOP venga ridotto:  
  
-   Utilizzando JOIN nella query.  L'influenza di JOIN sulla limitazione dipende dal piano di query.  
  
-   Utilizzando funzioni di aggregazione o riferimenti a funzioni di aggregazione nella clausola ORDER BY.  
  
 La formula per calcolare un valore N massimo supportato nel caso peggiore in TOP N è: `N = floor ( 65536 / number_of_tables * 8 + total_size+of+aggs )`.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)   
 [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](migration-issues-for-natively-compiled-stored-procedures.md)  
  
  
