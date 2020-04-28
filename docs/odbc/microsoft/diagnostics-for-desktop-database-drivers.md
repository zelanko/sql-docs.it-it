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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 99603c047e77d3cd3e077c1b07c2192eeb65f93c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303482"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnostica per i driver di database desktop
Tutti gli errori e gli avvisi non controllati o parzialmente controllati da Gestione driver vengono gestiti dal driver. Il driver esegue anche il mapping degli errori nativi o degli errori restituiti dall'origine dati a sqlstates. Ogni funzione elencata in *ODBC Programmer ' s Reference* contiene una sezione "Diagnostics" che specifica condizioni e messaggi.  
  
 Le applicazioni chiamano **SQLGetDiagRec** per recuperare SQLSTATE, il codice di errore nativo e i messaggi di diagnostica. Chiamando **SQLGetDiagField** e specificando il campo vengono recuperati i singoli campi di diagnostica. Il livello di supporto degli identificatori di diagnostica è elencato nella tabella seguente.  
  
|DiagIdentifiers|Livello di supporto|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Non supportato|  
|SQL_DIAG_CLASS_ORIGIN|Supportato. Sempre "ODBC 3,0" per le versioni 3,0 e successive di questo driver.|  
|SQL_DIAG_COLUMN_NUMBER|Supportato|  
|SQL_DIAG_CURSOR_ROW_COUNT|Non supportato|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Non supportato|  
|SQL_DIAG_MESSAGE_TEXT|Supportato|  
|SQL_DIAG_NATIVE|Supportato|  
|SQL_DIAG_NUMBER|Supportato|  
|SQL_DIAG_RETURNCODE|Supportato ma implementato da Gestione driver|  
|SQL_DIAG_ROW_COUNT|Supportato|  
|SQL_DIAG_ROW_NUMBER|Supportato|  
|SQL_DIAG_SERVER_NAME|Non supportato|  
|SQL_DIAG_SQLSTATE|Supportato|  
|SQL_DIAG_SUBCLASS_ORIGIN|Supportato|
