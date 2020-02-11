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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 24f80e0e81e4be8895d59256492b868c53aab7b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046788"
---
# <a name="enabling-tracing"></a>Abilitazione della traccia
La traccia può essere abilitata nei tre modi seguenti:  
  
-   Impostare le parole chiave **Trace** e **TraceFile** nella voce del registro di sistema ODBC. ini. In questo modo viene abilitata o disabilitata la traccia quando viene chiamato **SQLAllocHandle** con *HandleType* SQL_HANDLE_ENV. Queste opzioni vengono impostate nella scheda traccia della finestra di dialogo Amministrazione origine dati ODBC visualizzata durante la configurazione dell'origine dati. Per ulteriori informazioni, vedere [voci del registro di sistema per le origini dati](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chiamare **SQLSetConnectAttr** per impostare l'attributo di connessione SQL_ATTR_TRACE su SQL_OPT_TRACE_ON. In questo modo viene abilitata o disabilitata la traccia per la durata della connessione. Per ulteriori informazioni, vedere la descrizione della funzione [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) .  
  
-   Usare **ODBCSharedTraceFlag** per attivare o disattivare la traccia in modo dinamico. Per ulteriori informazioni, vedere l'argomento successivo, [traccia dinamica](../../../odbc/reference/develop-app/dynamic-tracing.md).
