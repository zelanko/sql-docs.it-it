---
title: Recuperare e aggiornare set di righe (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: rothja
ms.author: jroth
ms.openlocfilehash: 10f23e8a8e8c76160362af2f3efacfd297062254
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85018918"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Recuperare e aggiornare set di righe (ODBC)
    
### <a name="to-fetch-and-update-rowsets"></a>Per recuperare e aggiornare set di righe  
  
1.  Facoltativamente, chiamare [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) con SQL_ROW_ARRAY_SIZE per modificare il numero di righe (R) nel set di righe.  
  
2.  Chiamare [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) o [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) per ottenere un set di righe.  
  
3.  Se si utilizzano colonne associate, utilizzare i valori dei dati e le lunghezze dei dati disponibili nei buffer delle colonne associate per il set di righe.  
  
     Se vengono utilizzate colonne non associate, per ogni riga chiamare [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) con SQL_POSITION per impostare la posizione del cursore; quindi, per ogni colonna non associata:  
  
    -   Chiamare [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) una o più volte per ottenere i dati per le colonne non vincolate dopo l'ultima colonna associata del set di righe. Le chiamate a [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) devono essere in ordine di numero di colonna crescente.  
  
    -   Chiamare [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) più volte per ottenere dati da una colonna di tipo text o image.  
  
4.  Configurare tutte le colonne data-at-execution di tipo text o image.  
  
5.  Chiamare [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) o [SQLBulkOperations](https://go.microsoft.com/fwlink/?LinkId=58398) per impostare la posizione del cursore, aggiornare, aggiornare, eliminare o aggiungere righe all'interno del set di righe.  
  
     Se si utilizzano colonne data-at-execution di tipo text o image per un'operazione di aggiornamento o di aggiunta, è necessario gestirle.  
  
6.  Facoltativamente, eseguire un'istruzione UPDATE o DELETE posizionata, specificando il nome del cursore, disponibile da [SQLGetCursorName](../../native-client-odbc-api/sqlgetcursorname.md), e utilizzando un handle di istruzione diverso nella stessa connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per l'utilizzo di cursori &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)  
  
  
