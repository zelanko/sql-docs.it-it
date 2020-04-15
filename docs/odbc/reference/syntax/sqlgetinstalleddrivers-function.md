---
title: Proprietà SQLGetInstalledDrivers ( funzione) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24793473bf4f25253ac11673df852d10cfb2c558
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303328"
---
# <a name="sqlgetinstalleddrivers-function"></a>Funzione SQLGetInstalledDrivers
**Conformità**  
 Versione introdotta: ODBC 1.0  
  
 **Riepilogo**  
 **SQLGetInstalledDrivers** legge la sezione [ODBC Drivers] delle informazioni di sistema e restituisce un elenco di descrizioni dei driver installati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszBuf*  
 [Uscita] Elenco delle descrizioni dei driver installati. Per informazioni sulla struttura dell'elenco, vedere "Commenti".  
  
 *cbBufMax*  
 [Ingresso] Lunghezza di *lpszBuf*.  
  
 *pcbBufOut (informazioni in questo base sfiorare il pcb*  
 [Uscita] Numero totale di byte (escluso il byte di terminazione null) restituiti in *lpszBuf*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbBufMax*, l'elenco delle descrizioni dei driver in *lpszBuf* viene troncato a *cbBufMax* meno il carattere di terminazione null. L'argomento *pcbBufOut* può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetInstalledDrivers** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza buffer non valida|L'argomento *lpszBuf* era NULL o non valido oppure l'argomento *cbBufMax* era minore o uguale a 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente non trovato nel Registro di sistema|Il programma di installazione non è riuscito a trovare la sezione [ODBC Drivers] nel Registro di sistema.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 Ogni descrizione del driver viene terminata con un byte null e l'intero elenco viene terminato con un byte null. (Ovvero, due byte null segnano la fine dell'elenco.) Se il buffer allocato non è sufficientemente grande per contenere l'intero elenco, l'elenco viene troncato senza errori. Se un puntatore null viene passato come *lpszBuf*, viene restituito un errore.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione delle descrizioni e degli attributi dei driver|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
