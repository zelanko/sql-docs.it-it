---
title: MSmerge_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_sessions
- MSmerge_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_sessions system table
ms.assetid: 09ada8fc-c148-4379-9524-7826b1b0216c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c87de2327918c383b57e4baef7f4948d43ddd85e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/05/2020
ms.locfileid: "82805242"
---
# <a name="msmerge_sessions-transact-sql"></a>MSmerge_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabella **MSmerge_sessions** contiene righe di cronologia con i risultati delle sessioni di processo agente di merge precedenti. Viene aggiunta una nuova riga alla tabella per ogni esecuzione dell'agente di merge. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID della sessione del processo dell'agente di merge.|  
|**agent_id**|**int**|ID dell'agente di merge.|  
|**start_time**|**datetime**|Ora di inizio dell'esecuzione del processo.|  
|**end_time**|**datetime**|Ora di fine dell'esecuzione del processo.|  
|**duration**|**int**|Durata cumulativa, espressa in secondi, di questa sessione del processo.|  
|**delivery_time**|**int**|Numero di secondi necessari per applicare un batch di modifiche.|  
|**upload_time**|**int**|Numero di secondi necessari per il caricamento delle modifiche nel server di pubblicazione.|  
|**download_time**|**int**|Numero di secondi necessari per il download delle modifiche nel Sottoscrittore.|  
|**delivery_rate**|**float**|Numero medio di comandi recapitati al secondo.|  
|**time_remaining**|**int**|Numero stimato di secondi rimanenti in una sessione attiva.|  
|**percent_complete**|**decimal**|Percentuale stimata rispetto al totale delle modifiche già recapitate in una sessione attiva.|  
|**upload_inserts**|**int**|Numero di inserimenti applicati nel server di pubblicazione.|  
|**upload_updates**|**int**|Numero di aggiornamenti applicati nel server di pubblicazione.|  
|**upload_deletes**|**int**|Numero di eliminazioni applicate nel server di pubblicazione.|  
|**upload_conflicts**|**int**|Numero di conflitti che si sono verificati durante l'applicazione delle modifiche nel server di pubblicazione.|  
|**upload_conflicts_resolved**|**int**|Numero di conflitti che si sono verificati durante l'applicazione delle modifiche nel server di pubblicazione e che sono stati risolti.|  
|**upload_rows_retried**|**int**|Numero di righe con tentativi ripetuti di caricamento nel server di pubblicazione.|  
|**download_inserts**|**int**|Numero di inserimenti applicati nel Sottoscrittore.|  
|**download_updates**|**int**|Numero di aggiornamenti applicati nel Sottoscrittore.|  
|**download_deletes**|**int**|Numero di eliminazioni applicate nel Sottoscrittore.|  
|**download_conflicts**|**int**|Numero di conflitti che si sono verificati durante l'applicazione delle modifiche nel Sottoscrittore.|  
|**download_conflicts_resolved**|**int**|Numero di conflitti che si sono verificati durante l'applicazione delle modifiche nel Sottoscrittore e che sono stati risolti.|  
|**download_rows_retried**|**int**|Numero di righe con tentativi ripetuti di download nel Sottoscrittore.|  
|**schema_changes**|**int**|Numero di modifiche dello schema applicate durante la sessione.|  
|**metadata_rows_cleanedup**|**int**|Numero di righe di metadati rimossi durante la sessione.|  
|**runstatus**|**int**|Stato di esecuzione:<br /><br /> **1** = avvia.<br /><br /> **2** = esito positivo.<br /><br /> **3** = in corso.<br /><br /> **4** = inattivo.<br /><br /> **5** = nuovo tentativo.<br /><br /> **6** = esito negativo.|  
|**estimated_upload_changes**|**int**|Numero stimato di modifiche che devono essere applicate nel server di pubblicazione.|  
|**estimated_download_changes**|**int**|Numero stimato di modifiche che devono essere applicate nel Sottoscrittore.|  
|**connection_type**|**int**|Connessione utilizzata durante il caricamento:<br /><br /> **1** = rete locale (LAN).<br /><br /> **2** = connessione di rete remota.<br /><br /> **3** = sincronizzazione Web.|  
|**timestamp**|**timestamp**|Colonna timestamp della tabella.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
