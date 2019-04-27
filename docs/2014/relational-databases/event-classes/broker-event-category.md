---
title: Categoria di eventi Broker | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9918aca57caaef0dc460e810f5ed5ca2d1106ac3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62663810"
---
# <a name="broker-event-category"></a>Categoria di eventi Broker
  La categoria di eventi **Broker** include gli eventi generali di Service Broker.  
  
## <a name="in-this-section"></a>In questa sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Classe di evento Broker:Activation](broker-activation-event-class.md)|Evento generato quando un monitoraggio di coda avvia una stored procedure di attivazione.|  
|[Classe di evento Broker:Connection](broker-connection-event-class.md)|Evento generato per indicare lo stato di una connessione di trasporto gestita da Service Broker.|  
|[Classe di evento Broker:Conversation](broker-conversation-event-class.md)|Evento generato per indicare lo stato di una conversazione.|  
|[Classe di evento Broker:Conversation Group](broker-conversation-group-event-class.md)|Evento generato quando il database crea o elimina un gruppo di conversazione.|  
|[Classe di evento Broker:Corrupted Message](broker-corrupted-message-event-class.md)|Evento generato per indicare che il database ha ricevuto un messaggio danneggiato.|  
|[Classe di evento Broker:Forwarded Message Dropped](broker-forwarded-message-dropped-event-class.md)|Evento generato quando SQL Server elimina un messaggio di Service Broker per cui era previsto l'inoltro.|  
|[Classe di evento Broker:Forwarded Message Sent](broker-forwarded-message-sent-event-class.md)|Evento generato quando SQL Server inoltra un messaggio di Service Broker.|  
|[Classe di evento Broker:Message Classify](broker-message-classify-event-class.md)|Evento generato quando Service Broker stabilisce il routing di un messaggio.|  
|[Classe di evento Broker:Message Drop](broker-message-drop-event-class.md)|Evento generato quando Service Broker non è in grado di memorizzare un messaggio ricevuto che avrebbe dovuto essere recapitato a un servizio nell'istanza corrente.|  
|[Classe di evento Broker:Remote Message Ack](broker-remote-message-ack-event-class.md)|Evento generato quando Service Broker invia o riceve l'acknowledgement di un messaggio.|  
  
 Vengono inoltre generati due eventi di controllo della sicurezza per Service Broker. Per altre informazioni sugli eventi, vedere [Classe di evento Audit Broker Login](audit-broker-login-event-class.md) e [Classe di evento Audit Broker Conversation](audit-broker-conversation-event-class.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Categoria di eventi Controllo di sicurezza](https://docs.microsoft.com/bi-reference/trace-events/security-audit-event-category)  
  
  
