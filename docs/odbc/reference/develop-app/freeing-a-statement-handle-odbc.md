---
description: Rilascio di un handle di istruzione ODBC
title: Rilascio di un handle di istruzione ODBC | Microsoft Docs
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
ms.openlocfilehash: d199d00c007abc6836755f5a78e93e3fd85b140b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461463"
---
# <a name="freeing-a-statement-handle-odbc"></a>Rilascio di un handle di istruzione ODBC
Come indicato in precedenza, è più efficiente riutilizzare le istruzioni anziché eliminarle e allocarne di nuove. Prima di eseguire una nuova istruzione SQL su un'istruzione, le applicazioni devono assicurarsi che le impostazioni dell'istruzione corrente siano appropriate. Tra le impostazioni sono inclusi gli attributi di istruzione, le associazioni di parametri e le associazioni dei set di risultati. In genere, i parametri e i set di risultati per l'istruzione SQL precedente devono essere non associati (chiamando **SQLFreeStmt** con le opzioni SQL_RESET_PARAMS e SQL_UNBIND) e riassociati per la nuova istruzione SQL.  
  
 Al termine dell'utilizzo dell'istruzione, l'applicazione chiama **SQLFreeHandle** per liberare l'istruzione. Una volta liberata l'istruzione, si tratta di un errore di programmazione dell'applicazione per l'utilizzo dell'handle dell'istruzione in una chiamata a una funzione ODBC. Questa operazione ha conseguenze indefinite ma probabilmente fatali.  
  
 Quando viene chiamato **SQLFreeHandle** , il driver rilascia la struttura utilizzata per archiviare le informazioni sull'istruzione.  
  
 **Disconnect** libera automaticamente tutte le istruzioni in una connessione.
