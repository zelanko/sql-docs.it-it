---
title: DBCC OPENTRAN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_OPENTRAN_TSQL
- DBCC OPENTRAN
- OPENTRAN_TSQL
- OPENTRAN
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], transactions
- transactions [SQL Server], status information
- DBCC OPENTRAN statement
- open transactions
- displaying transaction information
- checking open transactions
- oldest transactions [SQL Server]
ms.assetid: 63163843-226f-42d3-9e2c-b634fbf06943
author: pmasl
ms.author: umajay
ms.openlocfilehash: 7075de83b3f2d13d80d0eb08db1d780827eddeec
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68039078"
---
# <a name="dbcc-opentran-transact-sql"></a>DBCC OPENTRAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

DBCC OPENTRAN consente di identificare le transazioni attive che potrebbero impedire il troncamento del log. In DBCC OPENTRAN vengono visualizzate informazioni sulle transazioni attive meno recenti e sulle eventuali transazioni di replica meno recenti, distribuite e non, all'interno del log delle transazioni del database specificato, se presenti. I risultati vengono visualizzati solo se nel log è presente una transazione attiva o se il database contiene informazioni di replica. In assenza di transazioni attive nel log, viene visualizzato un messaggio informativo.
  
> [!NOTE]
>  L'istruzione DBCC OPENTRAN non è supportata per server di pubblicazione non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
DBCC OPENTRAN   
[   
    ( [ database_name | database_id | 0 ] )   
    { [ WITH TABLERESULTS ]  
      [ , [ NO_INFOMSGS ] ]  
    }  
]   
```  
  
## <a name="arguments"></a>Argomenti  
 *database_name* | *database_id*| 0  
 Nome o ID del database per il quale visualizzare le informazioni sulle transazioni meno recenti. Se questo argomento viene omesso oppure se viene specificato il valore 0, viene utilizzato il database corrente. I nomi dei database devono essere conformi alle regole per gli [identificatori](../../relational-databases/databases/database-identifiers.md).  
  
 TABLERESULTS  
 Specifica i risultati in un formato tabulare caricabile in una tabella. Utilizzare questa opzione per creare una tabella di risultati che è possibile inserire in una tabella per l'esecuzione di confronti. Se questa opzione viene omessa, i risultati vengono formattati in modo da migliorare la leggibilità.  
  
 NO_INFOMSGS  
 Disattiva tutti i messaggi informativi.  
  
## <a name="remarks"></a>Osservazioni  
Utilizzare l'istruzione DBCC OPENTRAN per determinare se il log delle transazioni include una transazione aperta. Quando si utilizza l'istruzione BACKUP LOG, è possibile troncare solo la sezione inattiva del log. La presenza di una transazione aperta può comportare un troncamento incompleto del log. Per identificare una transazione aperta, utilizzare la stored procedure sp_who per ottenere l'ID del processo di sistema.
  
## <a name="result-sets"></a>Set di risultati  
In assenza di transazioni aperte, l'istruzione DBCC OPENTRAN restituisce il set di risultati seguente:
  
```sql
No active open transactions.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Autorizzazioni  
È richiesta l'appartenenza al ruolo predefinito del server **sysadmin** o al ruolo predefinito del database **db_owner** .
  
## <a name="examples"></a>Esempi  
### <a name="a-returning-the-oldest-active-transaction"></a>R. Restituzione della transazione attiva meno recente  
Nell'esempio seguente vengono recuperate le informazioni sulle transazioni per il database corrente. I risultati possono variare.
  
```sql  
CREATE TABLE T1(Col1 int, Col2 char(3));  
GO  
BEGIN TRAN  
INSERT INTO T1 VALUES (101, 'abc');  
GO  
DBCC OPENTRAN;  
ROLLBACK TRAN;  
GO  
DROP TABLE T1;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Transaction information for database 'master'.
Oldest active transaction:
SPID (server process ID) : 52
UID (user ID) : -1
Name          : user_transaction
LSN           : (518:1576:1)
Start time    : Jun  1 2004  3:30:07:197PM
SID           : 0x010500000000000515000000a065cf7e784b9b5fe77c87709e611500
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
  
> [!NOTE]  
>  Il risultato di "UID (ID utente)" non è significativo e sarà rimosso in una prossima versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="b-specifying-the-with-tableresults-option"></a>B. Specifica dell'opzione WITH TABLERESULTS  
Nell'esempio seguente vengono caricati i risultati del comando DBCC OPENTRAN in una tabella temporanea.
  
```sql  
-- Create the temporary table to accept the results.  
CREATE TABLE #OpenTranStatus (  
   ActiveTransaction varchar(25),  
   Details sql_variant   
   );  
-- Execute the command, putting the results in the table.  
INSERT INTO #OpenTranStatus   
   EXEC ('DBCC OPENTRAN WITH TABLERESULTS, NO_INFOMSGS');  
  
-- Display the results.  
SELECT * FROM #OpenTranStatus;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
[BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)  
[COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)
  
  
