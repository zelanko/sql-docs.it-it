---
title: Con valori di lunghezza e indicatore | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 442d0865ede4819ea3413d662411295daa5b48bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62501112"
---
# <a name="using-length-and-indicator-values"></a>Uso di valori di lunghezza e indicatore
Il buffer di lunghezza/indicatore viene utilizzato per passare la lunghezza in byte dei dati nel buffer di dati o un indicatore speciale, ad esempio SQL_NULL_DATA, che indica che i dati sono NULL. A seconda della funzione in cui viene utilizzato, un buffer di lunghezza/indicatore è definito come un SQLINTEGER o un SQLSMALLINT. Pertanto, un singolo argomento, è necessario per una descrizione. Se il buffer dei dati è un buffer di input nondeferred, questo argomento contiene la lunghezza in byte dei dati stessi o un valore dell'indicatore. È spesso denominata *StrLen_or_Ind* o un nome simile. Ad esempio, il codice seguente chiama **SQLPutData** per passare un buffer completo dei dati, la lunghezza in byte (*ValueLen*) viene passato direttamente perché il buffer dei dati (*ValuePtr*) è un buffer di input.  
  
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
  
 Se il buffer dei dati è un buffer di input posticipato, un buffer di output nondeferred o un buffer di output, l'argomento contiene l'indirizzo del buffer di lunghezza/indicatore. È spesso denominata *StrLen_or_IndPtr* o un nome simile. Ad esempio, il codice seguente chiama **SQLGetData** per recuperare un buffer completo dei dati; la lunghezza in byte viene restituita all'applicazione nel buffer di lunghezza/indicatore (*ValueLenOrInd*), il cui indirizzo è passato a **SQLGetData** perché il buffer di dati corrispondenti (*ValuePtr*) è un buffer di output nondeferred.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 A meno che non espressamente vietato, un argomento di buffer di lunghezza/indicatore può essere 0 (se input nondeferred) o un puntatore null (se posticipata input o output). Per i buffer di input, in questo modo il driver ignorare la lunghezza in byte dei dati. Restituisce un errore quando si passano dati a lunghezza variabile, ma è comune quando si passano dati a lunghezza fissa e non null, perché è necessaria una lunghezza, né un valore dell'indicatore. Per i buffer di output, in questo modo il driver per non restituire la lunghezza in byte dei dati o un valore dell'indicatore. Si tratta di un errore se i dati restituiti dal driver sono NULL, ma sono comuni quando si recuperano i dati a lunghezza fissa e non nullable, perché è necessaria una lunghezza, né un valore dell'indicatore.  
  
 Quando l'indirizzo di un buffer di dati posticipata viene passato al driver, l'indirizzo di un buffer di lunghezza/indicatore posticipata deve rimane valido fino a quando il buffer non è associato.  
  
 Le lunghezze seguenti sono valide come valori di lunghezza/indicatore:  
  
-   *n*, dove *n* > 0.  
  
-   0.  
  
-   SQL_NTS. Una stringa inviata al driver nel buffer di dati corrispondente è con terminazione null; Questo è un modo pratico per i programmatori di C da passare stringhe senza la necessità di calcolare la lunghezza in byte. Questo valore è valido solo quando l'applicazione invia i dati del driver. Quando il driver restituisce i dati all'applicazione, restituisce sempre la lunghezza in byte effettivi dei dati.  
  
 I valori seguenti sono validi come valori di lunghezza/indicatore. SQL_NULL_DATA viene archiviato nel campo del descrittore SQL_DESC_INDICATOR_PTR; tutti gli altri valori vengono archiviati nel campo del descrittore SQL_DESC_OCTET_LENGTH_PTR.  
  
-   SQL_NULL_DATA. I dati sono un valore di dati NULL e il valore nel buffer di dati corrispondente viene ignorato. Questo valore è consentito solo per i dati SQL inviati o recuperati dal driver.  
  
-   SQL_DATA_AT_EXEC. Il buffer di dati non contiene tutti i dati. Al contrario, verranno inviati i dati con **SQLPutData** quando viene eseguita l'istruzione o quando **SQLBulkOperations** oppure **SQLSetPos** viene chiamato. Questo valore è consentito solo per i dati SQL inviati al driver. Per altre informazioni, vedere [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Risultato della finestra di SQL_LEN_DATA_AT_EXEC (*lunghezza*) (macro). Questo valore è simile a SQL_DATA_AT_EXEC. Per altre informazioni, vedere [l'invio di dati Long](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. Il driver non è possibile determinare il numero di byte di dati long ancora disponibili a tornare in un buffer di output. Questo valore è consentito solo per i dati SQL recuperati dal driver.  
  
-   SQL_DEFAULT_PARAM. Una procedura consiste nell'usare il valore predefinito di un parametro di input in una procedura anziché il valore nel buffer di dati corrispondente.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** oppure **SQLSetPos** consiste nell'ignorare il valore nel buffer di dati. Quando si aggiorna una riga di dati da una chiamata a **SQLBulkOperations** oppure **SQLSetPos,** non viene modificato il valore della colonna. Quando si inserisce una nuova riga di dati da una chiamata a **SQLBulkOperations**, il valore della colonna è impostato sul valore predefinito o, se la colonna non dispone di un'impostazione predefinita, su NULL.
