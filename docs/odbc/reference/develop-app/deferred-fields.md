---
title: Campi posticipati | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305972"
---
# <a name="deferred-fields"></a>Campi posticipati
I valori dei *campi posticipati* non vengono usati quando sono impostati, ma il driver Salva gli indirizzi delle variabili per un effetto posticipato. Per un descrittore di parametri dell'applicazione, il driver utilizza il contenuto delle variabili al momento della chiamata a **SQLExecDirect** o **SQLExecute**. Nel caso di un descrittore di riga dell'applicazione, il driver usa il contenuto delle variabili al momento del recupero.  
  
 Di seguito sono riportati i campi posticipati:  
  
-   I campi SQL_DESC_DATA_PTR e SQL_DESC_INDICATOR_PTR di un record di descrittore.  
  
-   Campo SQL_DESC_OCTET_LENGTH_PTR di un record del descrittore dell'applicazione.  
  
-   Nel caso di un recupero più righe, i campi SQL_DESC_ARRAY_STATUS_PTR e SQL_DESC_ROWS_PROCESSED_PTR di un'intestazione del descrittore.  
  
 Quando si alloca un descrittore, i campi rinviati di ogni record di descrittore hanno inizialmente un valore null. Il significato del valore null è il seguente:  
  
-   Se SQL_DESC_ARRAY_STATUS_PTR ha un valore null, un recupero più righe non riesce a restituire questo componente delle informazioni di diagnostica per riga.  
  
-   Se SQL_DESC_DATA_PTR ha un valore null, il record non è associato.  
  
-   Se il SQL_DESC_OCTET_LENGTH_PTR campo di un ARD ha un valore null, il driver non restituisce informazioni sulla lunghezza per tale colonna.  
  
-   Se il campo SQL_DESC_OCTET_LENGTH_PTR di un oggetto APD ha un valore null e il parametro è una stringa di caratteri, il driver presuppone che la stringa sia con terminazione null. Per i parametri dinamici di output, un valore null in questo campo impedisce al driver di restituire informazioni sulla lunghezza. Se il campo SQL_DESC_TYPE non indica un parametro di stringa di caratteri, il campo SQL_DESC_OCTET_LENGTH_PTR viene ignorato.  
  
 L'applicazione non deve deallocare o annullare le variabili usate per i campi posticipati tra il momento in cui vengono associate ai campi e il momento in cui il driver li legge o li scrive.
