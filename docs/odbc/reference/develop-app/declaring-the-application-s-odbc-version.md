---
title: La dichiarazione dell'applicazione&#39;versione ODBC s | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c5bb124af74d1fa009a61237edb54a9c8baec74
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267686"
---
# <a name="declaring-the-application39s-odbc-version"></a>La dichiarazione dell'applicazione&#39;s versione ODBC
Prima di un'applicazione alloca una connessione, è necessario impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION. Questo attributo indica che l'applicazione segue di ODBC 2. *x* o ODBC 3. *x* specifica quando si usano gli elementi seguenti:  
  
-   **SQLSTATEs**. Numero di valori SQLSTATE è diverse in ODBC 2. *x* e ODBC 3. *x*.  
  
-   **Date, Time e gli identificatori di tipo Timestamp**. Nella tabella seguente mostra gli identificatori di tipo per data, ora e timestamp di ODBC 2. *x* e ODBC 3. *x*.  
  
    |ODBC 2.*x*|ODBC 3.*x*|  
    |----------------|----------------|  
    |**Identificatori dei tipi SQL**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**Identificatori di tipo C**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _CatalogName_**argomento nella SQLTables**. In ODBC 2. *x*, i caratteri jolly ("%" e "_") nel *CatalogName* argomento vengono trattati in modo letterale. In ODBC 3. *x*, essi vengono trattati come caratteri jolly. Di conseguenza, un'applicazione che segue di ODBC 2. *x* specifica non è possibile usarle come i caratteri jolly e non utilizzare caratteri di escape quando vengono utilizzati come valori letterali. Un'applicazione che segue il ODBC 3. *x* specifica può usare queste chiavi come caratteri jolly o utilizzare caratteri di escape e usarle come valori letterali. Per altre informazioni, vedere [argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 ODBC 3 *. x* gestione Driver mentre ODBC 3*x* i driver di controllare la versione della specifica di ODBC in cui verrà scritta un'applicazione e rispondere di conseguenza. Ad esempio, se l'applicazione segue di ODBC 2. *x* specification e le chiamate **SQLExecute** prima di chiamare **SQLPrepare**, ODBC 3*x* gestione Driver restituisce SQLSTATE S1010 ( Errore nella sequenza (funzione)). Se l'applicazione segue ODBC 3*x* specifica, gestione Driver restituisce SQLSTATE HY010 (funzione di errore nella sequenza). Per altre informazioni, vedere [garantire la compatibilità e conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Applicazioni che osservano ODBC 3. *x* specifica debba usare codice condizionale per evitare di utilizzare funzionalità nuove in ODBC 3. *x* quando si lavora con ODBC 2. *x* driver. ODBC 2. *x* driver non supportano funzionalità nuove in ODBC 3. *x* solo perché l'applicazione dichiara che segue il ODBC 3. *x* specifica. Inoltre, ODBC 3. *x* i driver non scade supportare la funzionalità nuova a ODBC 3. *x* solo perché l'applicazione dichiara che segue di ODBC 2. *x* specifica.
