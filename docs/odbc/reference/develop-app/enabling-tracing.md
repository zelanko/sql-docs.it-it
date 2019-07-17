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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046788"
---
# <a name="enabling-tracing"></a>Abilitazione della traccia
La traccia può essere abilitata nelle risorse seguenti tre modi:  
  
-   Impostare il **traccia** e **TraceFile** parole chiave nella voce del Registro di sistema ODBC. ini. Questo Abilita o disabilita la traccia quando **SQLAllocHandle** con un *HandleType* SQL_HANDLE_ENV viene chiamato. Queste opzioni vengono impostate nella scheda traccia della finestra di dialogo Amministrazione origine dati ODBC visualizzata durante l'installazione di origine dati. Per altre informazioni, vedere [le voci del Registro di sistema per le origini dati](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chiamare **SQLSetConnectAttr** su cui impostare l'attributo di connessione SQL_ATTR_TRACE SQL_OPT_TRACE_ON. Questo Abilita o disabilita la traccia per la durata della connessione. Per altre informazioni, vedere la [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descrizione della funzione.  
  
-   Uso **ODBCSharedTraceFlag** per attivare o disattivare la traccia in modo dinamico. (Per altre informazioni, vedere l'argomento successivo [traccia dinamica](../../../odbc/reference/develop-app/dynamic-tracing.md).)
