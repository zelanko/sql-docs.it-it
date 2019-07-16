---
title: Gli attributi di istruzione | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c74f1a79ef79b682bc2900d671e07bbe34c4dbf5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107268"
---
# <a name="statement-attributes"></a>Attributi di istruzione
Gli attributi di istruzione sono caratteristiche dell'istruzione. Ad esempio, se usare i segnalibri e ciò che tipo di cursore da utilizzare con il risultato dell'istruzione set sono gli attributi di istruzione.  
  
 Gli attributi di istruzione sono impostati con **SQLSetStmtAttr** e le relative impostazioni correnti recuperati con **SQLGetStmtAttr**. Non è necessario che un'applicazione impostare eventuali attributi di istruzione. tutti gli attributi di istruzione hanno impostazioni predefinite, alcune delle quali sono specifici del driver.  
  
 Quando un attributo di istruzione può essere impostato dipende l'attributo stesso. Gli attributi di istruzione SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR e SQL_ATTR_USE_BOOKMARKS devono essere impostati prima che venga eseguita l'istruzione. Gli attributi di istruzione SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_NOSCAN possono essere impostati in qualsiasi momento, ma non vengono applicati fino a quando non viene utilizzata nuovamente l'istruzione. Gli attributi di istruzione SQL_ATTR_MAX_LENGTH e SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT possono essere impostati in qualsiasi momento, ma è specifico del driver che vengono applicati prima che venga utilizzato nuovamente l'istruzione. In qualsiasi momento, è possono impostare gli attributi di istruzione rimanenti.  
  
> [!NOTE]  
>  La possibilità di impostare gli attributi di istruzione a livello di connessione chiamando **SQLSetConnectAttr** è stata deprecata in ODBC 3. *x*. ODBC 3. *x* applicazioni non devono mai impostato gli attributi di istruzione a livello di connessione. ODBC 3. *x* i driver necessitano supportano questa funzionalità solo se funzionano con l'API ODBC 2. *x* applicazioni. Per altre informazioni, vedere [Mapping di SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
>   
>  Un'eccezione è gli attributi SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, che sono entrambi gli attributi di connessione e gli attributi di istruzione e possono essere impostati a livello di connessione o il livello di istruzione.  
>   
>  Nessuno degli attributi di istruzione introdotti in ODBC 3. *x* (tranne SQL_ATTR_METADATA_ID) possono essere impostati a livello di connessione.  
  
 Per altre informazioni, vedere la [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descrizione della funzione.
