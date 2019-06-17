---
title: Funzione SQLRemoveTranslator | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42513e6dcf32e21030e56fd3b386800b7525f534
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537145"
---
# <a name="sqlremovetranslator-function"></a>Funzione SQLRemoveTranslator
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLRemoveTranslator** Rimuove informazioni su una funzione di conversione dalla sezione delle informazioni di sistema e decrementa Odbcinst. ini conteggio di utilizzo di componenti di Microsoft translator di 1.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszTranslator*  
 [Input] Il nome di funzione di conversione come registrato nella chiave Odbcinst. ini di informazioni di sistema.  
  
 *lpdwUsageCount*  
 [Output] Il conteggio di utilizzo del convertitore dopo la chiamata a questa funzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore. Se le informazioni di sistema non esiste alcuna voce quando questa funzione viene chiamata, la funzione restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRemoveTranslator** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente non trovato nel Registro di sistema|Il programma di installazione non è stato possibile rimuovere le informazioni di Microsoft translator perché non esiste nel Registro di sistema o non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_INVALID_NAME|Nome del driver o traduttore non valido|Il *lpszTranslator* argomento non è valido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Non è stato possibile incrementare o decrementare il conteggio di utilizzo del componente|Il programma di installazione non è stato possibile diminuire il conteggio di utilizzo del driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLRemoveTranslator** si integra con i [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) funzione e gli aggiornamenti di utilizzo componente conteggio nelle informazioni di sistema. Questa funzione deve essere chiamata solo da un'applicazione di installazione.  
  
 **SQLRemoveTranslator** verrà decrementa il conteggio di utilizzo del componente di 1. Se il conteggio di utilizzo del componente è pari a 0, la voce di Microsoft translator nelle informazioni di sistema verrà rimossa. La voce di Microsoft translator è nel seguente percorso nelle informazioni di sistema, sotto il nome di funzione di conversione:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** non vengono effettivamente rimossi tutti i file. Il programma chiamante è responsabile per l'eliminazione di file e mantenere il conteggio di utilizzo di file. Solo dopo che hanno raggiunto il conteggio di utilizzo del componente sia il conteggio di utilizzo file zero è un file eliminato fisicamente. È possibile eliminare alcuni file in un componente e ad altri utenti non eliminati, a seconda del fatto che i file vengono usati da altre applicazioni che hanno incrementato il conteggio di utilizzo di file.  
  
 **SQLRemoveTranslator** nota anche come parte di un processo di aggiornamento. Se un'applicazione rileva che deve eseguire un aggiornamento e il driver è installato in precedenza, il driver debba essere rimossi e reinstallato. **SQLRemoveTranslator** deve essere chiamato prima di tutto per diminuire il conteggio di utilizzo del componente, quindi **SQLInstallTranslatorEx** deve essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione deve sostituire fisicamente i file precedenti con i nuovi file. Il conteggio di utilizzo file rimarranno invariati e altre applicazioni che usano i file di versioni precedenti useranno la versione più recente.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Installazione di una funzione di conversione|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
