---
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.technology: data-warehouse
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: uc-msft
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 88738f857ab83b4a2f7927f75a2795a4f0eb1169
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034252"
---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Consente di visualizzare il piano di esecuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per una query in esecuzione in uno specifico nodo di controllo o di calcolo [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Consente di risolvere i problemi relativi alle prestazioni di query quando le query vengono eseguite sui nodi di calcolo e di controllo.
  
Dopo il rilevamento di problemi di prestazioni delle query per le query [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SMP in esecuzione nei nodi di calcolo, esistono diversi modi per migliorare le prestazioni. Le possibili soluzioni per migliorare le prestazioni delle query sui nodi di calcolo includono la creazione di statistiche multicolonna, la creazione di indici non cluster o l'uso di hint per la query.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
Sintassi per Azure SQL Data Warehouse:

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
Sintassi per Parallel Data Warehouse di Azure:
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *distribution_id*  
 Identificatore per la distribuzione in cui è in esecuzione il piano di query. È un valore intero e non può essere Null. Usato quando la destinazione è [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 *pdw_node_id*  
 Identificatore per il nodo in cui è in esecuzione il piano di query. È un valore intero e non può essere Null. Usato quando la destinazione è un'appliance.  
  
 *spid*  
 Identificatore per la sessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è in esecuzione il piano di query. È un valore intero e non può essere Null.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL per [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
È richiesta l'autorizzazione VIEW-SERVER-STATE nell'appliance.
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>Esempi: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>A. Sintassi di base DBCC PDW_SHOWEXECUTIONPLAN  
 Durante l'esecuzione su un'istanza [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], modificare la query precedente per selezionare anche distribution_id.  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
Verrà restituito il valore spid per ogni distribuzione effettivamente in esecuzione. Se si vuole sapere quale distribuzione 1 era in esecuzione nella sessione 375, eseguire il comando seguente.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>b. Sintassi di base DBCC PDW_SHOWEXECUTIONPLAN  
 La query che è in esecuzione da troppo tempo sta eseguendo un'operazione del piano di query DMS o un'operazione del piano di query SQL.  
  
Se la query sta eseguendo un'operazione del piano di query DMS, è possibile usare la query seguente per recuperare un elenco degli ID di nodo e di sessione per i passaggi che non sono stati completati.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
In base ai risultati della query precedente, usare sql_spid e pdw_node_id come parametri per DBCC PDW_SHOWEXECUTIONPLAN. Il comando seguente illustra ad esempio il piano di esecuzione per pdw_node_id 201001 e sql_spid 375.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>Vedere anche
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)
