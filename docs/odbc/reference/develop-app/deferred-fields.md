---
title: Proprietà Deferred Fields . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 094aba353e10ed568e1959b1d655109296507dee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305972"
---
# <a name="deferred-fields"></a>Campi posticipati
I valori dei *campi posticipati* non vengono utilizzati quando sono impostati, ma il driver salva gli indirizzi delle variabili per un effetto posticipato. Per un descrittore di parametri dell'applicazione, il driver utilizza il contenuto delle variabili al momento della chiamata a **SQLExecDirect** o **SQLExecute**. Per un descrittore di riga dell'applicazione, il driver utilizza il contenuto delle variabili al momento del recupero.  
  
 Di seguito sono riportati i campi posticipati:  
  
-   I campi SQL_DESC_DATA_PTR e SQL_DESC_INDICATOR_PTR di un record descrittore.  
  
-   Campo SQL_DESC_OCTET_LENGTH_PTR di un record descrittore dell'applicazione.  
  
-   Nel caso di un recupero a più righe, i SQL_DESC_ARRAY_STATUS_PTR e SQL_DESC_ROWS_PROCESSED_PTR campi di un'intestazione del descrittore.  
  
 Quando viene allocato un descrittore, i campi posticipati di ogni record del descrittore hanno inizialmente un valore null. Il significato del valore null è il seguente:  
  
-   Se SQL_DESC_ARRAY_STATUS_PTR ha un valore null, un recupero su più righe non riesce a restituire questo componente delle informazioni di diagnostica per riga.  
  
-   Se SQL_DESC_DATA_PTR ha un valore null, il record non è associato.  
  
-   Se il campo SQL_DESC_OCTET_LENGTH_PTR di un ARD ha un valore null, il driver non restituisce informazioni sulla lunghezza per tale colonna.  
  
-   Se il campo SQL_DESC_OCTET_LENGTH_PTR di un APD ha un valore null e il parametro è una stringa di caratteri, il driver presuppone che la stringa sia con terminazione null. Per i parametri dinamici di output, un valore null in questo campo impedisce al driver di restituire informazioni sulla lunghezza. Se il campo SQL_DESC_TYPE non indica un parametro stringa di caratteri, il campo SQL_DESC_OCTET_LENGTH_PTR viene ignorato.  
  
 L'applicazione non deve deallocare o eliminare le variabili utilizzate per i campi posticipati tra il momento in cui le associa ai campi e il momento in cui il driver li legge o li scrive.
