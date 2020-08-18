---
description: Recuperare e aggiornare set di righe (ODBC)
title: Recuperare e aggiornare set di righe (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [ODBC]
ms.assetid: cf0eb3b4-8b72-49fc-a845-95edc360cf93
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3130a5180b7727b45b7ecf650c0253908ebdb58f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88407797"
---
# <a name="fetch-and-update-rowsets-odbc"></a>Recuperare e aggiornare set di righe (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-fetch-and-update-rowsets"></a>Per recuperare e aggiornare set di righe  
  
1.  Facoltativamente, chiamare [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) con SQL_ROW_ARRAY_SIZE per modificare il numero di righe (R) nel set di righe.  
  
2.  Chiamare [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) o [SQLFetchScroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md) per ottenere un set di righe.  
  
3.  Se si utilizzano colonne associate, utilizzare i valori dei dati e le lunghezze dei dati disponibili nei buffer delle colonne associate per il set di righe.  
  
     Se vengono utilizzate colonne non associate, per ogni riga chiamare [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) con SQL_POSITION per impostare la posizione del cursore; quindi, per ogni colonna non associata:  
  
    -   Chiamare [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) una o più volte per ottenere i dati per le colonne non vincolate dopo l'ultima colonna associata del set di righe. Le chiamate a [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) devono essere in ordine di numero di colonna crescente.  
  
    -   Chiamare [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) più volte per ottenere dati da una colonna di tipo text o image.  
  
4.  Configurare tutte le colonne data-at-execution di tipo text o image.  
  
5.  Chiamare [SQLSetPos](https://go.microsoft.com/fwlink/?LinkId=58407) o [SQLBulkOperations](https://go.microsoft.com/fwlink/?LinkId=58398) per impostare la posizione del cursore, aggiornare, aggiornare, eliminare o aggiungere righe all'interno del set di righe.  
  
     Se si utilizzano colonne data-at-execution di tipo text o image per un'operazione di aggiornamento o di aggiunta, è necessario gestirle.  
  
6.  Facoltativamente, eseguire un'istruzione UPDATE o DELETE posizionata, specificando il nome del cursore, disponibile da [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md), e utilizzando un handle di istruzione diverso nella stessa connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per l'utilizzo di cursori &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
