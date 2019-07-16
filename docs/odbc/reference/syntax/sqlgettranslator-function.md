---
title: Funzione SQLGetTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTranslator
helpviewer_keywords:
- SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f769d3c5b2dcfe5d2aa8a431695cb18a52893b91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030647"
---
# <a name="sqlgettranslator-function"></a>Funzione SQLGetTranslator
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLGetTranslator** Visualizza una finestra di dialogo da cui un utente può selezionare una funzione di conversione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLGetTranslator(  
     HWND      hwndParent,  
     LPSTR     lpszName,  
     WORD      cbNameMax,  
     WORD *    pcbNameOut,  
     LPSTR     lpszPath,  
     WORD      cbPathMax,  
     WORD *    pcbPathOut,  
     DWORD *   pvOption);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwndParent*  
 [Input] Handle della finestra padre.  
  
 *lpszName*  
 [Input/Output] Nome del convertitore dalle informazioni di sistema.  
  
 *cbNameMax*  
 [Input] Lunghezza massima del *lpszName* buffer.  
  
 *pcbNameOut*  
 [Input/Output] Numero totale di byte (escluso il byte di terminazione null) passata o restituita nel *lpszName*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbNameMax*, il nome di funzione di conversione nella *lpszName* verrà troncato *cbNameMax* meno il carattere di terminazione null. Il *pcbNameOut* argomento può essere un puntatore null.  
  
 *lpszPath*  
 [Output] Percorso completo della DLL di conversione.  
  
 *cbPathMax*  
 [Input] Lunghezza massima del *lpszPath* buffer.  
  
 *pcbPathOut*  
 [Output] Numero totale di byte (escluso il byte di terminazione null) restituito in *lpszPath*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbPathMax*, il percorso della DLL nella traduzione *lpszPath* viene troncato a *cbPathMax* meno il carattere di terminazione null. Il *pcbPathOut* argomento può essere un puntatore null.  
  
 *pvOption*  
 Opzione di conversione a 32 bit [output].  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore o se l'utente annulla la finestra di dialogo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetTranslator** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza del buffer non valido|Il *cbNameMax* oppure *cbPathMax* argomento era minore o uguale a 0.|  
|ODBC_ERROR_INVALID_HWND|Handle della finestra valida|Il *hwndParent* argomento era NULL o non valido.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o traduttore non valido|Il *lpszName* argomento non è valido. Non trovato nel Registro di sistema.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Non è riuscito a caricare la libreria di programma di installazione driver o del convertitore.|Non è stato possibile caricare la libreria di Microsoft translator.|  
|ODBC_ERROR_INVALID_OPTION|Opzione di transazione non valido|Il *pvOption* argomento è presente un valore non valido.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 Se *hwndParent* è null o se *lpszName*, *lpszPath*, oppure *pvOption* è un puntatore null, **SQLGetTranslator** restituisce FALSE. In caso contrario, viene visualizzato l'elenco di traduttori installati nella finestra di dialogo seguente.  
  
 ![Selezionare la casella di dialogo Microsoft Translator](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 Se *lpszName* contiene un nome di funzione di conversione valido, questa opzione è selezionata. In caso contrario, \<Translator n > sia selezionata.  
  
 Se l'utente sceglie \<traduttore n >, il contenuto del *lpszName*, *lpszPath*, e *pvOption* non sono interessate. **SQLGetTranslator** imposta *pcbNameOut* e *pcbPathOut* su 0 e restituisce TRUE.  
  
 Se l'utente sceglie un traduttore **SQLGetTranslator** chiamate **ConfigTranslator** nella DLL di installazione di Microsoft translator. Se **ConfigTranslator** FALSO, restituisce **SQLGetTranslator** restituisce alla relativa finestra di dialogo. Se **ConfigTranslator** restituisce TRUE, **SQLGetTranslator** restituisce TRUE, insieme all'opzione di nome, percorso e traduzione Microsoft translator selezionato.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Configurazione di una funzione di conversione|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Recupero di un attributo di traduzione|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|L'impostazione di un attributo di traduzione|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
