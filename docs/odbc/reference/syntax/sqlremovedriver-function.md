---
title: Funzione SQLRemoveDriver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 274451cdd2d1c3d811e4105a6d646044537999f1
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537368"
---
# <a name="sqlremovedriver-function"></a>Funzione SQLRemoveDriver
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLRemoveDriver** modifica o rimuove le informazioni sul driver dalla voce Odbcinst. ini nelle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszDriver*  
 [Input] Il nome del driver come registrato nella chiave Odbcinst. ini di informazioni di sistema.  
  
 *fRemoveDSN*  
 [Input] I valori validi sono:  
  
 TRUE: Rimuovere associato con il driver specificato nel DSN *lpszDriver*. FALSE: Non rimuovere associato con il driver specificato nel DSN *lpszDriver*.  
  
 *lpdwUsageCount*  
 [Output] Il conteggio di utilizzo del driver dopo la chiamata a questa funzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore. Se le informazioni di sistema non esiste alcuna voce quando questa funzione viene chiamata, la funzione restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRemoveDriver** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente non trovato nel Registro di sistema|Il programma di installazione non è stato possibile rimuovere le informazioni del driver perché non esiste nel Registro di sistema o non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o traduttore non valido|Il *lpszDriver* argomento non è valido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Non è stato possibile incrementare o decrementare il conteggio di utilizzo del componente|Il programma di installazione non è stato possibile diminuire il conteggio di utilizzo del driver.|  
|ODBC_ERROR_REQUEST_FAILED|Richiesta non è riuscita|Il *fRemoveDSN* argomento era TRUE; tuttavia, non è stato possibile rimuovere uno o più DSN. La chiamata a **SQLConfigDriver** con la richiesta ODBC_REMOVE_DRIVER non è riuscita.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLRemoveDriver** si integra con i [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) funzione e gli aggiornamenti di utilizzo componente conteggio nelle informazioni di sistema. Questa funzione deve essere chiamata solo da un'applicazione di installazione.  
  
 **SQLRemoveDriver** verrà ridotto il valore del conteggio componente sull'utilizzo di 1. Se il conteggio di utilizzo del componente è pari a 0, si verificherà quanto segue:  
  
1.  Il **SQLConfigDriver** canonica con l'opzione ODBC_REMOVE_DRIVER verrà chiamato. Se il *fRemoveDSN* opzione è impostata su TRUE, il **ConfigDSN** chiamate di funzione **SQLRemoveDSNFromIni** per rimuovere tutte le origini dati associate con il driver specificato in *lpszDriver.* Se il *fRemoveDSN* opzione è impostata su FALSE, le origini dati non verranno eliminate.  
  
2.  Verrà rimossa la voce driver nelle informazioni di sistema. La voce driver è nel seguente percorso informazioni sistema, sotto il nome del driver:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** non vengono effettivamente rimossi tutti i file. Il programma chiamante è responsabile per l'eliminazione di file e mantenere il conteggio di utilizzo di file. Solo dopo che hanno raggiunto il conteggio di utilizzo del componente sia il conteggio di utilizzo file zero è un file eliminato fisicamente. È possibile eliminare alcuni file in un componente e ad altri utenti non eliminati, a seconda del fatto che i file vengono usati da altre applicazioni che hanno incrementato il conteggio di utilizzo di file.  
  
 **SQLRemoveDriver** nota anche come parte di un processo di aggiornamento. Se un'applicazione rileva che deve eseguire un aggiornamento e il driver è installato in precedenza, il driver debba essere rimossi e reinstallato. **SQLRemoveDriver** deve essere chiamato prima di tutto per diminuire il conteggio di utilizzo del componente, quindi **SQLInstallDriverEx** deve essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione è necessario sostituire i vecchi file con i nuovi file. Il conteggio di utilizzo file rimarranno invariati e altre applicazioni che usano i file di versioni precedenti useranno la versione più recente.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un driver|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (nel programma di installazione DLL)|  
|Aggiunta, modifica o rimozione di un driver|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Installazione di un driver|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
