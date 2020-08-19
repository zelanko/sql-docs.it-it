---
description: Abilitazione della traccia
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
ms.openlocfilehash: af9a78989a80124fb9a7f475edf17022e7942bde
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482984"
---
# <a name="enabling-tracing"></a>Abilitazione della traccia
La traccia può essere abilitata nei tre modi seguenti:  
  
-   Impostare le parole chiave **Trace** e **TraceFile** nella voce del registro di sistema Odbc.ini. In questo modo viene abilitata o disabilitata la traccia quando viene chiamato **SQLAllocHandle** con *HandleType* SQL_HANDLE_ENV. Queste opzioni vengono impostate nella scheda traccia della finestra di dialogo Amministrazione origine dati ODBC visualizzata durante la configurazione dell'origine dati. Per ulteriori informazioni, vedere [voci del registro di sistema per le origini dati](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Chiamare **SQLSetConnectAttr** per impostare l'attributo di connessione SQL_ATTR_TRACE su SQL_OPT_TRACE_ON. In questo modo viene abilitata o disabilitata la traccia per la durata della connessione. Per ulteriori informazioni, vedere la descrizione della funzione [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) .  
  
-   Usare **ODBCSharedTraceFlag** per attivare o disattivare la traccia in modo dinamico. Per ulteriori informazioni, vedere l'argomento successivo, [traccia dinamica](../../../odbc/reference/develop-app/dynamic-tracing.md).
