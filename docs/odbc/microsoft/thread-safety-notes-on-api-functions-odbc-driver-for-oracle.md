---
title: Note sulla sicurezza dei thread sulle funzioni API (driver ODBC per Oracle) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 489f0e99ea53d419ff94dddfeb22e37573abb874
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303072"
---
# <a name="thread-safety-notes-on-api-functions-odbc-driver-for-oracle"></a>Note di thread safety sulle funzioni API (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Microsoft ODBC driver for Oracle è thread-safe. Tuttavia, Oracle non consente più istruzioni simultanee in una singola connessione. Il driver impone questa restrizione. In altre parole, nelle applicazioni multithreading, sebbene qualsiasi thread possa chiamare il driver ODBC per Oracle in qualsiasi momento, il driver blocca qualsiasi altro thread dal driver sulla stessa connessione fino a quando il thread originale non esce dal driver.  
  
 Il driver non viene bloccato se sono presenti due istruzioni su due connessioni diverse. Tuttavia, se è presente una singola connessione con due istruzioni, è possibile che si verifichi un blocco.
