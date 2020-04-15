---
title: Funzione SQLGetTranslator . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcd5aeebab8539b8b94db56ff30892f4a7dbbac1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303272"
---
# <a name="sqlgettranslator-function"></a>Funzione SQLGetTranslator
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLGetTranslator** visualizza una finestra di dialogo da cui un utente può selezionare un traduttore.  
  
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
 *hwndPadre*  
 [Ingresso] Handle della finestra padre.  
  
 *lpszName*  
 [Ingresso/Uscita] Nome del traduttore dalle informazioni di sistema.  
  
 *CbNomeMax*  
 [Ingresso] Lunghezza massima del buffer *lpszName.*  
  
 *pcbNomeEsterno (informazioni in stato inaziendale)*  
 [Ingresso/Uscita] Numero totale di byte (escluso il byte di terminazione null) passati o restituiti in *lpszName*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbNameMax*, il nome del convertitore in *lpszName* verrà troncato a *cbNameMax* meno il carattere di terminazione null. L'argomento *pcbNameOut* può essere un puntatore null.  
  
 *LpszPath (percorso ipinoso)*  
 [Uscita] Percorso completo della DLL di conversione.  
  
 *CbPathMax (incui)*  
 [Ingresso] Lunghezza massima del buffer *lpszPath.*  
  
 *pcbPathOut (informazioni in questo modo in stato di insta*  
 [Uscita] Numero totale di byte (escluso il byte di terminazione null) restituiti in *lpszPath*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbPathMax*, il percorso della DLL di conversione in *lpszPath* viene troncato a *cbPathMax* meno il carattere di terminazione null. L'argomento *pcbPathOut* può essere un puntatore null.  
  
 *pvOption (Opzione)*  
 [Output] opzione di conversione a 32 bit.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo o se l'utente annulla la finestra di dialogo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetTranslator** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza buffer non valida|*L'argomento cbNameMax* o *cbPathMax* è minore o uguale a 0.|  
|ODBC_ERROR_INVALID_HWND|Handle di finestra non valido|L'argomento *hwndParent* non è valido o NULL.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o del traduttore non valido|L'argomento *lpszName* non è valido. Non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Impossibile caricare il driver o la libreria di installazione del convertitore|Impossibile caricare la libreria del traduttore.|  
|ODBC_ERROR_INVALID_OPTION|Opzione di transazione non valida|L'argomento *pvOption* contiene un valore non valido.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 Se *hwndParent* è null o *lpszName*, *lpszPath*o *pvOption* è un puntatore null, **SQLGetTranslator** restituisce FALSE. In caso contrario, viene visualizzato l'elenco dei traduttori installati nella finestra di dialogo seguente.  
  
 ![Finestra di dialogo Selezione convertitore](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 Se *lpszName* contiene un nome di traduttore valido, viene selezionato. In \<caso contrario, non è selezionata alcuna> traduttore.  
  
 Se l'utente \<sceglie Nessun traduttore>, il contenuto di *lpszName*, *lpszPath*e *pvOption* non viene toccato. **SQLGetTranslator** imposta *pcbNameOut* e *pcbPathOut* su 0 e restituisce TRUE.  
  
 Se l'utente sceglie un traduttore, **SQLGetTranslator** chiama **ConfigTranslator** nella DLL di installazione del convertitore. Se **ConfigTranslator** restituisce FALSE, **SQLGetTranslator** torna alla relativa finestra di dialogo. Se **ConfigTranslator** restituisce TRUE, **SQLGetTranslator** restituisce TRUE, insieme al nome del traduttore, al percorso e all'opzione di conversione selezionati.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Configurazione di un traduttore|[Traduttore di configurazione](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Ottenere un attributo di traduzioneGetting a translation attribute|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Impostazione di un attributo di traduzione|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
