---
title: sp_revoke_proxy_from_subsystem (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_subsystem
- sp_revoke_login_from_subsystem_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_proxy_from_subsystem
ms.assetid: b87bc8ba-3ea8-4aed-b54b-32c3d82d9d2a
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 4079a6afda1f303369a2d8b9defc8bbeb3c4608d
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527233"
---
# <a name="sprevokeproxyfromsubsystem-transact-sql"></a>sp_revoke_proxy_from_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoca l'accesso a un sottosistema da un proxy.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_revoke_proxy_from_subsystem   
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @proxy_id = ] id` Il numero di identificazione di proxy del proxy per revocare l'accesso a. Il *proxy_id* viene **int**, con un valore predefinito è NULL. Entrambi *proxy_id* oppure *proxy_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @proxy_name = ] 'proxy_name'` Il nome del proxy per revocare l'accesso a. Il *nome_proxy* viene **sysname**, con un valore predefinito è NULL. Entrambi *proxy_id* oppure *proxy_name* devono essere specificati, ma non è possibile specificarli entrambi.  
  
`[ @subsystem_id = ] id` Il numero di id del sottosistema a cui revocare l'accesso a. Il *subsystem_id* viene **int**, con un valore predefinito è NULL. Entrambi *subsystem_id* oppure *subsystem_name* devono essere specificati, ma non è possibile specificarli entrambi. Nella tabella seguente vengono elencati i valori disponibili per ogni sottosistema.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**2**|Script ActiveX<br /><br /> **\*\* Importanti \* \***  verrà rimosso dal sottosistema di Scripting ActiveX The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent in una versione futura di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata.|  
|**3**|Sistema operativo (CmdExec)|  
|**4**|Agente snapshot repliche|  
|**5**|Agente lettura log repliche|  
|**6**|Agente distribuzione repliche|  
|**7**|Agente merge repliche|  
|**8**|Agente di lettura coda repliche|  
|**9**|Comando di Analysis Services|  
|**10**|Query di Analysis Services|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] esecuzione del pacchetto|  
|**12**|Script di PowerShell|  
  
`[ @subsystem_name = ] 'subsystem_name'` Il nome del sottosistema a cui revocare l'accesso a. Il *subsystem_name* viene **sysname**, con un valore predefinito è NULL. Entrambi *subsystem_id* oppure *subsystem_name* devono essere specificati, ma non è possibile specificarli entrambi. Nella tabella seguente vengono elencati i valori disponibili per ogni sottosistema.  
  
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
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)] esecuzione del pacchetto|  
|PowerShell|Script di PowerShell|  
  
## <a name="remarks"></a>Note  
 La revoca dell'accesso a un sottosistema non modifica le autorizzazione per l'entità specificata nel proxy.  
  
> [!NOTE]  
>  Per determinare quali passaggi del processo fanno riferimento a un proxy, fare doppio clic sui **proxy** nodo sotto **SQL Server Agent** in Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], quindi fare clic su **proprietà**. Nel **proprietà Account Proxy** finestra di dialogo, seleziona la **riferimenti** pagina per visualizzare tutti i passaggi di processo che fanno riferimento a questo proxy.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_revoke_proxy_from_subsystem**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene revocato l'accesso al sottosistema [!INCLUDE[ssIS](../../includes/ssis-md.md)] per il proxy `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementazione di sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
