---
title: Elaborare i risultati (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- processing results [ODBC]
ms.assetid: 4810fe3f-78ee-4f0d-8bcc-a4659fbcf46f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21474aed83aac1fe86e2242b1238affa11ae64a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200311"
---
# <a name="process-results-odbc"></a>Elaborare i risultati (ODBC)
    
### <a name="to-process-results"></a>Per elaborare i risultati  
  
1.  Recuperare le informazioni sul set di risultati.  
  
2.  Se si usano colonne associate, per ogni colonna con cui si intende eseguire l'associazione, chiamare [SQLBindCol](../native-client-odbc-api/sqlbindcol.md) per associare un buffer del programma alla colonna.  
  
3.  Per ogni riga del set di risultati, effettuare le operazioni seguenti:  
  
    -   Chiamare [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) per ottenere la riga successiva.  
  
    -   Se si utilizzano colonne associate, utilizzare i dati disponibili nei relativi buffer.  
  
    -   Se si usano colonne non associate, chiamare [SQLGetData](../native-client-odbc-api/sqlgetdata.md) una o più volte per ottenere i dati relativi alle colonne non associate dopo l'ultima colonna associata. Le chiamate a `SQLGetData` devono essere effettuate nell'ordine di numero di colonna crescente.  
  
    -   Chiamare `SQLGetData` più volte per ottenere dati da una colonna di tipo text o image.  
  
4.  Quando [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) segnala la fine del set di risultati restituendo SQL_NO_DATA, chiamare [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) per determinare se è disponibile un altro set di risultati.  
  
    -   Se viene restituito SQL_SUCCESS, è disponibile un altro set di risultati.  
  
    -   Se viene restituito SQL_NO_DATA, non è più disponibile alcun set di risultati.  
  
    -   Se viene restituito SQL_SUCCESS_WITH_INFO o SQL_ERROR, chiamare [SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) per determinare se è disponibile l'output da un'istruzione PRINT o RAISERROR.  
  
         Se si utilizzano parametri di istruzione associati per i parametri di output o il valore restituito di una stored procedure, utilizzare i dati disponibili nei buffer dei parametri associati. Inoltre, quando si utilizzano parametri associati, ogni chiamata a [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) o [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) eseguirà l'istruzione SQL *S* volte, dove *S* è il numero di elementi nella matrice dei parametri associati. Di conseguenza, vi saranno *S* set di risultati da elaborare, in cui ogni set di risultati comprende tutti i set di risultati, i parametri di output e i codici restituiti normalmente da una singola esecuzione dell'istruzione SQL.  
  
    > [!NOTE]  
    >  Quando un set di risultati contiene righe di calcolo, ogni riga di calcolo viene resa disponibile come set di risultati distinto. Tali set di risultati di calcolo vengono intercalati all'interno delle normali righe e le suddividono in più set di risultati.  
  
5.  Facoltativamente, è possibile chiamare [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) con SQL_UNBIND per rilasciare qualsiasi buffer delle colonne associate.  
  
6.  Se è disponibile un altro set di risultati, andare al passaggio 1.  
  
> [!NOTE]  
>  Per annullare l'elaborazione di un set di risultati prima che [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) restituisca SQL_NO_DATA, chiamare [SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per i risultati di elaborazione &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  
