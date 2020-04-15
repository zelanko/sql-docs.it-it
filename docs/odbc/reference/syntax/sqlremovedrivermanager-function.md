---
title: SqlRemoveDriverManager (funzione) . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 27b32c1c4e0f3f4d5359af287ba07d40b033af00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301812"
---
# <a name="sqlremovedrivermanager-function"></a>Funzione SQLRemoveDriverManager
**Conformità**  
 Versione introdotta: ODBC 3.0: deprecato in Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 e sistemi operativi successivi.  
  
 **Riepilogo**  
 **SQLRemoveDriverManager** modifica o rimuove le informazioni sui componenti principali ODBC dalla voce Odbcinst.ini nelle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argomenti  
 *pdwUsageCount (conteggio utilizzo pdwUsageCount)*  
 [Uscita] Il conteggio di utilizzo di Gestione Driver dopo che questa funzione è stata chiamata.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo. Se non esiste alcuna voce nelle informazioni di sistema quando questa funzione viene chiamata, la funzione restituisce FALSE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRemoveDriverManager** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente non trovato nel Registro di sistema|Il programma di installazione non è riuscito a rimuovere le informazioni di Gestione Driver perché non esisteva nel Registro di sistema o non è stato trovato nel Registro di sistema.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Impossibile incrementare o diminuire il conteggio di utilizzo del componente|Il programma di installazione non è riuscito a diminuire il conteggio di utilizzo di Gestione Driver.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLRemoveDriverManager** integra la funzione **SQLInstallDriverManager** e aggiorna il conteggio di utilizzo dei componenti nelle informazioni di sistema. Questa funzione deve essere chiamata solo da un'applicazione di installazione.  
  
 **SQLRemoveDriverManager** decrementa il conteggio di utilizzo dei componenti di base di 1. Se il conteggio di utilizzo del componente è pari a 0, le informazioni di sistema della voce verranno rimosse. La voce principale del componente si trova nella seguente posizione nelle informazioni di sistema, sotto il titolo "ODBC Core":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Un'applicazione non deve rimuovere fisicamente i file di Driver Manager quando il conteggio di utilizzo dei componenti e il conteggio di utilizzo dei file raggiungono zero.  
  
 **SQLRemoveDriverManager** non rimuove effettivamente alcun file. Il programma chiamante è responsabile dell'eliminazione dei file e della gestione dei conteggi di utilizzo dei file. I file di Gestione Driver non devono tuttavia essere rimossi quando sia il conteggio di utilizzo dei componenti che il conteggio di utilizzo dei file hanno raggiunto lo zero, perché questi file possono essere utilizzati da altre applicazioni che non hanno incrementato il conteggio di utilizzo dei file.  
  
 **SQLRemoveDriverManager** viene chiamato come parte del processo di disinstallazione. I componenti di base ODBC (che includono Gestione Driver, Libreria di cursori, Programma di installazione, Libreria della lingua, Amministratore, thunking e così via) vengono disinstallati nel loro complesso. I seguenti file non vengono rimossi quando **SQLRemoveDriverManager** viene chiamato come parte del processo di disinstallazione:  
  
|||  
|-|-|  
|ODBC32DLL (ODBC32DLL)|ODBCCP32. DLL (DLL)|  
|ODBCCR32. DLL (DLL)|ODBC16GT. DLL (DLL)|  
|ODBCCU32. DLL (DLL)|ODBC32GT. DLL (DLL)|  
|ODBCINT. DLL (DLL)|DS16GT. DLL (DLL)|  
|ODBCTRAC. DLL (DLL)|DS32GT. DLL (DLL)|  
|MSVCRT40. DLL (DLL)|ODBCAD32. FILE EXE|  
|ODBCCP32. Cpl||  
  
 **SQLRemoveDriverManager** viene chiamato anche come parte di un processo di aggiornamento. Se un'applicazione rileva che è necessario eseguire un aggiornamento e ha installato il driver in precedenza, il driver deve essere rimosso e quindi reinstallato.  
  
 **SQLRemoveDriverManager** deve prima essere chiamato per diminuire il conteggio di utilizzo del componente. **SQLInstallDriverEx** deve quindi essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione deve sostituire i vecchi file dei componenti di base con i nuovi file. I conteggi di utilizzo dei file rimarranno invariati e le altre applicazioni che utilizzano i file dei componenti di base della versione precedente utilizzeranno ora i file della versione più recente.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Installazione di Gestione driver|[SQLInstallDriverManager (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
