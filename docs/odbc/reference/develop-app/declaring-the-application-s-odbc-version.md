---
title: Dichiarazione dell'applicazione&#39;versione ODBC di s Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba346ed7f7a261446110c5513026d20a86fd3a19
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285231"
---
# <a name="declaring-the-application39s-odbc-version"></a>Dichiarazione della versione ODBC di Application&#39;sDeclaring the Application&#39;s ODBC Version
Prima che un'applicazione allochi una connessione, è necessario impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION. Questo attributo indica che l'applicazione segue la specifica ODBC *2.x* o ODBC *3.x* quando si utilizzano i seguenti elementi:  
  
-   **SQLSTATEs**. Molti valori SQLSTATE sono diversi in ODBC *2.x* e ODBC *3.x*.  
  
-   **Identificatori**di tipo data, ora e timestamp . Nella tabella seguente vengono illustrati gli identificatori di tipo per i dati di data, ora e timestamp in ODBC *2.x* e ODBC *3.x*.  
  
    |ODBC *2.x*|ODBC *3.x*|  
    |----------------|----------------|  
    |**Identificatori dei tipi SQL**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**Identificatori di tipo C**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _CatalogName_  **Argomento in SQLTables**. In ODBC *2.x*i caratteri jolly ("%" e "_") nell'argomento *CatalogName* vengono trattati letteralmente. In ODBC *3.x*, vengono considerati come caratteri jolly. Pertanto, un'applicazione che segue la specifica ODBC *2.x* non può utilizzarli come caratteri jolly e non ne esegue l'escape quando vengono utilizzati come valori letterali. Un'applicazione che segue la specifica ODBC *3.x* può utilizzarli come caratteri jolly o eseguire l'escape e utilizzarli come valori letterali. Per ulteriori informazioni, vedere [Argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 I driver ODBC *3.x* Driver Manager e ODBC *3.x* controllano la versione della specifica ODBC in cui un'applicazione viene scritta e rispondono di conseguenza. Ad esempio, se l'applicazione segue la specifica ODBC *2.x* e chiama **SQLExecute** prima di chiamare **SQLPrepare**, Gestione Driver ODBC *3.x* restituisce SQLSTATE S1010 (errore di sequenza di funzioni). Se l'applicazione segue la specifica ODBC *3.x,* Gestione Driver restituisce SQLSTATE HY010 (errore di sequenza di funzione). Per ulteriori informazioni, vedere [Compatibilità con le versioni precedenti e conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Le applicazioni che seguono la specifica ODBC *3.x* devono utilizzare codice condizionale per evitare di utilizzare funzionalità nuove di ODBC *3.x* quando si utilizzano driver ODBC *2.x.* I driver ODBC *2.x* non supportano la funzionalità nuova di ODBC *3.x* solo perché l'applicazione dichiara di segue la specifica ODBC *3.x.* Inoltre, i driver ODBC *3.x* non cessano di supportare la funzionalità nuova di ODBC *3.x* solo perché l'applicazione dichiara di segue la specifica ODBC *2.x.*
