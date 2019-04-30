---
title: Parametri dell'istruzione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b366ddd7a665112e6b40b814b13037a517d623a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149359"
---
# <a name="statement-parameters"></a>Parametri delle istruzioni
Oggetto *parametro* è una variabile in un'istruzione SQL. Si supponga, ad esempio, che in una tabella con colonne denominate PartID, la descrizione e prezzo. Per aggiungere una parte senza parametri richiederebbe la costruzione di un'istruzione SQL, ad esempio:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Sebbene questa istruzione consente di inserire un nuovo ordine, non è un'ottima soluzione per un'applicazione di immissione dell'ordine perché i valori da inserire non possono essere impostate come hardcoded nell'applicazione. In alternativa è possibile costruire l'istruzione SQL in fase di esecuzione usando i valori da inserire. Non si tratta inoltre una buona soluzione, a causa della complessità di costruzione di istruzioni in fase di esecuzione. La soluzione migliore consiste nel sostituire gli elementi del **i valori** clausola dai punti interrogativi (?), o *marcatori di parametro*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Gli indicatori di parametro vengono quindi associati a variabili dell'applicazione. Per aggiungere una nuova riga, l'applicazione deve solo impostare i valori delle variabili ed eseguire l'istruzione. Il driver recupera quindi i valori correnti delle variabili e li invia all'origine dati. Se l'istruzione verrà eseguita più volte, l'applicazione può rendere ancora più efficiente il processo preparando l'istruzione.  
  
 L'istruzione appena illustrato potrebbe essere hardcoded in un'applicazione di immissione dell'ordine per inserire una nuova riga. Tuttavia, i marcatori di parametro non esistono applicazioni verticali. Per qualsiasi applicazione, consentono di semplificare le difficoltà di costruzione di istruzioni SQL in fase di esecuzione, evitando le conversioni da e verso il testo. Ad esempio, l'ID di parte appena illustrato è probabilmente archiviati nell'applicazione come integer. Se l'istruzione SQL viene costruita senza i marcatori di parametro, l'applicazione deve convertire l'ID di parte al testo e l'origine dati deve convertire i dati in un numero intero. Utilizzando un marcatore di parametro, l'applicazione può inviare l'ID di parte del driver come integer, che in genere possibile inviarlo all'origine dati come integer. In questo modo due conversioni. Per i valori di dati long, ciò è molto importante, perché le forme di testo di tali valori spesso superano la lunghezza consentita di un'istruzione SQL.  
  
 I parametri sono validi solo in determinate posizioni nelle istruzioni SQL. Ad esempio, non sono consentiti nell'elenco di selezione (l'elenco di colonne deve essere restituito da un **selezionare** istruzione), né sono consentiti come entrambi gli operandi dell'operatore binario, ad esempio il segno di uguale (=), poiché sarebbe impossibile ritestare per determinare il tipo di parametro. In generale, i parametri sono validi solo in istruzioni Data Manipulation Language (DML) e non nelle istruzioni Data Definition Language (DDL). Per altre informazioni, vedere [marcatori di parametro](../../../odbc/reference/appendixes/parameter-markers.md) nell'appendice c: Grammatica SQL.  
  
 Può essere usato quando l'istruzione SQL richiama una stored procedure, parametri denominata. I parametri denominati sono identificati dai relativi nomi, non in base alla posizione dell'istruzione SQL. Possono essere associate mediante una chiamata a **SQLBindParameter**, ma il parametro è identificato dal campo SQL_DESC_NAME del Descrittore (implementazione parametri), non dal *ParameterNumber* argomento di **SQLBindParameter**. Possono anche essere associate chiamando **SQLSetDescField** oppure **SQLSetDescRec**. Per altre informazioni sui parametri denominati, vedere [Binding Parameters by Name (Named Parameters)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md), più avanti in questa sezione. Per altre informazioni sui descrittori, vedere [descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di parametri](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Configurazione dei valori dei parametri](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Recupero di parametri di Output da SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Parametri di procedure](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Matrici di valori di parametro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
