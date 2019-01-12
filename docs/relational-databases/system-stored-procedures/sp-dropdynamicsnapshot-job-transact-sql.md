---
title: sp_dropdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e4612c7b20e448eecbd6c83a3d09d0796dcff542
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126261"
---
# <a name="spdropdynamicsnapshotjob-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove un processo di snapshot dei dati filtrati per una pubblicazione con filtri di riga con parametri. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione. Quando il processo viene eliminato, tutti i dati correlati viene eliminato dal [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) tabella di sistema.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=**] **'**_pubblicazione_**'**  
 Nome della pubblicazione da cui deve essere rimosso il processo di snapshot dei dati filtrati. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@dynamic_snapshot_jobname**=] **'**_dynamic_snapshot_jobname_**'**  
 Nome del processo di snapshot dei dati filtrati da rimuovere. *dynamic_snapshot_jobname*è di tipo sysname e se non è fornito le impostazioni predefinite a qualsiasi processo nome è associato *dynamic_snapshot_jobid*.  
  
 [ **@dynamic_snapshot_jobid**=] **'**_dynamic_snapshot_jobid_**'**  
 Identificatore per il processo di snapshot dei dati filtrati da rimuovere. *dynamic_snapshot_jobid*viene **uniqueidentifier**, con valore predefinito è NULL.  
  
> [!IMPORTANT]  
>  Solo *dynamic_snapshot_jobid*oppure *dynamic_snapshot_jobname* può essere specificato. Se non sono specificati valori per uno *dynamic_snapshot_jobid*oppure *dynamic_snapshot_jobname*, vengono rimossi tutti i processi di snapshot dinamico per la pubblicazione.  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 *ignore_distributor* viene **bit**, il valore predefinito è **0**. È possibile utilizzare questo parametro per rimuovere un processo di snapshot dinamico senza eseguire operazioni di pulizia dei riferimenti nel server di distribuzione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_dropdynamicsnapshot** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_dropdynamicsnapshot**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_adddynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
