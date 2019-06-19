---
title: Recupero di segnalibri | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d7d4bd52a5f6e5b03a084cef4402e0a9044f97d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861401"
---
# <a name="retrieving-bookmarks"></a>Recupero di segnalibri
Se l'applicazione utilizzerà i segnalibri, è necessario impostare l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE prima di preparazione o l'esecuzione dell'istruzione. Ciò è necessario perché creare e gestire i segnalibri possono essere un'operazione dispendiosa, in modo che i segnalibri devono essere abilitati solo quando un'applicazione può rendere buona loro utilizzo.  
  
 I segnalibri vengono restituiti come colonna 0 nel set di risultati. Esistono tre modi che possibile recuperarle in un'applicazione:  
  
-   Eseguire l'associazione colonna 0 nel set di risultati. **SQLFetch** oppure **SQLFetchScroll** restituisce i segnalibri per ogni riga nel set di righe con i dati per altri colonne associate.  
  
-   Chiamare **SQLSetPos** posizionarsi su una riga nel set di righe, quindi chiamare **SQLGetData** per la colonna 0. Se un driver supporta segnalibri, deve sempre supportare la possibilità di chiamare **SQLGetData** per la colonna 0, anche se non consente alle applicazioni di chiamare **SQLGetData** per le altre colonne prima l'ultimo associato a colonna.  
  
-   Chiamare **SQLBulkOperations** con il *operazione* argomento impostato su SQL_ADD e alla colonna 0 associato. Il cursore viene inserita la riga e restituisce il segnalibro per la riga nel buffer associato.
