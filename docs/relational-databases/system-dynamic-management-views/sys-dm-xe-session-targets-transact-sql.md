---
title: sys. dm_xe_session_targets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_session_targets
- dm_xe_session_targets_TSQL
- dm_xe_session_targets
- sys.dm_xe_session_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_session_targets dynamic management view
- extended events [SQL Server], views
ms.assetid: 76fbc3e1-ad88-4a47-8bf1-471c3bee5ad8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1a13b9642caa236e930dbf7861a0c6604760189d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898522"
---
# <a name="sysdm_xe_session_targets-transact-sql"></a>sys.dm_xe_session_targets (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Restituisce informazioni sulle destinazioni della sessione.  
  
  |Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|Indirizzo di memoria della sessione dell'evento. Ha una relazione molti-a-uno con sys.dm_xe_sessions.address. Non ammette i valori Null.|  
|target_name|**nvarchar(60)**|Nome della destinazione in una sessione. Non ammette i valori Null.|  
|target_package_guid|**uniqueidentifier**|GUID del pacchetto che contiene la destinazione. Non ammette i valori Null.|  
|execution_count|**bigint**|Numero di volte in cui la destinazione è stata eseguita per la sessione. Non ammette i valori Null.|  
|execution_duration_ms|**bigint**|Tempo totale di esecuzione della destinazione, espresso in millisecondi. Non ammette i valori Null.|  
|target_data|**nvarchar(max)**|Dati che la destinazione gestisce, ad esempio informazioni di aggregazione di evento. Ammette i valori Null.|  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione VIEW SERVER STATE per il server.  
  
### <a name="relationship-cardinalities"></a>Cardinalità delle relazioni  
  
|From|A|Relazione|  
|----------|--------|------------------|  
|sys.dm_xe_session_targets.event_session_address|sys.dm_xe_sessions.address|Molti-a-uno|  
  
## <a name="change-history"></a>Cronologia modifiche  
  
|Contenuto aggiornato|  
|---------------------|  
|Correzione relativa al tipo di dati della colonna target_data.|  
|Correzione della descrizione della colonna target_data per indicare che sono ammessi valori Null.|  
|Correzione della tabella "Cardinalità delle relazioni".|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni e viste a gestione dinamica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

