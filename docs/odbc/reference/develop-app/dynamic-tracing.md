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
manager: craigg
ms.openlocfilehash: 63dbfda01d96cad53e5830e598b5812ed79d8f04
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468778"
---
# <a name="dynamic-tracing"></a>Traccia dinamica
Traccia può essere abilitata o disabilitata in qualsiasi punto in un'esecuzione dell'applicazione. In questo modo un'applicazione per tenere traccia di qualsiasi numero di chiamate di funzione.  
  
 La variabile **ODBCSharedTraceFlag** è impostato per abilitare la traccia in modo dinamico. Questa variabile viene condivisa tra tutte le copie in esecuzione di gestione Driver. Se questa variabile viene impostata, qualsiasi applicazione traccia è abilitata per tutte le applicazioni ODBC attualmente in esecuzione. Per attivare la traccia off quando sono abilitato analisi dinamica, un'applicazione chiama **SQLSetConnectAttr** su cui impostare SQL_ATTR_TRACE SQL_TRACE_OFF. Questa chiamata attiva traccia per l'applicazione solo. Le applicazioni collegate con Odbc32.lib possono modificare questa variabile. I dati di traccia possono essere visualizzati in una finestra in tempo reale, anziché il file di traccia, che deve essere aperto dopo la sessione ODBC. Controlli possono essere aggiunti alla schermata di un'applicazione per attivare o disattivare la traccia in verrà.  
  
 La traccia DLL fornita con ODBC 3*x* non è thread-safe. Non è garantito che il file di log viene scritto in modo corretto se è abilitata la traccia globale (la variabile **ODBCSharedTraceFlag** è impostata) e più di un'applicazione scrive nel file di traccia nello stesso momento. Questa condizione non restituisce un errore.
