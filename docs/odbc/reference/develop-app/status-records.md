---
title: 'Record di stato : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 4a987f69-158f-4cc4-a31b-2b7dd8dcbb87
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4afef16137404fcdfd3e1d328642f1d314829538
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301372"
---
# <a name="status-records"></a>Record di stato
I campi nei record di stato contengono informazioni su errori o avvisi specifici restituiti da Gestione Driver, driver o origine dati, inclusi SQLSTATE, numero di errore nativo, messaggio di diagnostica, numero di colonna e numero di riga. I record di stato possono essere creati solo se la funzione restituisce SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA o SQL_STILL_EXECUTING. Per un elenco completo dei campi nei record di stato, vedere la descrizione della funzione [SQLGetDiagField.For](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) a complete list of fields in the status records, see the SQLGetDiagField function description.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Sequenza di record di stato](../../../odbc/reference/develop-app/sequence-of-status-records.md)  
  
-   [SQLSTATE](../../../odbc/reference/develop-app/sqlstates.md)  
  
-   [Messaggi di diagnostica](../../../odbc/reference/develop-app/diagnostic-messages.md)
