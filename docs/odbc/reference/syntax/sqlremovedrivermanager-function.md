---
title: Funzione SQLRemoveDriverManager | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriverManager
helpviewer_keywords:
- SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3413cf3c0e316e25ad52cc35ba348cab1694ae4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537409"
---
# <a name="sqlremovedrivermanager-function"></a>Funzione SQLRemoveDriverManager
**Conformità**  
 Versione introdotta: ODBC 3.0: Deprecato in Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 e versioni successive.  
  
 **Riepilogo**  
 **SQLRemoveDriverManager** modifica o rimuove le informazioni sui componenti principali di ODBC dalla voce Odbcinst. ini nelle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argomenti  
 *pdwUsageCount*  
 [Output] Il conteggio di utilizzo di gestione Driver dopo la chiamata a questa funzione.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore. Se le informazioni di sistema non esiste alcuna voce quando questa funzione viene chiamata, la funzione restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRemoveDriverManager** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente non trovato nel Registro di sistema|Il programma di installazione non è stato possibile rimuovere le informazioni sul Driver Manager perché non esiste nel Registro di sistema o non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Non è stato possibile incrementare o decrementare il conteggio di utilizzo del componente|Il programma di installazione non è stato possibile diminuire il conteggio di utilizzo di gestione Driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLRemoveDriverManager** si integra con i **SQLInstallDriverManager** funzione e gli aggiornamenti contare l'utilizzo di componenti nelle informazioni di sistema. Questa funzione deve essere chiamata solo da un'applicazione di installazione.  
  
 **SQLRemoveDriverManager** verrà decrementa il conteggio di utilizzo di componenti di base di 1. Se il conteggio di utilizzo del componente è pari a 0, vengono rimosse le informazioni relative alla voce del sistema. La voce di componente principale è nel seguente percorso nelle informazioni di sistema, sotto il titolo "ODBC Core":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Un'applicazione non rimuovere fisicamente i file di Driver Manager quando il conteggio di utilizzo del componente e il conteggio di utilizzo file raggiunge zero.  
  
 **SQLRemoveDriverManager** non vengono effettivamente rimossi tutti i file. Il programma chiamante è responsabile per l'eliminazione di file e mantenere l'utilizzo di file conta. File di Gestione driver non deve tuttavia, essere rimossi quando il conteggio di utilizzo del componente sia il conteggio di utilizzo di file hanno raggiunto lo zero, poiché questi file possono essere utilizzati da altre applicazioni che non hanno incrementato il conteggio di utilizzo di file.  
  
 **SQLRemoveDriverManager** viene chiamata come parte del processo di disinstallazione. Componenti ODBC (che includono gestione Driver, libreria di cursori, programma di installazione, libreria di linguaggio, amministratore, i file thunk e così via) vengono disinstallati nel suo complesso. I file seguenti non vengono rimossi quando **SQLRemoveDriverManager** viene chiamata come parte del processo di disinstallazione:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32.DLL|  
|ODBCCR32.DLL|ODBC16GT.DLL|  
|ODBCCU32.DLL|ODBC32GT.DLL|  
|ODBCINT.DLL|DS16GT.DLL|  
|ODBCTRAC.DLL|DS32GT.DLL|  
|MSVCRT40.DLL|ODBCAD32.EXE|  
|ODBCCP32.CPL||  
  
 **SQLRemoveDriverManager** nota anche come parte di un processo di aggiornamento. Se un'applicazione rileva che deve eseguire un aggiornamento e il driver è installato in precedenza, il driver debba essere rimossi e reinstallato.  
  
 **SQLRemoveDriverManager** deve innanzitutto essere chiamato per diminuire il conteggio di utilizzo del componente. **SQLInstallDriverEx** deve essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione è necessario sostituire i file dei componenti di base precedente con i nuovi file. Il conteggio degli utilizzi il file rimarrà invariato e altre applicazioni che usano i file dei componenti principali versione precedenti useranno i file della versione più recente.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Installazione di una gestione Driver|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
