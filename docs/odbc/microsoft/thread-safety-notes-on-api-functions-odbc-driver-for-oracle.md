---
title: Note sulla thread Safety sulle funzioni API (Driver ODBC per Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], threading
- threading options [ODBC]
- multiple concurrent statements [ODBC]
ms.assetid: f0c9bdfd-f79d-4088-9ecb-afcd8ca7fb73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d1faa7dfd8873b8c11cda5cb3e67d5408c35474
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633216"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Note di thread safety sulle funzioni API (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Il Driver ODBC di Microsoft per Oracle è thread-safe. Tuttavia, Oracle non supporta più istruzioni simultanee in una singola connessione. Il driver applica questa limitazione. In altre parole, nelle applicazioni multithreading, anche se uno o più thread può chiamare il Driver ODBC per Oracle in qualsiasi momento, il driver blocca altri thread dal driver nella stessa connessione fino a quando il thread originale lascia il driver.  
  
 Il driver non vengono bloccate se sono presenti due istruzioni in due diverse connessioni. Se è presente una sola connessione a due istruzioni, vi sono comunque possibili per il blocco.
