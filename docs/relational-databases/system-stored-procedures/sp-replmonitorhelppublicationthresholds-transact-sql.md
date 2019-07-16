---
title: sp_replmonitorhelppublicationthresholds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
author: stevestein
ms.author: sstein
ms.openlocfilehash: a80ff5308edee02d24d214a6520a090750600edc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950572"
---
# <a name="spreplmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce le metriche relative alle soglie impostate per una pubblicazione monitorata. Questa stored procedure, utilizzata per il monitoraggio della replica, viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replmonitorhelppublicationthresholds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del database pubblicato. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publication = ] 'publication'` È il nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publication_type = ] publication_type` Se il tipo di pubblicazione. *publication_type* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Pubblicazione transazionale.|  
|**1**|Pubblicazione snapshot.|  
|**2**|Pubblicazione di tipo merge.|  
|NULL (predefinito)|La replica tenta di determinare il tipo di pubblicazione.|  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|ID della misurazione delle prestazioni di replica. I possibili valori sono i seguenti:<br /><br /> **1expiration** -esegue il monitoraggio delle scadenze imminenti delle sottoscrizioni a pubblicazioni transazionali.<br /><br /> **2latency** -esegue il monitoraggio delle prestazioni delle sottoscrizioni di pubblicazioni transazionali.<br /><br /> **4mergeexpiration** -esegue il monitoraggio delle scadenze imminenti delle sottoscrizioni di pubblicazioni di tipo merge.<br /><br /> **5mergeslowrunduration** -monitora la durata delle sincronizzazioni di tipo merge attraverso connessioni a larghezza di banda ridotta (Remote).<br /><br /> **6mergefastrunduration** -monitora la durata delle sincronizzazioni di tipo merge attraverso connessioni a banda larga (LAN).<br /><br /> **7mergefastrunspeed** -monitora la frequenza di sincronizzazione delle sincronizzazioni di tipo merge attraverso connessioni a banda larga (LAN).<br /><br /> **8mergeslowrunspeed** -monitora la frequenza di sincronizzazione delle sincronizzazioni di tipo merge attraverso connessioni a larghezza di banda ridotta (Remote).|  
|**title**|**sysname**|Nome della misurazione delle prestazioni di replica.|  
|**Valore**|**int**|Valore soglia della misurazione delle prestazioni.|  
|**shouldalert**|**bit**|È se deve essere generato un avviso quando la metrica supera la soglia definita per la pubblicazione. un valore pari **1** indica che deve essere generato un avviso.|  
|**isenabled**|**bit**|È se il monitoraggio è abilitato per la metrica di prestazioni della replica per la pubblicazione. un valore pari **1** indica che il monitoraggio è attivato.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_replmonitorhelppublicationthresholds** viene utilizzato con tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **db_owner** oppure **replmonitor** ruolo predefinito del database nel database di distribuzione possono eseguire **sp_replmonitorhelppublicationthresholds**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare la replica a livello di programmazione](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
