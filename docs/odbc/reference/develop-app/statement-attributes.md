---
title: Proprietà Statement Attributes . Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299644"
---
# <a name="statement-attributes"></a>Attributi di istruzione
Gli attributi dell'istruzione sono caratteristiche dell'istruzione. Ad esempio, se utilizzare i segnalibri e il tipo di cursore da utilizzare con il set di risultati dell'istruzione sono attributi dell'istruzione.  
  
 Gli attributi dell'istruzione vengono impostati con **SQLSetStmtAttr** e le relative impostazioni correnti recuperate con **SQLGetStmtAttr**. Non è necessario che un'applicazione imposti attributi di istruzione; tutti gli attributi di istruzione hanno valori predefiniti, alcuni dei quali sono specifici del driver.  
  
 Quando è possibile impostare un attributo di istruzione dipende dall'attributo stesso. Gli attributi di istruzione SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR e SQL_ATTR_USE_BOOKMARKS devono essere impostati prima dell'esecuzione dell'istruzione. Gli attributi di istruzione SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_NOSCAN possono essere impostati in qualsiasi momento, ma non vengono applicati fino a quando l'istruzione non viene utilizzata nuovamente. SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS e SQL_ATTR_QUERY_TIMEOUT attributi di istruzione possono essere impostati in qualsiasi momento, ma è specifico del driver se vengono applicati prima che l'istruzione viene utilizzata nuovamente. Gli attributi dell'istruzione rimanenti possono essere impostati in qualsiasi momento.  
  
> [!NOTE]  
>  La possibilità di impostare gli attributi dell'istruzione a livello di connessione chiamando **SQLSetConnectAttr** è stata deprecata in ODBC 3. *x*. ODBC 3. *X* le applicazioni non devono mai impostare gli attributi di istruzione a livello di connessione. ODBC 3. *x* driver devono supportare questa funzionalità solo se devono funzionare con ODBC 2. *applicazioni x.* Per altre informazioni, vedere [Mapping di SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) nell'appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti.  
>   
>  Un'eccezione è il SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE attributi, che sono entrambi attributi di connessione e attributi di istruzione e possono essere impostati a livello di connessione o a livello di istruzione.  
>   
>  Nessuno degli attributi dell'istruzione introdotti in ODBC 3. *x* (ad eccezione di SQL_ATTR_METADATA_ID) può essere impostato a livello di connessione.  
  
 Per altre informazioni, vedere la descrizione della funzione [SQLSetStmtAttr.For](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) more information, see the SQLSetStmtAttr function description.
