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
ms.openlocfilehash: e5f780f9abc47a367a1825d51b12159292ace5da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020426"
---
# <a name="return-codes-odbc"></a>Codici restituiti ODBC
Ogni funzione in ODBC restituisce un codice, noto come *codice restituito,* che indica l'esito positivo o negativo complessivo della funzione. La logica del programma si basa generalmente sui codici restituiti.  
  
 Il codice seguente, ad esempio, chiama **SQLFetch** per recuperare le righe in un set di risultati. Verifica il codice restituito della funzione per determinare se è stata raggiunta la fine del set di risultati (SQL_NO_DATA), se sono state restituite informazioni di avviso (SQL_SUCCESS_WITH_INFO) o se si è verificato un errore (SQL_ERROR).  
  
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
  
 Nella tabella seguente vengono definiti i codici restituiti.  
  
|Codice restituito|Descrizione|  
|-----------------|-----------------|  
|SQL_SUCCESS|Funzione completata correttamente. L'applicazione chiama **SQLGetDiagField** per recuperare informazioni aggiuntive dal record di intestazione.|  
|SQL_SUCCESS_WITH_INFO|La funzione è stata completata correttamente, probabilmente con un errore non irreversibile (avviso). L'applicazione chiama **SQLGetDiagRec** o **SQLGetDiagField** per recuperare informazioni aggiuntive.|  
|SQL_ERROR|Funzione non riuscita. L'applicazione chiama **SQLGetDiagRec** o **SQLGetDiagField** per recuperare informazioni aggiuntive. Il contenuto di tutti gli argomenti di output della funzione non è definito.|  
|SQL_INVALID_HANDLE|Funzione non riuscita a causa di un ambiente, una connessione, un'istruzione o un handle di descrittore non valido. Ciò indica un errore di programmazione. Non sono disponibili informazioni aggiuntive da **SQLGetDiagRec** o **SQLGetDiagField**. Questo codice viene restituito solo quando l'handle è un puntatore null o è di tipo errato, ad esempio quando viene passato un handle di istruzione per un argomento che richiede un handle di connessione.|  
|SQL_NO_DATA|Non sono disponibili altri dati. L'applicazione chiama **SQLGetDiagRec** o **SQLGetDiagField** per recuperare informazioni aggiuntive. È possibile che vengano restituiti uno o più record di stato definiti dal driver nella classe 02xxx. **Nota:**  In ODBC 2. *x*, il codice restituito è denominato SQL_NO_DATA_FOUND.|  
|SQL_NEED_DATA|Sono necessari più dati, ad esempio quando i dati dei parametri vengono inviati in fase di esecuzione o sono necessarie informazioni aggiuntive sulla connessione. L'applicazione chiama **SQLGetDiagRec** o **SQLGetDiagField** per recuperare eventuali informazioni aggiuntive.|  
|SQL_STILL_EXECUTING|Una funzione avviata in modo asincrono è ancora in esecuzione. L'applicazione chiama **SQLGetDiagRec** o **SQLGetDiagField** per recuperare eventuali informazioni aggiuntive.|
