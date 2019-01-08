---
title: Funzione SQLInstallDriverManager | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47069f1003b9b3f9bddb1e8601b3b4284372ae7e
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205190"
---
# <a name="sqlinstalldrivermanager-function"></a>Funzione SQLInstallDriverManager
**Conformità**  
 Versione introdotta: ODBC 1.0: Deprecato in Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 e versioni successive  
  
 **Riepilogo**  
 **SQLInstallDriverManager** restituisce il percorso della directory di destinazione per l'installazione dei componenti ODBC core. Il programma chiamante effettivamente necessario copiare i file di gestione Driver nella directory di destinazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszPath*  
 [Output] Percorso della directory di destinazione dell'installazione.  
  
 *cbPathMax*  
 [Input] Lunghezza di *lpszPath*. Deve essere almeno byte di MAX_PATH.  
  
 *pcbPathOut*  
 [Output] Numero totale di byte (escluso il byte di terminazione null) restituito in *lpszPath*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbPathMax*, il percorso nella *lpszPath* verrà troncato *cbPathMax* meno la terminazione di tipo null carattere. Il *pcbPathOut* argomento può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLInstallDriverManager** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza del buffer non valido|Il *lpszPath* argomento non era sufficientemente grande da contenere il percorso di output. Il buffer contiene il percorso troncato.<br /><br /> Il *cbPathMax* argomento era inferiore a MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Non è stato possibile incrementare o decrementare il conteggio di utilizzo del componente|Il programma di installazione non riuscita a incrementare il conteggio di utilizzo ODBC core componente.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLInstallDriverManager** viene chiamata per restituire il percorso per il conteggio componenti di base ODBC e incrementare l'utilizzo di componenti nelle informazioni di sistema. Se esiste già una versione di gestione Driver, ma il conteggio di utilizzo del componente per il driver non esiste, il nuovo valore di conteggio dell'utilizzo di componente è impostato su 2.  
  
 Il programma di installazione dell'applicazione è responsabile per copiare fisicamente i file dei componenti di base e mantenendo l'utilizzo di file conta. Se un file di componente principale non è stato precedentemente installato, il programma di installazione dell'applicazione deve copiare il file e creare il conteggio di utilizzo di file. Se il file è stato precedentemente installato, il programma di installazione viene semplicemente incrementato il conteggio di utilizzo di file.  
  
 Se una versione precedente di gestione Driver è stato precedentemente installata dal programma di installazione dell'applicazione, i componenti di base devono essere disinstallati e reinstallati, in modo che il conteggio di utilizzo del componente principale è valido. **SQLRemoveDriverManager** deve innanzitutto essere chiamato per diminuire il conteggio di utilizzo del componente. **SQLInstallDriverManager** deve essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione è necessario sostituire i file dei componenti di base precedente con i nuovi file. Il conteggio degli utilizzi il file rimarrà invariato e altre applicazioni che utilizzato i file componente principale di versioni precedenti useranno i file della versione più recente.  
  
 In una nuova installazione di componenti di base di ODBC, driver e i traduttori, il programma di installazione dell'applicazione deve chiamare le funzioni seguenti in sequenza: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLConfigDriver** (con un *trattano* di ODBC_INSTALL_DRIVER) e quindi  **SQLInstallTranslatorEx**. In una disinstallazione dei componenti di base, driver e i traduttori, il programma di installazione dell'applicazione deve chiamare le funzioni seguenti in sequenza: **SQLRemoveTranslator**, **SQLRemoveDriver**, quindi **SQLRemoveDriverManager**. Queste funzioni devono essere chiamate in questa sequenza. In un aggiornamento di tutti i componenti, tutte le funzioni di disinstallazione devono essere chiamate in sequenza e quindi tutte le funzioni di installazione devono essere chiamate in sequenza.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un driver|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Installazione di un driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Installazione di una funzione di conversione|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Rimozione di un driver|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Rimozione di gestione Driver|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Rimozione di una funzione di conversione|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
