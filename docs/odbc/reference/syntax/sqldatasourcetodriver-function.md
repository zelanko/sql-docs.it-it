---
title: Funzione SQLDataSourceToDriver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSourceToDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSourceToDriver
helpviewer_keywords:
- SQLDataSourceToDriver function [ODBC]
ms.assetid: 0d87fcac-30a0-4303-ad8f-a5b53f4b428d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 022387847cb1371af13465cee7a9e3e1c21e5749
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537647"
---
# <a name="sqldatasourcetodriver-function"></a>Funzione SQLDataSourceToDriver
**SQLDataSourceToDriver** supportstranslations per i driver ODBC. Questa funzione non viene chiamata dalle applicazioni basate su ODBC; le applicazioni richiedono traduzione attraverso **SQLSetConnectAttr**. Il driver associato con il *ConnectionHandle* specificato in **SQLSetConnectAttr** chiama la DLL specificata per eseguire le traduzioni di tutti i dati provenienti dall'origine dati del driver. Una DLL di conversione predefinita può essere specificato nel file di inizializzazione ODBC.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLDataSourceToDriver(  
     UDWORD     fOption,  
     SWORD      fSqlType,  
     PTR        rgbValueIn,  
     SDWORD     cbValueIn,  
     PTR        rgbValueOut,  
     SDWORD     cbValueOutMax,  
     SDWORD *   pcbValueOut,  
     UCHAR *    szErrorMsg,  
     SWORD      cbErrorMsgMax,  
     SWORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argomenti  
 *fOption*  
 [Input] Valore dell'opzione.  
  
 *fSqlType*  
 [Input] Il tipo di dati SQL. Questo argomento indica al driver come convertire *rgbValueIn* in un formato accettabile per l'applicazione. Per un elenco di tipi di dati SQL validi, vedere la [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) sezione nell'appendice d: Tipi di dati.  
  
 *rgbValueIn*  
 [Input] Valore da convertire.  
  
 *cbValueIn*  
 [Input] Lunghezza di *rgbValueIn*.  
  
 *rgbValueOut*  
 [Output] Risultato della conversione.  
  
> [!NOTE]  
>  La DLL di conversione non null terminare questo valore.  
  
 *cbValueOutMax*  
 [Input] Lunghezza di *rgbValueOut*.  
  
 *pcbValueOut*  
 [Output] Il numero totale di byte (escluso il byte di terminazione null) disponibili per restituire *rgbValueOut*.  
  
 Per dati carattere o binario, se è maggiore o uguale a *cbValueOutMax*, i dati in *rgbValueOut* verrà troncato *cbValueOutMax* byte.  
  
 Per tutti gli altri tipi di dati, il valore di *cbValueOutMax* viene ignorato e la DLL di conversione si presuppone che la dimensione del *rgbValueOut* è la dimensione del tipo di dati C predefinito del tipo di dati SQL specificato con *fSqlType*.  
  
 Il *pcbValueOut* argomento può essere un puntatore null.  
  
 *szErrorMsg*  
 [Output] Puntatore alla risorsa di archiviazione per un messaggio di errore. Si tratta di una stringa vuota, a meno che la conversione non riuscita.  
  
 *cbErrorMsgMax*  
 [Input] Lunghezza di *szErrorMsg*.  
  
 *pcbErrorMsg*  
 [Output] Puntatore al numero totale di byte (escluso il byte di terminazione null) disponibili per restituire *szErrorMsg*. Se è maggiore o uguale a *cbErrorMsg*, i dati in *szErrorMsg* verrà troncato *cbErrorMsgMax* meno il carattere di terminazione null. Il *pcbErrorMsg* argomento può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 TRUE se la conversione ha esito positivo, FALSE se la conversione ha esito negativo.  
  
## <a name="comments"></a>Commenti  
 Il driver chiama **SQLDataSourceToDriver** per tradurre alldata (i dati dei set di risultati, i nomi di tabella, i conteggi delle righe, i messaggi di errore e così via) passando dai dati di origine del driver. La DLL di conversione potrebbe non tradurre alcuni dati, a seconda del tipo dei dati e lo scopo della traduzione DLL. ad esempio, una DLL che converte i dati di tipo carattere da una tabella codici a altra ignora tutti i dati numerici e binari.  
  
 Il valore di *fOption* è impostata sul valore di *vParam* specificata chiamando **SQLSetConnectAttr** con l'attributo SQL_ATTR_TRANSLATE_OPTION. È un valore a 32 bit che ha un significato specifico per una determinata DLL di conversione. Ad esempio, è possibile specificare che conversione del set di un determinato carattere.  
  
 Se il buffer stesso viene specificato per *rgbValueIn* e *rgbValueOut*, verrà eseguita la conversione dei dati nel buffer di posto.  
  
 Sebbene *cbValueIn*, *cbValueOutMax*, e *pcbValueOut* sono di tipo, SDWORD **SQLDataSourceToDriver** non necessariamente supporta i puntatori di grandi dimensioni.  
  
 Se **SQLDataSourceToDriver** restituisce FALSE, il troncamento dei dati sono stati generati durante la conversione. Se *pcbValueOut* (il numero di byte disponibili a tornare nel buffer di output) è maggiore *cbValueOutMax* (la lunghezza del buffer di output), quindi si è verificato un troncamento. Il driver deve determinare se il troncamento ha avuto accettabile. Se non si è verificato il troncamento, il **SQLDataSourceToDriver** ha restituito FALSE a causa di un altro errore. In entrambi i casi, viene restituito un messaggio di errore specifico nel *szErrorMsg*.  
  
 Per altre informazioni sulla conversione dei dati, vedere [DDL di traslazione](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Conversione di dati inviati all'origine dati|[SQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|Restituisce l'impostazione di un attributo di connessione|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Impostare un attributo di connessione|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
