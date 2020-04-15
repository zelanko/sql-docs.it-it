---
title: Recupero di segnalibri Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d146b2fb9bfc0e7294709e971f1b6752dc99ab3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300071"
---
# <a name="retrieving-bookmarks"></a>Recupero di segnalibri
Se l'applicazione utilizzerà i segnalibri, deve impostare l'attributo dell'istruzione SQL_ATTR_USE_BOOKMARKS su SQL_UB_VARIABLE prima di preparare o eseguire l'istruzione. Ciò è necessario perché la creazione e la gestione dei segnalibri può essere un'operazione costosa, pertanto i segnalibri devono essere abilitati solo quando un'applicazione può utilizzarli in modo corretto.  
  
 I segnalibri vengono restituiti come colonna 0 del set di risultati. Esistono tre modi in cui un'applicazione può recuperarli:There are three ways an application can retrieve them:  
  
-   Associare la colonna 0 del set di risultati. **SQLFetch** o **SQLFetchScroll** restituisce i segnalibri per ogni riga nel set di righe insieme ai dati per altre colonne associate.  
  
-   Chiamare **SQLSetPos** per posizionare su una riga nel set di righe e quindi chiamare SQLGetData per la colonna 0.Call SQLSetPos to position to a row in the rowset and then call **SQLGetData** for column 0. Se un driver supporta i segnalibri, deve sempre supportare la possibilità di chiamare **SQLGetData** per la colonna 0, anche se non consente alle applicazioni di chiamare **SQLGetData** per altre colonne prima dell'ultima colonna associata.  
  
-   Chiamare **SQLBulkOperations** con l'argomento *Operation* impostato su SQL_ADD e la colonna 0 associata. Il cursore inserisce la riga e restituisce il segnalibro per la riga nel buffer associato.
