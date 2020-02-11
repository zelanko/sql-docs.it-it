---
title: sp_trace_generateevent (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_generateevent_TSQL
- sp_trace_generateevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_generateevent
ms.assetid: 3ef05bfb-b467-4403-89cc-6e77ef9247dd
author: stevestein
ms.author: sstein
ms.openlocfilehash: cfeacf9f3c18d3f80b7ad83a3697e33a5797ba22
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096018"
---
# <a name="sp_trace_generateevent-transact-sql"></a>sp_trace_generateevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un evento definito dall'utente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
>**Nota:**  Questo stored procedure **non** è deprecato. Tutte le altre stored procedure correlate alle tracce sono deprecate.  
  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @eventid = ] event_id`ID dell'evento da attivare. *event_id* è di **tipo int**e non prevede alcun valore predefinito. L'ID deve essere uno dei numeri di evento compresi tra 82 e 91, che rappresentano gli eventi definiti dall'utente come impostati con [sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
`[ @userinfo = ] 'user_info'`Stringa facoltativa definita dall'utente che identifica il motivo dell'evento. *user_info* è di **tipo nvarchar (128)** e il valore predefinito è null.  
  
`[ @userdata = ] user_data`Dati facoltativi specificati dall'utente per l'evento. *user_data* è di tipo **varbinary (8000)** e il valore predefinito è null.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 Nella tabella seguente vengono descritti i possibili valori di codice visualizzati al completamento della stored procedure.  
  
|Codice restituito|Descrizione|  
|-----------------|-----------------|  
|**0**|Nessun errore.|  
|**1**|Errore sconosciuto.|  
|**3**|L'evento specificato non è valido, in quanto non esiste oppure non è appropriato per la stored procedure.|  
|**13**|memoria insufficiente. Restituito quando la quantità di memoria disponibile non è sufficiente per eseguire l'azione specificata.|  
  
## <a name="remarks"></a>Osservazioni  
 **sp_trace_generateevent** esegue molte delle azioni eseguite in precedenza dal **xp_trace_\* ** stored procedure estese. Utilizzare **sp_trace_generateevent** anziché **xp_trace_generate_event**.  
  
 Con **sp_trace_generateevent**è possibile utilizzare solo i numeri ID degli eventi definiti dall'utente. Se si utilizzano altri ID di evento, in[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà generato un errore.  
  
 I parametri di tutte le stored procedure di traccia SQL (**sp_trace_xx**) sono fortemente tipizzati. Se questi parametri non vengono chiamati con i tipi di dati corretti per i parametri di input, come indicato nella descrizione dell'argomento, la stored procedure restituirà un errore.  
  
## <a name="permissions"></a>Autorizzazioni  
 L'utente deve disporre delle autorizzazioni ALTER TRACE.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creato un evento configurabile dall'utente in una tabella di esempio.  
  
```  
--Create a sample table.  
CREATE TABLE user_config_test(col1 int, col2 char(10));  
  
--DROP the trigger if it already exists.  
IF EXISTS  
   (SELECT * FROM sysobjects WHERE name = 'userconfig_trg')  
   DROP TRIGGER userconfig_trg;  
  
--Create an ON INSERT trigger on the sample table.  
CREATE TRIGGER userconfig_trg  
   ON user_config_test FOR INSERT;  
AS  
EXEC master..sp_trace_generateevent  
   @event_class = 82, @userinfo = N'Inserted row into user_config_test';  
  
--When an insert action happens, the user-configurable event fires. If   
you were capturing the event id=82, you will see it in the Profiler output.  
INSERT INTO user_config_test VALUES(1, 'abc');  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys. fn_trace_geteventinfo &#40;&#41;Transact-SQL](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Traccia SQL](../../relational-databases/sql-trace/sql-trace.md)  
  
  
