---
description: Acquisizione dei dati degli eventi per i trigger di accesso
title: Acquisire i dati degli eventi per i trigger di accesso | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e05b1ab4-c10b-402a-9591-f6ec1e3db8c0
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 429afe57e13c6eb9285256f54f2e83e2609ff7c0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97403265"
---
# <a name="capture-logon-trigger-event-data"></a>Acquisizione dei dati degli eventi per i trigger di accesso
[!INCLUDE[tsql-appliesto-ss2008-appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
   Per acquisire dati XML sugli eventi LOGON da usare in trigger LOGON, è possibile usare la funzione [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md). L'evento LOGON restituisce lo schema di dati di evento seguente:  
  
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
  
  
