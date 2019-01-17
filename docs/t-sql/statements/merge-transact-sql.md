---
title: MERGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MERGE
- MERGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating data [SQL Server]
- modifying data [SQL Server], MERGE statement
- MERGE statement [SQL Server]
- adding data
- DML [SQL Server], MERGE statement
- table modifications [SQL Server], MERGE statement
- data manipulation language [SQL Server], MERGE statement
- inserting data
ms.assetid: c17996d6-56a6-482f-80d8-086a3423eecc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 939ba409a75d332d0aba97aa972db2ba9eecaf7a
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/02/2019
ms.locfileid: "53980017"
---
# <a name="merge-transact-sql"></a>MERGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

> [!div class="nextstepaction"]
> [Contribuisci a migliorare la documentazione di SQL Server](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

Esegue operazioni di inserimento, aggiornamento o eliminazione in una tabella di destinazione in base ai risultati di un join con una tabella di origine. È possibile ad esempio sincronizzare due tabelle inserendo, aggiornando o eliminando righe in una tabella in base alle differenze trovate nell'altra tabella.  
  
 **Suggerimento per le prestazioni:** il comportamento condizionale descritto per l'istruzione MERGE funziona meglio quando le due tabelle hanno una combinazione complessa di caratteristiche corrispondenti. Ad esempio, inserire una riga se non esiste o aggiornare la riga se corrisponde. Quando si aggiorna semplicemente una tabella in base alle righe di un'altra tabella, è possibile ottenere prestazioni e scalabilità migliori se si usano le istruzioni INSERT, UPDATE e DELETE di base. Ad esempio  
  
```  
INSERT tbl_A (col, col2)  
SELECT col, col2   
FROM tbl_B   
WHERE NOT EXISTS (SELECT col FROM tbl_A A2 WHERE A2.col = tbl_B.col);  
```  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
[ WITH <common_table_expression> [,...n] ]  
MERGE   
    [ TOP ( expression ) [ PERCENT ] ]   
    [ INTO ] <target_table> [ WITH ( <merge_hint> ) ] [ [ AS ] table_alias ]  
    USING <table_source>   
    ON <merge_search_condition>  
    [ WHEN MATCHED [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ WHEN NOT MATCHED [ BY TARGET ] [ AND <clause_search_condition> ]  
        THEN <merge_not_matched> ]  
    [ WHEN NOT MATCHED BY SOURCE [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ <output_clause> ]  
    [ OPTION ( <query_hint> [ ,...n ] ) ]      
;  
  
<target_table> ::=  
{   
    [ database_name . schema_name . | schema_name . ]  
  target_table  
}  
  
<merge_hint>::=  
{  
    { [ <table_hint_limited> [ ,...n ] ]  
    [ [ , ] INDEX ( index_val [ ,...n ] ) ] }  
}  
  
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ] [ <tablesample_clause> ]   
        [ WITH ( table_hint [ [ , ]...n ] ) ]   
  | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
  | user_defined_function [ [ AS ] table_alias ]  
  | OPENXML <openxml_clause>   
  | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]   
  | <joined_table>   
  | <pivoted_table>   
  | <unpivoted_table>   
}  
  
<merge_search_condition> ::=  
    <search_condition>  
  
<merge_matched>::=  
    { UPDATE SET <set_clause> | DELETE }  
  
<set_clause>::=  
SET  
  { column_name = { expression | DEFAULT | NULL }  
  | { udt_column_name.{ { property_name = expression  
                        | field_name = expression }  
                        | method_name ( argument [ ,...n ] ) }  
    }  
  | column_name { .WRITE ( expression , @Offset , @Length ) }  
  | @variable = expression  
  | @variable = column = expression  
  | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  } [ ,...n ]   
  
<merge_not_matched>::=  
{  
    INSERT [ ( column_list ) ]   
        { VALUES ( values_list )  
        | DEFAULT VALUES }  
}  
  
<clause_search_condition> ::=  
    <search_condition>  
  
<search condition> ::=  
    MATCH(<graph_search_pattern>) | <search_condition_without_match> | <search_condition> AND <search_condition>
    
<search_condition_without_match> ::=
    { [ NOT ] <predicate> | ( <search_condition_without_match> ) 
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition_without_match> ) } ]   
[ ,...n ]  

<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '< contains_search_condition >' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery ) }   

<graph_search_pattern> ::=
    { <node_alias> { 
                      { <-( <edge_alias> )- } 
                    | { -( <edge_alias> )-> }
                    <node_alias> 
                   } 
    }
  
<node_alias> ::=
    node_table_name | node_table_alias 

<edge_alias> ::=
    edge_table_name | edge_table_alias

<output_clause>::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table }  
        [ (column_list) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
  
<dml_select_list>::=  
    { <column_name> | scalar_expression }   
        [ [AS] column_alias_identifier ] [ ,...n ]  
  
<column_name> ::=  
    { DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>Argomenti  
 WITH \<common_table_expression>  
 Specifica la vista o il set di risultati denominato temporaneo, noto anche come espressione di tabella comune, definito nell'ambito di un'istruzione MERGE. Il set di risultati deriva da una query semplice e l'istruzione MERGE vi fa riferimento. Per altre informazioni, vedere [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 TOP (*expression*) [ PERCENT ]  
 Specifica il numero o la percentuale di righe interessate. Il valore di *expression* può essere un numero o una percentuale delle righe. Le righe cui viene fatto riferimento nell'espressione TOP non vengono disposte in alcun ordine. Per altre informazioni, vedere [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
 La clausola TOP viene applicata dopo l'unione in join dell'intera tabella di origine con l'intera tabella di destinazione e dopo la rimozione delle righe unite in join non qualificate per un'azione di inserimento, aggiornamento o eliminazione. La clausola TOP riduce ulteriormente il numero di righe unite in join in base al valore specificato e l'azione di inserimento, aggiornamento o eliminazione viene applicata alle righe unite in join rimanenti in modo non ordinato. Ciò significa che le righe vengono distribuite tra le azioni definite nelle clausole WHEN senza alcun ordine. La specifica della clausola TOP (10), ad esempio, influisce su 10 righe, 7 delle quali possono essere aggiornate e 3 inserite oppure 1 riga può essere eliminata, 5 aggiornate e 4 inserite e così via.  
  
 Poiché l'istruzione MERGE esegue un'analisi completa di entrambe le tabelle di origine e di destinazione, l'utilizzo della clausola TOP per modificare una tabella di grandi dimensioni creando più batch può influire sulle prestazioni di I/O. In questo scenario è importante assicurare che tutti i batch successivi vengano destinati a nuove righe.  
  
 *database_name*  
 Nome del database in cui si trova *target_table*.  
  
 *schema_name*  
 Visualizza il nome dello schema a cui appartiene la tabella *target_table*.  
  
 *target_table*  
 Tabella o vista rispetto alla quale vengono associate le righe di dati di \<table_source> in base a \<clause_search_condition>. *target_table* rappresenta la destinazione di qualsiasi operazione di inserimento, aggiornamento o eliminazione specificata dalle clausole WHEN dell'istruzione MERGE.  
  
 Se *target_table* è una vista, qualsiasi azione eseguita su di essa deve soddisfare le condizioni per l'aggiornamento delle viste. Per altre informazioni, vedere [Modificare i dati tramite una vista](../../relational-databases/views/modify-data-through-a-view.md).  
  
 *target_table* non può essere una tabella remota. Per *target_table* non può essere definita alcuna regola.  
  
 [AS] *table_alias*  
 Nome alternativo utilizzato per fare riferimento a una tabella.  
  
 USING \<table_source>  
 Specifica l'origine dati corrispondente alle righe di dati in *target_table* in base a \<merge_search condition>. Il risultato di questa corrispondenza determina le azioni che le clausole WHEN dell'istruzione MERGE devono eseguire. \<table_source> può essere una tabella remota o una tabella derivata con accesso a tabelle remote. 
  
 \<table_source> può essere una tabella derivata che usa il [costruttore di valori di tabella](../../t-sql/queries/table-value-constructor-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] per creare una tabella specificando più righe.  
  
 Per altre informazioni sulla sintassi e gli argomenti di questa clausola, vedere [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
 ON \<merge_search_condition>  
 Specifica le condizioni in base alle quali viene creato il join tra \<table_source> e *target_table* per stabilire i punti di corrispondenza. 
  
> [!CAUTION]  
>  È importante specificare solo le colonne della tabella di destinazione utilizzate ai fini della corrispondenza, ovvero specificare colonne della tabella di destinazione confrontate con quella corrispondente della tabella di origine. Non tentare di migliorare le prestazioni relative all'esecuzione delle query filtrando le righe della tabella di destinazione nella clausola ON, specificando ad esempio `AND NOT target_table.column_x = value`. Questa operazione potrebbe comportare la restituzione di risultati imprevisti e non corretti.  
  
 WHEN MATCHED THEN \<merge_matched>  
 Specifica che tutte le righe di *target_table* corrispondenti alle righe restituite da \<table_source> ON \<merge_search_condition> e che soddisfano eventuali condizioni di ricerca aggiuntive vengono aggiornate oppure eliminate in base alla clausola \<merge_matched>.  
  
 Nell'istruzione MERGE possono essere presenti al massimo due clausole WHEN MATCHED. Se vengono specificate due clausole, alla prima deve essere associata una clausola AND \<search_condition>. Per ogni riga specificata, la seconda clausola WHEN MATCHED viene applicata solo nel caso in cui non venga applicata la prima. Se sono presenti due clausole WHEN MATCHED, è necessario che una specifichi un'azione UPDATE e l'altra un'azione DELETE. Se nella clausola \<merge_matched> viene specificato UPDATE e se più righe di \<table_source> corrispondono a una riga di *target_table* in base a \<merge_search_condition>, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce un errore. L'istruzione MERGE non può aggiornare la stessa riga più di una volta né aggiornare ed eliminare la stessa riga.  
  
 WHEN NOT MATCHED [ BY TARGET ] THEN \<merge_not_matched>  
 Specifica che in *target_table* deve essere inserita una riga per ogni riga restituita da \<table_source> ON \<merge_search_condition> che non corrisponde a una riga in *target_table*, ma che soddisfa un'eventuale condizione di ricerca aggiuntiva. I valori da inserire vengono specificati dalla clausola \<merge_not_matched>. Nell'istruzione MERGE può essere presente solo una clausola WHEN NOT MATCHED.  
  
 WHEN NOT MATCHED BY SOURCE THEN \<merge_matched>  
 Specifica che tutte le righe di *target_table* che non corrispondono alle righe restituite da \<table_source> ON \<merge_search_condition> e che soddisfano eventuali condizioni di ricerca aggiuntive vengono aggiornate oppure eliminate in base alla clausola \<merge_matched>.  
  
 Nell'istruzione MERGE possono essere presenti al massimo due clausole WHEN NOT MATCHED BY SOURCE. Se vengono specificate due clausole, alla prima deve essere associata una clausola AND \<clause_search_condition>. Per ogni riga specificata, la seconda clausola WHEN NOT MATCHED BY SOURCE viene applicata solo nel caso in cui non venga applicata la prima. Se sono presenti due clausole WHEN NOT MATCHED BY SOURCE, è necessario che una specifichi un'azione UPDATE e l'altra un'azione DELETE. \<clause_search_condition> può fare riferimento solo a colonne della tabella di destinazione.  
  
 Se da \<table_source> non viene restituita alcuna riga, non è possibile accedere alle colonne della tabella di origine. Se l'azione di aggiornamento o eliminazione specificata nella clausola \<merge_matched> fa riferimento a colonne della tabella di origine, viene restituito l'errore 207 (Nome di colonna non valido). La clausola `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` può provocare, ad esempio, un errore nell'istruzione poiché non è possibile accedere a `Col1` nella tabella di origine.  
  
 AND \<clause_search_condition>  
 Specifica qualsiasi condizione di ricerca valida. Per altre informazioni, vedere [Condizione di ricerca&#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 \<table_hint_limited>  
 Specifica uno o più hint di tabella applicati alla tabella di destinazione per ogni azione di inserimento, aggiornamento o eliminazione eseguita dall'istruzione MERGE. La parola chiave WITH e le parentesi sono obbligatorie.  
  
 Le opzioni NOLOCK e READUNCOMMITTED non sono consentite. Per altre informazioni sugli hint di tabella, vedere [Hint di tabella &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 La specifica di un hint TABLOCK in una tabella di destinazione di un'istruzione INSERT equivale alla specifica dell'hint TABLOCKX poiché determina l'acquisizione di un blocco esclusivo sulla tabella. Quando viene specificato, FORCESEEK viene applicato all'istanza implicita della tabella di destinazione unita in join con la tabella di origine.  
  
> [!CAUTION]  
>  La specifica di READPAST con WHEN NOT MATCHED [BY TARGET] THEN INSERT può provocare l'esecuzione di operazioni INSERT che violano i vincoli UNIQUE.  
  
 INDEX ( index_val [ ,...n ] )  
 Specifica il nome o l'ID di uno o più indici della tabella di destinazione per eseguire un join implicito con la tabella di origine. Per altre informazioni, vedere [Hint di tabella &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 \<output_clause>  
 Restituisce una riga per ogni riga in *target_table* aggiornata, inserita o eliminata, senza alcun ordine specifico. Nella clausola di output è possibile specificare **$action**. **$action** è una colonna di tipo **nvarchar(10)** che restituisce uno dei tre valori per ogni riga: 'INSERT', 'UPDATE' o 'DELETE', secondo l'azione eseguita su quella riga. Per altre informazioni sugli argomenti di questa clausola, vedere [Clausola OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
 OPTION ( \<query_hint> [ ,...n ] )  
 Specifica che vengono utilizzati hint di ottimizzazione per personalizzare il modo in cui il Motore di database elabora l'istruzione. Per altre informazioni, vedere [Hint per la query &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
 \<merge_matched>  
 Specifica l'azione di aggiornamento o eliminazione applicata a tutte le righe di *target_table* che non corrispondono alle righe restituite da \<table_source> ON \<merge_search_condition> e che soddisfano eventuali condizioni di ricerca aggiuntive.  
  
 UPDATE SET \<set_clause>  
 Specifica l'elenco di colonne o di nomi di variabile da aggiornare nella tabella di destinazione e i valori in base ai quali eseguire l'aggiornamento.  
  
 Per altre informazioni sugli argomenti di questa clausola, vedere [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md). Non è consentito impostare una variabile sullo stesso valore di una colonna.  
  
 Elimina  
 Specifica che le righe corrispondenti alle righe di *target_table* vengono eliminate.  
  
 \<merge_not_matched>  
 Specifica i valori da inserire nella tabella di destinazione.  
  
 (*column_list*)  
 Elenco di una o più colonne della tabella di destinazione in cui inserire i dati. Le colonne devono essere specificate come un nome costituito da una sola parte. Il valore di *column_list* deve essere racchiuso tra parentesi e delimitato da virgole.  
  
 VALUES ( *values_list*)  
 Elenco delimitato da virgole di costanti, variabili o espressioni che restituiscono valori da inserire nella tabella di destinazione. Le espressioni non possono contenere un'istruzione EXECUTE.  
  
 DEFAULT VALUES  
 Forza l'immissione nella riga inserita dei valori predefiniti associati a ogni colonna.  
  
 Per altre informazioni su questa clausola, vedere [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
 \<search condition>  
 Specifica le condizioni di ricerca usate per specificare \<merge_search_condition> o \<clause_search_condition>. Per altre informazioni sugli argomenti di questa clausola, vedere [Condizione di ricerca &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  

 \<graph search pattern>  
 Specifica il modello di corrispondenza del grafico. Per altre informazioni sugli argomenti di questa clausola, vedere [MATCH &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)
  
## <a name="remarks"></a>Remarks  
 È necessario specificare almeno una delle tre clausole MATCHED, le quali possono essere tuttavia specificate in qualsiasi ordine. Non è possibile aggiornare una variabile più di una volta nella stessa clausola MATCHED.  
  
 Tutte le azioni di inserimento, aggiornamento o eliminazione specificate nella tabella di destinazione dall'istruzione MERGE sono limitate da qualsiasi vincolo definito sulla tabella, inclusi vincoli di integrità referenziale di propagazione. Se IGNORE_DUP_KEY è impostato su ON per qualsiasi indice univoco nella tabella di destinazione, MERGE ignora questa impostazione.  
  
 Nell'istruzione MERGE è necessario utilizzare un punto e virgola (;) come carattere di terminazione. In caso contrario, viene generato l'errore 10713.  
  
 Se usato dopo MERGE, [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md) restituisce al client il numero complessivo di righe inserite, aggiornate ed eliminate.  
  
 MERGE è una parola chiave completamente riservata se il livello di compatibilità del database è impostato su 100 o un valore più elevato. Sebbene l'istruzione MERGE sia disponibile per i livelli di compatibilità del database 90 e 100, se il livello di compatibilità è impostato su 90 la parola chiave non è completamente riservata.  
  
 È consigliabile non usare l'istruzione **MERGE** quando si usa la replica di aggiornamento in coda. **MERGE** e il trigger per l'aggiornamento in coda non sono compatibili. Sostituire l'istruzione **MERGE** con un'istruzione INSERT o UPDATE.  
  
## <a name="trigger-implementation"></a>Implementazione dei trigger  
 Per ogni azione di inserimento, aggiornamento o eliminazione specificata nell'istruzione MERGE, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono attivati i trigger AFTER corrispondenti definiti nella tabella di destinazione, senza garantire l'ordine di attivazione dei trigger per le azioni. I trigger definiti per la stessa azione rispettano l'ordine specificato dall'utente. Per altre informazioni sull'impostazione dell'ordine di attivazione dei trigger, vedere [Specifica dei primi e degli ultimi trigger](../../relational-databases/triggers/specify-first-and-last-triggers.md).  
  
 Se per la tabella di destinazione è abilitato un trigger INSTEAD OF definito nella tabella stessa per un'azione di inserimento, aggiornamento o eliminazione eseguita da un'istruzione MERGE, è necessario che per tale tabella sia abilitato un trigger INSTEAD OF per tutte le azioni specificate nell'istruzione MERGE.  
  
 Se in *target_table* è definito un trigger INSTEAD OF UPDATE o INSTEAD OF DELETE, le operazioni di aggiornamento o eliminazione non vengono eseguite, ma vengono attivati i trigger e le tabelle **inserite** ed **eliminate** vengono popolate di conseguenza.  
  
 Se in *target_table* è definito un trigger INSTEAD OF INSERT, l'operazione di inserimento non viene eseguita, ma viene attivato il trigger e la tabella **inserita** viene popolata di conseguenza.  
  
## <a name="permissions"></a>Permissions  
 È necessario disporre dell'autorizzazione SELECT per la tabella di origine e dell'autorizzazione INSERT, UPDATE o DELETE per quella di destinazione. Per altre informazioni, vedere gli argomenti relativi a [SELECT](../../t-sql/queries/select-transact-sql.md), [INSERT](../../t-sql/statements/insert-transact-sql.md), [UPDATE](../../t-sql/queries/update-transact-sql.md) e [DELETE](../../t-sql/statements/delete-transact-sql.md) nella sezione Autorizzazioni.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-merge-to-perform-insert-and-update-operations-on-a-table-in-a-single-statement"></a>A. Utilizzo di MERGE per eseguire operazioni INSERT e UPDATE in una tabella in un'unica istruzione  
 Uno scenario comune prevede l'aggiornamento di una o più colonne di una tabella nel caso in cui sia presente una riga corrispondente oppure l'inserimento dei dati come nuova riga nel caso in cui la riga corrispondente non sia presente. Questa operazione viene eseguita in genere passando i parametri a una stored procedure contenente le istruzioni UPDATE e INSERT appropriate. Con l'istruzione MERGE è possibile eseguire entrambe le attività in un'unica istruzione. Nell'esempio seguente viene illustrata una stored procedure nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] che contiene un'istruzione INSERT e un'istruzione UPDATE. La stored procedure viene quindi modificata per eseguire le operazioni equivalenti utilizzando una singola istruzione MERGE.  
  
```sql  
CREATE PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
-- Update the row if it exists.      
    UPDATE Production.UnitMeasure  
SET Name = @Name  
WHERE UnitMeasureCode = @UnitMeasureCode  
-- Insert the row if the UPDATE statement failed.  
IF (@@ROWCOUNT = 0 )  
BEGIN  
    INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name)  
    VALUES (@UnitMeasureCode, @Name)  
END  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Test Value';  
SELECT UnitMeasureCode, Name FROM Production.UnitMeasure  
WHERE UnitMeasureCode = 'ABC';  
GO  
  
-- Rewrite the procedure to perform the same operations using the 
-- MERGE statement.  
-- Create a temporary table to hold the updated or inserted values 
-- from the OUTPUT clause.  
CREATE TABLE #MyTempTable  
    (ExistingCode nchar(3),  
     ExistingName nvarchar(50),  
     ExistingDate datetime,  
     ActionTaken nvarchar(10),  
     NewCode nchar(3),  
     NewName nvarchar(50),  
     NewDate datetime  
    );  
GO  
ALTER PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
  
    MERGE Production.UnitMeasure AS target  
    USING (SELECT @UnitMeasureCode, @Name) AS source (UnitMeasureCode, Name)  
    ON (target.UnitMeasureCode = source.UnitMeasureCode)  
    WHEN MATCHED THEN   
        UPDATE SET Name = source.Name  
WHEN NOT MATCHED THEN  
    INSERT (UnitMeasureCode, Name)  
    VALUES (source.UnitMeasureCode, source.Name)  
    OUTPUT deleted.*, $action, inserted.* INTO #MyTempTable;  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'New Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'XYZ', @Name = 'Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Another Test Value';  
  
SELECT * FROM #MyTempTable;  
-- Cleanup   
DELETE FROM Production.UnitMeasure WHERE UnitMeasureCode IN ('ABC','XYZ');  
DROP TABLE #MyTempTable;  
GO  
```  
  
### <a name="b-using-merge-to-perform-update-and-delete-operations-on-a-table-in-a-single-statement"></a>b. Utilizzo di MERGE per eseguire operazioni UPDATE e DELETE in una tabella in un'unica istruzione  
 Nell'esempio seguente viene utilizzata l'istruzione MERGE per aggiornare la tabella `ProductInventory` nel database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] con frequenza giornaliera, in base agli ordini elaborati nella tabella `SalesOrderDetail`. La colonna `Quantity` della tabella `ProductInventory` viene aggiornata sottraendo il numero di ordini effettuati ogni giorno per ciascun prodotto nella tabella `SalesOrderDetail`. Se il numero di ordini per un prodotto riduce il livello delle scorte del prodotto a zero o a un valore inferiore, la riga relativa a tale prodotto viene eliminata dalla tabella `ProductInventory`.  
  
```sql  
CREATE PROCEDURE Production.usp_UpdateInventory  
    @OrderDate datetime  
AS  
MERGE Production.ProductInventory AS target  
USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
    JOIN Sales.SalesOrderHeader AS soh  
    ON sod.SalesOrderID = soh.SalesOrderID  
    AND soh.OrderDate = @OrderDate  
    GROUP BY ProductID) AS source (ProductID, OrderQty)  
ON (target.ProductID = source.ProductID)  
WHEN MATCHED AND target.Quantity - source.OrderQty <= 0  
    THEN DELETE  
WHEN MATCHED   
    THEN UPDATE SET target.Quantity = target.Quantity - source.OrderQty,   
                    target.ModifiedDate = GETDATE()  
OUTPUT $action, Inserted.ProductID, Inserted.Quantity, 
    Inserted.ModifiedDate, Deleted.ProductID,  
    Deleted.Quantity, Deleted.ModifiedDate;  
GO  
  
EXECUTE Production.usp_UpdateInventory '20030501'  
```  
  
### <a name="c-using-merge-to-perform-update-and-insert-operations-on-a-target-table-by-using-a-derived-source-table"></a>C. Utilizzo di MERGE per eseguire operazioni UPDATE e INSERT in una tabella di destinazione utilizzando una tabella di origine derivata  
 Nell'esempio seguente viene utilizzata l'istruzione MERGE per modificare la tabella `SalesReason` nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] eseguendo l'aggiornamento o l'inserimento di righe. Quando il valore di `NewName` nella tabella di origine corrisponde a un valore della colonna `Name` nella tabella di destinazione (`SalesReason`), la colonna `ReasonType` viene aggiornata nella tabella di destinazione. Quando il valore di `NewName` non corrisponde, la riga di origine viene inserita nella tabella di destinazione. La tabella di origine è una tabella derivata che utilizza il costruttore di valori di tabella [!INCLUDE[tsql](../../includes/tsql-md.md)] per specificare più righe per la tabella di origine. Per altre informazioni sull'uso del costruttore di valori di tabella in una tabella derivata, vedere [Costruttore di valori di tabella &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md). Nell'esempio viene inoltre illustrato come archiviare i risultati della clausola OUTPUT in una variabile di tabella e quindi creare un riepilogo dei risultati dell'istruzione MERGE eseguendo una semplice operazione di selezione che restituisce il numero di righe inserite e aggiornate.  
  
```sql  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), 
              ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
```  
  
### <a name="d-inserting-the-results-of-the-merge-statement-into-another-table"></a>D. Inserimento dei risultati dell'istruzione MERGE in un'altra tabella  
 Nell'esempio seguente vengono acquisiti i dati restituiti dalla clausola OUTPUT di un'istruzione MERGE e tali dati vengono inseriti in un'altra tabella. L'istruzione MERGE consente di aggiornare la colonna `Quantity` della tabella `ProductInventory` nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], in base agli ordini elaborati nella tabella `SalesOrderDetail`. In questo esempio vengono acquisite le righe aggiornate, inserite successivamente in un'altra tabella utilizzata per tenere traccia delle modifiche apportate alle scorte.  
  
```sql  
CREATE TABLE Production.UpdatedInventory  
    (ProductID INT NOT NULL, LocationID int, NewQty int, PreviousQty int,  
     CONSTRAINT PK_Inventory PRIMARY KEY CLUSTERED (ProductID, LocationID));  
GO  
INSERT INTO Production.UpdatedInventory  
SELECT ProductID, LocationID, NewQty, PreviousQty   
FROM  
(    MERGE Production.ProductInventory AS pi  
     USING (SELECT ProductID, SUM(OrderQty)   
            FROM Sales.SalesOrderDetail AS sod  
            JOIN Sales.SalesOrderHeader AS soh  
            ON sod.SalesOrderID = soh.SalesOrderID  
            AND soh.OrderDate BETWEEN '20030701' AND '20030731'  
            GROUP BY ProductID) AS src (ProductID, OrderQty)  
     ON pi.ProductID = src.ProductID  
    WHEN MATCHED AND pi.Quantity - src.OrderQty >= 0   
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0   
        THEN DELETE  
    OUTPUT $action, Inserted.ProductID, Inserted.LocationID, 
        Inserted.Quantity AS NewQty, Deleted.Quantity AS PreviousQty)  
 AS Changes (Action, ProductID, LocationID, NewQty, PreviousQty) 
 WHERE Action = 'UPDATE';  
GO  
```  

### <a name="e-using-merge-to-perform-insert-or-update-on-a-target-edge-table-in-a-graph-database"></a>E. Uso di MERGE per eseguire INSERT o UPDATE in una tabella bordi di destinazione in un database di grafi
In questo esempio si creano le tabelle nodi `Person` e `City` e la tabella bordi `livesIn`. Quindi si usa l'istruzione MERGE sul bordo `livesIn` per inserire una nuova riga se il bordo non esiste già tra un elemento `Person` e `City`. Se il bordo esiste già, viene aggiornato solo l'attributo StreetAddress sul bordo `livesIn`.

```sql
-- CREATE node and edge tables
CREATE TABLE Person
    (
        ID INTEGER PRIMARY KEY, 
        PersonName VARCHAR(100)
    )
AS NODE
GO

CREATE TABLE City
    (
        ID INTEGER PRIMARY KEY, 
        CityName VARCHAR(100), 
        StateName VARCHAR(100)
    )
AS NODE
GO

CREATE TABLE livesIn
    (
        StreetAddress VARCHAR(100)
    )
AS EDGE
GO

-- INSERT some test data into node and edge tables
INSERT INTO Person VALUES (1, 'Ron'), (2, 'David'), (3, 'Nancy')
GO

INSERT INTO City VALUES (1, 'Redmond', 'Washington'), (2, 'Seattle', 'Washington')
GO

INSERT livesIn SELECT P.$node_id, C.$node_id, c
FROM Person P, City C, (values (1,1, '123 Avenue'), (2,2,'Main Street')) v(a,b,c)
WHERE P.id = a AND C.id = b
GO

-- Use MERGE to update/insert edge data
CREATE OR ALTER PROCEDURE mergeEdge
    @PersonId integer,
    @CityId integer,
    @StreetAddress varchar(100)
AS
BEGIN
    MERGE livesIn
        USING ((SELECT @PersonId, @CityId, @StreetAddress) AS T (PersonId, CityId, StreetAddress)
                JOIN Person ON T.PersonId = Person.ID
                JOIN City ON T.CityId = City.ID)
        ON MATCH (Person-(livesIn)->City)
    WHEN MATCHED THEN
        UPDATE SET StreetAddress = @StreetAddress
    WHEN NOT MATCHED THEN
        INSERT ($from_id, $to_id, StreetAddress)
        VALUES (Person.$node_id, City.$node_id, @StreetAddress) ;
END
GO

-- Following will insert a new edge in the livesIn edge table
EXEC mergeEdge 3, 2, '4444th Avenue'
GO

-- Following will update the StreetAddress on the edge that connects Ron to Redmond
EXEC mergeEdge 1, 1, '321 Avenue'
GO

-- Verify that all the address were added/updated correctly
SELECT PersonName, CityName, StreetAddress
FROM Person , City , livesIn 
WHERE MATCH(Person-(livesIn)->city)
GO
```
  
## <a name="see-also"></a>Vedere anche  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Clausola OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md)   
 [MERGE nei pacchetti di Integration Services](../../integration-services/control-flow/merge-in-integration-services-packages.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Costruttore di valori di tabella &#40;Transact-SQL&#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)  
  
  

