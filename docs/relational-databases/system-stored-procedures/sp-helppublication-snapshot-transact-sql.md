---
title: sp_helppublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_snapshot
- sp_helppublication_snapshot_TSQL
helpviewer_keywords:
- sp_helppublication_snapshot
ms.assetid: 97b4a7ae-40a5-4328-88f1-ff5d105bbb34
author: stevestein
ms.author: sstein
ms.openlocfilehash: fa2697548212e3d5c27604533e69bbc07f480864
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137604"
---
# <a name="sphelppublicationsnapshot-transact-sql"></a>sp_helppublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sull'agente snapshot per una pubblicazione specifica. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_helppublication_snapshot [ @publication = ] 'publication'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publisher = ] 'publisher'` Specifica un non - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL.  
  
> [!NOTE]  
>  *server di pubblicazione* non deve essere utilizzata quando si aggiunge un articolo a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server di pubblicazione.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID dell'agente snapshot.|  
|**name**|**nvarchar(100)**|Nome dell'agente snapshot.|  
|**publisher_security_mode**|**smallint**|Modalità di sicurezza utilizzata dall'agente durante la connessione al server di pubblicazione. Le possibili modalità sono le seguenti:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticazione<br /><br /> **1** = autenticazione di Windows.|  
|**publisher_login**|**sysname**|Account di accesso utilizzato per la connessione al server di pubblicazione.|  
|**publisher_password**|**nvarchar(524)**|Per motivi di sicurezza, un valore pari **\* \* \* \* \* \* \* \* \* \*** è sempre restituito.|  
|**job_id**|**uniqueidentifier**|ID univoco del processo dell'agente.|  
|**job_login**|**nvarchar(512)**|L'account di Windows con cui viene eseguito l'agente Snapshot, viene restituito nel formato *DOMAIN*\\*username*.|  
|**job_password**|**sysname**|Per motivi di sicurezza, un valore pari **\* \* \* \* \* \* \* \* \* \*** è sempre restituito.|  
|**schedule_name**|**sysname**|Nome della pianificazione utilizzata per il processo dell'agente corrente.|  
|**frequency_type**|**int**|Frequenza pianificata per l'esecuzione dell'agente. I possibile valori sono i seguenti.<br /><br /> **1** = una sola volta<br /><br /> **2** = su richiesta<br /><br /> **4** = giornaliera<br /><br /> **8** = settimanale<br /><br /> **16** = mensile<br /><br /> **32** = mensile relativa<br /><br /> **64** = avvio automatico<br /><br /> **128** = periodica|  
|**frequency_interval**|**int**|Giorni in cui l'agente viene eseguito. I possibili valori sono i seguenti.<br /><br /> **1** = domenica<br /><br /> **2** = lunedì<br /><br /> **3** = martedì<br /><br /> **4** = mercoledì<br /><br /> **5** = giovedì<br /><br /> **6** = venerdì<br /><br /> **7** = sabato<br /><br /> **8** = giorno<br /><br /> **9** = giorni feriali<br /><br /> **10** = giorni festivi|  
|**frequency_subday_type**|**int**|È il tipo che definisce la frequenza con cui l'agente viene eseguito quando *frequency_type* viene **4** (giornaliera), i possibili valori sono i seguenti.<br /><br /> **1** = all'ora specificata<br /><br /> **2** = secondi<br /><br /> **4** = minuti<br /><br /> **8** = ore|  
|**frequency_subday_interval**|**int**|Numero di intervalli di *frequency_subday_type* tra le esecuzioni pianificate dell'agente.|  
|**frequency_relative_interval**|**int**|Settimana in cui viene eseguito l'agente in un determinato mese quando *frequency_type* viene **32** (mensile relativo), i possibili valori sono i seguenti.<br /><br /> **1** = prima<br /><br /> **2** = secondi<br /><br /> **4** = terza<br /><br /> **8** = quarta<br /><br /> **16** = ultima|  
|**frequency_recurrence_factor**|**int**|Numero di settimane o mesi tra le esecuzioni pianificate dell'agente.|  
|**active_start_date**|**int**|Data della prima esecuzione pianificata dell'agente nel formato YYYYMMDD.|  
|**active_end_date**|**int**|Data dell'ultima esecuzione pianificata dell'agente nel formato YYYYMMDD.|  
|**active_start_time**|**int**|Ora della prima esecuzione pianificata dell'agente nel formato HHMMSS.|  
|**active_end_time**|**int**|Ora dell'ultima esecuzione pianificata dell'agente nel formato HHMMSS.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **ssp_help_publication_snapshot** viene utilizzata in tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** nel server di pubblicazione o i membri del ruolo predefinito del server di **db_owner** ruolo predefinito del database nel database di pubblicazione possono eseguire **ssp_help_publication_snapshot** .  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)  
  
  
