---
title: Opzioni dell'istruzione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bf99aace8b058e429898846466294cc42612070
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948837"
---
# <a name="statement-options"></a>Opzioni delle istruzioni
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Queste opzioni consentono la personalizzazione di un'istruzione di esecuzione specifico all'interno di un'applicazione.  
  
|Opzione dell'istruzione|Note|  
|----------------------|-----------|  
|SQL_BIND_TYPE|Non può superare la memoria disponibile o pari a 2.147.483.647 byte.|  
|SQL_CONCURRENCY|Per i valori consentiti, vedere la [tipo di cursore e concorrenza combinazioni](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_CURSOR_TYPE|Il driver non supporta SQL_CURSOR_DYNAMIC. Visualizzare [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) per altre informazioni. Per i valori consentiti, vedere la [tipo di cursore e concorrenza combinazioni](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_GET_BOOKMARK|Restituisce un valore integer a 32 bit che rappresenta il segnalibro per il numero di record corrente. Introduzione di sola lettura. non è possibile impostare.|  
|SQL_KEYSET_SIZE|Può essere impostato solo su 0.|  
|SQL_MAX_ROWS|Il numero massimo di righe da restituire dal risultato di un set.|  
|SQL_ROW_NUMBER|Restituisce un intero a 32 bit che specifica la posizione della riga corrente nel set di risultati. Introduzione di sola lettura. non è possibile impostare.|  
|SQL_ROWSET_SIZE|Non può superare i 4.294.967.296 righe. Tuttavia, è necessario memoria virtuale sufficiente nel computer per gestire la richiesta.|  
|SQL_USE_BOOKMARKS|Supporta l'impostazione SQL_USE_BOOKMARKS su SQL_UB_ON ed espone i segnalibri di lunghezza fissa.|
