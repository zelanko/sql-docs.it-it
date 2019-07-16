---
title: sp_autostats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_autostats_TSQL
- sp_autostats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_autostats
ms.assetid: d1df8c15-ee73-49eb-9d13-6e98943c3e38
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d390cff9bf101167db277c1c7614ee68d10edb6a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046099"
---
# <a name="spautostats-transact-sql"></a>sp_autostats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Visualizza o modifica l'opzione di aggiornamento delle statistiche automatiche AUTO_UPDATE_STATISTICS per un indice, un oggetto statistiche, una tabella o una vista indicizzata.  
  
 Per altre informazioni sull'opzione AUTO_UPDATE_STATISTICS, vedere [opzioni ALTER DATABASE SET &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) e [statistiche](../../relational-databases/statistics/statistics.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_autostats [ @tblname = ] 'table_or_indexed_view_name'   
    [ , [ @flagc = ] 'stats_value' ]   
    [ , [ @indname = ] 'statistics_name' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @tblname = ] 'table_or_indexed_view_name'` Il nome della tabella o della vista per visualizzare l'opzione AUTO_UPDATE_STATISTICS su indicizzata. *table_or_indexed_view_name* viene **nvarchar(776)** , non prevede alcun valore predefinito.  
  
`[ @flagc = ] 'stats_value'` Aggiorna l'opzione AUTO_UPDATE_STATISTICS su uno dei valori seguenti:  
  
 **ON** = ON  
  
 **OFF** = OFF  
  
 Quando *stats_flag* non è specificato, viene visualizzata l'impostazione AUTO_UPDATE_STATISTICS corrente. *stats_value* viene **varchar (10)** , con un valore predefinito è NULL.  
  
`[ @indname = ] 'statistics_name'` È il nome delle statistiche per visualizzare o aggiornare l'opzione AUTO_UPDATE_STATISTICS su. Per visualizzare le statistiche per un indice, è possibile utilizzare il nome dell'indice, in quanto un indice e l'oggetto statistiche corrispondente hanno lo stesso nome.  
  
 *nome_statistiche* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Se *stats_flag* omette **sp_autostats** segnala l'operazione è stata eseguita, ma non restituisce Nessun set di risultati.  
  
 Se *stats_flag* non viene specificato, **sp_autostats** restituisce il set di risultati seguente.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Index Name**|**varchar(60)**|Nome dell'indice o delle statistiche.|  
|**AUTOSTATS**|**varchar(3)**|Valore corrente dell'opzione AUTO_UPDATE_STATISTICS.|  
|**Ultimo aggiornamento**|**datetime**|Data dell'aggiornamento più recente delle statistiche.|  
  
 Il set di risultati per una tabella o vista indicizzata include statistiche create per gli indici, statistiche a colonna singola generate con l'opzione AUTO_CREATE_STATISTICS e statistiche create con il [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) istruzione.  
  
## <a name="remarks"></a>Note  
 Se l'indice specificato è disabilitato oppure la tabella specificata include un indice cluster disabilitato, viene visualizzato un messaggio di errore.  
  
 AUTO_UPDATE_STATISTICS è sempre OFF per le tabelle ottimizzate per la memoria.  
  
## <a name="permissions"></a>Permissions  
 Per modificare il AUTO_UPDATE_STATISTICS opzione, è necessario il **db_owner** ruolo predefinito del database o l'autorizzazione ALTER per *table_name*. Per visualizzare il AUTO_UPDATE_STATISTICS, opzione richiede l'appartenenza al **pubblica** ruolo.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-display-the-status-of-all-statistics-on-a-table"></a>R. Visualizzazione dello stato di tutte le statistiche in una tabella  
 Nell'esempio seguente viene visualizzato lo stato di tutte le statistiche della tabella `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product';  
GO  
```  
  
### <a name="b-enable-autoupdatestatistics-for-all-statistics-on-a-table"></a>B. Abilitazione di AUTO_UPDATE_STATISTICS per tutte le statistiche di una tabella  
 In questo esempio viene abilitata l'opzione AUTO_UPDATE_STATISTICS per tutte le statistiche della tabella `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'ON';  
GO  
```  
  
### <a name="c-disable-autoupdatestatistics-for-a-specific-index"></a>C. Disabilitazione di AUTO_UPDATE_STATISTICS per un indice specifico  
 Nell'esempio seguente l'opzione AUTO_UPDATE_STATISTICS viene disabilitata per l'indice `AK_Product_Name` della tabella `Product`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_autostats 'Production.Product', 'OFF', AK_Product_Name;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Statistiche](../../relational-databases/statistics/statistics.md)   
 [Opzioni di ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_createstats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
