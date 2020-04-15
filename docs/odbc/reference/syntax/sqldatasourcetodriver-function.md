---
title: SqlDataSourceToDriver (funzione) . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92df58b76a9a11d0d4ab9821756bff014ecae29a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301191"
---
# <a name="sqldatasourcetodriver-function"></a>Funzione SQLDataSourceToDriver
**SQLDataSourceToDriver** supporta le traduzioni per i driver ODBC. Questa funzione non viene chiamata dalle applicazioni abilitate per ODBC; le applicazioni richiedono la conversione tramite **SQLSetConnectAttr**. Il driver associato al *ConnectionHandle* specificato in **SQLSetConnectAttr** chiama la DLL specificata per eseguire le conversioni di tutti i dati che scorrono dall'origine dati al driver. È possibile specificare una DLL di conversione predefinita nel file di inizializzazione ODBC.  
  
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
 *fOpzione*  
 [Ingresso] Valore dell'opzione.  
  
 *fSqlType (tipo di codice)*  
 [Ingresso] Tipo di dati SQL. Questo argomento indica al driver come convertire *rgbValueIn* in un formato accettabile per l'applicazione. Per un elenco dei tipi di dati SQL validi, vedere la sezione [Tipi di dati SQL](../../../odbc/reference/appendixes/sql-data-types.md) nell'Appendice D: Tipi di dati.  
  
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
 Il driver chiama **SQLDataSourceToDriver** per convertire tutti i dati (dati del set di risultati, nomi di tabelle, conteggi delle righe, messaggi di errore e così via) passando dall'origine dati al driver. La DLL di conversione potrebbe non tradurre alcuni dati, a seconda del tipo di dati e dello scopo della DLL di conversione. ad esempio, una DLL che converte i dati di tipo carattere da una tabella codici a un'altra ignora tutti i dati numerici e binari.  
  
 Il valore di *fOption* è impostato sul valore di *vParam* specificato chiamando **SQLSetConnectAttr** con il SQL_ATTR_TRANSLATE_OPTION attributo. Si tratta di un valore a 32 bit che ha un significato specifico per una determinata DLL di conversione. Ad esempio, potrebbe specificare una determinata conversione del set di caratteri.  
  
 Se viene specificato lo stesso buffer per *rgbValueIn* e *rgbValueOut*, verrà eseguita la conversione dei dati nel buffer.  
  
 Sebbene *cbValueIn*, *cbValueOutMax*e *pcbValueOut* siano di tipo SDWORD, **SQLDataSourceToDriver** non supporta necessariamente puntatori di grandi dimensioni.  
  
 Se **SQLDataSourceToDriver** restituisce FALSE, il troncamento dei dati potrebbe essersi verificato durante la conversione. Se *pcbValueOut* (il numero di byte disponibili per la restituzione nel buffer di output) è maggiore di *cbValueOutMax* (la lunghezza del buffer di output), si è verificato il troncamento. Il driver deve determinare se il troncamento è accettabile. Se il troncamento non si è verificato, **SQLDataSourceToDriver** ha restituito FALSE a causa di un altro errore. In entrambi i casi, viene restituito un messaggio di errore specifico in *szErrorMsg*.  
  
 Per ulteriori informazioni sulla conversione dei dati, vedere [DLL di conversione](../../../odbc/reference/develop-app/translation-dlls.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Traduzione dei dati inviati all'origine dati|[SQLDriverToDataSourceSQLDriverToDataSource](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|  
|Restituzione dell'impostazione di un attributo di connessioneReturning the setting of a connection attribute|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Impostazione di un attributo di connessione|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
