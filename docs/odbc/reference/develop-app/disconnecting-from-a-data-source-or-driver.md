---
title: Disconnessione da un'origine dati o da un driver Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- disconnecting from driver [ODBC]
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
- connecting to data source [ODBC], disconnecting
- connecting to driver [ODBC], disconnecting
- ODBC drivers [ODBC], disconnecting
ms.assetid: 83dbf0bf-b400-41fb-8537-9b016050dc3c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 154a571bce3a337d539216ce89c32420ab981bd8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300461"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Disconnessione da un'origine dati o driver
Quando un'applicazione ha terminato di utilizzare un'origine dati, chiama **SQLDisconnect**. **SQLDisconnect** libera tutte le istruzioni allocate nella connessione e disconnette il driver dall'origine dati. Restituisce un errore se una transazione è in corso.  
  
 Dopo la disconnessione, l'applicazione può chiamare **SQLFreeHandle** per liberare la connessione. Dopo aver liberato la connessione, è un errore di programmazione dell'applicazione utilizzare l'handle della connessione in una chiamata a una funzione ODBC; così facendo ha conseguenze indefinite, ma probabilmente fatali. Quando **SQLFreeHandle** viene chiamato, il driver rilascia la struttura utilizzata per archiviare le informazioni sulla connessione.  
  
 L'applicazione può anche riutilizzare la connessione, per connettersi a un'origine dati diversa o riconnettersi alla stessa origine dati. La decisione di rimanere connessi, anziché disconnettersi e riconnettersi in un secondo momento, richiede che il writer dell'applicazione consideri i relativi costi di ogni opzione; sia la connessione a un'origine dati che la connessione possono essere relativamente costose a seconda del supporto di connessione. Nel fare un compromesso corretto, l'applicazione deve anche fare supposizioni circa la probabilità e la tempistica di ulteriori operazioni sulla stessa origine dati.
