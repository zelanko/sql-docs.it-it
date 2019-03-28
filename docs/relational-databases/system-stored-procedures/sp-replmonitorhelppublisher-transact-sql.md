---
title: sp_replmonitorhelppublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f5f537dcb0f41c975ebbb7b5c6a27c2b2e306a09
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532173"
---
# <a name="spreplmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sullo stato corrente per uno o più server di pubblicazione associati a un server di distribuzione. Questa stored procedure, utilizzata per il monitoraggio della replica, viene eseguita nel database di distribuzione del server di distribuzione.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione viene monitorato lo stato dei quali. *server di pubblicazione* viene **sysname**, con un valore predefinito NULL. Se NULL, verranno restituite informazioni per tutti i server di pubblicazione che utilizzano il server di distribuzione.  
  
`[ @refreshpolicy = ] refreshpolicy` Solo uso interno.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|Nome del server di pubblicazione.|  
|**distribution_db**|**sysname**|Nome del database di distribuzione utilizzato dal server di pubblicazione specificato.|  
|**status**|**int**|Stato massimo di tutti gli agenti di replica associati alle pubblicazioni nel server di pubblicazione specificato. I possibili valori sono i seguenti:<br /><br /> **1** = avviato<br /><br /> **2** = ha avuto esito positivo<br /><br /> **3** = in corso<br /><br /> **4** = inattivo<br /><br /> **5** = nuovo tentativo in corso<br /><br /> **6** = non è riuscita|  
|**warning**|**int**|Avviso correlato alla soglia massima generata da una sottoscrizione appartenente a una pubblicazione nel server di pubblicazione specificato. Può essere il risultato di un'operazione OR logica su uno o più dei valori seguenti.<br /><br /> **1** = expiration - una sottoscrizione di una pubblicazione transazionale non sia stata sincronizzata entro la soglia di periodo di conservazione.<br /><br /> **2** = latency - il tempo necessario per replicare i dati da un server di pubblicazione transazionale al sottoscrittore supera la soglia, espresso in secondi.<br /><br /> **4** = mergeexpiration - una sottoscrizione a una pubblicazione di tipo merge non sia stata sincronizzata entro la soglia di periodo di conservazione.<br /><br /> **8** = mergefastrunduration - il tempo impiegato per completare la sincronizzazione di una sottoscrizione di tipo merge supera la soglia, espresso in secondi, tramite una connessione di rete veloce.<br /><br /> **16** = mergeslowrunduration - il tempo impiegato per completare la sincronizzazione di una sottoscrizione di tipo merge supera la soglia, espresso in secondi, tramite una connessione di rete lenta o remota.<br /><br /> **32** = mergefastrunspeed: la velocità di recapito delle righe durante la sincronizzazione di una sottoscrizione di tipo merge è minore della soglia, in righe al secondo, su una connessione di rete veloce.<br /><br /> **64** = mergeslowrunspeed: la velocità di recapito delle righe durante la sincronizzazione di una sottoscrizione di tipo merge è minore della soglia, in righe al secondo, su una connessione di rete lenta o remota.|  
|**publicationcount**|**int**|Numero di pubblicazioni appartenenti al server di pubblicazione.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_replmonitorhelppublisher** viene utilizzato con tutti i tipi di replica.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** nel server di distribuzione membri del ruolo predefinito del server il **db_owner** oppure **replmonitor** ruoli predefiniti del database nel database di distribuzione possono eseguire **sp_replmonitorhelppublisher**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare la replica a livello di programmazione](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
