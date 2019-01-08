---
title: sp_adddynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddynamicsnapshot_job
- sp_adddynamicsnapshot_job_TSQL
helpviewer_keywords:
- sp_adddynamicsnapshot_job
ms.assetid: ef50ccf6-e360-4e4b-91b9-6706b8fabefa
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 79412d81e0a16443f3fec515d1d866c3aff1804c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771223"
---
# <a name="spadddynamicsnapshotjob-transact-sql"></a>sp_adddynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un processo di agente che genera uno snapshot dei dati filtrati per una pubblicazione con filtri di riga con parametri. Questa stored procedure viene eseguita nel database di pubblicazione del server di pubblicazione. Questa stored procedure viene utilizzata da un amministratore per creare in modo manuale processi di snapshot dei dati filtrati per Sottoscrittori.  
  
> [!NOTE]  
>  Affinché venga creato un processo di snapshot dei dati filtrati, è necessario che esista già un processo di snapshot standard per la pubblicazione.  
  
 Per altre informazioni, vedere [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_adddynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]   
    [ , [ @host_name = ] 'host_name' ]   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' OUTPUT ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' OUTPUT ]   
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione a cui si desidera aggiungere il processo di snapshot dei dati filtrati. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@suser_sname**=] **'***suser_sname***'**  
 È il valore utilizzato per la creazione di uno snapshot dei dati filtrati per una sottoscrizione filtrata in base al valore della [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) funzione nel Sottoscrittore. *SUSER_SNAME* viene **sysname**, non prevede alcun valore predefinito. *SUSER_SNAME* deve essere NULL se questa funzione non viene utilizzata per filtrare in modo dinamico la pubblicazione.  
  
 [ **@host_name**=] **'***host_name***'**  
 È il valore utilizzato per la creazione di uno snapshot dei dati filtrati per una sottoscrizione filtrata in base al valore della [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) funzione nel Sottoscrittore. *HOST_NAME* viene **sysname**, non prevede alcun valore predefinito. *HOST_NAME* deve essere NULL se questa funzione non viene utilizzata per filtrare in modo dinamico la pubblicazione.  
  
 [ **@dynamic_snapshot_jobname**=] **'***dynamic_snapshot_jobname***'**  
 Nome del processo di snapshot dei dati filtrati creato. *dynamic_snapshot_jobname* viene **sysname**, con valore predefinito è NULL ed è un parametro OUTPUT facoltativo. Se specificato, *dynamic_snapshot_jobname* deve essere risolto in un processo univoco nel server di distribuzione. Se non viene specificato, verrà generato automaticamente e restituito nel set di risultati un nome di processo con il formato seguente:  
  
```  
'dyn_' + <name of the standard snapshot job> + <GUID>  
```  
  
> [!NOTE]  
>  Quando viene generato il nome del processo di snapshot dinamico, è possibile troncare il nome del processo di snapshot standard.  
  
 [ **@dynamic_snapshot_jobid**=] **'***dynamic_snapshot_jobid***'**  
 Identificatore del processo di snapshot dei dati filtrati creato. *dynamic_snapshot_jobid* viene **uniqueidentifier**, con valore predefinito è NULL ed è un parametro OUTPUT facoltativo.  
  
 [  **@frequency_type=**] *frequency_type*  
 Frequenza per l'esecuzione pianificata del processo di snapshot dei dati filtrati. *frequency_type* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Su richiesta|  
|**4** (impostazione predefinita)|Ogni giorno|  
|**8**|Settimanale|  
|**16**|Mensile|  
|**32**|Mensile relativa|  
|**64**|Avvio automatico|  
|**128**|Periodica|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 Periodo, espresso in giorni, durante il quale viene eseguito il processo di snapshot dei dati filtrati. *frequency_interval* viene **int**, con un valore predefinito pari a 1 e dipende dal valore di *frequency_type*.  
  
|Valore di *frequency_type*|Effetto su *frequency_interval*|  
|--------------------------------|-------------------------------------|  
|**1**|*frequency_interval* risulta inutilizzato.|  
|**4** (impostazione predefinita)|Ogni *frequency_interval* giorni, con un valore predefinito di ogni giorno.|  
|**8**|*frequency_interval* corrisponde a uno o più dei valori seguenti (combinato con un [ &#124; &#40;OR bit per&#41; &#40;Transact-SQL&#41; ](../../t-sql/language-elements/bitwise-or-transact-sql.md) operatore logico):<br /><br /> **1** = domenica &#124; **2** = lunedì &#124; **4** = martedì &#124; **8** = mercoledì &#124; **16** = Giovedì &#124; **32** = venerdì &#124; **64** = sabato|  
|**16**|Nel *frequency_interval* giorno del mese.|  
|**32**|*frequency_interval* è uno dei seguenti:<br /><br /> **1** = domenica &#124; **2** = lunedì &#124; **3** = martedì &#124; **4** = mercoledì &#124; **5** = Giovedì &#124; **6** = venerdì &#124; **7** = sabato &#124; **8** = giorno &#124; **9** = giorno feriale &#124; **10** = giorno festivo|  
|**64**|*frequency_interval* risulta inutilizzato.|  
|**128**|*frequency_interval* risulta inutilizzato.|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Specifica l'unità di misura *frequency_subday_interval*. *frequency_subday* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1**|Una volta|  
|**2**|Secondo|  
|**4** (impostazione predefinita)|Minuto|  
|**8**|Ora|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 È il numero di *frequency_subday* periodi che si verificano tra ogni esecuzione del processo. *frequency_subday_interval* viene **int**, con un valore predefinito è 5.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Occorrenza del processo di snapshot dei dati filtrati in ogni mese. Questo parametro viene utilizzato quando *frequency_type* è impostata su **32** (frequenza mensile relativa). *frequency_relative_interval* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1** (impostazione predefinita)|Primo|  
|**2**|Secondo|  
|**4**|Terzo|  
|**8**|Quarto|  
|**16**|Ultimo|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Fattore di occorrenza utilizzato da *frequency_type*. *frequency_recurrence_factor* viene **int**, con un valore predefinito è 0.  
  
 [  **@active_start_date=**] *active_start_date*  
 Data della prima esecuzione pianificata del processo di snapshot dei dati filtrati, nel formato YYYYMMDD. *active_start_date* viene **int**, con un valore predefinito è NULL.  
  
 [  **@active_end_date=**] *active_end_date*  
 Data dell'ultima esecuzione pianificata del processo di snapshot dei dati filtrati, nel formato YYYYMMDD. *active_end_date* viene **int**, con un valore predefinito è NULL.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Ora del giorno della prima esecuzione pianificata del processo di snapshot dei dati filtrati, nel formato HHMMSS. *active_start_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Ora del giorno dell'ultima esecuzione pianificata del processo di snapshot dei dati filtrati, nel formato HHMMSS. *active_end_time_of_day* viene **int**, con un valore predefinito è NULL.  
  
## <a name="result-set"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifica il processo di snapshot dei dati filtrati nella [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) tabella di sistema.|  
|**dynamic_snapshot_jobname**|**sysname**|Nome del processo di snapshot dei dati filtrati.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifica in modo univoco il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processo dell'agente nel server di distribuzione.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 0 (esito positivo) o 1 (esito negativo)  
  
## <a name="remarks"></a>Note  
 **sp_adddynamicsnapshot_job** viene utilizzata nella replica di tipo merge per le pubblicazioni che utilizzano un filtro con parametri.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-adddynamicsnapshot-jo_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server o il **db_owner** ruolo predefinito del database possono eseguire **sp_adddynamicsnapshot_job**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare uno Snapshot per una pubblicazione di tipo Merge con filtri con parametri](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [sp_dropdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdynamicsnapshot-job-transact-sql.md)   
 [sp_helpdynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)  
  
  
