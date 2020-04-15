---
title: Funzione SQLDriverToDataSource . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89e7db7e4b20a35e047dca94cb72d8a6888fb670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302752"
---
# <a name="sqldrivertodatasource-function"></a>Funzione SQLDriverToDataSource
**SQLDriverToDataSource** supporta le traduzioni per i driver ODBC. Questa funzione non viene chiamata dalle applicazioni abilitate per ODBC; le applicazioni richiedono la conversione tramite **SQLSetConnectAttr**. Il driver associato al *ConnectionHandle* specificato in **SQLSetConnectAttr** chiama la DLL specificata per eseguire le conversioni di tutti i dati che scorrono dal driver all'origine dati. È possibile specificare una DLL di conversione predefinita nel file di inizializzazione ODBC.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
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
 *fOpzione*  
 [Ingresso] Valore dell'opzione.  
  
 *fSqlType (tipo di codice)*  
 [Ingresso] Tipo di dati SQL ODBC. Questo argomento indica al driver come convertire *rgbValueIn* in un formato accettabile per l'origine dati. Per un elenco dei tipi di dati SQL validi, vedere [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md).  
  
 *rgbValueIn*  
 [Ingresso] Valore da tradurre.  
  
 *CbValueIn (informazioni in questo base base campi onCb*  
 [Ingresso] Lunghezza di *rgbValueIn*.  
  
 *rgbValueOut*  
 [Uscita] Risultato della traduzione.  
  
> [!NOTE]  
>  La DLL di conversione non termina con null questo valore.  
  
 *CbValueOutMax*  
 [Ingresso] Lunghezza di *rgbValueOut*.  
  
 *pcbValueOut (informazioni in questo campo)*  
 [Uscita] Numero totale di byte (escluso il byte di terminazione null) disponibili per la restituzione in *rgbValueOut*.  
  
 Per i dati di tipo carattere o binario, se è maggiore o uguale a *cbValueOutMax*, i dati in *rgbValueOut* vengono troncati a *cbValueOutMax* byte.  
  
 Per tutti gli altri tipi di dati, il valore di *cbValueOutMax* viene ignorato e la DLL di conversione presuppone che la dimensione di *rgbValueOut* sia la dimensione del tipo di dati C predefinito del tipo di dati SQL specificato con *fSqlType*.  
  
 L'argomento *pcbValueOut* può essere un puntatore null.  
  
 *Szerrormsg*  
 [Uscita] Puntatore all'archiviazione per un messaggio di errore. Si tratta di una stringa vuota a meno che la traduzione non sia riuscita.  
  
 *CbErrorMsgMax*  
 [Ingresso] Lunghezza di *szErrorMsg*.  
  
 *pcbErrorMsg (informazioni in due)*  
 [Uscita] Puntatore al numero totale di byte (escluso il byte di terminazione null) disponibile per la restituzione in *szErrorMsg*. Se è maggiore o uguale a *cbErrorMsg*, i dati in *szErrorMsg* vengono troncati in *cbErrorMsgMax* meno il carattere di terminazione null. L'argomento *pcbErrorMsg* può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 TRUE se la traduzione ha avuto esito positivo, FALSE se la traduzione non è riuscita.  
  
## <a name="comments"></a>Commenti  
 Il driver chiama **SQLDriverToDataSource** per convertire tutti i dati (istruzioni SQL, parametri e così via) passando dal driver all'origine dati. La DLL di conversione potrebbe non tradurre alcuni dati, a seconda del tipo di dati e dello scopo della DLL di conversione. Ad esempio, una DLL che converte i dati di tipo carattere da una tabella codici a un'altra ignora tutti i dati numerici e binari.  
  
 Il valore di *fOption* è impostato sul valore di *vParam* specificato chiamando **SQLSetConnectAttr** con il SQL_ATTR_TRANSLATE_OPTION attributo. Si tratta di un valore a 32 bit che ha un significato specifico per una determinata DLL di conversione. Ad esempio, potrebbe specificare una determinata conversione del set di caratteri.  
  
 Se viene specificato lo stesso buffer per *rgbValueIn* e *rgbValueOut*, verrà eseguita la conversione dei dati nel buffer.  
  
 Sebbene *cbValueIn*, *cbValueOutMax*e *pcbValueOut* siano di tipo SDWORD, **SQLDriverToDataSource** non supporta necessariamente puntatori di grandi dimensioni.  
  
 Se **SQLDriverToDataSource** restituisce FALSE, il troncamento dei dati potrebbe essersi verificato durante la conversione. Se *pcbValueOut* (il numero di byte disponibili per la restituzione nel buffer di output) è maggiore di *cbValueOutMax* (la lunghezza del buffer di output), si è verificato il troncamento. Il driver deve determinare se il troncamento è accettabile. Se il troncamento non si è verificato, **SQLDriverToDataSource** ha restituito FALSE a causa di un altro errore. In entrambi i casi, viene restituito un messaggio di errore specifico in *szErrorMsg*.  
  
 Per ulteriori informazioni sulla conversione dei dati, vedere [DLL di conversione](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Traduzione dei dati restituiti dall'origine dati|[SQLDataSourceToDriver (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|  
|Restituzione dell'impostazione di un attributo di connessioneReturning the setting of a connection attribute|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Impostazione di un attributo di connessione|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
