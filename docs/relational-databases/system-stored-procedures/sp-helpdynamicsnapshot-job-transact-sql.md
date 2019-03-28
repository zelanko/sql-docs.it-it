---
title: sp_helpdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdynamicsnapshot_TSQL
- sp_helpdynamicsnapshot_job_TSQL
- job_TSQL
- helpdynamicsnapshot
- job
- sp_helpdynamicsnapshot
- sp_helpdynamicsnapshot_job
- helpdynamicsnapshot_TSQL
helpviewer_keywords:
- sp_helpdynamicsnapshot_job
ms.assetid: d6dfdf26-f874-495f-a8a6-8780699646d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cede3c4419f4e11d2110e7c3f735c3dec2474ec4
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531483"
---
# <a name="sphelpdynamicsnapshotjob-transact-sql"></a>sp_helpdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sui processi di agente che generano snapshot dei dati filtrati. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helpdynamicsnapshot_job [ [ @publication = ] 'publication' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]  
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, il valore predefinito è **%**, che restituisce informazioni su tutti i processi di snapshot dei dati filtrati che corrispondono alla stringa *dynamic_ snapshot_jobid*e *dynamic_snapshot_jobname*per tutte le pubblicazioni.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'` È il nome di un processo di snapshot dei dati filtrati. *dynamic_snapshot_jobname*viene **sysname**, con valore predefinito è **%**', che restituisce tutti i processi dinamici per una pubblicazione con l'oggetto specificato *dynamic_ snapshot_jobid*. Se quando è stato creato il processo non è stato specificato in modo esplicito un nome di processo, il nome del processo verrà indicato nel formato seguente:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'` È un identificatore per un processo di snapshot dei dati filtrati. *dynamic_snapshot_jobid*viene **uniqueidentifier**, con valore predefinito è NULL, che restituisce tutti i processi di snapshot che corrispondono alla stringa *dynamic_snapshot_jobname*.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica il processo di snapshot dei dati filtrati.|  
|**job_name**|**sysname**|Nome del processo di snapshot dei dati filtrati.|  
|**job_id**|**uniqueidentifier**|Identifica la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo dell'agente nel server di distribuzione.|  
|**dynamic_filter_login**|**sysname**|Valore utilizzato per valutare il [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) funzione in un filtro di riga con parametri definito per la pubblicazione.|  
|**dynamic_filter_hostname**|**sysname**|Valore utilizzato per valutare il [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) funzione in un filtro di riga con parametri definito per la pubblicazione.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Percorso della cartella da cui i file di snapshot vengono letti se viene utilizzato un filtro di riga con parametri.|  
|**frequency_type**|**int**|Frequenza pianificata per l'esecuzione dell'agente. I possibile valori sono i seguenti.<br /><br /> **1** = una sola volta<br /><br /> **2** = su richiesta<br /><br /> **4** = giornaliera<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativa<br /><br /> **64** = avvio automatico<br /><br /> **128** = Recurring|  
|**frequency_interval**|**int**|Giorni in cui l'agente viene eseguito. I possibili valori sono i seguenti.<br /><br /> **1** = Sunday<br /><br /> **2** = lunedì<br /><br /> **3** = martedì<br /><br /> **4** = mercoledì<br /><br /> **5** = giovedì<br /><br /> **6** = Friday<br /><br /> **7** = sabato<br /><br /> **8** = giorno<br /><br /> **9** = giorni feriali<br /><br /> **10** = giorni festivi|  
|**frequency_subday_type**|**int**|È il tipo che definisce la frequenza con cui l'agente viene eseguito quando *frequency_type* viene **4** (giornaliera), i possibili valori sono i seguenti.<br /><br /> **1** = all'ora specificata<br /><br /> **2** = secondi<br /><br /> **4** = minuti<br /><br /> **8** = ore|  
|**frequency_subday_interval**|**int**|Numero di intervalli di *frequency_subday_type* tra le esecuzioni pianificate dell'agente.|  
|**frequency_relative_interval**|**int**|Settimana in cui viene eseguito l'agente in un determinato mese quando *frequency_type* viene **32** (mensile relativo), i possibili valori sono i seguenti.<br /><br /> **1** = prima<br /><br /> **2** = Second<br /><br /> **4** = terza<br /><br /> **8** = quarta<br /><br /> **16** = ultima|  
|**frequency_recurrence_factor**|**int**|Numero di settimane o mesi tra le esecuzioni pianificate dell'agente.|  
|**active_start_date**|**int**|Data della prima esecuzione pianificata dell'agente nel formato YYYYMMDD.|  
|**active_end_date**|**int**|Data dell'ultima esecuzione pianificata dell'agente nel formato YYYYMMDD.|  
|**active_start_time**|**int**|Ora della prima esecuzione pianificata dell'agente nel formato HHMMSS.|  
|**active_end_time**|**int**|Ora dell'ultima esecuzione pianificata dell'agente nel formato HHMMSS.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_helpdynamicsnapshot_job** viene utilizzata nella replica di tipo merge.  
  
 Se vengono utilizzati tutti i valori predefiniti dei parametri, verranno restituite informazioni su tutti i processi di snapshot dei dati partizionati per l'intero database di pubblicazione.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server, il **db_owner** corrette del database e l'elenco di accesso per la pubblicazione possono eseguire **sp_helpdynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
