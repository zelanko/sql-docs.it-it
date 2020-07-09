---
title: DBCC INPUTBUFFER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
author: pmasl
ms.author: umajay
ms.openlocfilehash: 0560bee16adc28205e5f05250c477ccea6a9683d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757242"
---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Visualizza l'ultima istruzione inviata da un client a un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argomenti  
*session_id*  
ID della sessione associata a ogni connessione principale attiva.  
  
*request_id*  
Richiesta esatta (batch) da cercare nella sessione corrente.  

La query seguente restituisce *request_id*:  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
WITH  
Consente di specificare opzioni.  
  
NO_INFOMSGS  
Evita la visualizzazione di tutti i messaggi informativi con livello di gravità compreso tra 0 e 10.  
  
## <a name="result-sets"></a>Set di risultati  
L'istruzione DBCC INPUTBUFFER restituisce un set di righe che include le colonne seguenti.
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**EventType**|**nvarchar(30)**|Tipo di evento. Può corrispondere a **RPC Event** o **Language Event**. Se non viene rilevato un ultimo evento, l'output sarà **No Event**.|  
|**Parameters**|**smallint**|0 = Testo<br /><br /> 1- *n* = Parametri|  
|**EventInfo**|**nvarchar(4000)**|Se il valore della colonna **EventType** è RPC Event, **EventInfo** contiene solo il nome della procedura. Se **EventType** corrisponde a Language Event, vengono visualizzati solo i primi 4000 caratteri dell'evento.|  
  
Se, ad esempio, l'ultimo evento del buffer è DBCC INPUTBUFFER(11), DBCC INPUTBUFFER restituisce il set di risultati seguente.
  
```
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  

> [!NOTE]
> A partire da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2, usare [sys.dm_exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) per restituire informazioni sulle istruzioni inviate a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="permissions"></a>Autorizzazioni  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è richiesta una delle condizioni seguenti:
-   L'utente deve essere membro del ruolo predefinito del server **sysadmin**.  
-   L'utente deve disporre di autorizzazione VIEW SERVER STATE.  
-   *session_id* deve corrispondere all'ID della sessione in cui è in esecuzione il comando. Per determinare l'ID di sessione, eseguire la query seguente:  
  
```sql
SELECT @@spid;  
```
  
Nei livelli Premium e Business Critical di [!INCLUDE[ssSDS](../../includes/sssds-md.md)] è richiesta l'autorizzazione VIEW DATABASE STATE nel database. Nei livelli Standard, Basic e Utilizzo generico del [!INCLUDE[ssSDS](../../includes/sssds-md.md)] è richiesto l'account amministratore del [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
## <a name="examples"></a>Esempi  
Nell'esempio seguente viene eseguito `DBCC INPUTBUFFER` in una seconda connessione durante una transazione di lunga durata su una connessione precedente.
  
```sql
CREATE TABLE dbo.T1 (Col1 int, Col2 char(3));  
GO  
DECLARE @i int = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS char(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  
