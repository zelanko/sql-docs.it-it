---
title: Traccia dinamica . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8cbd2dbae4f4b437f45845ce2791f4a9b0aa8c8b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305768"
---
# <a name="dynamic-tracing"></a>Traccia dinamica
La traccia può essere abilitata o disabilitata in qualsiasi momento in un'esecuzione dell'applicazione. Ciò consente a un'applicazione di tracciare un numero qualsiasi di chiamate di funzione.  
  
 La variabile **ODBCSharedTraceFlag** è impostata per consentire la traccia in modo dinamico. Questa variabile viene condivisa tra tutte le copie in esecuzione di Gestione Driver. Se un'applicazione imposta questa variabile, la traccia è abilitata per tutte le applicazioni ODBC attualmente in esecuzione. Per disattivare la traccia quando è abilitata la traccia dinamica, un'applicazione chiama **SQLSetConnectAttr** per impostare SQL_ATTR_TRACE su SQL_TRACE_OFF. Questa chiamata distoglierà la traccia solo per l'applicazione. Le applicazioni collegate a Odbc32.lib possono modificare l'utilizzo di questa variabile. I dati di traccia possono essere visualizzati in un intervallo in tempo reale, anziché il file di traccia, che deve essere aperto dopo la sessione ODBC. I controlli possono essere aggiunti alla schermata di un'applicazione per attivare o disattivare la traccia a turno.  
  
 La DLL di traccia fornita con ODBC 3 *.x* non è thread-safe. Non è garantito che il file di log venga scritto correttamente se la traccia globale è abilitata (la variabile **ODBCSharedTraceFlag** è impostata) e più applicazioni vengono scritte contemporaneamente nel file di traccia. Questa condizione non restituisce un errore.
