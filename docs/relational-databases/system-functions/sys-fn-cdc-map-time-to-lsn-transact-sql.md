---
title: sys.fn_cdc_map_time_to_lsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c22074e686f9dff1d988d7453c0c546fa6e049b5
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399935"
---
# <a name="sysfncdcmaptimetolsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce il valore di numero (LSN) di sequenza del log dal **start_lsn** colonna il [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabella di sistema per il tempo specificato. È possibile utilizzare questa funzione per eseguire sistematicamente il mapping degli intervalli datetime nell'intervallo basato su LSN richiesto per le funzioni di enumerazione di change data capture [CDC. fn_cdc_get_all_changes < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) e [cdc.fn _cdc_get_net_changes_. fn_cdc_get_net_changes < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) per restituire le modifiche ai dati all'interno dell'intervallo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.fn_cdc_map_time_to_lsn ( '<relational_operator>', tracking_time )  
  
<relational_operator> ::=  
{  largest less than  
 | largest less than or equal  
 | smallest greater than  
 | smallest greater than or equal  
}  
```  
  
## <a name="arguments"></a>Argomenti  
 **«**< relational_operator >**'** {più grande minore rispetto a | più grande minore di o uguale | più piccolo maggiore | più piccolo maggiore o uguale}  
 Viene usato per identificare un valore LSN distinto all'interno di **CDC. lsn_time_mapping** tabella con un oggetto associato **tran_end_time** che soddisfa la relazione quando vengono confrontati per il *tracking_time*  valore.  
  
 *relational_operator* viene **nvarchar(30)**.  
  
 *tracking_time*  
 Valore datetime da confrontare. *tracking_time* viene **datetime**.  
  
## <a name="return-type"></a>Tipo restituito  
 **binary(10)**  
  
## <a name="remarks"></a>Note  
 Per comprendere come il **Sys. fn_cdc_map_time_lsn** può essere utilizzato per eseguire il mapping di intervalli datetime intervalli LSN, considerare lo scenario seguente. Si supponga che un utente desideri estrarre su base giornaliera i dati delle modifiche. Ovvero, l'utente desidera solo le modifiche relative a un giorno specifico fino alla mezzanotte (inclusa). Il limite inferiore dell'intervallo di tempo raggiunge, ma non include, la mezzanotte del giorno precedente. Il limite superiore raggiunge e include la mezzanotte del giorno specificato. L'esempio seguente illustra come la funzione **Sys. fn_cdc_map_time_to_lsn** può essere utilizzato per eseguire sistematicamente il mapping in questo intervallo basate sull'ora nell'intervallo basato su LSN richiesto dalle funzioni di enumerazione di change data capture per restituire tutti i modifiche apportate all'interno dell'intervallo.  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 L'operatore relazionale '`smallest greater than`' è utilizzato per limitare le modifiche a quelle che si sono verificate dopo la mezzanotte del giorno precedente. Se più voci con LSN diversi valori di condivisione il **tran_end_time** valore identificato come limite inferiore nel [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabella, la funzione restituirà il valore LSN più piccolo assicurando che sono incluse tutte le voci. Per il limite superiore, l'operatore relazionale '`largest less than or equal to`' viene usata per garantire che l'intervallo includa tutte le voci per il giorno, comprese quelle con mezzanotte loro **tran_end_time** valore. Se più voci con LSN diversi valori di condivisione il **tran_end_time** valore identificato come limite superiore, la funzione restituirà il valore LSN più grande assicurando l'inclusione di tutte le voci.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo **public** .  
  
## <a name="examples"></a>Esempi  
 L'esempio seguente usa il `sys.fn_cdc_map_time_lsn` funzione per determinare se sono presenti tutte le righe del [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabella con un **tran_end_time** valore maggiore o uguale a mezzanotte. Questa query può essere utilizzata per determinare, ad esempio, se il processo di acquisizione ha già elaborato le modifiche di cui è stato eseguito il commit fino alla mezzanotte del giorno precedente, in modo tale che possa procedere l'estrazione di dati delle modifiche per il giorno specifico.  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>Vedere anche  
 [cdc.lsn_time_mapping &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
