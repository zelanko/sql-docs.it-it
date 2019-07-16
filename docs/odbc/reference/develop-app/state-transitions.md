---
title: Transizioni di stato | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d2512d277980b071523cfea6cbe132f2a3861b7d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107294"
---
# <a name="state-transitions"></a>Transizioni di stato
ODBC definisce discreti *stati* per ogni ambiente, ogni connessione e ogni istruzione. Ad esempio, l'ambiente ha tre stati possibili: Non allocato (in cui non è allocato alcun ambiente), allocato (in cui viene allocato un ambiente ma non le connessioni vengono allocate) e connessione (in cui un ambiente e una o più connessioni sono allocate). Le connessioni sono sette possibili stati; istruzioni hanno 13 stati possibili.  
  
 Un particolare elemento, come identificato dal relativo handle, viene spostato da uno stato a altro quando l'applicazione chiama una determinata funzione o funzioni e passa l'handle a quell'elemento. Viene chiamato tale spostamento una *transizione dello stato*. Ad esempio, allocare un handle di ambiente con **SQLAllocHandle** Sposta l'ambiente da non allocata allocato e rilascio con tale handle **SQLFreeHandle** restituirlo da allocato a Non allocato. ODBC definisce un numero limitato di transizioni di stato validi, ovvero un altro modo per dire che le funzioni devono essere chiamate in un determinato ordine.  
  
 Alcune funzioni, ad esempio **SQLGetConnectAttr**, influisce sullo stato affatto. Altre funzioni influiscono sullo stato di un singolo elemento. Ad esempio, **SQLDisconnect** sposta una connessione da uno stato di connessione a uno stato allocato. Infine, alcune funzioni influiscono sullo stato di più di un elemento. Ad esempio, allocare un handle di connessione con **SQLAllocHandle** sposta una connessione da un non allocata a uno stato allocato e passa l'ambiente da un allocato a uno stato di connessione.  
  
 Se un'applicazione chiama una funzione non in ordine, la funzione restituisce un *lo stato di errore di transizione*. Se, ad esempio, un ambiente si trova in uno stato di connessione e l'applicazione chiama **SQLFreeHandle** con tale handle di ambiente **SQLFreeHandle** restituisce SQLSTATE HY010 (funzione di errore nella sequenza), Poiché può essere chiamato solo quando l'ambiente è stato allocato. Definendo ciò come una transizione di stato non valido, ODBC impedisce all'applicazione di liberare l'ambiente mentre vi sono connessioni attive.  
  
 Alcune transizioni di stato sono inerenti la progettazione di ODBC. Non è ad esempio, possibile allocare un handle di connessione senza prima di allocare un handle di ambiente, in quanto la funzione che consente di allocare un handle di connessione richiede un handle di ambiente. Altre transizioni di stato vengono applicate da Gestione Driver e i driver. Ad esempio, **SQLExecute** esegue un'istruzione preparata. Se viene passato l'handle di istruzione a non è in uno stato preparato **SQLExecute** restituisce SQLSTATE HY010 (funzione di errore nella sequenza).  
  
 Dal punto di vista dell'applicazione, le transizioni di stato sono in genere semplici: Transizioni di stato validi tendono a passare in stretta associazione con il flusso di un'applicazione ben scritta. Transizioni di stato sono più complesse per la gestione di Driver e i driver perché è necessario tenere traccia dello stato dell'ambiente, ogni connessione e ogni istruzione. La maggior parte di questa attività viene eseguita da Gestione Driver; la maggior parte delle operazioni che devono essere eseguite dai driver si verifica con istruzioni e i risultati in sospeso.  
  
 Part 1 e 2 del presente manuale ("Introduzione a ODBC" e "Sviluppo di applicazioni e i driver") tendono a non menzioni esplicitamente le transizioni di stato. Al contrario, vengono descritti l'ordine in cui devono essere chiamate le funzioni. Ad esempio, "L'esecuzione di istruzioni" indica che un'istruzione deve essere preparata con **SQLPrepare** prima di poter essere eseguito con **SQLExecute**. Per una descrizione completa degli Stati e transizioni di stato, tra cui quali transizioni sono controllate da Gestione Driver e che devono essere controllate dal driver, vedere [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
