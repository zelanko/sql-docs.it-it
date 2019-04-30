---
title: Usare set di righe (ODBC) di associazione | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowset binding [ODBC]
ms.assetid: a7be05f0-6b11-4b53-9fbc-501e591eef09
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b416d9f7fdd07613f684fb2b27ac058b60d5b3c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200436"
---
# <a name="use-rowset-binding-odbc"></a>Utilizzare l'associazione di set di righe (ODBC)
    
### <a name="to-use-column-wise-binding"></a>Per utilizzare l'associazione per colonna  
  
1.  Per ogni colonna associata, eseguire le operazioni seguenti:  
  
    -   Allocare una matrice di R (o più) buffer di colonna per archiviare i valori dei dati, dove R è il numero di righe del set di righe.  
  
    -   Facoltativamente, allocare una matrice di R (o più) buffer di colonna per archiviare le lunghezze dei dati.  
  
    -   Chiamare [SQLBindCol](../../native-client-odbc-api/sqlbindcol.md) per associare la colonna valore dei dati e le matrici di lunghezza dati alla colonna del set di righe.  
  
2.  Chiamare [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) per impostare gli attributi seguenti:  
  
    -   Impostare SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe nel set di righe (R).  
  
    -   Impostare SQL_ATTR_ROW_BIND_TYPE su SQL_BIND_BY_COLUMN.  
  
    -   Impostare l'attributo SQL_ATTR_ROWS FETCHED_PTR affinché punti a una variabile SQLUINTEGER per mantenere il numero di righe recuperate.  
  
    -   Impostare SQL_ATTR_ROW_STATUS_PTR affinché punti a una matrice [R] di variabili SQLUSSMALLINT per mantenere gli indicatori di stato della riga.  
  
3.  Eseguire l'istruzione.  
  
4.  Ogni chiamata a [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) oppure [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) recupera R righe e trasferisce i dati nelle colonne associate.  
  
### <a name="to-use-row-wise-binding"></a>Per utilizzare l'associazione per riga  
  
1.  Allocare una matrice [R] di strutture, dove R è il numero di righe nel set di righe. La struttura dispone di un elemento per ogni colonna e ogni elemento dispone di due parti:  
  
    -   La prima parte è una variabile del tipo di dati appropriato per mantenere i dati della colonna.  
  
    -   La seconda parte è una variabile SQLINTEGER per mantenere l'indicatore di stato della colonna.  
  
2.  Chiamare [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) per impostare gli attributi seguenti:  
  
    -   Impostare SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe nel set di righe (R).  
  
    -   Impostare SQL_ATTR_ROW_BIND_TYPE sulla dimensione della struttura allocata nel Passaggio 1.  
  
    -   Impostare l'attributo SQL_ATTR_ROWS_FETCHED_PTR affinché punti a una variabile SQLUINTEGER per mantenere il numero di righe recuperate.  
  
    -   Impostare SQL_ATTR_PARAMS_STATUS_PTR affinché punti a una matrice [R] di variabili SQLUSSMALLINT per mantenere gli indicatori di stato della riga.  
  
3.  Per ogni colonna nel set di risultati, chiamare [SQLBindCol](../../native-client-odbc-api/sqlbindcol.md) in modo da puntare il valore dei dati e il puntatore di lunghezza dati della colonna alle relative variabili nel primo elemento della matrice di strutture allocate nel passaggio 1.  
  
4.  Eseguire l'istruzione.  
  
5.  Ogni chiamata a [SQLFetch](https://go.microsoft.com/fwlink/?LinkId=58401) oppure [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md) recupera R righe e trasferisce i dati nelle colonne associate.  
  
## <a name="see-also"></a>Vedere anche  
 [Usando procedure per cursori &#40;ODBC&#41;](using-cursors-how-to-topics-odbc.md)   
 [La modalità di implementazione dei cursori](../../native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)   
 [Utilizzare i cursori &#40;ODBC&#41;](use-cursors-odbc.md)  
  
  
