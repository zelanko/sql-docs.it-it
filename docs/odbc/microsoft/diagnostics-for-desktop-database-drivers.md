---
description: Diagnostica per i driver di database desktop
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
ms.openlocfilehash: eb5e4233ae77979df7b4b76ea845634fd7fd6ded
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471593"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnostica per i driver di database desktop
Tutti gli errori e gli avvisi non controllati o parzialmente controllati da Gestione driver vengono gestiti dal driver. Il driver esegue anche il mapping degli errori nativi o degli errori restituiti dall'origine dati a sqlstates. Ogni funzione elencata in *ODBC Programmer ' s Reference* contiene una sezione "Diagnostics" che specifica condizioni e messaggi.  
  
 Le applicazioni chiamano **SQLGetDiagRec** per recuperare SQLSTATE, il codice di errore nativo e i messaggi di diagnostica. Chiamando **SQLGetDiagField** e specificando il campo vengono recuperati i singoli campi di diagnostica. Il livello di supporto degli identificatori di diagnostica è elencato nella tabella seguente.  
  
|DiagIdentifiers|Livello di supporto|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Non supportate|  
|SQL_DIAG_CLASS_ORIGIN|Supportata. Sempre "ODBC 3,0" per le versioni 3,0 e successive di questo driver.|  
|SQL_DIAG_COLUMN_NUMBER|Funzionalità supportata|  
|SQL_DIAG_CURSOR_ROW_COUNT|Non supportate|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Non supportate|  
|SQL_DIAG_MESSAGE_TEXT|Funzionalità supportata|  
|SQL_DIAG_NATIVE|Funzionalità supportata|  
|SQL_DIAG_NUMBER|Funzionalità supportata|  
|SQL_DIAG_RETURNCODE|Supportato ma implementato da Gestione driver|  
|SQL_DIAG_ROW_COUNT|Funzionalità supportata|  
|SQL_DIAG_ROW_NUMBER|Funzionalità supportata|  
|SQL_DIAG_SERVER_NAME|Non supportate|  
|SQL_DIAG_SQLSTATE|Funzionalità supportata|  
|SQL_DIAG_SUBCLASS_ORIGIN|Funzionalità supportata|
