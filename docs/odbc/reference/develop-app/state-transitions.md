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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107294"
---
# <a name="state-transitions"></a>Transizioni di stato
ODBC definisce *gli Stati* discreti per ogni ambiente, ogni connessione e ogni istruzione. L'ambiente, ad esempio, può avere tre stati: non allocato (in cui non è allocato alcun ambiente), allocato (in cui un ambiente viene allocato ma nessuna connessione) e connessione (in cui un ambiente e una o più connessioni sono allocato). Le connessioni hanno sette stati possibili. le istruzioni hanno 13 stati possibili.  
  
 Un particolare elemento, identificato dal relativo handle, passa da uno stato a un altro quando l'applicazione chiama una funzione o funzioni specifiche e passa l'handle a tale elemento. Questo movimento viene chiamato *transizione di stato*. Ad esempio, l'allocazione di un handle di ambiente con **SQLAllocHandle** sposta l'ambiente da non allocato ad allocato e liberando tale handle con **SQLFreeHandle** lo restituisce da allocato a non allocato. ODBC definisce un numero limitato di transizioni di stato legali, un altro modo per indicare che le funzioni devono essere chiamate in un determinato ordine.  
  
 Alcune funzioni, ad esempio **SQLGetConnectAttr**, non influiscono sullo stato. Altre funzioni influiscono sullo stato di un singolo elemento. **Disconnect** , ad esempio, sposta una connessione da uno stato di connessione a uno stato allocato. Infine, alcune funzioni influiscono sullo stato di più di un elemento. Ad esempio, l'allocazione di un handle di connessione con **SQLAllocHandle** sposta una connessione da uno stato non allocato a uno stato allocato e sposta l'ambiente da uno allocato a uno stato di connessione.  
  
 Se un'applicazione chiama una funzione non ordinata, la funzione restituisce un *errore di transizione di stato*. Se, ad esempio, un ambiente è in uno stato di connessione e l'applicazione chiama **SQLFreeHandle** con tale handle di ambiente, **SQLFREEHANDLE** restituisce SQLSTATE HY010 (Error Sequence Function), perché può essere chiamato solo quando l'ambiente si trova in uno stato allocato. Definendo questa situazione come una transizione di stato non valida, ODBC impedisce all'applicazione di liberare l'ambiente mentre sono presenti connessioni attive.  
  
 Alcune transizioni di stato sono intrinseche nella progettazione di ODBC. Non è ad esempio possibile allocare un handle di connessione senza prima allocare un handle di ambiente, perché la funzione che alloca un handle di connessione richiede un handle di ambiente. Altre transizioni di stato vengono applicate da Gestione driver e dai driver. SQLExecute, **** ad esempio, esegue un'istruzione preparata. Se l'handle dell'istruzione passato non è in uno stato preparato, **SQLExecute** restituisce SQLSTATE HY010 (errore della sequenza di funzioni).  
  
 Dal punto di vista dell'applicazione, le transizioni di stato sono in genere semplici: le transizioni di stato giuridiche tendono a essere gestite con il flusso di un'applicazione ben scritta. Le transizioni di stato sono più complesse per Gestione driver e i driver perché devono tenere traccia dello stato dell'ambiente, di ogni connessione e di ogni istruzione. La maggior parte di queste operazioni viene eseguita da Gestione driver; la maggior parte delle operazioni che devono essere eseguite dai driver si verifica con istruzioni con risultati in sospeso.  
  
 Le parti 1 e 2 di questo manuale ("Introduzione a ODBC" e "sviluppo di applicazioni e driver") tendono a non citare in modo esplicito le transizioni di stato. Descrivono invece l'ordine in cui le funzioni devono essere chiamate. Ad esempio, "esecuzione di istruzioni" indica che un'istruzione deve essere preparata con **SQLPrepare** prima di poter essere eseguita con **SQLExecute**. Per una descrizione completa degli Stati e delle transizioni di stato, incluse le transizioni controllate da Gestione driver e che devono essere controllate dai driver, vedere [Appendice B: tabelle di transizione dello stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
