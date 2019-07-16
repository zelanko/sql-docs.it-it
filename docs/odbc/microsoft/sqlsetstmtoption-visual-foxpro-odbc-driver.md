---
title: SQLSetStmtOption (Driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905333"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: Livello 1  
  
 Imposta le opzioni relative a un handle di istruzione *hstmt*.  
  
|*fOption*|Valori consentiti|Commenti|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Se si prova a impostare questa *fOption*, il driver restituisce l'errore: "Driver non valido". Visual FoxPro non supporta l'esecuzione asincrona.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN o un valore a 32 bit che indica la lunghezza della struttura o un'istanza di un buffer in cui risultato colonne verranno associate.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|Il driver non consente SQL_CONCUR_ROWVER, perché Visual FoxPro non dispone delle versioni delle righe basato su timestamp.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|Il driver non supporta SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC; visualizzare [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) per altre informazioni.|  
|SQL_KEYSET_SIZE|Errore: "Non è in grado di driver"|Visual FoxPro non supporta il modello di cursore keyset.|  
|SQL_MAX_LENGTH|0|Se si prova a impostare questa *fOption* valore, il driver restituisce l'errore "Non è in grado di Driver".|  
|SQL_MAX_ROWS|0|Se si prova a impostare questa *fOption* valore, il driver restituisce l'errore "Non è in grado di Driver".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Se si prova a impostare questa *fOption* valore, il driver restituisce l'errore "Non è in grado di Driver".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|da 1 a 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Errore: "Non è in grado di driver"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Per altre informazioni, vedere [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) nel *riferimento per programmatori ODBC*.
