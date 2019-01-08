---
title: MSreplmonthresholdmetrics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2ce0bca2913dc6b0fbc9c8deaa4e4dd28f32f747
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796354"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Il **MSreplmonthresholdmetrics** tabella definisce la metrica fornita per il monitoraggio della replica. Questa tabella è archiviata nel **msdb** database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|Identifica una misurazione delle prestazioni di replica. Ecco i possibili valori:<br /><br /> **1** = expiration<br /><br /> **2** = latency<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|Nome della misurazione delle prestazioni di replica.|  
|**warningbitstatus**|**int**|Identificatore bit per bit utilizzato per generare un avviso per la violazione del valore soglia di una delle misurazioni seguenti:<br /><br /> **1** = expiration - una sottoscrizione di una pubblicazione transazionale ha superato il periodo di memorizzazione rispetto al valore soglia consentito, come percentuale del periodo di conservazione.<br /><br /> **2** = latency - il tempo necessario per replicare i dati da un server di pubblicazione transazionale al sottoscrittore supera la soglia, espresso in secondi.<br /><br /> **4** = mergeexpiration - una sottoscrizione a una pubblicazione di tipo merge ha superato il periodo di memorizzazione rispetto al valore soglia consentito, come percentuale del periodo di conservazione.<br /><br /> **8** = mergefastrunduration - il tempo impiegato per completare la sincronizzazione di una sottoscrizione di tipo merge supera la soglia, espresso in secondi, tramite una connessione di rete veloce.<br /><br /> **16** = mergeslowrunduration - il tempo impiegato per completare la sincronizzazione di una sottoscrizione di tipo merge supera la soglia, espresso in secondi, tramite una connessione di rete lenta o remota.<br /><br /> **32** = mergefastrunspeed: la velocità di recapito delle righe durante la sincronizzazione di una sottoscrizione di tipo merge è minore della soglia, in righe al secondo, su una connessione di rete veloce.<br /><br /> **64** = mergeslowrunspeed: la velocità di recapito delle righe durante la sincronizzazione di una sottoscrizione di tipo merge è minore della soglia, in righe al secondo, su una connessione di rete lenta o remota.|  
|**alertmessageid**|**int**|ID del messaggio di errore visualizzato quando si verifica la condizione per la generazione di un avviso per la violazione del valore soglia.|  
|**description**|**nvarchar(3000)**|Descrizione della misurazione delle prestazioni di replica.|  
|**default_value**|**sql_variant**|Valore predefinito della misurazione delle prestazioni di replica.|  
|**MIN_VALUE**|**sql_variant**|Valore minimo per una misurazione delle prestazioni di replica con limitazioni.|  
|**MAX_VALUE**|**sql_variant**|Valore massimo per una misurazione delle prestazioni di replica con limitazioni.|  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle di replica &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Viste della replica &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
