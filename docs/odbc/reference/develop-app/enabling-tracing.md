---
title: Abilitazione della traccia | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80bd4023a0260b67d11d7b4ded1bb810b81e0ab2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287351"
---
# <a name="enabling-tracing"></a>Abilitazione della traccia
La traccia può essere abilitata nei tre modi seguenti:  
  
-   Impostare le parole chiave **Trace** e **TraceFile** nella voce del registro di sistema ODBC. ini. In questo modo viene abilitata o disabilitata la traccia quando viene chiamato **SQLAllocHandle** con *HandleType* SQL_HANDLE_ENV. Queste opzioni vengono impostate nella scheda traccia della finestra di dialogo Amministrazione origine dati ODBC visualizzata durante la configurazione dell'origine dati. Per ulteriori informazioni, vedere [voci del registro di sistema per le origini dati](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chiamare **SQLSetConnectAttr** per impostare l'attributo di connessione SQL_ATTR_TRACE su SQL_OPT_TRACE_ON. In questo modo viene abilitata o disabilitata la traccia per la durata della connessione. Per ulteriori informazioni, vedere la descrizione della funzione [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) .  
  
-   Usare **ODBCSharedTraceFlag** per attivare o disattivare la traccia in modo dinamico. Per ulteriori informazioni, vedere l'argomento successivo, [traccia dinamica](../../../odbc/reference/develop-app/dynamic-tracing.md).
