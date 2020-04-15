---
title: Utilizzo dei valori di lunghezza e indicatore Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0c878c9038b26aa996ed206c6b8adfe8d6c21e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306762"
---
# <a name="using-length-and-indicator-values"></a>Uso di valori di lunghezza e indicatore
Il buffer di lunghezza/indicatore viene utilizzato per passare la lunghezza in byte dei dati nel buffer di dati o un indicatore speciale, ad esempio SQL_NULL_DATA, che indica che i dati sono NULL. A seconda della funzione in cui viene utilizzato, un buffer di lunghezza/indicatore è definito come SQLINTEGER o SQLSMALLINT. Pertanto, è necessario un singolo argomento per descriverlo. Se il buffer di dati è un buffer di input non posticipato, questo argomento contiene la lunghezza in byte dei dati stessi o un valore dell'indicatore. È spesso chiamato *StrLen_or_Ind* o un nome simile. Ad esempio, il codice seguente chiama **SQLPutData** per passare un buffer pieno di dati; la lunghezza in byte (*ValueLen*) viene passata direttamente perché il buffer di dati (*ValuePtr*) è un buffer di input.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLen;  
  
// Call local function to place data in ValuePtr. In ValueLen, return the  
// number of bytes of data placed in ValuePtr. If there is not enough  
// data, this will be less than 50.  
FillBuffer(ValuePtr, sizeof(ValuePtr), &ValueLen);  
  
// Call SQLPutData to send the data to the driver.  
SQLPutData(hstmt, ValuePtr, ValueLen);  
```  
  
 Se il buffer di dati è un buffer di input posticipato, un buffer di output non posticipato o un buffer di output, l'argomento contiene l'indirizzo del buffer di lunghezza/indicatore. È spesso chiamato *StrLen_or_IndPtr* o un nome simile. Ad esempio, il codice seguente chiama **SQLGetData** per recuperare un buffer pieno di dati; la lunghezza dei byte viene restituita all'applicazione nel buffer di lunghezza/indicatore (*ValueLenOrInd*), il cui indirizzo viene passato a **SQLGetData** perché il buffer di dati corrispondente (*ValuePtr*) è un buffer di output non posticipato.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 A meno che non sia specificamente proibito, un argomento buffer di lunghezza/indicatore può essere 0 (se input non differito) o un puntatore null (se l'output o l'input posticipato). Per i buffer di input, in questo modo il driver ignorare la lunghezza in byte dei dati. Restituisce un errore quando si passano dati a lunghezza variabile, ma è comune quando si passano dati non null a lunghezza fissa, perché non è necessaria né una lunghezza né un valore dell'indicatore. Per i buffer di output, in questo modo il driver non restituire la lunghezza in byte dei dati o un valore dell'indicatore. Si tratta di un errore se i dati restituiti dal driver sono NULL ma è comune quando si recuperano dati a lunghezza fissa e non nullable, perché non è necessaria né una lunghezza né un valore dell'indicatore.  
  
 Come quando l'indirizzo di un buffer di dati posticipato viene passato al driver, l'indirizzo di un buffer di lunghezza/indicatore posticipato deve rimanere valido fino a quando il buffer non è associato.  
  
 Le lunghezze seguenti sono valide come valori di lunghezza/indicatore:  
  
-   *n*, dove *n* > 0.  
  
-   0.  
  
-   SQL_NTS. Una stringa inviata al driver nel buffer di dati corrispondente è con terminazione null; questo è un modo pratico per i programmatori C di passare stringhe senza dover calcolare la lunghezza in byte. Questo valore è valido solo quando l'applicazione invia dati al driver. Quando il driver restituisce dati all'applicazione, restituisce sempre la lunghezza effettiva in byte dei dati.  
  
 I valori seguenti sono validi come valori di lunghezza/indicatore. SQL_NULL_DATA è memorizzato nel campo descrittore SQL_DESC_INDICATOR_PTR; tutti gli altri valori vengono memorizzati nel campo descrittore SQL_DESC_OCTET_LENGTH_PTR.  
  
-   SQL_NULL_DATA. I dati sono un valore di dati NULL e il valore nel buffer di dati corrispondente viene ignorato. Questo valore è valido solo per i dati SQL inviati o recuperati dal driver.  
  
-   SQL_DATA_AT_EXEC. Il buffer di dati non contiene dati. Al contrario, i dati verranno inviati con **SQLPutData** quando viene eseguita l'istruzione o quando **SQLBulkOperations** o **SQLSetPos** viene chiamato. Questo valore è valido solo per i dati SQL inviati al driver. Per ulteriori informazioni, vedere [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Risultato della macro SQL_LEN_DATA_AT_EXEC(*length*). Questo valore è simile a SQL_DATA_AT_EXEC. Per ulteriori informazioni, vedere [Invio di dati lunghi](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. Il driver non è in grado di determinare il numero di byte di dati long ancora disponibili per la restituzione in un buffer di output. Questo valore è valido solo per i dati SQL recuperati dal driver.  
  
-   SQL_DEFAULT_PARAM. Una procedura consiste nell'utilizzare il valore predefinito di un parametro di input in una routine anziché il valore nel buffer di dati corrispondente.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** o **SQLSetPos** consiste nel ignorare il valore nel buffer di dati. Quando si aggiorna una riga di dati da una chiamata a **SQLBulkOperations** o **SQLSetPos,** il valore della colonna non viene modificato. Quando si inserisce una nuova riga di dati mediante una chiamata a **SQLBulkOperations**, il valore della colonna viene impostato sul valore predefinito o, se la colonna non dispone di un valore predefinito, su NULL.
