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
manager: craigg
ms.openlocfilehash: 153c2e2b8c75c21451dca3b673129a059d78e3a6
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527333"
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [**@dbname=**] **'***dbname***'**  
 Database per cui si desidera impostare l'opzione del database di replica. *db_name* viene **sysname**, non prevede alcun valore predefinito.  
  
 [**@optname=**] **'***optname***'**  
 Opzione del database di replica che si desidera abilitare o disabilitare. *optname* viene **sysname**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**pubblicazione di tipo merge**|Specifica se il database può essere utilizzato per pubblicazioni di tipo merge.|  
|**publish**|Specifica se il database può essere utilizzato per altri tipi di pubblicazione.|  
|**subscribe**|Specifica se si tratta di un database di sottoscrizione.|  
|**la sincronizzazione con backup**|Specifica se il database è abilitato per il backup coordinato. Per altre informazioni, vedere [attivare backup coordinati per la replica transazionale &#40;programmazione Transact-SQL della replica&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).|  
  
`[ @value = ] 'value'` Indica se abilitare o disabilitare l'opzione di database di replica specificato. *valore* viene **sysname**e può essere **true** oppure **false**. Quando questo valore è **false** e *optname* viene **pubblicazione di tipo merge**, vengono eliminate anche le sottoscrizioni per il database pubblicato di tipo merge.  
  
`[ @ignore_distributor = ] ignore_distributor` Indica se questa stored procedure viene eseguita senza stabilire la connessione al server di distribuzione. *ignore_distributor* viene **bit**, il valore predefinito è **0**, vale a dire il server di distribuzione deve essere connesso a e aggiornare il nuovo stato del database di pubblicazione. Il valore **1** deve essere specificato solo se il server di distribuzione non è accessibile e **sp_replicationdboption** viene utilizzata per disattivare la pubblicazione.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_replicationdboption** viene utilizzata nella replica snapshot, la replica transazionale e di tipo merge.  
  
 Questa procedura crea o elimina tabelle del sistema di replica specifiche, account di sicurezza specifici e così via a seconda delle opzioni impostate. Imposta la categoria corrispondente bit nel **sysdatabases** tabella di sistema e crea le tabelle di sistema necessarie.  
  
 Per disabilitare la pubblicazione, è necessario che il database di pubblicazione sia online. Se esiste uno snapshot per il database di pubblicazione, deve essere eliminato prima della disabilitazione della pubblicazione. Uno snapshot del database è una copia offline e di sola lettura di un database e non è correlato a uno snapshot di replica. Per altre informazioni, vedere [Snapshot del database &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_replicationdboption**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare la pubblicazione e la distribuzione](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Eliminazione di una pubblicazione](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Disabilitare la pubblicazione e la distribuzione](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.sysdatabases &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [Stored procedure per la replica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
