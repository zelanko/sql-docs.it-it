---
title: Liberare un'istruzione Handle ODBC . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01e4cb46edf1b1a0f1c6dfaa0273c1dd5b392686
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305616"
---
# <a name="freeing-a-statement-handle-odbc"></a>Rilascio di un handle di istruzione ODBC
Come accennato in precedenza, è più efficiente riutilizzare le istruzioni piuttosto che eliminarle e allocarne di nuove. Prima di eseguire una nuova istruzione SQL in un'istruzione, le applicazioni devono assicurarsi che le impostazioni dell'istruzione corrente siano appropriate. Tra le impostazioni sono inclusi gli attributi di istruzione, le associazioni di parametri e le associazioni dei set di risultati. In genere, i parametri e i set di risultati per l'istruzione SQL precedente devono essere non associati (chiamando **SQLFreeStmt** con le opzioni SQL_RESET_PARAMS e SQL_UNBIND) e riassociati per la nuova istruzione SQL.  
  
 Quando l'applicazione ha terminato di utilizzare l'istruzione, chiama **SQLFreeHandle** per liberare l'istruzione. Dopo aver liberato l'istruzione, è un errore di programmazione dell'applicazione utilizzare l'handle dell'istruzione in una chiamata a una funzione ODBC; così facendo ha conseguenze indefinite, ma probabilmente fatali.  
  
 Quando **SQLFreeHandle** viene chiamato, il driver rilascia la struttura utilizzata per archiviare le informazioni sull'istruzione.  
  
 **SQLDisconnect** libera automaticamente tutte le istruzioni in una connessione.
