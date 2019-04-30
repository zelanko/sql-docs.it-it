---
title: I driver di Database di diagnostica per il Desktop | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d6c21af2ef3f47c05aacf4b47673ab42a170f506
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128074"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>Diagnostica per i driver di database desktop
Tutti gli errori e avvisi non selezionato o controllo parzialmente selezionato da Gestione Driver vengono gestiti dal driver. Il driver esegue il mapping anche native errori o gli errori restituiti dall'origine dati, a SQLSTATE. Ogni funzione elencata nel *riferimento per programmatori ODBC* contiene una sezione "Diagnostica" che specifica le condizioni e i messaggi.  
  
 Le applicazioni chiamano **SQLGetDiagRec** per recuperare i messaggi di diagnostica, codice di errore nativo e SQLSTATE. La chiamata **SQLGetDiagField** e specificando il campo consente di recuperare i singoli campi di diagnostica. Il livello di supporto degli identificatori di diagnostica viene elencato nella tabella seguente.  
  
|DiagIdentifiers|Livello di supporto|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|Non supportato|  
|SQL_DIAG_CLASS_ORIGIN|Supportato. Sempre "ODBC 3.0" per le versioni 3.0 e versioni successive di questo driver.|  
|SQL_DIAG_COLUMN_NUMBER|Supportato|  
|SQL_DIAG_CURSOR_ROW_COUNT|Non supportato|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|Non supportato|  
|SQL_DIAG_MESSAGE_TEXT|Supportato|  
|SQL_DIAG_NATIVE|Supportato|  
|SQL_DIAG_NUMBER|Supportato|  
|SQL_DIAG_RETURNCODE|Supportato ma implementata da Gestione Driver|  
|SQL_DIAG_ROW_COUNT|Supportato|  
|SQL_DIAG_ROW_NUMBER|Supportato|  
|SQL_DIAG_SERVER_NAME|Non supportato|  
|SQL_DIAG_SQLSTATE|Supportato|  
|SQL_DIAG_SUBCLASS_ORIGIN|Supportato|
