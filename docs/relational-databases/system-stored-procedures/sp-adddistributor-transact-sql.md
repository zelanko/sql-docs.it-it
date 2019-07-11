---
title: sp_adddistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistributor
- sp_adddistributor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adddistributor
ms.assetid: 35415502-68d0-40f6-993c-180e50004f1e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8cf36a02d81b8732d80beb7c97d025a74138cd43
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716732"
---
# <a name="spadddistributor-transact-sql"></a>sp_adddistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una voce nella [sysservers](../../relational-databases/system-compatibility-views/sys-sysservers-transact-sql.md) tabella (se non esiste uno), contrassegna la voce del server come server di distribuzione e archivia le informazioni sulle proprietà. Questa stored procedure viene eseguita nel database master del server di distribuzione per registrare e contrassegnare il server come server di distribuzione. Nel caso di un server di distribuzione remoto la stored procedure viene eseguita nel database master del server di pubblicazione per registrare il server di distribuzione remoto.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_adddistributor [ @distributor= ] 'distributor'   
    [ , [ @heartbeat_interval= ] heartbeat_interval ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @from_scripting= ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @distributor = ] 'distributor'` È il nome del server di distribuzione. *server di distribuzione* viene **sysname**, non prevede alcun valore predefinito. Questo parametro viene utilizzato solo per la configurazione di un server di distribuzione remoto. Aggiunge voci per le proprietà del server di distribuzione nel **msdb... MSdistributor** tabella.  
  
`[ @heartbeat_interval = ] heartbeat_interval` È il numero massimo di minuti quale un agente può non registrare alcun messaggio di stato di avanzamento. *heartbeat_interval* viene **int**, con un valore predefinito è 10 minuti. Viene creato un processo di SQL Server Agent che viene eseguito in base a questo intervallo per controllare lo stato degli agenti di replica in esecuzione.  
  
`[ @password = ] 'password']` Password del **distributor_admin** account di accesso. *la password* viene **sysname**, con un valore predefinito è NULL. Se il valore è NULL o una stringa vuota, la password viene reimpostata su un valore casuale. La password deve essere configurata quando viene aggiunto il primo server di distribuzione remoto. **distributor_admin** account di accesso e *password* vengono archiviati per la voce di server collegato utilizzata per una *server di distribuzione* connessione RPC, incluse le connessioni locali. Se *distributore* è locale, la password per **distributor_admin** è impostata su un nuovo valore. Per i server di pubblicazione con un server di distribuzione remoto, lo stesso valore per *password* deve essere specificato quando si esegue **sp_adddistributor** sia il server di pubblicazione di distribuzione. [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) può essere utilizzato per modificare la password del server di distribuzione.  
  
> [!IMPORTANT]  
>  Se possibile, richiedere agli utenti di immettere le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è fondamentale proteggere il file per evitare accessi non autorizzati.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_adddistributor** viene utilizzata nella replica snapshot, la replica transazionale e di tipo merge.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistributor-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_adddistributor**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_dropdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurare la distribuzione](../../relational-databases/replication/configure-distribution.md)  
  
  
