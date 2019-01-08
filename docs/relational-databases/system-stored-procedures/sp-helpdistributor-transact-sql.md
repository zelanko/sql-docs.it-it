---
title: sp_helpdistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributor_TSQL
- sp_helpdistributor
helpviewer_keywords:
- sp_helpdistributor
ms.assetid: 37b0983e-3b69-4f0f-977e-20efce0a0b97
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 63441a20a5ac4f6faed366c06fc55638073b09f4
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591395"
---
# <a name="sphelpdistributor-transact-sql"></a>sp_helpdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elenca le informazioni sul server di distribuzione, database di distribuzione, directory di lavoro e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account utente dell'agente. Questa stored procedure viene eseguita nel database di pubblicazione o in qualsiasi database del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpdistributor [ [ @distributor= ] 'distributor' OUTPUT ]  
    [ , [ @distribdb= ] 'distribdb' OUTPUT ]  
    [ , [ @directory= ] 'directory' OUTPUT ]  
    [ , [ @account= ] 'account' OUTPUT ]  
    [ , [ @min_distretention= ] min_distretention OUTPUT ]  
    [ , [ @max_distretention= ] max_distretention OUTPUT ]  
    [ , [ @history_retention= ] history_retention OUTPUT ]  
    [ , [ @history_cleanupagent= ] 'history_cleanupagent' OUTPUT ]  
    [ , [ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @local = ] 'local' ]  
    [ , [ @rpcsrvname= ] 'rpcsrvname' OUTPUT ]  
    [ , [ @publisher_type = ] 'publisher_type' OUTPUT ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@distributor=**] **'**_distributore_**'** OUTPUT  
 Nome del server di distribuzione. Server di distribuzione **sysname**, il valore predefinito è **%**, che è l'unico valore che restituisce un set di risultati.  
  
 [  **@distribdb=**] **'**_distribdb_**'** OUTPUT  
 Nome del database di distribuzione. *distribdb* viene **sysname**, il valore predefinito è **%**, che è l'unico valore che restituisce un set di risultati.  
  
 [  **@directory=**] **'**_directory_**'** OUTPUT  
 Directory di lavoro. *directory* viene **nvarchar(255**, il valore predefinito è **%**, che è l'unico valore che restituisce un set di risultati.  
  
 [  **@account=**] **'**_account_**' OUTPUT**  
 Account utente di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. *account*viene **nvarchar(255**, il valore predefinito è **%**, che è l'unico valore che restituisce un set di risultati.  
  
 [  **@min_distretention=**] _min_distretention_**OUTPUT**  
 Periodo di memorizzazione minimo per la distribuzione espresso in ore. *min_distretention* viene **int**, il valore predefinito è **-1**.  
  
 [  **@max_distretention=**] _max_distretention_**OUTPUT**  
 Periodo di memorizzazione massimo per la distribuzione espresso in ore. *max_distretention* viene **int**, il valore predefinito è **-1**.  
  
 [  **@history_retention=**] _history_retention_**OUTPUT**  
 Periodo di memorizzazione della cronologia espresso in ore. *history_retention* viene **int**, il valore predefinito è **-1**.  
  
 [  **@history_cleanupagent=**] **'**_history_cleanupagent_**' OUTPUT**  
 Nome dell'agente per la pulizia del contenuto della cronologia. *history_cleanupagent* viene **nvarchar(100)**, il valore predefinito è **%**, che è l'unico valore che restituisce un set di risultati.  
  
 [  **@distrib_cleanupagent =**] **'**_distrib_cleanupagent_**' OUTPUT**  
 Nome dell'agente per l'eliminazione dei riferimenti di distribuzione *distrib_cleanupagent* viene **nvarchar(100)**, il valore predefinito è **%**, che è l'unico valore che restituisce un set di risultati.  
  
 [  **@publisher=**] **'**_editore_**'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
 [  **@local=**] **'**_locale_**'**  
 Indica se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve recuperare o meno i valori del server locale. *locale* viene **nvarchar(5**, con un valore predefinito è NULL.  
  
 [  **@rpcsrvname=**] **'**_rpcsrvname_**' OUTPUT**  
 Nome del server che esegue chiamate di procedure remote. *rpcsrvname* viene **sysname**, il valore predefinito è **%**, che è l'unico valore che restituisce un set di risultati.  
  
 [ **@publisher_type**=] **'**_publisher_type_**' OUTPUT**  
 Tipo del server di pubblicazione. *publisher_type* viene **sysname**, il valore predefinito è **%**, che è l'unico valore che restituisce un set di risultati.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**server di distribuzione**|**sysname**|Nome del server di distribuzione.|  
|**database di distribuzione**|**sysname**|Nome del database di distribuzione.|  
|**Directory**|**nvarchar(255)**|Nome della directory di lavoro.|  
|**account**|**nvarchar(255)**|Nome dell'account utente di Windows.|  
|**conservazione di distrib min**|**int**|Periodo di memorizzazione minimo per la distribuzione.|  
|**distrib massima conservazione**|**int**|Periodo di memorizzazione massimo per la distribuzione.|  
|**periodo memorizzazione cronologia**|**int**|Periodo di memorizzazione per la cronologia.|  
|**agente di pulizia della cronologia**|**Nvarchar(100)**|Nome dell'agente di pulizia del contenuto della cronologia.|  
|**agente**|**Nvarchar(100)**|Nome dell'agente di pulizia dei riferimenti alla distribuzione.|  
|**nome del server RPC**|**sysname**|Nome del server di distribuzione remoto o locale.|  
|**nome account di accesso RPC**|**sysname**|Account di accesso utilizzato per le chiamate di procedure remote al server di distribuzione remoto.|  
|**tipo di server di pubblicazione**|**sysname**|Tipo di server di pubblicazione. Può essere uno dei tipi seguenti:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE GATEWAY**|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpdistributor** viene utilizzata in tutti i tipi di replica.  
  
 Se vengono specificati uno o più parametri di output durante l'esecuzione **sp_helpdistributor**, tutti i parametri di output, impostati su NULL vengono assegnati i valori in uscita e non viene restituito alcun set di risultati. Se non viene specificato alcun parametro di output, viene restituito un set di risultati.  
  
## <a name="permissions"></a>Permissions  
 Il seguenti set di risultati le colonne o parametri di output vengono restituiti ai membri del **sysadmin** ruolo predefinito del server nel server di pubblicazione e il **db_owner** ruolo predefinito del database nel database di pubblicazione:  
  
|Colonna del set di risultati|Parametro di output|  
|-----------------------|----------------------|  
|account|**@account**|  
|min distrib retention|**@min_distretention**|  
|max distrib retention|**@max_distretention**|  
|history retention|**@history_retention**|  
|history cleanup agent|**@history_cleanupagent**|  
|distribution cleanup agent|**@distrib_cleanupagent**|  
|rpc login name|none|  
  
 La colonna del set dei risultati seguente viene restituita agli utenti nell'elenco di accesso alla pubblicazione per una pubblicazione nel server di distribuzione:  
  
-   directory  
  
 Le seguenti colonne del set di risultati vengono restituite a tutti gli utenti.  
  
|Colonna del set di risultati|Parametro di output|  
|-----------------------|----------------------|  
|distributor|**@distributor**|  
|database di distribuzione|**@distribdb**|  
|rpc server name|**@rpcsrvname**|  
|publisher type|**@publisher_type**|  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
