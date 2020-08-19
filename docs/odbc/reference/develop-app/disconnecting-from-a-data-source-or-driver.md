---
description: Disconnessione da un'origine dati o driver
title: Disconnessione da un'origine dati o da un driver | Microsoft Docs
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
ms.openlocfilehash: fc14ca0ebf29a2ab203a4408db4b5681ad667497
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476693"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Disconnessione da un'origine dati o driver
Quando un'applicazione ha terminato di usare un'origine dati, chiama **SQLConnect**. **SQLConnect** libera tutte le istruzioni allocate sulla connessione e disconnette il driver dall'origine dati. Restituisce un errore se una transazione è in corso.  
  
 Dopo la disconnessione, l'applicazione può chiamare **SQLFreeHandle** per liberare la connessione. Una volta liberata la connessione, si tratta di un errore di programmazione dell'applicazione per l'utilizzo dell'handle della connessione in una chiamata a una funzione ODBC. Questa operazione ha conseguenze indefinite ma probabilmente fatali. Quando viene chiamato **SQLFreeHandle** , il driver rilascia la struttura utilizzata per archiviare le informazioni sulla connessione.  
  
 L'applicazione può anche riutilizzare la connessione per connettersi a un'origine dati diversa oppure riconnettersi alla stessa origine dati. La decisione di rimanere connessa, anziché disconnettersi e riconnettersi in un secondo momento, richiede che il writer di applicazioni consideri i costi relativi di ogni opzione. la connessione a un'origine dati e rimanente connessa può essere relativamente costosa a seconda del supporto di connessione. Per garantire un compromesso corretto, l'applicazione deve anche ipotizzare la probabilità e la tempistica di ulteriori operazioni sulla stessa origine dati.
