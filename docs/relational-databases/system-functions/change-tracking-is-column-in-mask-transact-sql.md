---
title: CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6f7e9d8d9ab99ebe4a7c5749033eacf85b8feb5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68042988"
---
# <a name="change_tracking_is_column_in_mask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Interpreta il valore SYS_CHANGE_COLUMNS restituito dalla funzione CHANGETABLE (CHANGEs...). Consente a un'applicazione di determinare se la colonna specificata è inclusa nei valori restituiti per SYS_CHANGE_COLUMNS.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>Argomenti  
 *column_id*  
 ID della colonna sottoposta a verifica. L'ID di colonna può essere ottenuto tramite la funzione [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) .  
  
 *change_columns*  
 Dati binari della colonna SYS_CHANGE_COLUMNS dei dati [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) .  
  
## <a name="return-type"></a>Tipo restituito  
 **bit**  
  
## <a name="return-values"></a>Valori restituiti  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK restituisce i valori seguenti.  
  
|Valore restituito|Descrizione|  
|------------------|-----------------|  
|0|La colonna specificata non è presente nell'elenco *change_columns* .|  
|1|La colonna specificata si trova nell'elenco *change_columns* .|  
  
## <a name="remarks"></a>Osservazioni  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK non esegue alcun controllo per convalidare il valore *column_id* o che è stato ottenuto il parametro *change_columns* dalla tabella da cui è stato ottenuto il *column_id* .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene determinato se è stata aggiornata la colonna `Salary` della tabella `Employees`. La `COLUMNPROPERTY` funzione restituisce l'ID della `Salary` colonna. La variabile locale `@change_columns` deve essere impostata sui risultati di una query utilizzando CHANGETABLE come origine dati.  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni Rilevamento modifiche &#40;&#41;Transact-SQL](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;&#41;Transact-SQL](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [Rilevare le modifiche ai dati &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
