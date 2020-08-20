---
description: MSsnapshot_history (Transact-SQL)
title: MSsnapshot_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsnapshot_history
- MSsnapshot_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_history system table
ms.assetid: 56bf4128-1689-4963-9343-432dd0898d31
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7dcc8a6e5a35ca9062bf97dd4dece2afca078fb2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460327"
---
# <a name="mssnapshot_history-transact-sql"></a>MSsnapshot_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabella **MSsnapshot_history** contiene righe di cronologia per gli agenti snapshot associati al server di distribuzione locale. Questa tabella è archiviata nel database di distribuzione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ID dell'agente snapshot.|  
|**runstatus**|**int**|Stato di esecuzione:<br /><br /> **1** = avvia.<br /><br /> **2** = esito positivo.<br /><br /> **3** = in corso.<br /><br /> **4** = inattivo.<br /><br /> **5** = nuovo tentativo.<br /><br /> **6** = esito negativo.|  
|**start_time**|**datetime**|Ora di inizio dell'esecuzione del processo.|  
|**time**|**datetime**|Ora di registrazione del messaggio.|  
|**duration**|**int**|Durata espressa in secondi della sessione del messaggio.|  
|**Commenti**|**nvarchar(255)**|Testo del messaggio.|  
|**delivered_transactions**|**int**|Numero totale di transazioni recapitate durante la sessione.|  
|**delivered_commands**|**int**|Numero di comandi recapitati al secondo.|  
|**delivery_rate**|**float(53)**|Numero medio dei comandi recapitati al secondo.|  
|**error_id**|**int**|ID dell'errore nella tabella di sistema [MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md) .|  
|**timestamp**|**timestamp**|Colonna timestamp della tabella.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
