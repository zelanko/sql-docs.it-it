---
description: Recupero di risultati (avanzato)
title: Recupero dei risultati (avanzate) | Microsoft Docs
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
ms.openlocfilehash: 12f5c2ddd1e04b1aef96b7ef1544db9b58a9a58e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461373"
---
# <a name="retrieving-results-advanced"></a>Recupero di risultati (avanzato)
Un'applicazione può specificare che un offset viene aggiunto agli indirizzi del buffer dei dati associati e agli indirizzi di buffer di lunghezza/indicatore corrispondenti quando viene chiamato **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos** . I risultati di queste aggiunte determinano gli indirizzi utilizzati in queste operazioni.  
  
 Gli offset di binding consentono a un'applicazione di modificare i binding senza chiamare **SQLBindCol** per le colonne precedentemente associate. Una chiamata a **SQLBindCol** per riassociare i dati modifica l'indirizzo del buffer e il puntatore di lunghezza/indicatore. Il riassociazione con un offset, d'altra parte, aggiunge semplicemente un offset all'indirizzo del buffer dei dati associato esistente e all'indirizzo del buffer di lunghezza/indicatore. Quando si utilizzano gli offset, i binding sono un "modello" di come sono disposti i buffer dell'applicazione e l'applicazione può spostare questo "modello" in aree di memoria diverse modificando l'offset. Un nuovo offset può essere specificato in qualsiasi momento e viene sempre aggiunto ai valori associati originariamente.  
  
 Per specificare un offset di binding, l'applicazione imposta l'attributo dell'istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR sull'indirizzo di un buffer SQLINTEGER. Prima che l'applicazione chiami una funzione che usa i binding, ad esempio **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**, inserisce un offset in byte in questo buffer, purché né l'indirizzo del buffer di dati né l'indirizzo del buffer di lunghezza/indicatore è 0 e fino a quando la colonna associata è nel set di risultati. La somma dell'indirizzo e dell'offset deve essere un indirizzo valido. Ciò significa che sia l'offset che l'indirizzo a cui viene aggiunto l'offset possono essere non validi, purché la somma sia un indirizzo valido. L'attributo SQL_ATTR_ROW_BIND_OFFSET_PTR Statement è un puntatore in modo che il valore di offset possa essere applicato a più di un set di dati di associazione, che possono essere modificati cambiando un valore di offset. Un'applicazione deve verificare che il puntatore rimanga valido finché il cursore non viene chiuso.  
  
> [!NOTE]  
>  Gli offset di binding non sono supportati da ODBC 2. driver *x* .  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Cursori rettangolari](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [Libreria di cursori ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md)
