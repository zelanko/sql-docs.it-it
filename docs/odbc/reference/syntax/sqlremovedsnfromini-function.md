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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 848e82741954ab24941d5d519699292727ca25d6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301800"
---
# <a name="sqlremovedsnfromini-function"></a>Funzione SQLRemoveDSNFromIni
**Conformità**  
 Versione introdotta: ODBC 1,0  
  
 **Riepilogo**  
 **SQLRemoveDSNFromIni** rimuove un'origine dati dalle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszDSN*  
 Input Nome dell'origine dati da rimuovere.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se l'origine dati viene rimossa o se l'origine dati non è presente nel file ODBC. ini. Restituisce FALSE se non è possibile rimuovere l'origine dati.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLRemoveDSNFromIni** restituisce false, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. La tabella seguente elenca i * \*valori pfErrorCode* che possono essere restituiti da **SQLInstallerError** e ne illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non è stato specificato alcun errore di programma di installazione.|  
|ODBC_ERROR_INVALID_DSN|DSN non valido|L'argomento *lpszDSN* non è valido.|  
|ODBC_ERROR_REQUEST_FAILED|Richiesta non riuscita|Il programma di installazione non è riuscito a rimuovere le informazioni DSN dal registro di sistema.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa di memoria insufficiente.|  
  
## <a name="comments"></a>Commenti  
 **SQLRemoveDSNFromIni** rimuove il nome dell'origine dati dalla sezione [origini dati ODBC] delle informazioni sul sistema. Consente inoltre di rimuovere la sezione specifica dell'origine dati dalle informazioni di sistema.  
  
 Questa funzione deve essere chiamata solo da una libreria di installazione driver.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Aggiunta, modifica o rimozione di un'origine dati|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Aggiunta, modifica o rimozione di un'origine dati|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Rimozione dell'origine dati predefinita|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Aggiunta di un nome di origine dati alle informazioni sul sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
