---
title: sp_sequence_get_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_sequence_get_range
- sp_sequence_get_range_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sp_sequence_get_range procedure
- sp_sequence_get_range
ms.assetid: 8ca6b0c6-8d9c-4eee-b02f-51ddffab4492
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 66ec81fdc6ebdbecf83791c6fffa5735a37723bc
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527943"
---
# <a name="spsequencegetrange-transact-sql"></a>sp_sequence_get_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  Restituisce un intervallo di valori di sequenza da un oggetto sequenza. L'oggetto sequenza genera e pubblica il numero richiesto di valori e fornisce all'applicazione i metadati relativi all'intervallo.  
  
 Per altre informazioni sui numeri di sequenza, vedere [numeri di sequenza](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_sequence_get_range [ @sequence_name = ] N'<sequence>'   
     , [ @range_size = ] range_size  
     , [ @range_first_value = ] range_first_value OUTPUT   
    [, [ @range_last_value = ] range_last_value OUTPUT ]  
    [, [ @range_cycle_count = ] range_cycle_count OUTPUT ]  
    [, [ @sequence_increment = ] sequence_increment OUTPUT ]  
    [, [ @sequence_min_value = ] sequence_min_value OUTPUT ]  
    [, [ @sequence_max_value = ] sequence_max_value OUTPUT ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @sequence_name = ] N'sequence'` Il nome dell'oggetto sequenza. Lo schema è facoltativo. *sequence_name* viene **nvarchar(776)**.  
  
`[ @range_size = ] range_size` Il numero di valori da recuperare dalla sequenza. **@range_size** viene **bigint**.  
  
`[ @range_first_value = ] range_first_value` Parametro di output restituisce il primo valore (minimo o massimo) dell'oggetto sequenza utilizzato per calcolare l'intervallo richiesto. **@range_first_value** viene **sql_variant** con lo stesso tipo di base a quello dell'oggetto sequenza utilizzato nella richiesta.  
  
`[ @range_last_value = ] range_last_value` Parametro di output facoltativo restituisce l'ultimo valore dell'intervallo richiesto. **@range_last_value** viene **sql_variant** con lo stesso tipo di base a quello dell'oggetto sequenza utilizzato nella richiesta.  
  
`[ @range_cycle_count = ] range_cycle_count` Parametro di output facoltativo restituisce il numero di volte in cui è stato riavviato l'oggetto sequenza per restituire l'intervallo richiesto. **@range_cycle_count** viene **int**.  
  
`[ @sequence_increment = ] sequence_increment` Il parametro output facoltativo restituisce l'incremento dell'oggetto sequenza utilizzato per calcolare l'intervallo richiesto. **@sequence_increment** viene **sql_variant** con lo stesso tipo di base a quello dell'oggetto sequenza utilizzato nella richiesta.  
  
`[ @sequence_min_value = ] sequence_min_value` Parametro di output facoltativo restituisce il valore minimo dell'oggetto sequenza. **@sequence_min_value** viene **sql_variant** con lo stesso tipo di base a quello dell'oggetto sequenza utilizzato nella richiesta.  
  
`[ @sequence_max_value = ] sequence_max_value` Parametro di output facoltativo restituisce il valore massimo dell'oggetto sequenza. **@sequence_max_value** viene **sql_variant** con lo stesso tipo di base a quello dell'oggetto sequenza utilizzato nella richiesta.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 sp_sequence_get_rangeis in di sys. lo schema e può essere specificata come sys.sp_sequence_get_range.  
  
### <a name="cycling-sequences"></a>Sequenze con riavvio  
 Se necessario, l'oggetto sequenza verrà riavviato il numero di volte opportuno a servire l'intervallo richiesto. Il numero di riavvii viene restituito al chiamante tramite il parametro `@range_cycle_count`.  
  
> [!NOTE]  
>  Quando viene eseguito il ciclo, un oggetto sequenza viene riavviato dal valore minimo per una sequenza con ordine crescente e dal valore massimo per una sequenza con ordine decrescente, non dal valore iniziale dell'oggetto sequenza.  
  
### <a name="non-cycling-sequences"></a>Sequenze senza riavvio  
 Se il numero di valori nell'intervallo richiesto è maggiore dei valori disponibili rimanenti nell'oggetto sequenza, l'intervallo richiesto non viene dedotto dall'oggetto sequenza e viene restituito l'errore 11732 seguente:  
  
 `The requested range for sequence object '%.*ls' exceeds the maximum or minimum limit. Retry with a smaller range.`  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione UPDATE per l'oggetto sequenza o lo schema dell'oggetto sequenza.  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti usano un oggetto sequenza denominato Test.RangeSeq. Usare l'istruzione seguente per creare la sequenza Test.RangeSeq.  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.RangeSeq  
    AS int   
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 25  
    CYCLE  
    CACHE 10  
;  
```  
  
### <a name="a-retrieving-a-range-of-sequence-values"></a>A. Recupero di un intervallo di valori di sequenza  
 L'istruzione seguente ottiene quattro numeri di sequenza dall'oggetto sequenza Test.RangeSeq e restituisce il primo numero all'utente.  
  
```  
DECLARE @range_first_value sql_variant ,   
        @range_first_value_output sql_variant ;  
  
EXEC sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 4  
, @range_first_value = @range_first_value_output OUTPUT ;  
  
SELECT @range_first_value_output AS FirstNumber ;  
  
```  
  
### <a name="b-returning-all-output-parameters"></a>B. Restituzione di tutti i parametri di output  
 L'esempio seguente restituisce tutti i valori di output della procedura sp_sequence_get_range.  
  
```  
DECLARE    
  @FirstSeqNum sql_variant  
, @LastSeqNum sql_variant  
, @CycleCount int  
, @SeqIncr sql_variant  
, @SeqMinVal sql_variant  
, @SeqMaxVal sql_variant ;  
  
EXEC sys.sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 5  
, @range_first_value = @FirstSeqNum OUTPUT   
, @range_last_value = @LastSeqNum OUTPUT   
, @range_cycle_count = @CycleCount OUTPUT  
, @sequence_increment = @SeqIncr OUTPUT  
, @sequence_min_value = @SeqMinVal OUTPUT  
, @sequence_max_value = @SeqMaxVal OUTPUT ;  
  
-- The following statement returns the output values  
SELECT  
  @FirstSeqNum AS FirstVal  
, @LastSeqNum AS LastVal  
, @CycleCount AS CycleCount  
, @SeqIncr AS SeqIncrement  
, @SeqMinVal AS MinSeq  
, @SeqMaxVal AS MaxSeq ;  
  
```  
  
 La modifica dell'argomento `@range_size` in un numero maggiore, ad esempio 75, provocherà il riavvio dell'oggetto sequenza. Controllare l'argomento `@range_cycle_count` per determinare se e quante volte l'oggetto sequenza è stato riavviato.  
  
### <a name="c-example-using-adonet"></a>C. Esempio con ADO.NET  
 Nell'esempio seguente ottiene un intervallo dal Test.RangeSeq tramite ADO.NET.  
  
```  
SqlCommand cmd = new SqlCommand();  
cmd.Connection = conn;  
cmd.CommandType = CommandType.StoredProcedure;  
cmd.CommandText = "sys.sp_sequence_get_range";  
cmd.Parameters.AddWithValue("@sequence_name", "Test.RangeSeq");  
cmd.Parameters.AddWithValue("@range_size", 10);  
  
// Specify an output parameter to retreive the first value of the generated range.  
SqlParameter firstValueInRange = new SqlParameter("@range_first_value", SqlDbType.Variant);  
firstValueInRange.Direction = ParameterDirection.Output;  
cmd.Parameters.Add(firstValueInRange);  
  
conn.Open();  
cmd.ExecuteNonQuery();  
  
// Output the first value of the generated range.  
Console.WriteLine(firstValueInRange.Value);  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Numeri di sequenza](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
