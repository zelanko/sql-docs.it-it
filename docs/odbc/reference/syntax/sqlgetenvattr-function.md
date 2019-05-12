---
title: Funzione SQLGetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d09182bc39d99a99f3d03957e296c91101b0fe5
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538140"
---
# <a name="sqlgetenvattr-function"></a>Funzione SQLGetEnvAttr
**Conformità**  
 Versione introdotta: Conformità agli standard 3.0 di ODBC: ISO 92  
  
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
 [Input] Handle di ambiente.  
  
 *Attribute*  
 [Input] Attributo da recuperare.  
  
 *ValuePtr*  
 [Output] Puntatore a un buffer in cui restituire il valore corrente dell'attributo specificato da *attributo*.  
  
 Se *ValuePtr* sia impostato su NULL *StringLengthPtr* continuerà a restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta  *ValuePtr*.  
  
 *BufferLength*  
 [Input] Se *ValuePtr* punta a una stringa di caratteri, la lunghezza di questo argomento deve essere \* *ValuePtr*. Se \* *ValuePtr* è un intero *BufferLength* viene ignorato. Se  *\*ValuePtr* è una stringa Unicode (quando si chiama **SQLGetEnvAttrW**), il *BufferLength* argomento deve essere un numero pari. Se il valore dell'attributo non è una stringa di caratteri *BufferLength* risulta inutilizzato.  
  
 *StringLengthPtr*  
 [Output] Un puntatore a un buffer in cui restituire il numero totale di byte (escluso il carattere di terminazione null) disponibili per restituire  *\*ValuePtr*. Se *ValuePtr* è un puntatore null, non viene restituita alcuna lunghezza. Se il valore dell'attributo è una stringa di caratteri e il numero di byte disponibili da restituire è maggiore o uguale a *BufferLength*, i dati in \* *ValuePtr* viene troncato a  *BufferLength* meno la lunghezza di un carattere di terminazione null ed è con terminazione null dal driver.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetEnvAttr** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato possono essere ottenuti chiamando **SQLGetDiagRec** con un *HandleType* di SQL _ HANDLE_ENV e un *gestiscono* dei *EnvironmentHandle*. Nella tabella seguente sono elencati i valori SQLSTATE comunemente restituiti da **SQLGetEnvAttr** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|Messaggio informativo specifico del driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|I dati restituiti nella \* *ValuePtr* sono stati troncati per essere *BufferLength* meno il carattere di terminazione null. Viene restituita la lunghezza del valore della stringa non troncato **StringLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|Il driver è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) **SQL_ATTR_ODBC_VERSION** non è ancora stata impostata tramite **SQLSetEnvAttr**. Non è necessario impostare **SQL_ATTR_ODBC_VERSION** in modo esplicito se si usa **SQLAllocHandleStd**.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY092|Identificatore di attributo/opzione non è valido|Il valore specificato per l'argomento *attributo* non è valido per la versione di ODBC supportati dal driver.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Funzionalità opzionale non implementata|Il valore specificato per l'argomento *attributo* era un attributo di ambiente ODBC valido per la versione di ODBC supportati dal driver, ma non era supportata dal driver.|  
|IM001|Driver non supporta questa funzione|(DM) il driver corrispondente per il *EnvironmentHandle* non supporta la funzione.|  
  
## <a name="comments"></a>Commenti  
 Per un elenco di attributi, vedere [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Non sono presenti attributi di ambiente specifiche del driver. Se *attributo* specifica un attributo che restituisce una stringa *ValuePtr* deve essere un puntatore a un buffer in cui restituire la stringa. La lunghezza massima della stringa, incluso il byte di terminazione null, saranno *BufferLength* byte.  
  
 **SQLGetEnvAttr** può essere chiamato in qualsiasi momento tra l'allocazione e la liberazione di un handle di ambiente. Tutti gli attributi di ambiente è stati impostati dall'applicazione per l'ambiente vengono mantenute fino **SQLFreeHandle** viene chiamato sulle *EnvironmentHandle* con un *HandleType*SQL_HANDLE_ENV. Più di un handle di ambiente può essere allocato contemporaneamente in ODBC 3*x*. Un attributo di ambiente in un unico ambiente non viene modificato quando è stato allocato un altro ambiente.  
  
> [!NOTE]
>  L'attributo di ambiente SQL_ATTR_OUTPUT_NTS è supportato dalle applicazioni conformi agli standard. Quando **SQLGetEnvAttr** viene chiamato, ODBC 3*x* gestione Driver restituisce sempre SQL_TRUE per questo attributo. SQL_ATTR_OUTPUT_NTS può essere impostato su SQL_TRUE solo da una chiamata a **SQLSetEnvAttr**.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituisce l'impostazione di un attributo di connessione|[Funzione SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Restituisce l'impostazione di un attributo di istruzione|[Funzione SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Impostare un attributo di connessione|[Funzione SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|L'impostazione di un attributo di ambiente|[Funzione SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|L'impostazione di un attributo di istruzione|[Funzione SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
