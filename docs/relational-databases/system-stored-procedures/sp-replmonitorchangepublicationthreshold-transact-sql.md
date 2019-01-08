---
title: sp_replmonitorchangepublicationthreshold (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d557fccc94c6502bb664f8345d1d7a6bd982124
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52789333"
---
# <a name="spreplmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica la metrica del valore soglia di monitoraggio di una pubblicazione. Questa stored procedure, utilizzata per il monitoraggio della replica, viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@publisher** =] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Nome del database pubblicato. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@publication** =] **'***pubblicazione***'**  
 Nome della pubblicazioni di cui si desidera modificare gli attributi del valore soglia di monitoraggio. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@publication_type** =] *publication_type*  
 Tipo di pubblicazione. *publication_type* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Pubblicazione transazionale.|  
|**1**|Pubblicazione snapshot.|  
|**2**|Pubblicazione di tipo merge.|  
|NULL (predefinito)|La replica cerca di determinare il tipo di pubblicazione.|  
  
 [ **@metric_id** =] *metric_id*  
 ID della metrica della soglia per la pubblicazione che si desidera modificare. *metric_id* viene **int**, con un valore predefinito NULL e i possibili valori sono i seguenti.  
  
|Value|Nome misurazione|  
|-----------|-----------------|  
|**1**|**expiration** : esegue il monitoraggio delle scadenze imminenti delle sottoscrizioni di pubblicazioni transazionali.|  
|**2**|**latency** : esegue il monitoraggio delle prestazioni delle sottoscrizioni di pubblicazioni transazionali.|  
|**4**|**mergeexpiration** : esegue il monitoraggio delle scadenze imminenti delle sottoscrizioni di pubblicazioni di tipo merge.|  
|**5**|**mergeslowrunduration** -monitora la durata delle sincronizzazioni di tipo merge attraverso connessioni a larghezza di banda ridotta (Remote).|  
|**6**|**mergefastrunduration** -monitora la durata delle sincronizzazioni di tipo merge attraverso connessioni a banda larga rete locale (LAN).|  
|**7**|**mergefastrunspeed** - esegue il monitoraggio della frequenza delle sincronizzazioni di tipo merge su connessioni tramite rete locale (LAN) a larghezza di banda elevata.|  
|**8**|**mergeslowrunspeed** -monitora la frequenza di sincronizzazione delle sincronizzazioni di tipo merge attraverso connessioni a larghezza di banda ridotta (Remote).|  
  
 È necessario specificare *metric_id* oppure *thresholdmetricname*. Se *thresholdmetricname* è specificato, quindi *metric_id* deve essere NULL.  
  
 [ **@thresholdmetricname** =] **'***thresholdmetricname***'**  
 Nome della metrica del valore soglia della pubblicazione che si desidera modificare. *thresholdmetricname* viene **sysname**, con un valore predefinito NULL. È necessario specificare *thresholdmetricname* oppure *metric_id*. Se *metric_id* è specificato, quindi *thresholdmetricname* deve essere NULL.  
  
 [ **@value** =] *valore*  
 Nuovo valore della metrica del valore soglia della pubblicazione. *valore* viene **int**, con un valore predefinito NULL. Se **null**, quindi il valore della metrica non viene aggiornato.  
  
 [ **@shouldalert** =] *shouldalert*  
 Indica se viene generato un avviso quando viene raggiunta la metrica del valore soglia di una pubblicazione. *shouldalert* viene **bit**, con un valore predefinito è NULL. Un valore pari **1** indica che viene generato un avviso, mentre il valore di **0** significa che non viene generato un avviso.  
  
 [ **@mode** =] *modalità*  
 Indica se è abilitata la metrica del valore soglia della pubblicazione. *modalità* viene **tinyint**, il valore predefinito è **1**. Un valore pari **1** indica che il monitoraggio della metrica è abilitato, mentre il valore di **2** significa che il monitoraggio di questa metrica è disabilitato.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_replmonitorchangepublicationthreshold** viene utilizzato con tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **db_owner** oppure **replmonitor** ruolo predefinito del database nel database di distribuzione possono eseguire **sp_replmonitorchangepublicationthreshold**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare la replica a livello di programmazione](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
