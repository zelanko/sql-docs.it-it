---
title: sp_replmonitorhelpmergesessiondetail (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesessiondetail
- sp_replmonitorhelpmergesessiondetail_TSQL
helpviewer_keywords:
- sp_replmonitorhelpmergesessiondetail
ms.assetid: 805c92fc-3169-410c-984d-f37e063b791d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dbafa8dd407269fa23ca37574f18a12be519c448
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534634"
---
# <a name="spreplmonitorhelpmergesessiondetail-transact-sql"></a>sp_replmonitorhelpmergesessiondetail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni dettagliate a livello di articolo su una specifica sessione di replica dell'agente di merge, utilizzato per monitorare la replica di tipo merge. Il set di risultati include una riga di dettaglio per ogni articolo sincronizzato durante la sessione, nonché una riga che rappresenta l'inizializzazione della sessione e righe che riepilogano le fasi di caricamento e scaricamento della sessione. Questa stored procedure viene eseguita nel database di distribuzione del server di distribuzione oppure nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replmonitorhelpmergesessiondetail [ @session_id = ] session_id  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @session_id = ] session_id` Specifica una sessione dell'agente. *session_id* viene **int** non prevede alcun valore predefinito.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**PhaseID**|**int**|Fase della sessione di sincronizzazione. I possibili valori sono i seguenti.<br /><br /> **0** = inizializzazione o riga di riepilogo<br /><br /> **1** = caricamento<br /><br /> **2** = download|  
|**ArticleName**|**sysname**|Nome dell'articolo in fase di sincronizzazione. **ArticleName** contiene anche informazioni di riepilogo per le righe nel set di risultati che non rappresentano dettagli del caso.|  
|**PercentComplete**|**decimal**|Indica la percentuale delle modifiche totali applicate in una riga di dettaglio dell'articolo per le sessioni in esecuzione e quelle non riuscite.|  
|**RelativeCost**|**decimal**|Indica il tempo dedicato alla sincronizzazione dell'articolo come percentuale del tempo totale di sincronizzazione per la sessione.|  
|**Durata**|**int**|Durata della sessione dell'agente.|  
|**Inserts**|**int**|Numero di inserimenti in una sessione.|  
|**Aggiornamenti**|**int**|Numero di aggiornamenti in una sessione.|  
|**Eliminazioni**|**int**|Numero di eliminazioni in una sessione.|  
|**Conflitti**|**int**|Numero di conflitti verificatisi in una sessione.|  
|**ErrorID**|**int**|ID di un errore di sessione.|  
|**SeqNo**|**int**|Ordine delle sessioni nel set di risultati.|  
|**RowType**|**int**|Indica il tipo di informazioni rappresentato da ogni riga nel set di risultati.<br /><br /> **0** = inizializzazione<br /><br /> **1** = riepilogo del caricamento<br /><br /> **2** = dettagli di caricamento dell'articolo<br /><br /> **3** = riepilogo del download<br /><br /> **4** = dettagli di scaricamento dell'articolo|  
|**SchemaChanges**|**int**|Numero di modifiche dello schema in una sessione.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_replmonitorhelpmergesessiondetail** viene usato per monitorare la replica di tipo merge.  
  
 Quando viene eseguito sul sottoscrittore **sp_replmonitorhelpmergesessiondetail** solo restituisce informazioni dettagliate sulle ultime 5 sessioni dell'agente di Merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **db_owner** oppure **replmonitor** ruolo predefinito del database nel database di distribuzione nel server di distribuzione o nel database di sottoscrizione del sottoscrittore possono eseguire **sp _ replmonitorhelpmergesessiondetail**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare la replica a livello di programmazione](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
