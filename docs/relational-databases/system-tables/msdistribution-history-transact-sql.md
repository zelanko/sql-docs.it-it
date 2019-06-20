---
title: MSdistribution_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistribution_history
- MSdistribution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_history system table
ms.assetid: 55665bd2-9e1d-4efc-8f60-c63a24f66b28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 305223fca45bb1916598f02c16cc4e38981e861d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62903696"
---
# <a name="msdistributionhistory-transact-sql"></a>MSdistribution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSdistribution_history** tabella contiene righe di cronologia per gli agenti di distribuzione associati al server di distribuzione locale. Questa tabella è archiviata nel database di distribuzione.  
  
## <a name="definition"></a>Definizione  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ID dell'agente di distribuzione.|  
|**runstatus**|**int**|Stato di esecuzione:<br /><br /> **1** = Start.<br /><br /> **2** = Succeed.<br /><br /> **3** = in corso.<br /><br /> **4** = inattivo.<br /><br /> **5** = nuovo tentativo.<br /><br /> **6** = esito negativo.|  
|**start_time**|**datetime**|Ora di inizio dell'esecuzione del processo.|  
|**time**|**datetime**|Ora di registrazione del messaggio.|  
|**duration**|**int**|Durata espressa in secondi della sessione del messaggio.|  
|**comments**|**nvarchar(4000)**|Testo del messaggio.|  
|**xact_seqno**|**varbinary(16)**|Numero di sequenza dell'ultima transazione elaborata.|  
|**current_delivery_rate**|**float**|Numero medio di comandi recapitati al secondo dopo l'ultima voce di cronologia.|  
|**current_delivery_latency**|**int**|Latenza tra l'immissione del comando nel database di distribuzione e l'applicazione del comando al Sottoscrittore dopo l'ultima voce di sottoscrizione. In millisecondi.|  
|**delivered_transactions**|**int**|Numero totale di transazioni recapitate durante la sessione.|  
|**delivered_commands**|**int**|Numero totale di comandi recapitati durante la sessione.|  
|**average_commands**|**int**|Numero medio di comandi recapitati durante la sessione.|  
|**delivery_rate**|**float**|Numero medio dei comandi recapitati al secondo.|  
|**delivery_latency**|**int**|Latenza tra l'immissione del comando nel database di distribuzione e la sua applicazione al Sottoscrittore. In millisecondi.|  
|**total_delivered_commands**|**bigint**|Numero totale di comandi recapitati dalla creazione dell'ultima sottoscrizione.|  
|**error_id**|**int**|L'ID dell'errore nella **MSrepl_error** tabella di sistema.|  
|**updateable_row**|**bit**|Impostare su **1** se la riga di cronologia può essere sovrascritto.|  
|**timestamp**|**timestamp**|Colonna timestamp della tabella.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
