---
title: sp_help_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 904a694d73613bb1c40c671b18ca33e5d9b5d0e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085281"
---
# <a name="sphelpproxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Visualizza le informazioni per uno o più proxy.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @proxy_id = ] id` Il numero di identificazione per elencare le informazioni per il proxy. Il *proxy_id* viene **int**, con un valore predefinito è NULL. Entrambi i *id* o nella *proxy_name* può essere specificato.  
  
`[ @proxy_name = ] 'proxy_name'` Il nome del proxy da elenco di informazioni. Il *nome_proxy* viene **sysname**, con un valore predefinito è NULL. Entrambi i *id* o nella *proxy_name* può essere specificato.  
  
`[ @subsystem_name = ] 'subsystem_name'` Il nome del sottosistema per elenco di proxy. Il *subsystem_name* viene **sysname**, con un valore predefinito è NULL. Quando *subsystem_name* omette *nome* deve essere specificato anche.  
  
 Nella tabella seguente vengono elencati i valori disponibili per ogni sottosistema.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|ActiveScripting|Script ActiveX|  
|CmdExec|Sistema operativo (CmdExec)|  
|Snapshot|Agente snapshot repliche|  
|LogReader|Agente lettura log repliche|  
|Distribuzione|Agente distribuzione repliche|  
|Merge|Agente merge repliche|  
|QueueReader|Agente di lettura coda repliche|  
|ANALYSISQUERY|Comando di Analysis Services|  
|ANALYSISCOMMAND|Query di Analysis Services|  
|Dts|Esecuzione pacchetti SSIS|  
|PowerShell|Script di PowerShell|  
  
`[ @name = ] 'name'` Il nome di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso per l'elenco dei proxy. Il nome è **nvarchar(256)** , con un valore predefinito è NULL. Quando *nome* omette *subsystem_name* deve essere specificato anche.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Numero di identificazione del proxy.|  
|**name**|**sysname**|Nome del proxy.|  
|**credential_identity**|**sysname**|Nome utente e del dominio Microsoft Windows per le credenziali associate al proxy.|  
|**enabled**|**tinyint**|Indica se il proxy è attivato. { **0** = non abilitata, **1** = attivato}|  
|**description**|**nvarchar(1024)**|Descrizione del proxy.|  
|**user_sid**|**varbinary(85)**|ID di sicurezza (SID) di Windows dell'utente di Windows per questo proxy.|  
|**credential_id**|**int**|Identificatore per le credenziali associate a questo proxy.|  
|**credential_identity_exists**|**int**|Indica se credential_identity esiste. { 0 = non esiste, 1 = esiste }|  
  
## <a name="remarks"></a>Note  
 Quando viene specificato alcun parametro, **sp_help_proxy** Elenca le informazioni per tutti i proxy nell'istanza.  
  
 Per determinare quali proxy un account di accesso è possibile usare per un determinato sottosistema, specificare *name* e *subsystem_name*. Quando vengono specificati questi argomenti, **sp_help_proxy** proxy che l'account di accesso specificata possono accedere e che possono essere utilizzati per il sottosistema specificato.  
  
## <a name="permissions"></a>Permissions  
 Per impostazione predefinita, questa stored procedure può essere eseguita dai membri del ruolo predefinito del server **sysadmin** . Gli altri utenti devono appartenere al ruolo predefinito del database **SQLAgentOperatorRole** nel database **msdb** .  
  
 Per informazioni dettagliate sui **SQLAgentOperatorRole**, vedere [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
> [!NOTE]  
>  Il **credential_identity** e **user_sid** le colonne vengono restituite solo nel set di risultati quando i membri del **sysadmin** eseguire questa stored procedure.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-listing-information-for-all-proxies"></a>R. Visualizzazione di un elenco di informazioni per tutti i proxy  
 Nell'esempio seguente viene visualizzato un elenco di informazioni per tutti i proxy nell'istanza.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>B. Visualizzazione di un elenco di informazioni per un proxy specifico  
 Nell'esempio seguente viene visualizzato un elenco di informazioni per il proxy denominato `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
