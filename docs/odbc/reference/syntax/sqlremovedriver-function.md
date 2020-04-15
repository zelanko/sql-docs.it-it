---
title: SQLRemoveDriver (funzione) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriver
helpviewer_keywords:
- SQLRemoveDriver function [ODBC]
ms.assetid: 9a3b4f8b-982b-44b9-ade6-754ff026dc90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 205c5b46e5f6cea195094f7a50e81d7509927d1a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303932"
---
# <a name="sqlremovedriver-function"></a>Funzione SQLRemoveDriver
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLRemoveDriver** modifica o rimuove le informazioni sul driver dalla voce Odbcinst.ini nelle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszDriver*  
 [Ingresso] Nome del driver registrato nella chiave Odbcinst.ini delle informazioni di sistema.  
  
 *fRemoveDSN (RimozioneDSN)*  
 [Ingresso] I valori validi sono:  
  
 TRUE: rimuovere i DSN associati al driver specificato in *lpszDriver*. FALSE: non rimuovere i DSN associati al driver specificato in *lpszDriver*.  
  
 *lpdwUsageCount (conteggio informazioni in lingua lingua instato)*  
 [Uscita] Il conteggio di utilizzo del driver dopo la chiamata a questa funzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo. Se non esiste alcuna voce nelle informazioni di sistema quando questa funzione viene chiamata, la funzione restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRemoveDriver** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente non trovato nel Registro di sistema|Il programma di installazione non è riuscito a rimuovere le informazioni sul driver perché non esisteva nel Registro di sistema o non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o del traduttore non valido|L'argomento *lpszDriver* non è valido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Impossibile incrementare o diminuire il conteggio di utilizzo del componente|Il programma di installazione non è riuscito a diminuire il conteggio di utilizzo del driver.|  
|ODBC_ERROR_REQUEST_FAILED|Richiesta non riuscita|L'argomento *fRemoveDSN* era VERO. Tuttavia, non è stato possibile rimuovere uno o più DSN. La chiamata a **SQLConfigDriver** con la richiesta di ODBC_REMOVE_DRIVER non riuscita.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLRemoveDriver** integra la funzione [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) e aggiorna il conteggio di utilizzo dei componenti nelle informazioni di sistema. Questa funzione deve essere chiamata solo da un'applicazione di installazione.  
  
 **SQLRemoveDriver** decrementa il valore del conteggio di utilizzo del componente di 1. Se il conteggio di utilizzo del componente è pari a 0, si verificherà quanto segue:  
  
1.  Verrà chiamata la funzione **SQLConfigDriver** con l'opzione ODBC_REMOVE_DRIVER. Se l'opzione *fRemoveDSN* è impostata su TRUE, la funzione **ConfigDSN** chiama **SQLRemoveDSNFromIni** per rimuovere tutte le origini dati associate al driver specificato in *lpszDriver.* Se l'opzione *fRemoveDSN* è impostata su FALSE, le origini dati non verranno eliminate.  
  
2.  La voce del driver nelle informazioni di sistema verrà rimossa. La voce del driver si trova nel seguente percorso di informazioni di sistema, sotto il nome del driver:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** non rimuove effettivamente alcun file. Il programma chiamante è responsabile dell'eliminazione dei file e della gestione del conteggio di utilizzo dei file. Solo dopo che sia il conteggio di utilizzo del componente che il conteggio di utilizzo dei file hanno raggiunto lo zero, un file viene eliminato fisicamente. Alcuni file in un componente possono essere eliminati e altri non eliminati, a seconda che i file siano utilizzati da altre applicazioni che hanno incrementato il conteggio di utilizzo dei file.  
  
 **SQLRemoveDriver** viene chiamato anche come parte di un processo di aggiornamento. Se un'applicazione rileva che è necessario eseguire un aggiornamento e ha installato il driver in precedenza, il driver deve essere rimosso e quindi reinstallato. **SQLRemoveDriver** deve prima essere chiamato per diminuire il conteggio di utilizzo del componente e quindi **SQLInstallDriverEx** deve essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione deve sostituire i vecchi file con i nuovi file. Il conteggio di utilizzo dei file rimarrà invariato e altre applicazioni che utilizzano i file della versione precedente utilizzeranno ora la versione più recente.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (nella DLL del programma di installazione)|  
|Aggiunta, modifica o rimozione di un driver|[SQLConfigDriver (driver)](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Installazione di un driver|[SQLInstallDriverEx (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
