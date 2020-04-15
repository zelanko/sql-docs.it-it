---
title: 'Funzione SQLRemoveTranslator : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 348d2c5da0731ba88ccd4dd6406d3754890f7906
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301788"
---
# <a name="sqlremovetranslator-function"></a>Funzione SQLRemoveTranslator
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLRemoveTranslator** rimuove le informazioni su un traduttore dalla sezione Odbcinst.ini delle informazioni di sistema e decrementa il conteggio dell'utilizzo dei componenti del convertitore di 1.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszTranslator*  
 [Ingresso] Nome del traduttore registrato nella chiave Odbcinst.ini delle informazioni di sistema.  
  
 *lpdwUsageCount (conteggio informazioni in lingua lingua instato)*  
 [Uscita] Conteggio di utilizzo del traduttore dopo la chiamata a questa funzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo. Se non esiste alcuna voce nelle informazioni di sistema quando questa funzione viene chiamata, la funzione restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRemoveTranslator** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente non trovato nel Registro di sistema|Il programma di installazione non è riuscito a rimuovere le informazioni sul traduttore perché non esisteva nel Registro di sistema o non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o del traduttore non valido|L'argomento *lpszTranslator* non è valido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Impossibile incrementare o diminuire il conteggio di utilizzo del componente|Il programma di installazione non è riuscito a diminuire il conteggio di utilizzo del driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLRemoveTranslator** integra la funzione [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) e aggiorna il conteggio di utilizzo dei componenti nelle informazioni di sistema. Questa funzione deve essere chiamata solo da un'applicazione di installazione.  
  
 **SQLRemoveTranslator** decrementa il conteggio di utilizzo del componente di 1. Se il conteggio di utilizzo del componente è pari a 0, la voce del traduttore nelle informazioni di sistema verrà rimossa. La voce del traduttore si trova nella seguente posizione nelle informazioni di sistema, sotto il nome del traduttore:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** non rimuove effettivamente alcun file. Il programma chiamante è responsabile dell'eliminazione dei file e della gestione del conteggio di utilizzo dei file. Solo dopo che sia il conteggio di utilizzo del componente che il conteggio di utilizzo dei file hanno raggiunto lo zero, un file viene eliminato fisicamente. Alcuni file in un componente possono essere eliminati e altri non eliminati, a seconda che i file siano utilizzati da altre applicazioni che hanno incrementato il conteggio di utilizzo dei file.  
  
 **SQLRemoveTranslator** viene chiamato anche come parte di un processo di aggiornamento. Se un'applicazione rileva che è necessario eseguire un aggiornamento e ha installato il driver in precedenza, il driver deve essere rimosso e quindi reinstallato. **SQLRemoveTranslator** deve prima essere chiamato per diminuire il conteggio di utilizzo del componente, quindi **SQLInstallTranslatorEx** deve essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione deve sostituire fisicamente i vecchi file con i nuovi file. Il conteggio di utilizzo dei file rimarrà invariato e altre applicazioni che utilizzano i file della versione precedente utilizzeranno ora la versione più recente.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Installazione di un traduttore|[SQLInstallTranslatorEx (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
