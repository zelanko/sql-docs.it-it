---
title: Opzioni istruzione | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca40765dff98e9102fbe36e88c7e79535f311d97
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299211"
---
# <a name="statement-options"></a>Opzioni delle istruzioni
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Queste opzioni consentono la personalizzazione di un'istruzione di esecuzione specifica all'interno di un'applicazione.  
  
|Opzione Statement|Note|  
|----------------------|-----------|  
|SQL_BIND_TYPE|Non può superare 2.147.483.647 byte o la memoria disponibile.|  
|SQL_CONCURRENCY|Per i valori consentiti, vedere il [tipo di cursore e le combinazioni di concorrenza](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_CURSOR_TYPE|Il driver non consente SQL_CURSOR_DYNAMIC. Per ulteriori informazioni, vedere [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) . Per i valori consentiti, vedere il [tipo di cursore e le combinazioni di concorrenza](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md).|  
|SQL_GET_BOOKMARK|Restituisce un valore integer a 32 bit che rappresenta il segnalibro per il numero di record corrente. Solo Get; non è possibile impostare.|  
|SQL_KEYSET_SIZE|Può essere impostato solo su 0.|  
|SQL_MAX_ROWS|Numero massimo di righe da restituire da un set di risultati.|  
|SQL_ROW_NUMBER|Restituisce un intero a 32 bit che specifica la posizione della riga corrente all'interno del set di risultati. Solo Get; non è possibile impostare.|  
|SQL_ROWSET_SIZE|Non può superare 4.294.967.296 righe; Tuttavia, è necessario disporre di una quantità di memoria virtuale sufficiente nel computer per gestire la richiesta.|  
|SQL_USE_BOOKMARKS|Supporta l'impostazione di SQL_USE_BOOKMARKS per SQL_UB_ON ed espone segnalibri a lunghezza fissa.|
