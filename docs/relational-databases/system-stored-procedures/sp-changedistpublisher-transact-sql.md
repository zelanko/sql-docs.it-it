---
title: sp_changedistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 06a0e5e2edb793a94e8d8542ca17734f23824121
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62997826"
---
# <a name="spchangedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica le proprietà del server di pubblicazione della distribuzione. Questa stored procedure viene eseguita in qualsiasi database del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @storage_connection_string = ] 'storage_connection_string']
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome dell'editore. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @property = ] 'property'` È una proprietà da modificare per il server di pubblicazione specificato. *proprietà* viene **sysname** i possibili valori sono i seguenti.  
  
`[ @value = ] 'value'` È il valore per la proprietà specificata. *valore* viene **nvarchar(255**, con un valore predefinito è NULL.  
  
`[ @storage_connection_string = ] 'storage_connection_string'` È necessaria per l'istanza gestita di Database SQL, deve corrispondere alla chiave di accesso per il volume di archiviazione di Database SQL di Azure. 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 Nella tabella seguente vengono descritte le proprietà valide dei server di pubblicazione e i valori corrispondenti.  
  
|Proprietà|Valori|Descrizione|  
|--------------|------------|-----------------|  
|**active**|**true**|Attiva il server di pubblicazione.|  
||**false**|Disattiva il server di pubblicazione.|  
|**distribution_db**||Nome del database di distribuzione.|  
|**login**||Nome dell'account di accesso.|  
|**password**||Password complessa per l'account di accesso fornito.|  
|**security_mode**|**1**|Esegue la connessione al server di pubblicazione utilizzando l'autenticazione di Windows. *Non può essere modificato per non -* [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *server di pubblicazione.*|  
||**0**|Esegue la connessione al server di pubblicazione utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Non può essere modificato per non -* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *server di pubblicazione.*|  
|**working_directory**||Directory di lavoro utilizzata per archiviare i file dei dati e di schema per la pubblicazione.|  
|NULL (predefinito)||Tutti disponibili *proprietà* opzioni vengono stampate.| 
|**storage_connection_string**| Chiave di accesso | La chiave di accesso per la directory di lavoro quando il database è l'istanza gestita di Azure SQL Database. 
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_changedistpublisher** viene utilizzata in tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_changedistpublisher**.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
