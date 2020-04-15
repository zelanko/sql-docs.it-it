---
title: Parametri dell'Istruzione . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02327ff4bb6a1ac3ac57fbf7d3c6b09b70c11534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306822"
---
# <a name="statement-parameters"></a>Parametri delle istruzioni
Un *parametro* è una variabile in un'istruzione SQL. Si supponga, ad esempio, che una tabella Parts condisponga di colonne denominate PartID, Description e Price. Per aggiungere una parte senza parametri sarebbe necessario costruire un'istruzione SQL come:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Anche se questa istruzione inserisce un nuovo ordine, non è una buona soluzione per un'applicazione di immissione ordini perché i valori da inserire non possono essere hardcoded nell'applicazione. Un'alternativa consiste nel costruire l'istruzione SQL in fase di esecuzione, utilizzando i valori da inserire. Anche questa non è una buona soluzione, a causa della complessità della costruzione di istruzioni in fase di esecuzione. La soluzione migliore consiste nel sostituire gli elementi della clausola **VALUES** con punti interrogativi (?) o *indicatori di parametro:*  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Gli indicatori di parametro vengono quindi associati a variabili dell'applicazione. Per aggiungere una nuova riga, l'applicazione deve solo impostare i valori delle variabili ed eseguire l'istruzione. Il driver recupera quindi i valori correnti delle variabili e li invia all'origine dati. Se l'istruzione verrà eseguita più volte, l'applicazione può rendere il processo ancora più efficiente preparando l'istruzione.  
  
 L'istruzione appena illustrata potrebbe essere hardcoded in un'applicazione di immissione ordini per inserire una nuova riga. Tuttavia, gli indicatori di parametro non sono limitati alle applicazioni verticali. Per qualsiasi applicazione, semplificano la difficoltà di costruire istruzioni SQL in fase di esecuzione evitando le conversioni da e verso il testo. Ad esempio, l'ID parte appena visualizzato viene probabilmente archiviato nell'applicazione come numero intero. Se l'istruzione SQL viene costruita senza indicatori di parametro, l'applicazione deve convertire l'ID parte in testo e l'origine dati deve riconvertirlo in un numero intero. Utilizzando un indicatore di parametro, l'applicazione può inviare l'ID parte al driver come numero intero, che in genere può inviarlo all'origine dati come numero intero. In questo modo vengono salvate due conversioni. Per valori di dati lunghi, questo è molto importante, perché le forme di testo di tali valori spesso superano la lunghezza consentita di un'istruzione SQL.  
  
 I parametri sono validi solo in determinate posizioni nelle istruzioni SQL. Ad esempio, non sono consentiti nell'elenco di selezione (l'elenco di colonne che deve essere restituito da un'istruzione **SELECT),** né sono consentiti come entrambi gli operandi di un operatore binario, ad esempio il segno di uguale ,), perché sarebbe impossibile determinare il tipo di parametro. In genere, i parametri sono validi solo nelle istruzioni DML (Data Manipulation Language) e non nelle istruzioni DDL (Data Definition Language). Per altre informazioni, vedere indicatori di [parametro](../../../odbc/reference/appendixes/parameter-markers.md) nell'Appendice C: grammatica SQL.  
  
 Quando l'istruzione SQL richiama una routine, è possibile utilizzare parametri denominati. I parametri denominati sono identificati dai relativi nomi, non dalla loro posizione nell'istruzione SQL. Possono essere associati da una chiamata a **SQLBindParameter**, ma il parametro è identificato dal campo SQL_DESC_NAME dell'IPD (descrittore del parametro di implementazione), non dall'argomento *ParameterNumber* di **SQLBindParameter**. Possono inoltre essere associati chiamando **SQLSetDescField** o **SQLSetDescRec**. Per ulteriori informazioni sui parametri denominati, vedere [Associazione di parametri in base al nome (parametri denominati)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)più avanti in questa sezione. Per ulteriori informazioni sui descrittori, vedere [Descrittori](../../../odbc/reference/develop-app/descriptors.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di parametri](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Configurazione dei valori dei parametri](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Recupero dei parametri di output tramite SQLGetDataRetrieving Output Parameters by SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Parametri di procedure](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Matrici di valori di parametro](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
