---
title: Informazioni sui blocchi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], locking
- locks [ADO], about locking
ms.assetid: f8989555-28c6-4c17-9bf8-7f44a8a5c407
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 744ae9a9541b5c73d579e097f375b4141e771fce
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501758"
---
# <a name="what-is-a-lock"></a>Informazioni sui blocchi
Il blocco è il processo mediante il quale un DBMS limita l'accesso a una riga in un ambiente multiutente. Quando una riga o colonna viene bloccato in modo esclusivo, altri utenti non sono consentiti per accedere ai dati bloccati fino a quando il blocco viene rilasciato. Ciò garantisce che due utenti non è possibile aggiornare contemporaneamente la stessa colonna in una riga.  
  
 I blocchi possono essere molto onerosa dal punto di vista della risorsa e devono essere utilizzati solo quando necessario per mantenere l'integrità dei dati. In un database in cui è stato possibile cercare centinaia o migliaia di utenti per accedere a un record di ogni secondo, ad esempio un database connesso a Internet - numero eccessivo di blocchi può rapidamente comportare rallentamento delle prestazioni nell'applicazione.  
  
 È possibile controllare come l'origine dati e la libreria di cursori di ADO gestire la concorrenza, scegliendo l'opzione di blocco appropriato.  
  
 Impostare il **LockType** proprietà prima di aprire un **Recordset** per specificare il tipo di blocco che il provider deve utilizzare all'apertura dell'oggetto. Leggere la proprietà per restituire il tipo di blocco in uso su un elemento aperto **Recordset** oggetto.  
  
 I provider potrebbero non supportare tutti i tipi di blocco. Se un provider non supporta l'oggetto richiesto **LockType** impostazione, sostituirà un altro tipo di blocco. Per determinare la funzionalità di blocco disponibile in un **Recordset** dell'oggetto, utilizzare il [supporta](../../../ado/reference/ado-api/supports-method.md) metodo con **valori adUpdate** e **adUpdateBatch**.  
  
 Il **adLockPessimistic** impostazione non è supportata se il [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) viene impostata su **adUseClient.** Se è impostato un valore non supportato, non verrà generato alcun errore; è supportato il più vicino **LockType** verrà utilizzato.  
  
 Il **LockType** è di lettura/scrittura quando il **Recordset** è chiuso e di sola lettura quando è aperto.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di blocchi](../../../ado/guide/data/types-of-locks.md)
