---
title: Utilizzo di valori length e Indicator | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3a0b54617d55033addabc729adbd078680022fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67902473"
---
# <a name="using-length-and-indicator-values"></a>Uso di valori di lunghezza e indicatore
Il buffer di lunghezza/indicatore viene utilizzato per passare la lunghezza in byte dei dati nel buffer di dati o un indicatore speciale, ad esempio SQL_NULL_DATA, che indica che i dati sono NULL. A seconda della funzione in cui viene utilizzata, un buffer di lunghezza/indicatore viene definito come SQLINTEGER o SQLSMALLINT. Pertanto, è necessario un singolo argomento per la relativa descrizione. Se il buffer dei dati è un buffer di input nondeferred, questo argomento contiene la lunghezza in byte dei dati stessi o un valore indicatore. Spesso è denominato *StrLen_Or_Ind* o un nome simile. Il codice seguente, ad esempio, chiama **SQLPutData** per passare un buffer pieno di dati; la lunghezza in byte (*ValueLen*) viene passata direttamente perché il buffer dei dati (*ValuePtr*) è un buffer di input.  
  
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
  
 Se il buffer dei dati è un buffer di input posticipato, un buffer di output nondeferred o un buffer di output, l'argomento contiene l'indirizzo del buffer di lunghezza/indicatore. Spesso è denominato *StrLen_or_IndPtr* o un nome simile. Il codice seguente, ad esempio, chiama **SQLGetData** per recuperare un buffer pieno di dati; la lunghezza in byte viene restituita all'applicazione nel buffer di lunghezza/indicatore (*ValueLenOrInd*), il cui indirizzo viene passato a **SQLGetData** perché il buffer dei dati corrispondente (*ValuePtr*) è un buffer di output nondeferred.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 A meno che non sia esplicitamente vietato, un argomento buffer di lunghezza/indicatore può essere 0 (se nondeferred input) o un puntatore null (se l'output o l'input posticipato). Per i buffer di input, il driver ignora la lunghezza in byte dei dati. Viene restituito un errore durante il passaggio di dati a lunghezza variabile, ma è comune quando si passano dati non null a lunghezza fissa, perché non è necessaria una lunghezza né un valore indicatore. Per i buffer di output, il driver non restituisce la lunghezza in byte dei dati o un valore indicatore. Si tratta di un errore se i dati restituiti dal driver sono NULL ma sono comuni quando si recuperano dati a lunghezza fissa non nullable, perché non è necessaria alcuna lunghezza né un valore indicatore.  
  
 Quando l'indirizzo di un buffer di dati posticipato viene passato al driver, l'indirizzo di un buffer di lunghezza/indicatore posticipato deve rimanere valido fino a quando il buffer non è associato.  
  
 Le lunghezze seguenti sono valide come valori di lunghezza/indicatore:  
  
-   *n*, dove *n* > 0.  
  
-   0.  
  
-   SQL_NTS. Una stringa inviata al driver nel buffer dei dati corrispondente è con terminazione null. si tratta di un modo pratico per i programmatori C per passare stringhe senza dover calcolare la lunghezza in byte. Questo valore è valido solo quando l'applicazione invia dati al driver. Quando il driver restituisce i dati all'applicazione, restituisce sempre la lunghezza effettiva in byte dei dati.  
  
 I valori seguenti sono validi come valori di lunghezza/indicatore. SQL_NULL_DATA viene archiviato nel campo del descrittore SQL_DESC_INDICATOR_PTR. tutti gli altri valori vengono archiviati nel campo del descrittore SQL_DESC_OCTET_LENGTH_PTR.  
  
-   SQL_NULL_DATA. I dati sono un valore di dati NULL e il valore nel buffer dei dati corrispondente viene ignorato. Questo valore è valido solo per i dati SQL inviati o recuperati dal driver.  
  
-   SQL_DATA_AT_EXEC. Il buffer dei dati non contiene dati. Al contrario, i dati verranno inviati con **SQLPutData** quando viene eseguita l'istruzione o quando viene chiamato **SQLBulkOperations** o **SQLSetPos** . Questo valore è valido solo per i dati SQL inviati al driver. Per ulteriori informazioni, vedere [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Risultato della macro SQL_LEN_DATA_AT_EXEC (*length*). Questo valore è simile a SQL_DATA_AT_EXEC. Per ulteriori informazioni, vedere [invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. Il driver non è in grado di determinare il numero di byte di dati lunghi ancora disponibili per la restituzione in un buffer di output. Questo valore è valido solo per i dati SQL recuperati dal driver.  
  
-   SQL_DEFAULT_PARAM. Una procedura prevede l'utilizzo del valore predefinito di un parametro di input in una procedura anziché del valore nel buffer dei dati corrispondente.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** o **SQLSetPos** ignora il valore nel buffer dei dati. Quando si aggiorna una riga di dati tramite una chiamata a **SQLBulkOperations** o **SQLSetPos,** il valore della colonna non viene modificato. Quando si inserisce una nuova riga di dati tramite una chiamata a **SQLBulkOperations**, il valore della colonna viene impostato sul valore predefinito o, se la colonna non ha un valore predefinito, su null.
