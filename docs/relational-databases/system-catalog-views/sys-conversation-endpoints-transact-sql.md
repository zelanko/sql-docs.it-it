---
title: Sys. conversation_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- conversation_endpoints_TSQL
- conversation_endpoints
- sys.conversation_endpoints
- sys.conversation_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.conversation_endpoints catalog view
ms.assetid: 2ed758bc-2a9d-4831-8da2-4b80e218f3ea
author: stevestein
ms.author: sstein
ms.openlocfilehash: 16d29272e4229ac93b3dd5b1eaf5502a07fb0a2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109546"
---
# <a name="sysconversationendpoints-transact-sql"></a>sys.conversation_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ogni lato di una conversazione di [!INCLUDE[ssSB](../../includes/sssb-md.md)] è rappresentato da un endpoint di conversazione. In questa vista del catalogo è contenuta una riga per endpoint di conversazione nel database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|conversation_handle|**uniqueidentifier**|Identificatore dell'endpoint di conversazione. Non ammette i valori Null.|  
|conversation_id|**uniqueidentifier**|Identificatore della conversazione. Questo identificatore viene condiviso da entrambi i partecipanti alla conversazione e, analogamente alla colonna is_initiator, è univoco nel database. Non ammette i valori Null.|  
|is_initiator|**tinyint**|Indica se l'endpoint funge da initiator o da destinazione della conversazione.  Non ammette i valori Null.<br /><br /> 1 = Initiator<br /><br /> 0 = Destinazione|  
|service_contract_id|**int**|Identificatore del contratto per la conversazione. Non ammette i valori Null.|  
|conversation_group_id|**uniqueidentifier**|Identificatore del gruppo di conversazioni a cui appartiene la conversazione. Non ammette i valori Null.|  
|service_id|**int**|Identificatore del servizio per il lato specificato della conversazione. Non ammette i valori Null.|  
|lifetime|**datetime**|Data/ora di scadenza della conversazione. Non ammette i valori Null.|  
|state|**char(2)**|Stato corrente della conversazione. Non ammette i valori Null. I possibili valori sono i seguenti:<br /><br /> Quindi, avviata in uscita. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stata elaborata un'istruzione BEGIN CONVERSATION per la conversazione, ma non sono ancora stati inviati messaggi.<br /><br /> SI avviata in ingresso. Un'altra istanza ha avviato una nuova conversazione con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ma il primo messaggio non è ancora stato ricevuto completamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può creare una conversazione con questo stato se il primo messaggio è frammentato oppure se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] riceve messaggi non in ordine. Tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe tuttavia venire creata la conversazione con lo stato CO se la prima trasmissione ricevuta per la conversazione contiene il primo messaggio per intero.<br /><br /> CO in conversazione. La conversazione è stabilita ed entrambi i lati della conversazione possono inviare messaggi. La maggior parte delle comunicazioni di un comune servizio avviene quando la conversazione è in questo stato.<br /><br /> L'inserimento delle dipendenze disconnessa in ingresso. Il lato remoto della conversazione ha eseguito un'istruzione END CONVERSATION. La conversazione rimane in questo stato finché il lato locale della conversazione non esegue un'istruzione END CONVERSATION. Un'applicazione può ancora ricevere messaggi per la conversazione. Poiché sul lato remoto la conversazione è terminata, non può invece inviare messaggi nella conversazione. Quando un'applicazione esegue un'istruzione END CONVERSATION, la conversazione passa allo stato CD.<br /><br /> Eseguire l'operazione disconnessa in uscita. Il lato locale della conversazione ha eseguito un'istruzione END CONVERSATION. La conversazione rimane in questo stato finché il lato remoto della conversazione invia un acknowledgement dell'istruzione END CONVERSATION. Un'applicazione non può inviare o ricevere messaggi per la conversazione. Quando il lato remoto della conversazione invia un acknowledgement per END CONVERSATION, la conversazione passa allo stato CD.<br /><br /> Errore di Expressroute. In questo endpoint si è verificato un errore. Il messaggio di errore viene posizionato nella coda dell'applicazione. Se la coda dell'applicazione è vuota, l'applicazione ha già utilizzato il messaggio di errore.<br /><br /> Recapito Continuo è stato chiuso. L'endpoint di conversazione non è più in uso.|  
|state_desc|**nvarchar(60)**|Descrizione dello stato di endpoint conversazione. Questa colonna ammette valori Null. I possibili valori sono i seguenti:<br /><br /> **STARTED_OUTBOUND**<br /><br /> **STARTED_INBOUND**<br /><br /> **IN CONVERSAZIONE**<br /><br /> **DISCONNECTED_INBOUND**<br /><br /> **DISCONNECTED_OUTBOUND**<br /><br /> **CHIUSO**<br /><br /> **ERROR**|  
|far_service|**nvarchar(256)**|Nome del servizio nel lato remoto della conversazione. Non ammette i valori Null.|  
|far_broker_instance|**nvarchar(128)**|Istanza di Service Broker per il lato remoto della conversazione. Ammette valori Null.|  
|principal_id|**int**|Identificatore dell'entità il cui certificato viene utilizzato dal lato locale del dialogo. Non ammette i valori Null.|  
|far_principal_id|**int**|Identificatore dell'utente il cui certificato viene utilizzato dal lato remoto del dialogo. Non ammette i valori Null.|  
|outbound_session_key_identifier|**uniqueidentifier**|Identificatore della chiave di crittografia in uscita per il dialogo. Non ammette i valori Null.|  
|inbound_session_key_identifier|**uniqueidentifier**|Identificatore della chiave di crittografia in ingresso per il dialogo. Non ammette i valori Null.|  
|security_timestamp|**datetime**|Ora di creazione della chiave della sessione locale. Non ammette i valori Null.|  
|dialog_timer|**datetime**|Ora in cui il timer di conversazione per il dialogo corrente invia un messaggio DialogTimer. Non ammette i valori Null.|  
|send_sequence|**bigint**|Numero di messaggio successivo nella sequenza di invio. Non ammette i valori Null.|  
|last_send_tran_id|**binary(6)**|ID di transazione interna dell'ultima transazione che ha inviato un messaggio. Non ammette i valori Null.|  
|end_dialog_sequence|**bigint**|Numero di sequenza del messaggio di fine dialogo. Non ammette i valori Null.|  
|receive_sequence|**bigint**|Numero di messaggio successivo previsto nella sequenza di ricezione dei messaggi. Non ammette i valori Null.|  
|receive_sequence_frag|**int**|Numero di frammento di messaggio successivo previsto nella sequenza di ricezione dei messaggi. Non ammette i valori Null.|  
|system_sequence|**bigint**|Numero di sequenza dell'ultimo messaggio di sistema per il dialogo. Non ammette i valori Null.|  
|first_out_of_order_sequence|**bigint**|Numero di sequenza del primo messaggio nei messaggi non in ordine per il dialogo. Non ammette i valori Null.|  
|last_out_of_order_sequence|**bigint**|Numero di sequenza dell'ultimo messaggio nei messaggi non in ordine per il dialogo. Non ammette i valori Null.|  
|last_out_of_order_frag|**int**|Numero di sequenza dell'ultimo messaggio nei frammenti dei messaggi non in ordine per il dialogo. Non ammette i valori Null.|  
|is_system|**bit**|1 se si tratta di un dialogo di sistema. Non ammette i valori Null.|  
|priorità|**tinyint**|Priorità di conversazione assegnata a questo endpoint di conversazione. Non ammette i valori Null.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Per altre informazioni, vedere [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
