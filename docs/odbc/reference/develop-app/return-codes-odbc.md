---
title: Codici restituiti ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aee8914493c66ff451d7bca7f56fc8723d2a7ca0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63254134"
---
# <a name="return-codes-odbc"></a>Codici restituiti ODBC
Ogni funzione in ODBC restituisce un codice, noto come relativo *codice restituito,* che indica l'esito positivo o negativo complessivo della funzione. La logica del programma si basa generalmente sui codici restituiti.  
  
 Ad esempio, il codice seguente chiama **SQLFetch** per recuperare le righe in un set di risultati. Controlla il codice restituito della funzione per determinare se (SQL_NO_DATA), è stata raggiunta la fine del set di risultati se eventuali informazioni di avviso è stati restituiti (SQL_SUCCESS_WITH_INFO) o se si è verificato un errore (SQL_ERROR).  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
while ((rc=SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (rc == SQL_SUCCESS_WITH_INFO) {  
      // Call function to display warning information.  
   } else if (rc == SQL_ERROR) {  
      // Call function to display error information.  
      break;  
   }  
   // Process row.  
}  
```  
  
 Il codice restituito SQL_INVALID_HANDLE indica sempre un errore di programmazione e non dovrebbe essere mai rilevato in fase di esecuzione. Tutti gli altri codici restituiti forniscono informazioni di runtime, anche se SQL_ERROR potrebbe indicare un errore di programmazione.  
  
 Nella tabella seguente definisce i codici restituiti.  
  
|Codice restituito|Descrizione|  
|-----------------|-----------------|  
|SQL_SUCCESS|Funzione è stata completata correttamente. L'applicazione chiama **SQLGetDiagField** per recuperare informazioni aggiuntive dal record di intestazione.|  
|SQL_SUCCESS_WITH_INFO|Funzione è stata completata correttamente, eventualmente con un errore non irreversibile (avviso). L'applicazione chiama **SQLGetDiagRec** oppure **SQLGetDiagField** per recuperare informazioni aggiuntive.|  
|SQL_ERROR|Funzione non riuscita. L'applicazione chiama **SQLGetDiagRec** oppure **SQLGetDiagField** per recuperare informazioni aggiuntive. Il contenuto di qualsiasi argomento di output della funzione è indefinito.|  
|SQL_INVALID_HANDLE|Funzione non riuscita a causa di un handle di ambiente, connessione, istruzione o descrittore non valido. Ciò indica un errore di programmazione. Nessuna informazione aggiuntiva è disponibile dal **SQLGetDiagRec** oppure **SQLGetDiagField**. Questo codice viene restituito solo quando l'handle è un puntatore null o è di tipo errato, ad esempio quando viene passato un handle di istruzione per un argomento che richiede un handle di connessione.|  
|SQL_NO_DATA|Non esistono altri dati erano disponibili. L'applicazione chiama **SQLGetDiagRec** oppure **SQLGetDiagField** per recuperare informazioni aggiuntive. Uno o più record di stato definiti dal driver nella classe 02xxx possono essere restituiti. **Nota:**  In ODBC 2. *x*, questo restituisce codice è stato denominato SQL_NO_DATA_FOUND.|  
|SQL_NEED_DATA|Sono necessari più dati, ad esempio quando i dati dei parametri viene inviati in fase di esecuzione o sono necessarie informazioni di connessione aggiuntive. L'applicazione chiama **SQLGetDiagRec** oppure **SQLGetDiagField** per recuperare informazioni aggiuntive, se presente.|  
|SQL_STILL_EXECUTING|Una funzione che è stata avviata in modalità asincrona è ancora in esecuzione. L'applicazione chiama **SQLGetDiagRec** oppure **SQLGetDiagField** per recuperare informazioni aggiuntive, se presente.|
