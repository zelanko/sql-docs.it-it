---
title: Funzione SQLGetEnvAttr . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77cd24386a8eea6769aee59f3674b681c516d9ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285311"
---
# <a name="sqlgetenvattr-function"></a>Funzione SQLGetEnvAttr
**Conformità**  
 Versione introdotta: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLGetEnvAttr** restituisce l'impostazione corrente di un attributo di ambiente.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *EnvironmentHandle*  
 [Ingresso] Maniglia dell'ambiente.  
  
 *Attributo*  
 [Ingresso] Attributo da recuperare.  
  
 *ValuePtr*  
 [Uscita] Puntatore a un buffer in cui restituire il valore corrente dell'attributo specificato da *Attribute*.  
  
 Se *ValuePtr* è NULL, *StringLengthPtr* restituirà comunque il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *ValuePtr*.  
  
 *BufferLength*  
 [Ingresso] Se *ValuePtr* punta a una stringa di caratteri, questo argomento deve essere la lunghezza di \* *ValuePtr*. Se \* *ValuePtr* è un numero intero, *BufferLength* viene ignorato. Se * \*ValuePtr* è una stringa Unicode (quando si chiama **SQLGetEnvAttrW**), l'argomento *BufferLength* deve essere un numero pari. Se il valore dell'attributo non è una stringa di caratteri, *BufferLength* è inutilizzato.  
  
 *StringLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il carattere di terminazione null) disponibile per la restituzione in * \*ValuePtr*. Se *ValuePtr* è un puntatore null, non viene restituita alcuna lunghezza. Se il valore dell'attributo è una stringa di caratteri e il numero di byte disponibili da restituire è maggiore o uguale a *BufferLength*, i dati in \* *ValuePtr* vengono troncati a *BufferLength* meno la lunghezza di un carattere di terminazione null e sono con terminazione null dal driver.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetEnvAttr** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_ENV e un *handle* di *EnvironmentHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetEnvAttr** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|I dati restituiti in \* *ValuePtr* sono stati troncati per essere *BufferLength* meno il carattere di terminazione null. La lunghezza del valore di stringa non troncato viene restituita in *, StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|Il driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) **SQL_ATTR_ODBC_VERSION** non è ancora stato impostato tramite **SQLSetEnvAttr**. Non è necessario impostare **SQL_ATTR_ODBC_VERSION** in modo esplicito se si utilizza **SQLAllocHandleStd**.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I092 (informazioni in stato IN CUI|Identificatore di attributo/opzione non valido|Il valore specificato per l'argomento *attributo* non è valido per la versione di ODBC supportata dal driver.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità facoltativa non implementataOptional feature not implemented|Il valore specificato per l'argomento *attributo* è un attributo di ambiente ODBC valido per la versione di ODBC supportata dal driver, ma non è supportato dal driver.|  
|IM001|Il driver non supporta questa funzione|(DM) Il driver corrispondente a *EnvironmentHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Per un elenco di attributi, vedere [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Non sono presenti attributi di ambiente specifici del driver. Se *Attribute* specifica un attributo che restituisce una stringa, *ValuePtr* deve essere un puntatore a un buffer in cui restituire la stringa. La lunghezza massima della stringa, incluso il byte di terminazione null, sarà *BufferLength* byte.  
  
 **SQLGetEnvAttr** può essere chiamato in qualsiasi momento tra l'allocazione e la liberazione di un handle di ambiente. Tutti gli attributi di ambiente impostati correttamente dall'applicazione per l'ambiente persistono fino a quando **SQLFreeHandle** viene chiamato su *EnvironmentHandle* con un *HandleType* di SQL_HANDLE_ENV. È possibile allocare contemporaneamente più handle di ambiente in ODBC 3 *.x*. Un attributo di ambiente in un ambiente non è interessato quando è stato allocato un altro ambiente.  
  
> [!NOTE]
>  L'attributo SQL_ATTR_OUTPUT_NTS environment è supportato da applicazioni conformi agli standard. Quando **SQLGetEnvAttr** viene chiamato, il Gestore Driver *.x* ODBC 3 restituisce sempre SQL_TRUE per questo attributo. SQL_ATTR_OUTPUT_NTS può essere impostata su SQL_TRUE solo da una chiamata a **SQLSetEnvAttr**.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione dell'impostazione di un attributo di connessioneReturning the setting of a connection attribute|[Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Restituzione dell'impostazione di un attributo di istruzioneReturning the setting of a statement attribute|[Funzione SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Impostazione di un attributo di connessione|[Pagina relativa alla funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Impostazione di un attributo di ambiente|[Funzione SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Impostazione di un attributo di istruzioneSetting a statement attribute|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
