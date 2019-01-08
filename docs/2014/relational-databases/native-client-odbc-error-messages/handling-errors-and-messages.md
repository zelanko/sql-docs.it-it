---
title: Gestione degli errori e i messaggi | Documenti di Microsoft
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4a4d87ccae235aee1a11e58aff60fe8e34d6205
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376383"
---
# <a name="handling-errors-and-messages"></a>Gestione di errori e messaggi
  Quando un'applicazione chiama una funzione ODBC, il driver esegue la funzione e restituisce le informazioni di diagnostica in due modi: Un codice restituito indica l'esito positivo o negativo complessivo di una funzione ODBC e i record di diagnostica forniscono informazioni dettagliate sulla funzione. I record di diagnostica includono un record di intestazione e record di stato. Anche se la funzione riesce, viene restituito almeno un record di diagnostica, ovvero il record di intestazione.  
  
 Le informazioni di diagnostica vengono utilizzate in fase di sviluppo per rilevare errori di programmazione, ad esempio handle ed errori di sintassi non validi nelle istruzioni SQL hard-coded. Vengono utilizzate anche in fase di esecuzione per rilevare avvisi ed errori di runtime, ad esempio troncamento di dati, violazioni di regole ed errori di sintassi nelle istruzioni SQL immesse dall'utente. La logica del programma si basa generalmente sui codici restituiti.  
  
 Ad esempio, dopo che un'applicazione chiama **SQLFetch** per recuperare le righe in un set di risultati, il codice restituito indica se è stata raggiunta la fine del set di risultati (SQL_NO_DATA), se tutti i messaggi informativi restituiti (SQL_SUCCESS_ WITH_INFO), o se si è verificato un errore (SQL_ERROR).  
  
 Se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client restituisce un valore diverso da SQL_SUCCESS, l'applicazione può chiamare **SQLGetDiagRec** per recuperare informativi o messaggi di errore. Uso **SQLGetDiagRec** scorrere su e giù messaggio impostato se è presente più di un messaggio.  
  
 Il codice restituito SQL_INVALID_HANDLE indica sempre un errore di programmazione e non dovrebbe essere mai rilevato in fase di esecuzione. Tutti gli altri codici restituiti forniscono informazioni di runtime, anche se SQL_ERROR potrebbe indicare un errore di programmazione.  
  
 Originale [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API native, DB-Library per C, consente a un'applicazione installare i callback degli errori e le funzioni di gestione dei messaggi che restituiscono errori o messaggi. Alcune istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)], ad esempio PRINT, RAISERROR, DBCC e SET, restituiscono i risultati alla funzione di gestione dei messaggi di DB-Library anziché a un set di risultati. L'API ODBC invece non presenta alcuna funzionalità di callback di questo tipo. Quando la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client rileva messaggi che provengono da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], imposta il codice restituito di ODBC su SQL_SUCCESS_WITH_INFO o SQL_ERROR e restituisce il messaggio con uno o più record di diagnostica. Pertanto, un'applicazione ODBC deve testare attentamente questi codici restituiti e chiamare **SQLGetDiagRec** per recuperare i dati del messaggio.  
  
 Per informazioni sulla traccia degli errori, vedere [Data Access Tracing](https://go.microsoft.com/fwlink/?LinkId=125805) (Traccia di accesso ai dati). Per informazioni sui miglioramenti alla tracciatura errore aggiunto in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], vedere [accesso a informazioni diagnostiche nel registro eventi di esteso](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Elaborazione di istruzioni che generano messaggi](processing-statements-that-generate-messages.md)  
  
-   [Campi e record di diagnostica](diagnostic-records-and-fields.md)  
  
-   [Numeri di errori nativi](native-error-numbers.md)  
  
-   [SQLSTATE &#40;codici di errore ODBC&#41;](sqlstate-odbc-error-codes.md)  
  
-   [Messaggi di errore](error-messages.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
