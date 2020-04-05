---
title: proprietà sys.dm_external_script_requests . Documenti Microsoft
ms.custom: ''
ms.date: 10/28/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_requests
- sys.dm_external_script_requests_TSQL
- dm_external_script_requests
- dm_external_script_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_requests dynamic management view
ms.assetid: e7e7c50f-b8b2-403c-b8c8-1955da5636c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 67e24b9c5c4ccd5f6ab2159ed5924474ff77bc84
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664283"
---
# <a name="sysdm_external_script_requests"></a>sys.dm_external_script_requests
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Restituisce una riga per ogni account di lavoro attivo che esegue uno script esterno.
  
> [!NOTE] 
>  
> Questa vista a gestione dinamica (DMV) è disponibile solo se è stata installata e abilitata la funzionalità che supporta l'esecuzione di script esterni. Per altre informazioni, vedere [R Services in SQL Server 2016](../../machine-learning/r/sql-server-r-services.md) e Machine Learning Services [(R, Python) in SQL Server 2017 e versioni successive.](../../machine-learning/what-is-sql-server-machine-learning.md)  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|external_script_request_id|**unique identifier**|ID del processo che ha inviato la richiesta di script esterni. Corrisponde all'ID del processo ricevuto da[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]|  
|Linguaggio|**nvarchar**|Parola chiave che rappresenta un linguaggio di scripting supportato. |  
|degree_of_parallelism|**Int**|Numero che indica il numero di processi paralleli che sono stati creati. Questo valore potrebbe essere diverso dal numero di processi paralleli che sono stati richiesti.|  
|external_user_name|**nvarchar**|Account di lavoro di Windows con cui è stato eseguito lo script.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE nel server.  
  
> [!NOTE]
>   
>  Gli utenti che eseguono script esterni devono avere l'autorizzazione aggiuntiva EXECUTE ANY EXTERNAL SCRIPT, tuttavia, questa DMV può essere usata dagli amministratori senza tale autorizzazione. 
  
## <a name="remarks"></a>Osservazioni  

Questa vista può essere filtrata usando l'identificatore del linguaggio di scripting.

La vista restituisce anche l'account di lavoro con cui viene eseguito lo script. Per informazioni sugli account di lavoro utilizzati dagli script esterni, vedere la sezione Identità utilizzate nell'elaborazione (SQLRUserGroup) in Panoramica della sicurezza per il framework di [estensibilità in Sql Server Machine Learning Services](../../machine-learning/concepts/security.md#sqlrusergroup).

Il GUID restituito nel campo **external_script_request_id** rappresenta anche il nome file della directory protetta in cui vengono archiviati i file temporanei. Ogni account di lavoro come MSSQLSERVER01 rappresenta un singolo account di accesso SQL o un utente di Windows e potrebbe essere usato per eseguire più richieste di script. Per impostazione predefinita, la pulizia di questi file temporanei viene eseguita dopo il completamento dello script richiesto.
 
Questa DMV monitora solo i processi attivi e non può segnalare gli script che sono già stati completati. Se è necessario tenere traccia della durata degli script, è consigliabile aggiungere le informazioni sulla misurazione del tempo nello script e acquisire tali informazioni come parte dell'esecuzione dello script.

## <a name="examples"></a>Esempi  
  
### <a name="viewing-the-currently-active-r-scripts-for-a-particular-process"></a>Visualizzazione degli script R attualmente attivi per un determinato processo 
 L'esempio seguente visualizza il numero di esecuzioni dello script esterno completate nell'istanza corrente.  
  
```  
SELECT external_script_request_id 
  , [language]
  , degree_of_parallelism
  , external_user_name
FROM sys.dm_external_script_requests; 
```  

Risultati  


external_script_request_id  |Linguaggio  |degree_of_parallelism  |external_user_name  
---------|---------|---------|---------
183EE6FC-7399-4318-AA2E-7A6C68E435A8     |     R    |      1   |  MSSQLSERVER01       


  
## <a name="see-also"></a>Vedere anche  
 [Viste a gestione dinamica e funzioni &#40;&#41;Transact-SQLDynamic Management Views and Functions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funzioni e viste a gestione dinamica relative all'esecuzione &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) dm_external_script_execution_stats di sistema  
  

