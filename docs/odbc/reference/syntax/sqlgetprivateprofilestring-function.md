---
title: Funzione SQLGetPrivateProfileString . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c12fc8d08535960cbb239c14e017b2ad5faa6c0e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303293"
---
# <a name="sqlgetprivateprofilestring-function"></a>Funzione SQLGetPrivateProfileString
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLGetPrivateProfileString** ottiene un elenco di nomi di valori o dati corrispondenti a un valore delle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszSezione*  
 [Ingresso] Punta a una stringa con terminazione null che specifica la sezione contenente il nome della chiave. Se questo argomento è NULL, la funzione copia tutti i nomi di sezione nel file nel buffer fornito.  
  
 *LpszEntry (ingresso )*  
 [Ingresso] Punta alla stringa con terminazione null contenente il nome della chiave di cui deve essere recuperata la stringa associata. Se questo argomento è NULL, tutti i nomi di chiave nella sezione specificata dall'argomento *lpszSection* vengono copiati nel buffer specificato dall'argomento *RetBuffer.*  
  
 *lpszDefault (impostazione predefinita)*  
 [Ingresso] Punta a una stringa con terminazione null che specifica il valore predefinito per la chiave specificata se non è possibile trovare la chiave nel file di inizializzazione. Questo argomento non può essere null.  
  
 *RetBuffer (RetBuffer)*  
 [Uscita] Punta al buffer che riceve la stringa recuperata.  
  
 *cbRetBuffer (t).*  
 [Ingresso] Specifica la dimensione, in caratteri, del buffer a cui punta l'argomento *RetBuffer.*  
  
 *LpszNome utente*  
 [Ingresso] Punta a una stringa con terminazione null che denomina il file di inizializzazione. Se questo argomento non contiene un percorso completo del file, viene eseguita la ricerca nella directory predefinita.  
  
## <a name="returns"></a>Valori di codice restituiti  
 **SQLGetPrivateProfileString** restituisce un valore intero che indica il numero di caratteri letti.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando una chiamata a **SQLGetPrivateProfileString** ha esito negativo, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLGetPrivateProfileString** viene fornito come un modo semplice per convertire i driver e le DLL di installazione dei driver da Microsoft® Windows® a Microsoft Windows NT®/Windows 2000. Le chiamate a **GetPrivateProfileString** che recuperano una stringa di profilo dal file Odbc.ini devono essere sostituite con chiamate a **SQLGetPrivateProfileString**. **SQLGetPrivateProfileString** chiama le funzioni nell'API ® Win32 per recuperare i nomi richiesti di valori o dati corrispondenti a un valore della sottochiave Odbc.ini delle informazioni di sistema.  
  
 La modalità di configurazione (come impostata da **SQLSetConfigMode**) indica la posizione della voce Odbc.ini in cui si trovano i valori DSN nelle informazioni di sistema. Se il DSN è un DSN utente (la modalità di configurazione è USERDSN_ONLY), la funzione legge dalla voce Odbc.ini in HKEY_CURRENT_USER. Se il DSN è un DSN di sistema (SYSTEMDSN_ONLY), la funzione legge dalla voce Odbc.ini in HKEY_LOCAL_MACHINE. Se la modalità di configurazione è BOTHDSN, HKEY_CURRENT_USER viene tentata e, in caso di errore, viene utilizzato HKEY_LOCAL_MACHINE.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Scrittura di un valore per le informazioni di sistema|[OGGETTO SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
