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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 96e044b94244492202058d6dc2b2f048a9c1db6c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68123816"
---
# <a name="sp_grant_proxy_to_subsystem-transact-sql"></a>sp_grant_proxy_to_subsystem (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede a un proxy l'accesso a un sottosistema.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
sp_grant_proxy_to_subsystem  
     { [ @proxy_id = ] proxy_id | [ @proxy_name = ] 'proxy_name' },  
     { [ @subsystem_id = ] subsystem_id | [ @subsystem_name = ] 'subsystem_name' }  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @proxy_id = ] id`Numero di identificazione del proxy per il quale concedere l'accesso. Il *proxy_id* è di **tipo int**e il valore predefinito è null. È necessario specificare *proxy_id* o *proxy_name* , ma non è possibile specificarli entrambi.  
  
`[ @proxy_name = ] 'proxy_name'`Nome del proxy per il quale concedere l'accesso. Il *proxy_name* è di **tipo sysname**e il valore predefinito è null. È necessario specificare *proxy_id* o *proxy_name* , ma non è possibile specificarli entrambi.  
  
`[ @subsystem_id = ] id`Numero ID del sottosistema a cui concedere l'accesso. Il *subsystem_id* è di **tipo int**e il valore predefinito è null. È necessario specificare *subsystem_id* o *subsystem_name* , ma non è possibile specificarli entrambi. Nella tabella seguente vengono elencati i valori disponibili per ogni sottosistema.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]Script ActiveX<br /><br /> ** \* Importante \* \* ** Il sottosistema di scripting ActiveX verrà rimosso da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata.|  
|**3**|Sistema operativo (**CmdExec**)|  
|**4**|Agente snapshot repliche|  
|**5**|Agente lettura log repliche|  
|**6**|Agente distribuzione repliche|  
|**7**|Agente merge repliche|  
|**8**|Agente di lettura coda repliche|  
|**9**|Query di Analysis Services|  
|**10**|Comando di Analysis Services|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)]esecuzione del pacchetto|  
|**12**|Script PowerShell|  
| &nbsp; | &nbsp; |
  
`[ @subsystem_name = ] 'subsystem_name'`Nome del sottosistema a cui concedere l'accesso. Il **subsystem_name** è di **tipo sysname**e il valore predefinito è null. È necessario specificare *subsystem_id* o *subsystem_name* , ma non è possibile specificarli entrambi. Nella tabella seguente vengono elencati i valori disponibili per ogni sottosistema.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**ActiveScripting**|Script ActiveX|  
|**CmdExec**|Sistema operativo (**CmdExec**)|  
|**Snapshot**|Agente snapshot repliche|  
|**Lettura log**|Agente lettura log repliche|  
|**Distribuzione**|agente di distribuzione di replica|  
|**Merge**|Agente merge repliche|  
|**Processo QueueReader**|Agente di lettura coda repliche|  
|**ANALYSISQUERY**|Query di Analysis Services|  
|**ANALYSISCOMMAND**|Comando di Analysis Services|  
|**DTS**|Esecuzione di pacchetti SSIS|  
|**PowerShell**|Script PowerShell|  
| &nbsp; | &nbsp; |
  
## <a name="remarks"></a>Osservazioni  
 Concedendo a un proxy l'accesso a un sottosistema non vengono modificate le autorizzazione per l'entità specificata nel proxy.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_grant_proxy_to_subsystem**.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-granting-access-to-a-subsystem-by-id"></a>R. Concessione dell'accesso a un sottosistema in base all'ID  
 Nell'esempio seguente viene concesso al proxy `Catalog application proxy` l'accesso al sottosistema script ActiveX.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_id = 2;  
GO  
```  
  
### <a name="b-granting-access-to-a-subsystem-by-name"></a>B. Concessione dell'accesso a un sottosistema in base al nome.  
 Nell'esempio seguente viene concesso al proxy `Catalog application proxy` l'accesso al sottosistema di esecuzione pacchetti SSIS.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = N'Catalog application proxy',  
    @subsystem_name = N'Dts' ;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Implementare SQL Server Agent sicurezza](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_revoke_proxy_from_subsystem &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-revoke-proxy-from-subsystem-transact-sql.md)   
 [sp_add_proxy &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_update_proxy &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-proxy-transact-sql.md)  
  
  
