---
title: Attributi di istruzione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec24cc43e8c57e47ddda9f20fac1807f42453e84
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299644"
---
# <a name="statement-attributes"></a>Attributi di istruzione
Gli attributi di istruzione sono caratteristiche dell'istruzione. Se, ad esempio, si desidera utilizzare i segnalibri e il tipo di cursore da utilizzare con il set di risultati dell'istruzione sono gli attributi di istruzione.  
  
 Gli attributi di istruzione vengono impostati con **SQLSetStmtAttr** e le impostazioni correnti recuperate con **SQLGetStmtAttr**. Non è necessario che un'applicazione imposti attributi di istruzione. per tutti gli attributi di istruzione sono disponibili impostazioni predefinite, alcune delle quali sono specifiche del driver.  
  
 Quando è possibile impostare un attributo di istruzione dipende dall'attributo stesso. È necessario impostare gli attributi dell'istruzione SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR e SQL_ATTR_USE_BOOKMARKS prima dell'esecuzione dell'istruzione. Gli attributi dell'istruzione SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_NOSCAN possono essere impostati in qualsiasi momento, ma non vengono applicati fino a quando l'istruzione non viene riutilizzata. Gli attributi di istruzione SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS e SQL_ATTR_QUERY_TIMEOUT possono essere impostati in qualsiasi momento, ma sono specifici del driver se vengono applicati prima che l'istruzione venga riutilizzata. Gli attributi di istruzione rimanenti possono essere impostati in qualsiasi momento.  
  
> [!NOTE]  
>  La possibilità di impostare gli attributi di istruzione a livello di connessione chiamando **SQLSetConnectAttr** è stata deprecata in ODBC 3. *x*. ODBC 3. le applicazioni *x* non devono mai impostare gli attributi di istruzione a livello di connessione. ODBC 3. i driver *x* devono supportare questa funzionalità solo se dovrebbero funzionare con ODBC 2. applicazioni *x* . Per ulteriori informazioni, vedere [SQLSetConnectOption mapping](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) in Appendice G: linee guida sui driver per la compatibilità con le versioni precedenti.  
>   
>  Un'eccezione è rappresentata dagli attributi SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, ovvero attributi di connessione e attributi di istruzione, che possono essere impostati a livello di connessione o di istruzione.  
>   
>  Nessuno degli attributi di istruzione introdotti in ODBC 3. è possibile impostare *x* (ad eccezione di SQL_ATTR_METADATA_ID) a livello di connessione.  
  
 Per ulteriori informazioni, vedere la descrizione della funzione [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) .
