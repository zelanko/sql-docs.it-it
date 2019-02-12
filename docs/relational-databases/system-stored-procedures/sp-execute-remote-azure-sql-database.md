---
title: sp_execute_remote (Database SQL di Azure) | Microsoft Docs
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
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a475ba50aa8d3ba140ea551306d8b9f17fe66d22
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035902"
---
# <a name="spexecuteremote-azure-sql-database"></a>sp_execute_remote (database SQL di Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Esegue un [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione in un singolo Database SQL di Azure remoto o un set di database fungono da partizioni in uno schema di partizionamento orizzontale.  
  
 La stored procedure è parte della funzionalità di query elastica.  Visualizzare [panoramica delle query su database elastico del Database SQL di Azure](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) e [query di database elastico per il partizionamento orizzontale (partizionamento orizzontale)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ \@data_source_name =] *datasourcename*  
 Identifica l'origine dati esterna in cui viene eseguita l'istruzione. Visualizzare [Crea origine dati esterna &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md). L'origine dati esterna può essere di tipo "Sistema RDBMS" o "SHARD_MAP_MANAGER".  
  
 [ \@stmt= ] *statement*  
 È una stringa Unicode che contiene un [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o il batch. \@stmt deve essere una costante Unicode o una variabile Unicode. Non sono consentite le espressioni Unicode più complesse, ad esempio per la concatenazione di due stringhe tramite l'operatore +. Le costanti di tipo carattere non sono consentite. Se viene specificata una costante Unicode, devono essere preceduto da un **N**. Ad esempio, la costante Unicode **n' sp_who'** valido, ma la costante carattere **'sp_who'** non. Le dimensioni massime della stringa dipendono dalla memoria disponibile nel server di database. Nei server a 64 bit, le dimensioni della stringa sono limitate a 2 GB, la dimensione massima del **nvarchar (max)**.  
  
> [!NOTE]  
>  \@stmt può contenere parametri con lo stesso formato di un nome di variabile, ad esempio: `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Ogni parametro incluso in \@stmt deve avere una voce corrispondente in entrambe le \@params elenco di definizioni di parametro e il parametro di elenco di valori.  
  
 [ \@params= ] N'\@*parameter_name**data_type* [ ,... *n* ] '  
 Stringa che contiene le definizioni di tutti i parametri che sono stati incorporati in \@stmt. La stringa deve essere una costante o una variabile Unicode. Ogni definizione di parametro è costituita da un nome del parametro e da un tipo di dati. *n* è un segnaposto che indica definizioni di parametro aggiuntive. Ogni parametro specificato in \@stmtmust essere definite in \@params. Se il [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o il batch nel \@stmt non contiene parametri, \@params non è obbligatorio. Il valore predefinito per questo parametro è NULL.  
  
 [ \@param1 =] '*value1*'  
 Valore per il primo parametro definito nella stringa di parametri. Il valore può essere una costante o una variabile Unicode. Deve esistere un valore di parametro per ogni parametro incluso in \@stmt. I valori non sono necessari se il [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione o il batch in \@stmt non ha parametri.  
  
 *n*  
 Segnaposto per i valori di parametri aggiuntivi. I valori possono essere solo costanti o variabili. Non sono consentite espressioni più complesse quali funzioni o espressioni compilate tramite operatori.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o valore diverso da zero (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
 Restituisce il risultato impostato dalla prima istruzione SQL.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione `ALTER ANY EXTERNAL DATA SOURCE`.  
  
## <a name="remarks"></a>Note  
 `sp_execute_remote` come descritto nella sezione relativa alla sintassi precedente, è necessario specificare i parametri nell'ordine specifico. Se i parametri non vengono immessi in ordine, verrà visualizzato un messaggio di errore.  
  
 `sp_execute_remote` ha lo stesso comportamento come [EXECUTE &#40;Transact-SQL&#41; ](../../t-sql/language-elements/execute-transact-sql.md) in termini di batch e l'ambito dei nomi. L'istruzione Transact-SQL o il batch nel sp_execute_remote  *\@stmt* parametro non viene compilato finché non viene eseguita l'istruzione sp_execute_remote.  
  
 `sp_execute_remote` Aggiunge un'ulteriore colonna al set di risultati denominato '$ShardName' che contiene il nome del database remoto che ha generato la riga.  
  
 `sp_execute_remote` può essere usato simile a [sp_executesql &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md).  
  
## <a name="examples"></a>Esempi  
### <a name="simple-example"></a>Esempio semplice  
 Nell'esempio seguente crea ed esegue un'istruzione SELECT semplice in un database remoto.  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>Esempio con più parametri  
Creare una credenziale con ambito database in un database utente, specificare le credenziali di amministratore per il database master. Creare un'origine dati esterna che punta al database master e si specifica la credenziale con ambito database. Comando seguente, riportato nel database utente, viene eseguito il `sp_set_firewall_rule` procedure nel database master. Il `sp_set_firewall_rule` procedure richiede 3 parametri ed è necessario il `@name` parametro sia Unicode.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>Vedere anche:

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
