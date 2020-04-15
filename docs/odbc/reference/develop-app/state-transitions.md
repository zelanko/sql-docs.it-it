---
title: Transizioni di Stato Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a480b7ff8953ef94f0efc4886a09731730a61b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299694"
---
# <a name="state-transitions"></a>Transizioni di stato
ODBC definisce *stati* discreti per ogni ambiente, ogni connessione e ogni istruzione. Ad esempio, l'ambiente dispone di tre stati possibili: Non allocato (in cui non viene allocato alcun ambiente), Allocato (in cui viene allocato un ambiente ma non viene allocato alcuna connessione) e Connessione (in cui vengono allocate un ambiente e una o più connessioni). Le connessioni hanno sette stati possibili; dichiarazioni hanno 13 stati possibili.  
  
 Un elemento specifico, identificato dal relativo handle, si sposta da uno stato a un altro quando l'applicazione chiama una o più funzioni specifiche e passa l'handle a tale elemento. Tale movimento è chiamato *transizione di stato*. Ad esempio, l'allocazione di un handle di ambiente con **SQLAllocHandle** sposta l'ambiente da Non allocato a Allocato e liberando tale handle con **SQLFreeHandle** lo restituisce da Allocato a Non allocato. ODBC definisce un numero limitato di transizioni di stato legale, che è un altro modo per dire che le funzioni devono essere chiamate in un determinato ordine.  
  
 Alcune funzioni, ad esempio **SQLGetConnectAttr**, non influiscono sullo stato. Altre funzioni influiscono sullo stato di un singolo elemento. Ad esempio, **SQLDisconnect** sposta una connessione da uno stato di connessione a uno stato allocato. Infine, alcune funzioni influiscono sullo stato di più di un elemento. Ad esempio, l'allocazione di un handle di connessione con **SQLAllocHandle** sposta una connessione da uno stato Non allocato a uno allocato e sposta l'ambiente da uno stato Allocato a una connessione.  
  
 Se un'applicazione chiama una funzione non in ordine, la funzione restituisce un errore di *transizione dello stato.* Ad esempio, se un ambiente è in uno stato di connessione e l'applicazione chiama **SQLFreeHandle** con tale handle di ambiente, **SQLFreeHandle** restituisce SQLSTATE HY010 (errore di sequenza di funzione), perché può essere chiamato solo quando l'ambiente è in uno stato allocato. Definendo questa definizione come una transizione di stato non valida, ODBC impedisce all'applicazione di liberare l'ambiente mentre sono presenti connessioni attive.  
  
 Alcune transizioni di stato sono inerenti alla progettazione di ODBC. Ad esempio, non è possibile allocare un handle di connessione senza prima allocare un handle di ambiente, perché la funzione che alloca un handle di connessione richiede un handle di ambiente. Altre transizioni di stato vengono applicate da Gestione Driver e dai driver. Ad esempio, **SQLExecute** esegue un'istruzione preparata. Se l'handle dell'istruzione passato non è in uno stato Prepared, **SQLExecute** restituisce SQLSTATE HY010 (errore di sequenza di funzioni).  
  
 Dal punto di vista dell'applicazione, le transizioni di stato sono in genere semplici: le transizioni di stato legale tendono ad andare di pari passo con il flusso di un'applicazione ben scritta. Le transizioni di stato sono più complesse per Gestione Driver e i driver perché devono tenere traccia dello stato dell'ambiente, di ogni connessione e di ogni istruzione. La maggior parte di questo lavoro è fatto da Driver Manager; la maggior parte del lavoro che deve essere fatto dai driver si verifica con dichiarazioni con risultati in sospeso.  
  
 Le parti 1 e 2 di questo manuale ("Introduzione a ODBC" e "Sviluppo di applicazioni e driver") tendono a non menzionare esplicitamente le transizioni di stato. Al contrario, descrivono l'ordine in cui le funzioni devono essere chiamate. Ad esempio, "Esecuzione di istruzioni" indica che un'istruzione deve essere preparata con **SQLPrepare** prima di poter essere eseguita con **SQLExecute**. Per una descrizione completa dello stato e delle transizioni di stato, incluse le transizioni controllate da Gestione Driver e che devono essere controllate dai driver, vedere [Appendice B: Tabelle](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC .
