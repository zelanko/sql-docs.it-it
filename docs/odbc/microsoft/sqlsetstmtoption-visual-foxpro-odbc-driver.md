---
title: SQLSetStmtOption (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a026922cb98fdb520c9eeab223c8b34a231a179e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905333"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello 1  
  
 Imposta le opzioni correlate a un handle di istruzione, *HSTMT*.  
  
|*fOption*|Valori consentiti|Commenti|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Se si tenta di impostare questo *fOption*, il driver restituirà l'errore: "driver non in grado". Visual FoxPro non supporta l'esecuzione asincrona.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN o un valore a 32 bit che indica la lunghezza della struttura o un'istanza di un buffer in cui verranno vincolate le colonne di risultati.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|Il driver non consente SQL_CONCUR_ROWVER, perché Visual FoxPro non dispone del controllo delle versioni delle righe basato su timestamp.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|Il driver non consente SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC; Per ulteriori informazioni, vedere [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) .|  
|SQL_KEYSET_SIZE|Errore: "driver non in grado di supportare"|Visual FoxPro non supporta il modello di cursore keyset.|  
|SQL_MAX_LENGTH|0|Se si tenta di impostare questo valore *fOption* , il driver restituisce l'errore "driver non in grado".|  
|SQL_MAX_ROWS|0|Se si tenta di impostare questo valore *fOption* , il driver restituisce l'errore "driver non in grado".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Se si tenta di impostare questo valore *fOption* , il driver restituisce l'errore "driver non in grado".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|da 1 a 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Errore: "driver non in grado di supportare"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Per ulteriori informazioni, vedere [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) in *ODBC Programmer ' s Reference*.
