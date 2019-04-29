---
title: Recupero dei risultati (avanzati) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5199fb82cbc6b2a9da644554db12dc525cc0be40
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62998898"
---
# <a name="retrieving-results-advanced"></a>Recupero di risultati (avanzato)
Un'applicazione può specificare che venga aggiunto un offset di associare gli indirizzi di buffer dei dati e di lunghezza/indicatore corrispondente buffer indirizzi quando **SQLBulkOperations**, **SQLFetch**,  **SQLFetchScroll**, oppure **SQLSetPos** viene chiamato. I risultati di queste aggiunte determinano gli indirizzi usati in queste operazioni.  
  
 Offset di associazione consentono a un'applicazione modificare le associazioni senza chiamare **SQLBindCol** per le colonne associate in precedenza. Una chiamata a **SQLBindCol** per riassociare i dati viene modificato l'indirizzo del buffer e il puntatore di lunghezza/indicatore. Riassociazione con un offset, d'altra parte, semplicemente aggiunge un offset all'indirizzo di buffer di dati associati esistenti e indirizzo di buffer di lunghezza/indicatore. Quando vengono utilizzati gli offset, le associazioni sono un "modello" della modalità di disposizione i buffer dell'applicazione e l'applicazione può passare questa "modello" a diverse aree di memoria tramite la modifica dell'offset. Un nuovo offset può essere specificato in qualsiasi momento e viene sempre aggiunto ai valori originariamente associati.  
  
 Per specificare un offset di associazione, l'applicazione imposta l'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR all'indirizzo di un buffer SQLINTEGER. Prima che l'applicazione chiama una funzione che utilizza le associazioni, ad esempio **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**, che inserisce un offset in byte di questo buffer, purché l'indirizzo del buffer dei dati, né l'indirizzo del buffer di lunghezza/indicatore è 0, e, purché la colonna associata viene nel set di risultati. La somma dell'indirizzo e l'offset deve essere un indirizzo valido. (Ciò significa che uno o entrambi l'offset e l'indirizzo a cui viene aggiunta l'offset può essere valide, purché la somma è un indirizzo valido). L'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR è un puntatore in modo che il valore di offset può essere applicato a più di un set di dati, ognuno dei quali può essere modificato impostando un valore di offset di associazione. Un'applicazione deve verificare che il puntatore rimane valido fino a quando il cursore è chiuso.  
  
> [!NOTE]  
>  Offset di associazione non sono supportati da ODBC 2. *x* driver.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Cursori rettangolari](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [Libreria di cursori ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Risultati multipli](../../../odbc/reference/develop-app/multiple-results.md)
