---
title: sp_helpserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpserver
- sp_helpserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpserver
ms.assetid: e8f42de7-c738-41c3-8bf5-dbd559dc7184
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31caafde6ea3cdd93355910f244ed5872b6990ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62635888"
---
# <a name="sphelpserver-transact-sql"></a>sp_helpserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni su un particolare server remoto o di replica oppure su tutti i server di entrambi i tipi. Specifica il nome del server, il nome di rete del server, lo stato di replica del server, il numero di identificazione del server e il nome delle regole di confronto nonché i valori di timeout per la connessione a server collegati o l'esecuzione di query su server collegati.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpserver [ [ @server = ] 'server' ]   
  [ , [ @optname = ] 'option' ]   
  [ , [ @show_topology = ] 'show_topology' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @server = ] 'server'` È il server su cui vengono restituite informazioni. Quando *server* non viene specificato, i report su tutti i server nella **Servers**. *server* viene **sysname**, con un valore predefinito è NULL.  
  
`[ @optname = ] 'option'` L'opzione che descrive il server. *opzione* viene **varchar (** 35 **)** , con un valore predefinito è NULL e deve essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**regole di confronto compatibili**|L'utilizzo di questa opzione influisce sull'esecuzione delle query distribuite in server collegati. Se questa opzione è impostata su true,|  
|**accesso ai dati**|Consente di attivare e disabilitare un server collegato per l'accesso a query distribuite.|  
|**dist**|Server di distribuzione.|  
|**dpub**|Server di pubblicazione remoto associato al server di distribuzione corrente.|  
|**convalida differita dello schema**|Ignora il controllo dello schema delle tabelle remote all'inizio della query.|  
|**pub**|Server di pubblicazione.|  
|**rpc**|Attiva l'esecuzione di chiamate RPC dal server specificato.|  
|**rpc out**|Viene abilitata l'esecuzione di chiamate RPC al server specificato.|  
|**sub**|Sottoscrittore.|  
|**system**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**usare regole di confronto remote**|Consente di utilizzare le regole di confronto di una colonna remota anziché quelle del server locale.|  
  
`[ @show_topology = ] 'show_topology'` È la relazione del server specificato ad altri server. *show_topology* viene **varchar (** 1 **)** , con un valore predefinito è NULL. Se *show_topology* non è uguale a **t** oppure è NULL, **sp_helpserver** restituisce le colonne elencate nella sezione set di risultati. Se *show_topology* è uguale a **t**, oltre alle colonne elencate nel set di risultati **sp_helpserver** restituisce inoltre **topx** e **topy** informazioni.  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome del server.|  
|**network_name**|**sysname**|Nome di rete del server.|  
|**status**|**varchar(** 70 **)**|Stato del server.|  
|**id**|**char(** 4 **)**|Numero di identificazione del server.|  
|**nome_regole_di_confronto**|**sysname**|Regole di confronto del server.|  
|**connect_timeout**|**int**|Valore di timeout per la connessione al server collegato.|  
|**query_timeout**|**int**|Valore di timeout per le query eseguite sul server collegato.|  
  
## <a name="remarks"></a>Note  
 A un server possono essere associati più stati.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni non vengono controllate.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-displaying-information-about-all-servers"></a>A. Visualizzazione di informazioni su tutti i server  
 Nell'esempio seguente vengono visualizzate informazioni su tutti i server tramite l'esecuzione di `sp_helpserver` senza parametri.  
  
```  
USE master;  
GO  
EXEC sp_helpserver;  
```  
  
### <a name="b-displaying-information-about-a-specific-server"></a>B. Visualizzazione di informazioni su un server specifico  
 Nell'esempio seguente vengono visualizzate tutte le informazioni sul server `SEATTLE2`.  
  
```  
USE master;  
GO  
EXEC sp_helpserver 'SEATTLE2';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Motore di database le Stored procedure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
