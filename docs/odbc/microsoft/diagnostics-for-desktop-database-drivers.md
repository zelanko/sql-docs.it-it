---
title: Diagnostica per i driver del database desktop | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4e7c8ea96708886f9edf54047bd2a2104ba0ec8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031217"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnostica per i driver di database desktop
Tutti gli errori e gli avvisi non controllati o parzialmente controllati da Gestione driver vengono gestiti dal driver. Il driver esegue anche il mapping degli errori nativi o degli errori restituiti dall'origine dati a sqlstates. Ogni funzione elencata in *ODBC Programmer ' s Reference* contiene una sezione "Diagnostics" che specifica condizioni e messaggi.  
  
 Le applicazioni chiamano **SQLGetDiagRec** per recuperare SQLSTATE, il codice di errore nativo e i messaggi di diagnostica. Chiamando **SQLGetDiagField** e specificando il campo vengono recuperati i singoli campi di diagnostica. Il livello di supporto degli identificatori di diagnostica è elencato nella tabella seguente.  
  
|DiagIdentifiers|Livello di supporto|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Non supportate|  
|SQL_DIAG_CLASS_ORIGIN|Supportato. Sempre "ODBC 3,0" per le versioni 3,0 e successive di questo driver.|  
|SQL_DIAG_COLUMN_NUMBER|Supportato|  
|SQL_DIAG_CURSOR_ROW_COUNT|Non supportate|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Non supportate|  
|SQL_DIAG_MESSAGE_TEXT|Supportato|  
|SQL_DIAG_NATIVE|Supportato|  
|SQL_DIAG_NUMBER|Supportato|  
|SQL_DIAG_RETURNCODE|Supportato ma implementato da Gestione driver|  
|SQL_DIAG_ROW_COUNT|Supportato|  
|SQL_DIAG_ROW_NUMBER|Supportato|  
|SQL_DIAG_SERVER_NAME|Non supportate|  
|SQL_DIAG_SQLSTATE|Supportato|  
|SQL_DIAG_SUBCLASS_ORIGIN|Supportato|
