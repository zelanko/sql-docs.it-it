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
ms.openlocfilehash: 5994201f7e6b2b859ef85a7a24e0c0465f59ec31
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68056491"
---
# <a name="sp_dropdynamicsnapshot_job-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove un processo di snapshot dei dati filtrati per una pubblicazione con filtri di riga con parametri. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione. Quando il processo viene eliminato, tutti i dati correlati vengono eliminati dalla tabella di sistema [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) .  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'`Nome della pubblicazione da cui viene rimosso il processo di snapshot dei dati filtrati. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`Nome del processo di snapshot dei dati filtrati da rimuovere. *dynamic_snapshot_jobname*è di tipo sysname. se non viene specificato, il nome del processo è associato a *dynamic_snapshot_jobid*.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`Identificatore del processo di snapshot dei dati filtrati da rimuovere. *dynamic_snapshot_jobid*è di tipo **uniqueidentifier**e il valore predefinito è null.  
  
> [!IMPORTANT]  
>  È possibile specificare solo *dynamic_snapshot_jobid*o *dynamic_snapshot_jobname* . Se non vengono specificati valori per *dynamic_snapshot_jobid*o *dynamic_snapshot_jobname*, vengono rimossi tutti i processi di snapshot dinamici per la pubblicazione.  
  
`[ @ignore_distributor = ] ignore_distributor`*ignore_distributor* è di **bit**e il valore predefinito è **0**. È possibile utilizzare questo parametro per rimuovere un processo di snapshot dinamico senza eseguire operazioni di pulizia dei riferimenti nel server di distribuzione.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_dropdynamicsnapshot** viene utilizzata nella replica di tipo merge.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** o del ruolo predefinito del database **db_owner** possono eseguire **sp_dropdynamicsnapshot**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_adddynamicsnapshot_job &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
