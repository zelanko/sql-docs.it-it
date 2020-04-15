---
title: Recupero dei risultati (base) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f7d01bf92fcee07940e449a2fb4bbac4f0fe6ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304332"
---
# <a name="retrieving-results-basic"></a>Recupero di risultati (di base)
Un set di *risultati* è un set di righe nell'origine dati che corrisponde a determinati criteri. Si tratta di una tabella concettuale risultante da una query e disponibile per un'applicazione in formato tabulare. Le istruzioni **SELECT,** le funzioni di catalogo e alcune procedure creano set di risultati. Nell'esempio seguente, la prima istruzione SQL crea un set di risultati contenente tutte le righe e tutte le colonne della tabella Orders e la seconda istruzione SQL crea un set di risultati contenente le colonne OrderID, SalesPerson e Status per le righe della tabella Orders in cui lo stato è APERTO:  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 Un set di risultati può essere vuoto, che è diverso da nessun set di risultati. Ad esempio, l'istruzione SQL seguente crea un set di risultati vuoto:For example, the following SQL statement creates an empty result set:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 Un set di risultati vuoto non è diverso da qualsiasi altro set di risultati, ad eccezione del fatto che non contiene righe. Ad esempio, l'applicazione può recuperare i metadati per il set di risultati, può tentare di recuperare le righe e deve chiudere il cursore sul set di risultati.  
  
 Il processo di recupero delle righe dall'origine dati e di restituzione all'applicazione è denominato *recupero*. In questa sezione vengono illustrate le parti di base di tale processo. Per informazioni su argomenti più avanzati, ad esempio cursori a blocchi e scorrevoli, vedere [Cursori](../../../odbc/reference/develop-app/block-cursors.md) a blocchi e [Cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md). Per informazioni sull'aggiornamento, l'eliminazione e l'inserimento di righe, vedere [Panoramica dell'aggiornamento dei dati](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Verifica della creazione di un set di risultati](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [Metadati del set di risultati](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [Associazione di colonne](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [Recupero di dati](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [Chiusura del cursore](../../../odbc/reference/develop-app/closing-the-cursor.md)
