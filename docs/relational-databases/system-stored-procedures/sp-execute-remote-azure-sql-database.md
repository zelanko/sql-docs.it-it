---
description: sp_execute_remote (database SQL di Azure)
title: sp_execute_remote (database SQL di Azure) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1642baedb44cc6eab4474616d03abd2f429f4276
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447158"
---
# <a name="sp_execute_remote-azure-sql-database"></a>sp_execute_remote (database SQL di Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Esegue un' [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione in un singolo database SQL di Azure remoto o in un set di database che funge da partizione in uno schema di partizionamento orizzontale.  
  
 Il stored procedure fa parte della funzionalità di query elastica.  Vedere [Panoramica delle query sul database elastico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) del database SQL di Azure e [query sul database elastico per il partizionamento orizzontale (partizionamento orizzontale)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ \@ data_source_name =] *DataSourceName*  
 Identifica l'origine dati esterna in cui viene eseguita l'istruzione. Vedere [creare un'origine dati esterna &#40;&#41;Transact-SQL ](../../t-sql/statements/create-external-data-source-transact-sql.md). L'origine dati esterna può essere di tipo "RDBMS" o "SHARD_MAP_MANAGER".  
  
 [ \@ stmt =] ( *istruzione* )  
 Stringa Unicode che contiene un' [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o un batch. \@stmt deve essere una costante Unicode o una variabile Unicode. Non sono consentite le espressioni Unicode più complesse, ad esempio per la concatenazione di due stringhe tramite l'operatore +. Le costanti di tipo carattere non sono consentite. Se viene specificata una costante Unicode, è necessario che sia preceduta da un valore **N**. La costante Unicode **N'sp_who '** , ad esempio, è valida, ma la costante carattere **' sp_who '** non lo è. Le dimensioni massime della stringa dipendono dalla memoria disponibile nel server di database. Nei server a 64 bit, le dimensioni della stringa sono limitate a 2 GB, ovvero la dimensione massima di **nvarchar (max)**.  
  
> [!NOTE]  
>  \@stmt può contenere parametri con lo stesso formato di un nome di variabile, ad esempio: `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Ogni parametro incluso in \@ stmt deve avere una voce corrispondente nell'elenco di \@ definizioni dei parametri params e nell'elenco dei valori dei parametri.  
  
 [ \@ params =] n' \@ *parameter_name * * data_type* [,... *n* ]'  
 È una stringa che contiene le definizioni di tutti i parametri incorporati in \@ stmt. La stringa deve essere una costante Unicode o una variabile Unicode. Ogni definizione di parametro è costituita da un nome del parametro e da un tipo di dati. *n* è un segnaposto che indica definizioni di parametro aggiuntive. Ogni parametro specificato in \@ stmtmust deve essere definito in \@ params. Se l' [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o il batch in \@ stmt non contiene parametri, \@ params non è necessario. Il valore predefinito per questo parametro è NULL.  
  
 [ \@ param1 =]'*value1*'  
 Valore per il primo parametro definito nella stringa di parametri. Il valore può essere una costante o una variabile Unicode. È necessario specificare un valore di parametro per ogni parametro incluso in \@ stmt. I valori non sono necessari se l' [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o il batch in \@ stmt non dispone di parametri.  
  
 *n*  
 Segnaposto per i valori di parametri aggiuntivi. I valori possono essere solo costanti o variabili. Non sono consentite espressioni più complesse quali funzioni o espressioni compilate tramite operatori.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 0 (esito positivo) o valore diverso da zero (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce il set di risultati dalla prima istruzione SQL.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione `ALTER ANY EXTERNAL DATA SOURCE`.  
  
## <a name="remarks"></a>Osservazioni  
 `sp_execute_remote` i parametri devono essere specificati nell'ordine specifico, come descritto nella sezione precedente della sintassi. Se i parametri non vengono immessi in ordine, verrà visualizzato un messaggio di errore.  
  
 `sp_execute_remote` ha lo stesso comportamento di [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md) per quanto riguarda i batch e l'ambito dei nomi. L'istruzione o il batch Transact-SQL nel sp_execute_remote parametro * \@ stmt* non viene compilato finché non viene eseguita l'istruzione sp_execute_remote.  
  
 `sp_execute_remote` aggiunge una colonna aggiuntiva al set di risultati denominato ' $ShardName ' contenente il nome del database remoto che ha prodotto la riga.  
  
 `sp_execute_remote` può essere utilizzato in modo analogo a [sp_executesql &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md).  
  
## <a name="examples"></a>Esempi  
### <a name="simple-example"></a>Esempio semplice  
 Nell'esempio seguente viene creata ed eseguita una semplice istruzione SELECT su un database remoto.  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>Esempio con più parametri  
Creare una credenziale con ambito database in un database utente, specificando le credenziali di amministratore per il database master. Creare un'origine dati esterna che punta al database master e specificare le credenziali con ambito database. In seguito, ad esempio, nel database utente viene eseguita la `sp_set_firewall_rule` procedura nel database master. `sp_set_firewall_rule`Per la procedura sono necessari 3 parametri e il `@name` parametro deve essere Unicode.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>Vedere anche:

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
