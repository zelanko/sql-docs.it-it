---
title: Traccia dinamica | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8420589761a1f8cb1f9cf8a3022842863fd30758
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046895"
---
# <a name="dynamic-tracing"></a>Traccia dinamica
La traccia può essere abilitata o disabilitata in qualsiasi punto dell'esecuzione di un'applicazione. Questo consente a un'applicazione di tracciare un numero qualsiasi di chiamate di funzione.  
  
 La variabile **ODBCSharedTraceFlag** è impostata per abilitare la traccia in modo dinamico. Questa variabile è condivisa tra tutte le copie in esecuzione di gestione driver. Se questa variabile viene impostata da un'applicazione, la traccia è abilitata per tutte le applicazioni ODBC attualmente in esecuzione. Per disattivare la traccia quando è abilitata la traccia dinamica, un'applicazione chiama **SQLSetConnectAttr** per impostare SQL_ATTR_TRACE su SQL_TRACE_OFF. Questa chiamata disattiva la traccia solo per l'applicazione. Le applicazioni collegate con odbc32. lib possono modificare l'uso di questa variabile. I dati di traccia possono essere visualizzati in una finestra in tempo reale, anziché nel file di traccia, che deve essere aperto dopo la sessione ODBC. I controlli possono essere aggiunti alla schermata di un'applicazione per attivare o disattivare la traccia in corrispondenza di.  
  
 La DLL di traccia fornita con ODBC 3 *. x* non è thread-safe. Non è garantito che il file di log venga scritto correttamente se è abilitata la traccia globale (la variabile **ODBCSharedTraceFlag** è impostata) e più di un'applicazione scrive nel file di traccia nello stesso momento. Questa condizione non restituisce un errore.
