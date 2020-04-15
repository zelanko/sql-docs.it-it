---
title: SqlInstallDriverManager (funzione) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverManager
helpviewer_keywords:
- SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0788de0493439a360c0446733b31606a02e12422
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302112"
---
# <a name="sqlinstalldrivermanager-function"></a>Funzione SQLInstallDriverManager
**Conformità**  
 Versione introdotta: ODBC 1.0: deprecato in Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 e sistemi operativi successivi  
  
 **Riepilogo**  
 **SQLInstallDriverManager** restituisce il percorso della directory di destinazione per l'installazione dei componenti di base ODBC. Il programma chiamante deve effettivamente copiare i file di Gestione Driver nella directory di destinazione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>Argomenti  
 *LpszPath (percorso ipinoso)*  
 [Uscita] Percorso della directory di destinazione dell'installazione.  
  
 *CbPathMax (incui)*  
 [Ingresso] Lunghezza di *lpszPath*. Deve essere di almeno _MAX_PATH byte.  
  
 *pcbPathOut (informazioni in questo modo in stato di insta*  
 [Uscita] Numero totale di byte (escluso il byte di terminazione null) restituiti in *lpszPath*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbPathMax*, il percorso in *lpszPath* verrà troncato a *cbPathMax* meno il carattere di terminazione null. L'argomento *pcbPathOut* può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLInstallDriverManager** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza buffer non valida|L'argomento *lpszPath* non è sufficientemente grande per contenere il percorso di output. Il buffer contiene il percorso troncato.<br /><br /> L'argomento *cbPathMax* era minore di _MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Impossibile incrementare o diminuire il conteggio di utilizzo del componente|Il programma di installazione non è riuscito a incrementare il conteggio di utilizzo dei componenti di base ODBC.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLInstallDriverManager** viene chiamato per restituire il percorso per i componenti di base ODBC e incrementare il conteggio di utilizzo dei componenti nelle informazioni di sistema. Se esiste già una versione di Gestione Driver ma il conteggio di utilizzo del componente per il driver non esiste, il nuovo valore del conteggio di utilizzo del componente è impostato su 2.  
  
 Il programma di installazione dell'applicazione è responsabile della copia fisica dei file dei componenti principali e della gestione dei conteggi di utilizzo dei file. Se in precedenza non è stato installato un file componente principale, il programma di installazione dell'applicazione deve copiare il file e creare il conteggio di utilizzo del file. Se il file è stato installato in precedenza, il programma di installazione incrementa semplicemente il conteggio di utilizzo del file.  
  
 Se una versione precedente di Gestione Driver è stata installata in precedenza dal programma di installazione dell'applicazione, i componenti di base devono essere disinstallati e quindi reinstallati, in modo che il conteggio di utilizzo dei componenti di base sia valido. **SQLRemoveDriverManager** deve prima essere chiamato per diminuire il conteggio di utilizzo del componente. **SQLInstallDriverManager** deve quindi essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione deve sostituire i vecchi file dei componenti di base con i nuovi file. I conteggi di utilizzo dei file rimarranno invariati e le altre applicazioni che utilizzavano i file dei componenti di base della versione precedente utilizzeranno i file della versione più recente.  
  
 In una nuova installazione dei componenti di base, dei driver e dei traduttori ODBC, il programma di installazione dell'applicazione deve chiamare le seguenti funzioni in sequenza: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLConfigDriver** (con *una richiesta* di ODBC_INSTALL_DRIVER) e quindi **SQLInstallTranslatorEx**. In una disinstallazione dei componenti di base, dei driver e dei traduttori, il programma di installazione dell'applicazione deve chiamare le seguenti funzioni in sequenza: **SQLRemoveTranslator**, **SQLRemoveDriver**e quindi **SQLRemoveDriverManager**. Queste funzioni devono essere chiamate in questa sequenza. In un aggiornamento di tutti i componenti, tutte le funzioni di disinstallazione devono essere chiamate in sequenza e quindi tutte le funzioni di installazione devono essere chiamate in sequenza.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un driver|[SQLConfigDriver (driver)](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Installazione di un driver|[SQLInstallDriverEx (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Installazione di un traduttore|[SQLInstallTranslatorEx (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Rimozione di un driver|[SQLRemoveDriver (sqlRemoveDriver)](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Rimozione di Gestione driver|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Rimozione di un traduttore|[SQLRemoveTranslator (TraduttorediSQLRemoveTranslator)](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
