---
title: Abilitazione della traccia. Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287351"
---
# <a name="enabling-tracing"></a>Abilitazione della traccia
La traccia può essere abilitata nei tre modi seguenti:Tracing can be enabled in the following three ways:  
  
-   Impostare le parole chiave **Trace** e **TraceFile** nella voce del Registro di sistema Odbc.ini. In questo modo viene abilitata o disabilitata la traccia quando **SQLAllocHandle** con un *HandleType* di SQL_HANDLE_ENV viene chiamato. Queste opzioni vengono impostate nella scheda Traccia della finestra di dialogo Amministratore origine dati ODBC visualizzata durante l'impostazione dell'origine dati. Per ulteriori informazioni, vedere [Voci del Registro di sistema per le origini dati](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chiamare **SQLSetConnectAttr** per impostare l'attributo di connessione SQL_ATTR_TRACE su SQL_OPT_TRACE_ON. In questo modo viene abilitata o disabilitata la traccia per la durata della connessione. Per altre informazioni, vedere la descrizione della funzione [SQLSetConnectAttr.For](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) more information, see the SQLSetConnectAttr function description.  
  
-   Utilizzare **ODBCSharedTraceFlag** per attivare o disattivare la traccia in modo dinamico. Per ulteriori informazioni, vedere l'argomento successivo, [Traccia dinamica.](../../../odbc/reference/develop-app/dynamic-tracing.md)
