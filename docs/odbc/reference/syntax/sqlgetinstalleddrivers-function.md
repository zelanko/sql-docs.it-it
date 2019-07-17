---
title: Funzione SQLGetInstalledDrivers | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e7b079e2b66f4e1ba7b3233a6aaa20cd9908a67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061519"
---
# <a name="sqlgetinstalleddrivers-function"></a>Funzione SQLGetInstalledDrivers
**Conformità**  
 Versione introdotta: ODBC 1.0  
  
 **Riepilogo**  
 **SQLGetInstalledDrivers** legge la sezione [ODBC Drivers] le informazioni di sistema e restituisce un elenco di descrizioni dei driver installati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszBuf*  
 [Output] Elenco delle descrizioni dei driver installati. Per informazioni sulla struttura dell'elenco, vedere "Commenti".  
  
 *cbBufMax*  
 [Input] Lunghezza di *lpszBuf*.  
  
 *pcbBufOut*  
 [Output] Numero totale di byte (escluso il byte di terminazione null) restituito in *lpszBuf*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbBufMax*, l'elenco delle descrizioni di driver in *lpszBuf* verrà troncato *cbBufMax* meno di carattere di terminazione null. Il *pcbBufOut* argomento può essere un puntatore null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLGetInstalledDrivers** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza del buffer non valido|Il *lpszBuf* argomento era NULL o non valido, o il *cbBufMax* argomento era minore o uguale a 0.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente non trovato nel Registro di sistema|Il programma di installazione non è stato possibile trovare la sezione [ODBC Drivers] del Registro di sistema.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 Ogni descrizione del driver viene terminata con un byte null e l'intero elenco viene terminata con un byte null. (Vale a dire, due byte null contrassegnano la fine dell'elenco.) Se il buffer allocato non è sufficientemente grande da contenere l'elenco completo, l'elenco viene troncato senza errori. Viene restituito un errore se un puntatore null viene passato come *lpszBuf*.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione di attributi e le descrizioni di driver|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
