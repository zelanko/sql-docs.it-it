---
title: SQLDriverToDataSource Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDriverToDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDriverToDataSource
helpviewer_keywords:
- SQLDriverToDataSource function [ODBC]
ms.assetid: 0de28eb5-8aa9-43e4-a87f-7dbcafe800dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f5450bbabb43b1f5cbc8c0fd7cb1a83da3a8bc7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061447"
---
# <a name="sqldrivertodatasource-function"></a>Funzione SQLDriverToDataSource
**SQLDriverToDataSource** supporta le traduzioni per i driver ODBC. Questa funzione non viene chiamata dalle applicazioni basate su ODBC; le applicazioni richiedono traduzione attraverso **SQLSetConnectAttr**. Il driver associato con il *ConnectionHandle* specificato in **SQLSetConnectAttr** chiama la DLL specificata per eseguire le traduzioni di tutti i dati che passano dal driver per l'origine dati. Una DLL di conversione predefinita può essere specificato nel file di inizializzazione ODBC.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BOOL SQLDriverToDataSource(  
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
 [Input] Il tipo di dati SQL ODBC. Questo argomento indica al driver come convertire *rgbValueIn* in un formato accettabile per l'origine dati. Per un elenco di tipi di dati SQL validi, vedere [tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md).  
  
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
 Il driver chiama **SQLDriverToDataSource** per convertire tutti i dati (istruzioni SQL, parametri e così via) passando dal driver per l'origine dati. La DLL di conversione potrebbe non tradurre alcuni dati, a seconda del tipo dei dati e lo scopo della DLL di conversione. Ad esempio, una DLL che converte i dati di tipo carattere da una tabella codici a altra ignora tutti i dati numerici e binari.  
  
 Il valore di *fOption* è impostata sul valore di *vParam* specificata chiamando **SQLSetConnectAttr** con l'attributo SQL_ATTR_TRANSLATE_OPTION. È un valore a 32 bit che ha un significato specifico per una determinata DLL di conversione. Ad esempio, è possibile specificare che conversione del set di un determinato carattere.  
  
 Se il buffer stesso viene specificato per *rgbValueIn* e *rgbValueOut*, verrà eseguita la conversione dei dati nel buffer di posto.  
  
 Sebbene *cbValueIn*, *cbValueOutMax*, e *pcbValueOut* sono di tipo, SDWORD **SQLDriverToDataSource** non necessariamente supporta i puntatori di grandi dimensioni.  
  
 Se **SQLDriverToDataSource** restituisce FALSE, il troncamento dei dati sono stati generati durante la conversione. Se *pcbValueOut* (il numero di byte disponibili a tornare nel buffer di output) è maggiore *cbValueOutMax* (la lunghezza del buffer di output), quindi si è verificato un troncamento. Il driver deve determinare se il troncamento è stato accettato. Se non si è verificato il troncamento, il **SQLDriverToDataSource** ha restituito FALSE a causa di un altro errore. In entrambi i casi, viene restituito un messaggio di errore specifico nel *szErrorMsg*.  
  
 Per altre informazioni sulla conversione dei dati, vedere [DDL di traslazione](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Conversione dei dati restituiti dall'origine dati|[SQLDataSourceToDriver](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Restituisce l'impostazione di un attributo di connessione|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Impostare un attributo di connessione|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
