---
title: Gestione di errori e messaggi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 31216e5a6670ff29c0d7e7ab4f1ee31cc5af0564
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705385"
---
# <a name="handling-errors-and-messages"></a>Gestione di errori e messaggi
  Quando un'applicazione chiama una funzione ODBC, il driver esegue la funzione e restituisce le informazioni di diagnostica in due modi: un codice restituito indica l'esito positivo o negativo complessivo di una funzione ODBC e i record di diagnostica forniscono informazioni dettagliate sulla funzione. I record di diagnostica includono un record di intestazione e record di stato. Anche se la funzione riesce, viene restituito almeno un record di diagnostica, ovvero il record di intestazione.  
  
 Le informazioni di diagnostica vengono utilizzate in fase di sviluppo per rilevare errori di programmazione, ad esempio handle ed errori di sintassi non validi nelle istruzioni SQL hard-coded. Vengono utilizzate anche in fase di esecuzione per rilevare avvisi ed errori di runtime, ad esempio troncamento di dati, violazioni di regole ed errori di sintassi nelle istruzioni SQL immesse dall'utente. La logica del programma si basa generalmente sui codici restituiti.  
  
 Ad esempio, dopo che un'applicazione chiama **SQLFetch** per recuperare le righe in un set di risultati, il codice restituito indica se è stata raggiunta la fine del set di risultati (SQL_NO_DATA), se sono stati restituiti messaggi informativi (SQL_SUCCESS_WITH_INFO) o se si è verificato un errore (SQL_ERROR).  
  
 Se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client restituisce un valore diverso da SQL_SUCCESS, l'applicazione può chiamare **SQLGetDiagRec** per recuperare qualsiasi messaggio informativo o di errore. Utilizzare **SQLGetDiagRec** per scorrere verso l'alto e verso il basso il set di messaggi se è presente più di un messaggio.  
  
 Il codice restituito SQL_INVALID_HANDLE indica sempre un errore di programmazione e non dovrebbe essere mai rilevato in fase di esecuzione. Tutti gli altri codici restituiti forniscono informazioni di runtime, anche se SQL_ERROR potrebbe indicare un errore di programmazione.  
  
 L' [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API nativa originale, DB-Library per C, consente a un'applicazione di installare le funzioni di gestione degli errori di callback e di gestione dei messaggi che restituiscono errori o messaggi. Alcune istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)], ad esempio PRINT, RAISERROR, DBCC e SET, restituiscono i risultati alla funzione di gestione dei messaggi di DB-Library anziché a un set di risultati. L'API ODBC invece non presenta alcuna funzionalità di callback di questo tipo. Quando il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client rileva messaggi provenienti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , imposta il codice ODBC restituito su SQL_SUCCESS_WITH_INFO o SQL_ERROR e restituisce il messaggio come uno o più record di diagnostica. Pertanto, un'applicazione ODBC deve testare attentamente questi codici restituiti e chiamare **SQLGetDiagRec** per recuperare i dati del messaggio.  
  
 Per informazioni sulla traccia degli errori, vedere [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (Traccia di accesso ai dati). Per informazioni sui miglioramenti apportati alla traccia degli errori aggiunta in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], vedere [Accesso alle informazioni di diagnostica nel log degli eventi estesi](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Elaborazione di istruzioni che generano messaggi](processing-statements-that-generate-messages.md)  
  
-   [Campi e record di diagnostica](diagnostic-records-and-fields.md)  
  
-   [Numeri di errori nativi](native-error-numbers.md)  
  
-   [Codici di errore SQLSTATE &#40;ODBC&#41;](sqlstate-odbc-error-codes.md)  
  
-   [messaggi di errore](error-messages.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
