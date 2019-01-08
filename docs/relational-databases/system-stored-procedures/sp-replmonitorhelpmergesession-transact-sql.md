---
title: sp_replmonitorhelpmergesession (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesession_TSQL
- sp_replmonitorhelpmergesession
helpviewer_keywords:
- sp_replmonitorhelpmergesession
ms.assetid: a0400ba8-9609-4901-917e-925e119103a1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e08a08bbd3343386ed4b07749bde5216ae23c8b4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52789193"
---
# <a name="spreplmonitorhelpmergesession-transact-sql"></a>sp_replmonitorhelpmergesession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce informazioni sulle sessioni passate per un agente di merge specifico. Viene restituita una riga per ogni sessione che soddisfa i criteri del filtro. Questa stored procedure, utilizzata per il monitoraggio della replica di tipo merge, viene eseguita nel database di distribuzione del server di distribuzione o nel database di sottoscrizione del Sottoscrittore.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_replmonitorhelpmergesession [ [ @agent_name = ] 'agent_name' ]  
    [ , [ @hours = ] hours ]  
    [ , [ @session_type = ] session_type ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]   
```  
  
## <a name="arguments"></a>Argomenti  
 [ **@agent_name** =] **'***agent_name***'**  
 Nome dell'agente. *agent_name* viene **nvarchar(100)** non prevede alcun valore predefinito.  
  
 [ **@hours** =] *ore*  
 Intervallo di tempo, espresso in ore, per cui vengono restituite informazioni sulle sessioni passate dell'agente. *ore* viene **int**, che può essere uno degli intervalli seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|< **0**|Restituisce informazioni sulle esecuzioni passate dell'agente, per al massimo 100 esecuzioni.|  
|**0** (predefinito)|Restituisce informazioni su tutte le esecuzioni passate dell'agente.|  
|> **0**|Restituisce informazioni sull'agente di esecuzioni che si sono verificati nelle ultime *ore* numero di ore.|  
  
 [ **@session_type** =] *session_type*  
 Filtra il set di risultati in base al risultato finale della sessione. *session_type* viene **int**, i possibili valori sono i seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**1** (impostazione predefinita)|Sessioni dell'agente con esito positivo o da ritentare.|  
|**0**|Sessioni dell'agente con esito negativo.|  
  
 [ **@publisher** =] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, con un valore predefinito è NULL. Questo parametro viene usato quando si esegue **sp_replmonitorhelpmergesession** nel Sottoscrittore.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Nome del database di pubblicazione. *publisher_db* viene **sysname**, con un valore predefinito è NULL. Questo parametro viene usato quando si esegue **sp_replmonitorhelpmergesession** nel Sottoscrittore.  
  
 [  **@publication=** ] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, con un valore predefinito è NULL. Questo parametro viene usato quando si esegue **sp_replmonitorhelpmergesession** nel Sottoscrittore.  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**Session_id**|**int**|ID della sessione del processo dell'agente.|  
|**Stato**|**int**|Stato dell'esecuzione dell'agente:<br /><br /> **1** = avvio<br /><br /> **2** = esito positivo<br /><br /> **3** = in corso<br /><br /> **4** = inattivo<br /><br /> **5** = nuovo tentativo<br /><br /> **6** = esito negativo|  
|**StartTime**|**datetime**|Data e ora di inizio della sessione del processo dell'agente.|  
|**EndTime**|**datetime**|Data e ora di completamento della sessione del processo dell'agente.|  
|**Durata**|**int**|Durata cumulativa, espressa in secondi, della sessione del processo.|  
|**UploadedCommands**|**int**|Numero di comandi caricati durante la sessione dell'agente.|  
|**DownloadedCommands**|**int**|Numero di comandi scaricati durante la sessione dell'agente.|  
|**ErrorMessages**|**int**|Numero di messaggi di errore generati durante la sessione dell'agente.|  
|**ErrorID**|**int**|ID dell'errore che si è verificato|  
|**PercentageDone**|**decimal**|Percentuale stimata del numero totale di modifiche già recapitate in una sessione attiva.|  
|**TimeRemaining**|**int**|Numero stimato di secondi rimanenti in una sessione attiva.|  
|**CurrentPhase**|**int**|Fase corrente di una sessione attiva. I possibili valori sono i seguenti.<br /><br /> **1** = caricamento<br /><br /> **2** = download|  
|**LastMessage**|**nvarchar(500)**|Ultimo messaggio registrato dall'agente di merge durante la sessione.|  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_replmonitorhelpmergesession** viene usato per monitorare la replica di tipo merge.  
  
 Quando viene eseguito sul sottoscrittore **sp_replmonitorhelpmergesession** solo restituisce informazioni sulle ultime cinque sessioni dell'agente di Merge.  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **db_owner** oppure **replmonitor** ruolo predefinito del database nel database di distribuzione nel server di distribuzione o nel database di sottoscrizione del sottoscrittore possono eseguire **sp _ replmonitorhelpmergesession**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare la replica a livello di programmazione](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
