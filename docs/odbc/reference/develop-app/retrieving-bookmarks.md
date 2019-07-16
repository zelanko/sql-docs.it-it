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
ms.openlocfilehash: f18b87adf31f19d2a93bb3af3e14c265ae3940af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020569"
---
# <a name="retrieving-bookmarks"></a>Recupero di segnalibri
Se l'applicazione utilizzerà i segnalibri, è necessario impostare l'attributo di istruzione SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE prima di preparazione o l'esecuzione dell'istruzione. Ciò è necessario perché creare e gestire i segnalibri possono essere un'operazione dispendiosa, in modo che i segnalibri devono essere abilitati solo quando un'applicazione può rendere buona loro utilizzo.  
  
 I segnalibri vengono restituiti come colonna 0 nel set di risultati. Esistono tre modi che possibile recuperarle in un'applicazione:  
  
-   Eseguire l'associazione colonna 0 nel set di risultati. **SQLFetch** oppure **SQLFetchScroll** restituisce i segnalibri per ogni riga nel set di righe con i dati per altri colonne associate.  
  
-   Chiamare **SQLSetPos** posizionarsi su una riga nel set di righe, quindi chiamare **SQLGetData** per la colonna 0. Se un driver supporta segnalibri, deve sempre supportare la possibilità di chiamare **SQLGetData** per la colonna 0, anche se non consente alle applicazioni di chiamare **SQLGetData** per le altre colonne prima l'ultimo associato a colonna.  
  
-   Chiamare **SQLBulkOperations** con il *operazione* argomento impostato su SQL_ADD e alla colonna 0 associato. Il cursore viene inserita la riga e restituisce il segnalibro per la riga nel buffer associato.
