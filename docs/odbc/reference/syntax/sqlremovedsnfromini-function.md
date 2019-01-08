---
title: Funzione SQLRemoveDSNFromIni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbd405189d17051c4f1a6f07c943f77d6a6289c4
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207800"
---
# <a name="sqlremovedsnfromini-function"></a>Funzione SQLRemoveDSNFromIni
**Conformità**  
 Versione introdotta: ODBC 1.0  
  
 **Riepilogo**  
 **SQLRemoveDSNFromIni** rimuove un'origine dati dalle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszDSN*  
 [Input] Nome dell'origine dati da rimuovere.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se rimuove l'origine dati o l'origine dati non è presente nel file ini. Restituisce FALSE se non riesce a rimuovere l'origine dati.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRemoveDSNFromIni** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_DSN|DSN valido|Il *lpszDSN* argomento non è valido.|  
|ODBC_ERROR_REQUEST_FAILED|Richiesta non è riuscita|Il programma di installazione non è stato possibile rimuovere le informazioni di DSN dal Registro di sistema.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="comments"></a>Commenti  
 **SQLRemoveDSNFromIni** rimuove il nome dell'origine dati nella sezione [ODBC Zdroje dat] le informazioni di sistema. Rimuove inoltre la sezione specifica di origine dati dalle informazioni di sistema.  
  
 Questa funzione deve essere chiamata solo da una libreria di programma di installazione di driver.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un'origine dati|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Aggiunta, modifica o rimozione di un'origine dati|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Rimozione dell'origine dati predefinita|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Aggiunta di un nome dell'origine dati per le informazioni di sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
