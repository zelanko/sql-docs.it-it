---
title: sp_grant_proxy_to_subsystem (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_subsystem_TSQL
- sp_grant_login_to_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_proxy_to_subsystem
ms.assetid: 866aaa27-a1e0-453a-9b1b-af39431ad9c2
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7eecd8743d24ab783e163ab10abc0441362b37a4
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528133"
---
# <a name="spgrantproxytosubsystem-transact-sql"></a>sp_grant_proxy_to_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede a un proxy l'accesso a un sottosistema.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_grant_proxy_to_subsystem  
     { [ @proxy_id = ] proxy_id | [ @proxy_name = ] 'proxy_name' },  
     { [ @subsystem_id = ] subsystem_id | [ @subsystem_name = ] 'subsystem_name' }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @proxy_id = ] id` Il numero di identificazione per concedere l'accesso per il proxy. Il *proxy_id* viene **int**, con un valore predefinito è NULL. Entrambi *proxy_id* oppure *proxy_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @proxy_name = ] 'proxy_name'` Il nome del proxy per concedere l'accesso. Il *nome_proxy* viene **sysname**, con un valore predefinito è NULL. Entrambi *proxy_id* oppure *proxy_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @subsystem_id = ] id` Il numero di id del sottosistema a cui concedere l'accesso a. Il *subsystem_id* viene **int**, con un valore predefinito è NULL. Entrambi *subsystem_id* oppure *subsystem_name* devono essere specificati, ma non è possibile specificarli entrambi. Nella tabella seguente vengono elencati i valori disponibili per ogni sottosistema.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**2**|Script [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX<br /><br /> **\*\* Importanti \* \***  verrà rimosso dal sottosistema di Scripting ActiveX The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata.|  
|**3**|Sistema operativo (**CmdExec**)|  
|**4**|Agente snapshot repliche|  
|**5**|Agente lettura log repliche|  
|**6**|Agente distribuzione repliche|  
|**7**|Agente merge repliche|  
|**8**|Agente di lettura coda repliche|  
|**9**|Query di Analysis Services|  
|**10**|Comando di Analysis Services|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] esecuzione del pacchetto|  
|**12**|Script di PowerShell|  
  
`[ @subsystem_name = ] 'subsystem_name'` Il nome del sottosistema a cui concedere l'accesso a. Il **subsystem_name** viene **sysname**, con un valore predefinito è NULL. Entrambi *subsystem_id* oppure *subsystem_name* devono essere specificati, ma non è possibile specificarli entrambi. Nella tabella seguente vengono elencati i valori disponibili per ogni sottosistema.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**ActiveScripting**|Script ActiveX|  
|**CmdExec**|Sistema operativo (**CmdExec**)|  
|**Snapshot**|Agente snapshot repliche|  
|**LogReader**|Agente lettura log repliche|  
|**Distribuzione**|Agente distribuzione repliche|  
|**Merge**|Agente merge repliche|  
|**QueueReader**|Agente di lettura coda repliche|  
|**ANALYSISQUERY**|Query di Analysis Services|  
|**ANALYSISCOMMAND**|Comando di Analysis Services|  
|**Dts**|Esecuzione pacchetti SSIS|  
|**PowerShell**|Script di PowerShell|  
  
## <a name="remarks"></a>Note  
 Concedendo a un proxy l'accesso a un sottosistema non vengono modificate le autorizzazione per l'entità specificata nel proxy.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_grant_proxy_to_subsystem**.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-granting-access-to-a-subsystem-by-id"></a>A. Concessione dell'accesso a un sottosistema in base all'ID  
 Nell'esempio seguente viene concesso al proxy `Catalog application proxy` l'accesso al sottosistema script ActiveX.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_id = 2;  
GO  
```  
  
### <a name="b-granting-access-to-a-subsystem-by-name"></a>B. Concessione dell'accesso a un sottosistema in base al nome.  
 Nell'esempio seguente viene concesso al proxy `Catalog application proxy` l'accesso al sottosistema di esecuzione pacchetti SSIS.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = N'Catalog application proxy',  
    @subsystem_name = N'Dts' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_revoke_proxy_from_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-proxy-from-subsystem-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_update_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-proxy-transact-sql.md)  
  
  
