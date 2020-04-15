---
title: SqlSetStmtOption (driver ODBC di Visual FoxPro) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb9677a9ccf307be847089c657964d96904eb20b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299401"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello 1ODBC API Conformance: Level 1  
  
 Imposta le opzioni relative a un handle di istruzione, *hstmt*.  
  
|*fOpzione*|Valori consentiti|Commenti|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Se si tenta di impostare questo *fOption*, il driver restituisce l'errore: "Driver not capable". Visual FoxPro non supporta l'esecuzione asincrona.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN o un valore a 32 bit che indica la lunghezza della struttura o un'istanza di un buffer a cui verranno associate le colonne dei risultati.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|Il driver non consente SQL_CONCUR_ROWVER, perché Visual FoxPro non dispone di controllo delle versioni delle righe basato sui timestamp.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|Il conducente non consente SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC; Vedere [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) per ulteriori informazioni.|  
|SQL_KEYSET_SIZE|Errore: "Driver non in grado"|Visual FoxPro non supporta il modello di cursore keyset.|  
|SQL_MAX_LENGTH|0|Se si tenta di impostare questo valore *fOption,* il driver restituisce l'errore "Driver non in grado".|  
|SQL_MAX_ROWS|0|Se si tenta di impostare questo valore *fOption,* il driver restituisce l'errore "Driver non in grado".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Se si tenta di impostare questo valore *fOption,* il driver restituisce l'errore "Driver non in grado".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|Da 1 a 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Errore: "Driver non in grado"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Per ulteriori informazioni, vedere [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) in *ODBC Programmer's Reference*.
