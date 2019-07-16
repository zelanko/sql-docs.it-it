---
title: Rilascio di un Handle di istruzione ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 638cf9fb3c7af73130cf1413559b9baee2a354c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069783"
---
# <a name="freeing-a-statement-handle-odbc"></a>Rilascio di un handle di istruzione ODBC
Come accennato in precedenza, è più efficiente riutilizzare le istruzioni di to eliminarli e allocarne di nuovi. Prima di eseguire una nuova istruzione SQL in un'istruzione, le applicazioni devono assicurarsi che le impostazioni delle istruzioni correnti siano appropriate. Tra le impostazioni sono inclusi gli attributi di istruzione, le associazioni di parametri e le associazioni dei set di risultati. In generale, i parametri e set di risultati per l'istruzione SQL precedente devono essere non associata (chiamando **SQLFreeStmt** con le opzioni SQL_RESET_PARAMS e SQL_UNBIND) e riassociato per la nuova istruzione SQL.  
  
 Quando l'applicazione ha terminato di utilizzare l'istruzione, viene chiamato **la funzione SQLFreeHandle** per liberare l'istruzione. Dopo avere liberato l'istruzione, è un'applicazione di un errore di programmazione da usare l'handle di istruzione in una chiamata a una funzione ODBC; Questa operazione ha conseguenze non definiti, ma probabilmente irreversibile.  
  
 Quando **SQLFreeHandle** viene chiamato, le versioni di driver la struttura utilizzata per archiviare le informazioni sull'istruzione.  
  
 **SQLDisconnect** libera automaticamente tutte le istruzioni in una connessione.
