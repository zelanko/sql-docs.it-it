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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2c229d31941d5cef0da253545cecd7d1496ee4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076817"
---
# <a name="deferred-fields"></a>Campi posticipati
I valori della *posticipata campi* non vengono usati quando sono impostati, ma il driver vengono salvati gli indirizzi delle variabili per un effetto posticipata. Per un descrittore di parametri dell'applicazione, il driver utilizza il contenuto delle variabili al momento della chiamata a **SQLExecDirect** oppure **SQLExecute**. Per un descrittore riga dell'applicazione, il driver utilizza il contenuto delle variabili al momento dell'operazione di recupero.  
  
 Di seguito sono campi posticipati:  
  
-   I campi SQL_DESC_DATA_PTR e SQL_DESC_INDICATOR_PTR di un record del descrittore.  
  
-   Il campo SQL_DESC_OCTET_LENGTH_PTR di un record del descrittore dell'applicazione.  
  
-   Nel caso di un'operazione di recupero con più righe, i campi SQL_DESC_ARRAY_STATUS_PTR e SQL_DESC_ROWS_PROCESSED_PTR di un'intestazione del descrittore.  
  
 Quando si alloca un descrittore, i campi posticipati di ogni record del descrittore inizialmente sono associati un valore null. Come indicato di seguito è riportato il significato del valore null:  
  
-   Se SQL_DESC_ARRAY_STATUS_PTR ha un valore null, un'operazione di recupero con più righe non riesce a restituire questo componente per ogni riga informazioni di diagnostica.  
  
-   Se SQL_DESC_DATA_PTR ha un valore null, il record è non associato.  
  
-   Se il campo SQL_DESC_OCTET_LENGTH_PTR di un ARD ha un valore null, il driver non restituisce informazioni sulla lunghezza della colonna.  
  
-   Se il campo SQL_DESC_OCTET_LENGTH_PTR di un APD ha un valore null e il parametro è una stringa di caratteri, il driver presuppone che stringa con terminazione null. Per i parametri dinamici di output, un valore null in questo campo impedisce il driver di restituzione di informazioni sulla lunghezza. (Se il campo SQL_DESC_TYPE non indica un parametro di stringa di caratteri, viene ignorato il campo SQL_DESC_OCTET_LENGTH_PTR.)  
  
 L'applicazione non deve deallocare o eliminare le variabili usate per campi posticipati tra il momento che li associa i campi e l'ora il driver legge o scrive.
