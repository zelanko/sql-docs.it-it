---
title: sp_replicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac51409db23f4b8eefb3616d5daf5ca43b3ab0f6
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771246"
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Imposta un'opzione del database di replica per il database specificato. Questa stored procedure viene eseguita in qualsiasi database del server di pubblicazione o del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argomenti  
 **[@dbname=** ] **'***dbname***'**  
 Database per cui si desidera impostare l'opzione del database di replica. *db_name* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
 [ **@optname=** ] **'***optname***'**  
 Opzione del database di replica che si desidera abilitare o disabilitare. *optname* è di **tipo sysname**. i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**pubblicazione di tipo merge**|Specifica se il database può essere utilizzato per pubblicazioni di tipo merge.|  
|**publish**|Specifica se il database può essere utilizzato per altri tipi di pubblicazione.|  
|**sottoscrivere**|Specifica se si tratta di un database di sottoscrizione.|  
|**Sincronizza con backup**|Specifica se il database è abilitato per il backup coordinato. Per ulteriori informazioni, vedere [abilitare backup coordinati &#40;per la programmazione&#41;Transact-SQL della](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)replica transazionale.|  
  
`[ @value = ] 'value'`Indica se abilitare o disabilitare l'opzione del database di replica specificata. *value* è di **tipo sysname**e può essere **true** o **false**. Se questo valore è **false** e *optname* è **merge publish**, vengono eliminate anche le sottoscrizioni del database di pubblicazione di tipo merge.  
  
`[ @ignore_distributor = ] ignore_distributor`Indica se questo stored procedure viene eseguito senza connettersi al server di distribuzione. *ignore_distributor* è di **bit**e il valore predefinito è **0**, che indica che il server di distribuzione deve essere connesso e aggiornato con il nuovo stato del database di pubblicazione. È necessario specificare il valore **1** solo se il server di distribuzione non è accessibile e si utilizza **sp_replicationdboption** per disabilitare la pubblicazione.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_replicationdboption** viene utilizzata per la replica snapshot, la replica transazionale e la replica di tipo merge.  
  
 Questa procedura crea o elimina tabelle del sistema di replica specifiche, account di sicurezza specifici e così via a seconda delle opzioni impostate. Imposta il bit di categoria corrispondente nella tabella di sistema **master. sysdatabases** e crea le tabelle di sistema necessarie.  
  
 Per disabilitare la pubblicazione, è necessario che il database di pubblicazione sia online. Se esiste uno snapshot per il database di pubblicazione, deve essere eliminato prima della disabilitazione della pubblicazione. Uno snapshot del database è una copia offline e di sola lettura di un database e non è correlato a uno snapshot di replica. Per altre informazioni, vedere [Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del ruolo predefinito del server **sysadmin** possono eseguire **sp_replicationdboption**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Eliminare una pubblicazione](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Disabilitare la pubblicazione e la distribuzione](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.sysdatabases &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
