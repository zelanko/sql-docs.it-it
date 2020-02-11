---
title: Recupero di risultati (di base) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abe4dd2f0bfb0b5302022d8e50cddc7df84f192
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020475"
---
# <a name="retrieving-results-basic"></a>Recupero di risultati (di base)
Un *set di risultati* è un set di righe nell'origine dati che corrisponde a determinati criteri. Si tratta di una tabella concettuale risultante da una query che è disponibile per un'applicazione in formato tabulare. Istruzioni **Select** , funzioni di catalogo e alcune procedure per la creazione di set di risultati. Nell'esempio seguente, la prima istruzione SQL crea un set di risultati contenente tutte le righe e tutte le colonne della tabella Orders e la seconda istruzione SQL crea un set di risultati contenente le colonne OrderID, SalesPerson e status per le righe della tabella Orders. in cui lo stato è aperto:  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 Un set di risultati può essere vuoto, che è diverso da nessun set di risultati. L'istruzione SQL seguente, ad esempio, crea un set di risultati vuoto:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 Un set di risultati vuoto non è diverso da qualsiasi altro set di risultati, ad eccezione del fatto che non contiene righe. Ad esempio, l'applicazione può recuperare i metadati per il set di risultati, può tentare di recuperare le righe ed è necessario chiudere il cursore sul set di risultati.  
  
 Il processo di recupero delle righe dall'origine dati e della relativa restituzione all'applicazione viene chiamato *recupero*. In questa sezione vengono illustrate le parti di base di tale processo. Per informazioni sugli argomenti più avanzati, ad esempio i cursori Block e scroll [, vedere cursori e cursori](../../../odbc/reference/develop-app/block-cursors.md) [scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md). Per informazioni sull'aggiornamento, l'eliminazione e l'inserimento di righe, vedere [Cenni preliminari sull'aggiornamento dei dati](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Verifica della creazione di un set di risultati](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [Metadati del set di risultati](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [Associazione di colonne](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [Recupero di dati](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [Chiusura del cursore](../../../odbc/reference/develop-app/closing-the-cursor.md)
