---
title: Recupero dei risultati (avanzato) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca02b4ff911c8edff06b38d5341eeaa288cc194c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294641"
---
# <a name="retrieving-results-advanced"></a>Recupero di risultati (avanzato)
Un'applicazione può specificare che un offset viene aggiunto agli indirizzi del buffer di dati associati e gli indirizzi del buffer di lunghezza/indicatore corrispondenti quando vengono chiamati **SQLBulkOperations**, **SQLFetch** **, SQLFetchScroll**o **SQLSetPos** . I risultati di queste aggiunte determinano gli indirizzi utilizzati in queste operazioni.  
  
 Gli offset di binding consentono a un'applicazione di modificare le associazioni senza chiamare **SQLBindCol** per le colonne associate in precedenza. Una chiamata a **SQLBindCol** per riassociare i dati modifica l'indirizzo del buffer e il puntatore di lunghezza/indicatore. La riassociazione con un offset, d'altra parte, aggiunge semplicemente un offset all'indirizzo del buffer di dati associato esistente e all'indirizzo del buffer di lunghezza/indicatore. Quando vengono utilizzati gli offset, le associazioni sono un "modello" di come vengono disposti i buffer dell'applicazione e l'applicazione può spostare questo "modello" in diverse aree di memoria modificando l'offset. Un nuovo offset può essere specificato in qualsiasi momento e viene sempre aggiunto ai valori associati in origine.  
  
 Per specificare un offset di associazione, l'applicazione imposta l'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR sull'indirizzo di un buffer SQLINTEGER. Prima che l'applicazione chiami una funzione che utilizza le associazioni, ad esempio **SQLBulkOperations**, **SQLFetch** **, SQLFetchScroll**o **SQLSetPos**, inserisce un offset in byte in questo buffer, purché né l'indirizzo del buffer di dati sia 0 e purché la colonna associata sia nel set di risultati. La somma dell'indirizzo e dell'offset deve essere un indirizzo valido. Ciò significa che uno o entrambi l'offset e l'indirizzo a cui viene aggiunto l'offset possono non essere validi, purché la somma sia un indirizzo valido. L'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR è un puntatore in modo che il valore di offset possa essere applicato a più set di dati di associazione, tutti modificati modificando un valore di offset. Un'applicazione deve assicurarsi che il puntatore rimanga valido fino alla chiusura del cursore.  
  
> [!NOTE]  
>  Gli offset di associazione non sono supportati da ODBC 2. *x* driver.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Cursori rettangolari](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [Libreria di cursori ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md)
