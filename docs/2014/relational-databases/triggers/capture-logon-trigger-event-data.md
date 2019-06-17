---
title: Acquisire i dati degli eventi per i trigger di accesso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e9ee204d55114b7e31a9a9550d86cae3baa4dffc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63130361"
---
# <a name="capture-logon-trigger-event-data"></a>Acquisizione dei dati degli eventi per i trigger di accesso
  Per acquisire dati XML per gli eventi LOGON da utilizzare in trigger LOGON, è possibile utilizzare la funzione [EVENTDATA](/sql/t-sql/functions/eventdata-transact-sql) . L'evento LOGON restituisce lo schema di dati di evento seguente:  
  
 `<EVENT_INSTANCE>`  
  
 `<EventType>event_type</EventType>`  
  
 `<PostTime>post_time</PostTime>`  
  
 `<SPID>spid</SPID>`  
  
 `<ServerName>server_name</ServerName>`  
  
 `<LoginName>login_name</LoginName>`  
  
 `<LoginType>login_type</LoginType>`  
  
 `<SID>sid</SID>`  
  
 `<ClientHost>client_host</ClientHost>`  
  
 `<IsPooled>is_pooled</IsPooled>`  
  
 `</EVENT_INSTANCE>`  
  
 `<EventType>`  
 Contiene `LOGON`.  
  
 `<PostTime>`  
 Contiene l'ora in cui viene richiesta l'attivazione di una sessione.  
  
 `<SID>`  
 Contiene il flusso binario codificato in base 64 dell'ID di sicurezza (SID) per il nome di account di accesso specificato.  
  
 `<ClientHost>`  
 Contiene il nome host del client da cui viene attivata la connessione. Il valore è '`<local_machine>`' se il nome del client e del server coincidono. In caso contrario, il valore corrisponde all'indirizzo IP del client.  
  
 `<IsPooled>`  
 Il valore è `1` se la connessione viene riutilizzata tramite pool di connessioni. In caso contrario, il valore è `0`.  
  
  
