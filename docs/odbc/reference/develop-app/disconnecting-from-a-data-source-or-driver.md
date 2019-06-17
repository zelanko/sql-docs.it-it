---
title: Disconnessione da una Data sorgente o il Driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2189c0fcc65fd4192e94da140e2d55ac86826137
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62936000"
---
# <a name="disconnecting-from-a-data-source-or-driver"></a>Disconnessione da un'origine dati o driver
Quando un'applicazione ha terminato di utilizzare un'origine dati, viene chiamato **SQLDisconnect**. **SQLDisconnect** libera le istruzioni allocate nella connessione e disconnette il driver dell'origine dati. Restituisce un errore se una transazione è in corso.  
  
 Dopo la disconnessione, l'applicazione può chiamare **SQLFreeHandle** per liberare la connessione. Dopo avere liberato la connessione, è un'applicazione un errore di programmazione per l'uso di handle di connessione in una chiamata a una funzione ODBC; Questa operazione ha conseguenze non definiti, ma probabilmente irreversibile. Quando **SQLFreeHandle** viene chiamato, le versioni di driver la struttura utilizzata per archiviare le informazioni sulla connessione.  
  
 L'applicazione può anche riutilizzare la connessione, per connettersi a un'origine dati diversa o riconnettersi alla stessa origine dati. La decisione di rimanere connessi, invece di disconnessione e riconnessione in seguito, è necessario che il writer dell'applicazione dei costi relativi di ogni opzione. sia la connessione a un'origine dati e rimanere connessi può essere relativamente costosi a seconda del supporto di connessione. Effettuare un compromesso corretto, l'applicazione deve anche fare ipotesi sulla probabilità e sui tempi di altre operazioni sulla stessa origine dati.
