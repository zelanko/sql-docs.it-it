---
title: Sysmergesubscriptions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergesubscriptions_TSQL
- sysmergesubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubscriptions system table
ms.assetid: 6adc78da-991d-4c08-98c3-ecb4762e0e99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1cd32e7224b66c012d3422a3754cb0b4e0ca325b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029780"
---
# <a name="sysmergesubscriptions-transact-sql"></a>sysmergesubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Viene inclusa una riga per ogni Sottoscrittore noto ed è una tabella locale nel server di pubblicazione. Questa tabella è archiviata nei database di pubblicazione e di sottoscrizione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|subscriber_server|**sysname**|ID del server utilizzato per eseguire il mapping del campo srvid al valore specifico del server nella migrazione di una copia del database di sottoscrizione in un server diverso.|  
|db_name|**sysname**|Nome del database di sottoscrizione.|  
|pubid|**uniqueidentifier**|ID della pubblicazione da cui è stata creata la sottoscrizione corrente.|  
|datasource_type|**int**|Tipo di origine dati:<br /><br /> **0** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **2** = jet OLE DB.|  
|subid|**uniqueidentifier**|Numero di identificazione univoco per la sottoscrizione.|  
|replnickname|**binary**|Nome alternativo compresso per la replica.|  
|replicastate|**uniqueidentifier**|Identificatore univoco utilizzato per determinare se la sincronizzazione precedente ha avuto esito positivo confrontando il valore nel server di pubblicazione con il valore nel Sottoscrittore.|  
|status|**tinyint**|Stato della sottoscrizione:<br /><br /> **0** = inattiva.<br /><br /> **1** = attivo.<br /><br /> **2** = eliminato.|  
|subscriber_type|**int**|Tipo di Sottoscrittore:<br /><br /> **1** = globale.<br /><br /> **2** = locale.<br /><br /> **3** = anonimo.|  
|subscription_type|**int**|Tipo di sottoscrizione:<br /><br /> **0** = push.<br /><br /> **1** = pull.<br /><br /> **2** = anonimo.|  
|sync_type|**tinyint**|Tipo di sincronizzazione:<br /><br /> **1** = automatic.<br /><br /> **2** non = Nessuna sincronizzazione.|  
|description|**nvarchar(255)**|Breve descrizione della sottoscrizione.|  
|priorità|**real**|Viene specificata la priorità della sottoscrizione e viene consentita l'implementazione della risoluzione dei conflitti in base alla priorità È uguale a **0,00** per tutte le sottoscrizioni anonime o locali.|  
|recgen|**bigint**|Numero dell'ultima generazione ricevuta.|  
|recguid|**uniqueidentifier**|ID univoco dell'ultima generazione ricevuta.|  
|sentgen|**bigint**|Numero dell'ultima generazione inviata.|  
|sentguid|**uniqueidentifier**|ID univoco dell'ultima generazione inviata.|  
|schemaversion|**int**|Numero dell'ultimo schema ricevuto.|  
|schemaguid|**uniqueidentifier**|ID univoco dell'ultimo schema ricevuto.|  
|last_validated|**datetime**|Il **datetime** dell'ultima convalida dei dati del sottoscrittore.|  
|attempted_validate|**datetime**|L'ultima **datetime** tentativo di convalida della sottoscrizione.|  
|last_sync_date|**datetime**|Il **datetime** della sincronizzazione.|  
|last_sync_status|**int**|Stato della sottoscrizione:<br /><br /> **0** = tutti i processi sono in attesa dell'avvio.<br /><br /> **1** = uno o più processi di avvio.<br /><br /> **2** = tutti i processi sono stati eseguiti correttamente.<br /><br /> **3** = almeno un processo è in esecuzione.<br /><br /> **4** = tutti i processi sono pianificati e inattivi.<br /><br /> **5** = almeno un processo sta tentando l'esecuzione dopo un errore precedente.<br /><br /> **6** = almeno un processo non è stato eseguito correttamente.|  
|last_sync_summary|**sysname**|Descrizione dei risultati dell'ultima sincronizzazione.|  
|metadatacleanuptime|**datetime**|L'ultima **datetime** dei metadati scaduti è stata rimossa dalle tabelle di sistema di replica di tipo merge.|  
|partition_id|**int**|Viene identificata la partizione precalcolata alla quale appartiene la sottoscrizione.|  
|cleanedup_unsent_changes|**bit**|Viene indicato che i metadati relativi alle modifiche non inviate sono stati rimossi nel Sottoscrittore.|  
|replica_version|**int**|Identifica la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il Sottoscrittore al quale appartiene la sottoscrizione. I possibili valori sono i seguenti:<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|supportability_mode|**int**|Solo per uso interno.|  
|application_name|**nvarchar(128)**|Solo per uso interno.|  
|subscriber_number|**int**|Solo per uso interno.|  
|last_makegeneration_datetime|**datetime**|L'ultima **datetime** che è stato eseguito per il server di pubblicazione. Per altre informazioni, vedere il parametro - MakeGenerationInterval [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
