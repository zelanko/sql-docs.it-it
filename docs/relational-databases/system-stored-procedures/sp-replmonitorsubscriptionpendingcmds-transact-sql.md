---
title: sp_replmonitorsubscriptionpendingcmds (T-SQL)
description: Viene descritta la sp_replmonitorsubscriptionpendingcmds stored procedure che restituisce informazioni sul numero di comandi in sospeso per una sottoscrizione di una pubblicazione transazionale.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorsubscriptionpendingcmds_TSQL
- sp_replmonitorsubscriptionpendingcmds
helpviewer_keywords:
- sp_replmonitorsubscriptionpendingcmds
ms.assetid: df5b955a-feb0-4863-9b3b-7f71e9653b3d
author: stevestein
ms.author: sstein
ms.openlocfilehash: a493ef87ad2f980f21a99c50da1cb39dfdcda8cf
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/20/2019
ms.locfileid: "75319984"
---
# <a name="sp_replmonitorsubscriptionpendingcmds-transact-sql"></a>sp_replmonitorsubscriptionpendingcmds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Restituisce informazioni sul numero di comandi in sospeso per una sottoscrizione di una pubblicazione transazionale e una stima approssimativa del tempo necessario per l'elaborazione di tali comandi. Questa stored procedure restituisce una riga per ogni sottoscrizione restituita. Questa stored procedure, utilizzata per il monitoraggio della replica, viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento all'argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replmonitorsubscriptionpendingcmds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @subscription_type = ] subscription_type  
```  
  
## <a name="arguments"></a>Arguments  
`[ @publisher = ] 'publisher'`Nome del server di pubblicazione. *Publisher* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @publisher_db = ] 'publisher_db'`Nome del database pubblicato. *publisher_db* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @publication = ] 'publication'`Nome della pubblicazione. *Publication* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @subscriber = ] 'subscriber'`Nome del Sottoscrittore. *Subscriber* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @subscriber_db = ] 'subscriber_db'`Nome del database di sottoscrizione. *subscriber_db* è di **tipo sysname**e non prevede alcun valore predefinito.  
  
`[ @subscription_type = ] subscription_type`Se il tipo di sottoscrizione. *publication_type* è di **tipo int**e non prevede alcun valore predefinito. i possibili valori sono i seguenti.  
  
|Value|Description|  
|-----------|-----------------|  
|**0**|Sottoscrizione push|  
|**1**|Sottoscrizione pull|  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Description|  
|-----------------|---------------|-----------------|  
|**pendingcmdcount**|**int**|Numero di comandi in sospeso per la sottoscrizione.|  
|**estimatedprocesstime**|**int**|Stima del numero di secondi necessari per il recapito di tutti i comandi in sospeso al Sottoscrittore.|  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 **0** (esito positivo) o **1** (esito negativo)  
  
## <a name="remarks"></a>Osservazioni  
 **sp_replmonitorsubscriptionpendingcmds** viene utilizzato con la replica transazionale.  
  
## <a name="permissions"></a>Autorizzazioni  
 Solo i membri del ruolo predefinito del server **sysadmin** nel server di distribuzione o i membri del ruolo predefinito del database **db_owner** nel database di distribuzione possono eseguire **sp_replmonitorsubscriptionpendingcmds**. I membri dell'elenco di accesso alla pubblicazione per una pubblicazione che utilizza il database di distribuzione possono eseguire **sp_replmonitorsubscriptionpendingcmds** per restituire i comandi in sospeso per la pubblicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare la replica a livello di codice](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
