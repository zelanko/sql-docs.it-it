---
title: sys.dm_db_objects_disabled_on_compatibility_level_change (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_objects_disabled_on_compatibility_level_change
- dm_db_objects_disabled_on_compatibility_level_change_TSQL
- sys.dm_db_objects_disabled_on_compatibility_level_change
- sys.dm_db_objects_disabled_on_compatibility_level_change_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_objects_disabled_on_compatibility_level_change catalog view
ms.assetid: a5d70064-0330-48b9-b853-01eba50755d0
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 30c3a5d7358e49c1e1762fbb9851066bdaf30871
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809898"
---
# <a name="spatial-data---sysdm_db_objects_disabled_on_compatibility_level_change"></a>Dati spaziali-sys. dm _db_objects_disabled_on_compatibility_level_change
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Elenca gli indici e i vincoli che saranno disabilitati come risultato della modifica del livello di compatibilità in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Indici e vincoli che contengono colonne calcolate persistenti le cui espressioni utilizzano tipi definiti dall'utente spaziali saranno disabilitati dopo l'aggiornamento o la modifica del livello di compatibilità. Utilizzare questa funzione a gestione dinamica per determinare l'impatto di una modifica nel livello di compatibilità.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```sql  
sys.dm_db_objects_disabled_on_compatibility_level_change ( compatibility_level )   
```  
  
##  <a name="Arguments"></a> Argomenti  
 *compatibility_level*  
 **int** che identifica il livello di compatibilità che si intende impostare.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**class**|**int**|1 = vincoli<br /><br /> 7 = indici e heap|  
|**class_desc**|**nvarchar(60)**|OBJECT o COLUMN per i vincoli<br /><br /> INDEX per indici e heap|  
|**major_id**|**int**|OBJECT ID dei vincoli<br /><br /> OBJECT ID della tabella che contiene indici e heap|  
|**minor_id**|**int**|NULL per i vincoli<br /><br /> Index_id per indici e heap|  
|**dependency**|**nvarchar(60)**|Descrizione della dipendenza che provoca la disabilitazione del vincolo o dell'indice. Gli stessi valori vengono utilizzati inoltre negli avvisi generati durante l'aggiornamento. Negli esempi vengono illustrati gli aspetti seguenti:<br /><br /> "space" per una funzione intrinseco<br /><br /> 'geometry' per un tipo definito dall'utente del sistema<br /><br /> 'geography::Parse' per un metodo di un tipo definito dall'utente del sistema|  
  
## <a name="general-remarks"></a>Osservazioni generali  
 Le colonne calcolate persistenti in cui sono utilizzate alcune funzioni intrinseche vengono disabilitate quando il livello di compatibilità viene modificato. In modo analogo, anche le colonne calcolate persistenti che utilizzano metodi geometry o geography vengono disabilitate quando un database viene aggiornato.  
  
### <a name="which-functions-cause-persisted-computed-columns-to-be-disabled"></a>Funzioni che provocano la disabilitazione delle colonne calcolate persistenti  
 Quando le funzioni seguenti vengono utilizzate nell'espressione di una colonna calcolata persistente, provocano la disabilitazione di indici e vincoli che fanno riferimento a tali colonne quando il livello di compatibilità viene modificato da 80 a 90:  
  
-   **IsNumeric**  
  
 Quando le funzioni seguenti vengono utilizzate nell'espressione di una colonna calcolata persistente, provocano la disabilitazione di indici e vincoli che fanno riferimento a tali colonne quando il livello di compatibilità viene modificato da 100 a 110 o un valore maggiore:  
  
-   **SOUNDEX**  
  
-   **Geografia:: GeomFromGML**  
  
-   **Geografia:: STGeomFromText**  
  
-   **Geografia:: STLineFromText**  
  
-   **Geografia:: STPolyFromText**  
  
-   **Geografia:: STMPointFromText**  
  
-   **Geografia:: STMLineFromText**  
  
-   **Geografia:: STMPolyFromText**  
  
-   **Geografia:: STGeomCollFromText**  
  
-   **Geografia:: STGeomFromWKB**  
  
-   **Geografia:: STLineFromWKB**  
  
-   **Geografia:: STPolyFromWKB**  
  
-   **Geografia:: STMPointFromWKB**  
  
-   **Geografia:: STMLineFromWKB**  
  
-   **Geografia:: STMPolyFromWKB**  
  
-   **Geografia:: STUnion**  
  
-   **Geografia:: STIntersection**  
  
-   **Geografia:: STDifference**  
  
-   **Geografia:: STSymDifference**  
  
-   **Geografia:: STBuffer**  
  
-   **Geografia:: BufferWithTolerance**  
  
-   **Geografia:: Analizzare**  
  
-   **Geografia:: Ridurre**  
  
### <a name="behavior-of-the-disabled-objects"></a>Comportamento degli oggetti disabilitati  
 **Indici**  
  
 Se l'indice cluster è disabilitato o se viene forzato un indice non cluster, viene generato l'errore seguente: "Query processor non è in grado di generare un piano perché l'indice '%. \*ls ' nella tabella o nella vista '%. \*ls ' è disabilitato. " Per abilitare nuovamente questi oggetti, ricompilare gli indici dopo l'aggiornamento **chiamando alter index on... REBUILD**.  
  
 **Cumuli**  
  
 Se viene utilizzata una tabella con un heap disabilitato, viene generato l'errore seguente. Per abilitare nuovamente questi oggetti, ricompilare dopo l'aggiornamento chiamando **alter index all on... REBUILD**.  
  
```  
// ErrorNumber: 8674  
// ErrorSeverity: EX_USER  
// ErrorFormat: The query processor is unable to produce a plan because the table or view '%.*ls' is disabled.  
// ErrorCause: The table has a disabled heap.   
// ErrorCorrectiveAction: Rebuild the disabled heap to enable it.   
// ErrorInserts: table or view name   
// ErrorOwner: mtintor   
// ErrorFirstProduct: SQL11  
```  
  
 Se si tenta di ricompilare l'heap durante un'operazione online, viene generato un errore.  
  
 **Vincoli check e chiavi esterne**  
  
 Sebbene vincoli CHECK e chiavi esterne disabilitati non generino alcun errore, i vincoli non vengono applicati quando vengono modificate le righe. Per abilitare nuovamente questi oggetti, verificare i vincoli dopo l'aggiornamento chiamando **ALTER TABLE... VINCOLO**CHECK.  
  
 **Colonne calcolate rese permanente**  
  
 Poiché non è possibile disabilitare una sola colonna, l'intera tabella viene disabilitata applicando questa operazione all'indice cluster o all'heap.  
  
## <a name="security"></a>Sicurezza  
  
### <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione VIEW DATABASE STATE.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata una query su **sys. dm _db_objects_disabled_on_compatibility_level_change** per trovare gli oggetti interessati dalla modifica del livello di compatibilità a 120.  
  
```sql  
SELECT * FROM sys.dm_db_objects_disabled_on_compatibility_level_change(120);  
GO  
  
```  
  
  
