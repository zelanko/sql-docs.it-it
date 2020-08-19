---
description: Dichiarazione della versione ODBC dell'applicazione&#39;s
title: Dichiarazione della versione ODBC dell'applicazione&#39;s | Microsoft Docs
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
ms.openlocfilehash: 0ff41a7a8b56133b0a44947980805c5b46238bad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424722"
---
# <a name="declaring-the-application39s-odbc-version"></a>Dichiarazione della versione ODBC dell'applicazione&#39;s
Prima di allocare una connessione, un'applicazione deve impostare l'attributo dell'ambiente SQL_ATTR_ODBC_VERSION. Questo attributo indica che l'applicazione segue la specifica ODBC *2. x* o ODBC *3. x* quando si utilizzano gli elementi seguenti:  
  
-   **Sqlstates**. Molti valori SQLSTATE sono diversi in ODBC *2. x* e ODBC *3. x*.  
  
-   **Identificatori di tipo data, ora e timestamp**. Nella tabella seguente vengono illustrati gli identificatori di tipo per i dati di data, ora e timestamp in ODBC *2. x* e ODBC *3. x*.  
  
    |ODBC *2. x*|ODBC *3. x*|  
    |----------------|----------------|  
    |**Identificatori dei tipi SQL**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**Identificatori di tipi C**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   Argomento _CatalogName_**in SQLTables**.   In ODBC *2. x*, i caratteri jolly ("%" e "_") nell'argomento *CatalogName* vengono trattati letteralmente. In ODBC *3. x*vengono considerati caratteri jolly. Pertanto, un'applicazione che segue la specifica ODBC *2. x* non può utilizzarle come caratteri jolly e non ne esegue l'escape quando vengono utilizzate come valori letterali. Un'applicazione che segue la specifica ODBC *3. x* può usarla come caratteri jolly o come escape e usarla come valori letterali. Per ulteriori informazioni, vedere [arguments in Catalog Functions](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 I driver ODBC *3. x* driver Manager e ODBC *3. x* controllano la versione della specifica ODBC in cui un'applicazione viene scritta e rispondono di conseguenza. Se, ad esempio, l'applicazione segue la specifica ODBC *2. x* e chiama **SQLExecute** prima di chiamare **SQLPrepare**, gestione driver ODBC *3. x* restituisce SQLSTATE S1010 (errore della sequenza di funzioni). Se l'applicazione segue la specifica ODBC *3. x* , gestione driver restituisce SQLSTATE HY010 (errore della sequenza di funzioni). Per altre informazioni, vedere [compatibilità con le versioni precedenti e conformità agli standard](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
> [!IMPORTANT]  
>  Le applicazioni che seguono la specifica ODBC *3. x* devono utilizzare il codice condizionale per evitare l'utilizzo di funzionalità nuove di ODBC *3. x* quando si utilizzano i driver ODBC *2. x* . I driver ODBC *2. x* non supportano le nuove funzionalità di ODBC *3.* x solo perché l'applicazione dichiara che segue la specifica ODBC *3. x* . Inoltre, i driver ODBC *3. x* non smettono di supportare la nuova funzionalità di ODBC *3. x* solo perché l'applicazione dichiara che segue la specifica ODBC *2. x* .
